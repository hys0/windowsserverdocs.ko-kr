---
title: 저장소 공간 다이렉트의 볼륨 할당을 구분 합니다.
ms.author: cosmosdarwin
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 03/29/2018
ms.openlocfilehash: c93cbf4ba418f6702cf8747508605952d993508d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889054"
---
# <a name="delimit-the-allocation-of-volumes-in-storage-spaces-direct"></a>저장소 공간 다이렉트의 볼륨 할당을 구분 합니다.
> 적용 대상: Windows Server Insider Preview 빌드 17093 이상

Windows Server Insider Preview에는 수동으로 저장소 공간 다이렉트의 볼륨 할당을 구분 하는 옵션이 도입 되었습니다. 이렇게 하면 특정 조건에서 내결함성을 크게 높일 수 있도록 하지만 적용 일부 추가 관리 고려 사항 및 복잡성입니다. 이 항목에서는 작동 하며 powershell에서 예제를 제공 하는 방법을 설명 합니다.

   > [!IMPORTANT]
   > 이 기능은 Windows Server Insider Preview 빌드 17093 이상에서 새로운 기능입니다. Windows Server 2016에서 사용할 수 없는 합니다. IT 전문가 연결할 것을 권해 드립니다 합니다 [Windows Server Insider 프로그램](https://aka.ms/serverinsider) 조직에 대해 더 잘 작동 하는 Windows Server를 확인 하는 방법에 대 한 피드백을 제공 하 합니다.

## <a name="prerequisites"></a>사전 요구 사항

### <a name="green-checkmark-iconmediadelimit-volume-allocationsupportedpng-consider-using-this-option-if"></a>![녹색 확인 표시 아이콘입니다.](media/delimit-volume-allocation/supported.png) 하는 경우이 옵션을 사용 하는 것이 좋습니다.

- 클러스터에 6 개 이상 서버 및
- 클러스터만 사용 하 여 [3 방향 미러](storage-spaces-fault-tolerance.md#mirroring) 복원 력

### <a name="red-x-iconmediadelimit-volume-allocationunsupportedpng-do-not-use-this-option-if"></a>![빨간색 X 아이콘입니다.](media/delimit-volume-allocation/unsupported.png) 경우에이 옵션을 사용 하지 마십시오.

- 클러스터에 6 개 미만의 서버; 또는
- 클러스터에서 사용 [패리티](storage-spaces-fault-tolerance.md#parity) 하거나 [패리티 미러 가속](storage-spaces-fault-tolerance.md#mirror-accelerated-parity) 복원 력

## <a name="understand"></a>이해

### <a name="review-regular-allocation"></a>일반 할당을 검토 합니다.

일반 3 방향 미러링을 사용 하 여 볼륨 많은 작은 "줄임" 세 번 복사 하 고 클러스터의 모든 서버에서 모든 드라이브에 고르게 분산 하는으로 나뉩니다. 자세한 내용은 참조 하세요 [심층 분석 블로그](https://blogs.technet.microsoft.com/filecab/2016/11/21/deep-dive-pool-in-spaces-direct/)합니다.

![볼륨 줄임의 세 가지 스택으로 구분 되 고 모든 서버에 균등 하 게 분산을 보여 주는 다이어그램입니다.](media/delimit-volume-allocation/regular-allocation.png)

이 기본 할당 최대화 동시 읽기 및 쓰기, 더 나은 성능을 위해 이며 간소에 매력적인: 모든 서버가 동일 하 게, 모든 드라이브는 동일 하 게 전체 이므로 모든 볼륨이 온라인 상태를 유지 또는 함께 오프 라인으로 전환 합니다. 모든 볼륨으로 최대 2 개의 동시 오류를 견딜 수 보장이 [이 이와](storage-spaces-fault-tolerance.md#examples) 보여 줍니다.

그러나이 할당을 사용 하 여 볼륨 3 개 동시 장애를 견딜 수 없습니다. 세 명의 서버를 한 번에 실패할 경우 어느 정도의 줄임 (가능성이 매우 높음)으로 할당 된 드라이브 세 개를 정확 하 게 또는 실패 한 서버에 있으므로 볼륨 드라이브 세 명의 서버에서 한 번에 실패할 경우 액세스할 수 없게 합니다.

아래 예제 서버 1, 3, 5와 동시에 실패합니다. 많은 줄임이 복사 되지 않고 남아 있지만 일부 하지 않습니다.

![전체 볼륨과 빨간색으로 강조 표시 하는 6 명의 서버 중 세 가지를 보여 주는 다이어그램은 빨간색입니다.](media/delimit-volume-allocation/regular-does-not-survive.png)

볼륨이 오프 라인 상태로 전환 및 서버를 복구할 때까지 액세스할 수 없게 됩니다.

### <a name="new-delimited-allocation"></a>신규: 할당을 구분

구분 기호로 분리 된 할당 (3 방향 미러 서버에 대 한 최소 3 개)를 사용 하 여 서버의 하위 집합을 지정 합니다. 볼륨 세 번 전과 같이, 하지만 모든 서버에서 할당 하는 대신 복사 되는 줄임 나뉩니다 **지정할 서버의 하위 집합에만 할당 되는 줄임**합니다.

![볼륨 줄임의 세 가지 스택으로 구분 되어 6 대의 서버 중 세 가지만 배포를 보여 주는 다이어그램입니다.](media/delimit-volume-allocation/delimited-allocation.png)

#### <a name="advantages"></a>장점

이 할당 된 볼륨은 세 개의 동시 오류에서 존속 할: 사실 서바이벌 확률 증가 (일반 할당)을 통해 0%에서 95% (구분 기호로 분리 된 할당)을 통해이 경우! 직관적으로 이므로 해당 오류에 의해 영향을 받지 않습니다 있도록 4, 5 또는 6 서버에 종속 되지 않습니다.

위의 예제에서는 1, 3 및 5 서버는 동시에 실패합니다. 구분 기호로 분리 된 할당 마다 slab 복사본을 포함 하는 해당 서버 2 보장, 때문에 모든 slab 존속 복사본이 고 볼륨이 온라인 상태이 고 액세스할 수 있는 유지:

![전체 볼륨은 녹색는 6 개 서버가 빨간색으로 강조 표시 된 세 가지를 보여 주는 다이어그램입니다.](media/delimit-volume-allocation/delimited-does-survive.png)

서버 및 기타 요인의 수에 따라 달라 집니다 서바이벌 확률을 참조 하세요 [분석](#analysis) 세부 정보에 대 한 합니다.

#### <a name="disadvantages"></a>단점

구분 기호로 분리 된 할당 일부 추가 관리 고려 사항 및 복잡성을 적용 합니다.

1. 관리자는에 설명 된 대로 서버에서 저장소 사용률을 분산 하 여 생존을 확률이 높은 규정 각 볼륨 할당을 구분 하는 일을 담당 합니다 [모범 사례](#best-practices) 섹션입니다.

2. 구분 기호로 분리 된 할당에 해당 하는 예약 **서버 (무제한) 당 하나의 용량 드라이브**합니다. 이 보다 [권장 사항 게시](plan-volumes.md#choosing-the-size-of-volumes) 총 드라이브 4 용량 초과 최대로 일반 할당에 대 한 합니다.

3. 서버 실패 하 고에 설명 된 대로 교체 해야 [서버와 해당 드라이브가 제거](remove-servers.md#remove-a-server-and-its-drives), 관리자는 새 서버를 추가 하 고 실패 한 one – 예제를 제거 하 여 영향을 받는 볼륨의 delimitation 업데이트 아래.

## <a name="usage-in-powershell"></a>PowerShell에서 사용

사용할 수는 `New-Volume` 저장소 공간 다이렉트에서 볼륨을 만드는 cmdlet입니다.

예를 들어, 일반적인 3 방향 미러 볼륨을 만들려면:

```PowerShell
New-Volume -FriendlyName "MyRegularVolume" -Size 100GB
```

### <a name="create-a-volume-and-delimit-its-allocation"></a>볼륨 만들기 및 해당 할당을 구분 합니다.

3 방향 미러 볼륨 만들기 및 해당 할당을 구분 합니다.

1. 클러스터의 서버 변수에 먼저 할당 `$Servers`:

    ```PowerShell
    $Servers = Get-StorageFaultDomain -Type StorageScaleUnit | Sort FriendlyName
    ```

   > [!TIP]
   > 저장소 공간 다이렉트의 용어 ' 저장소 배율 단위 ' 직접 연결 된 드라이브 및 드라이브를 사용 하 여 직접 연결 된 외부 엔클로저를 포함 하 여 하나의 서버에 연결 된 모든 원시 저장소를 가리킵니다. 이 컨텍스트에서 것 'server'와 동일 합니다.

2. 사용할 새 서버를 지정할 `-StorageFaultDomainsToUse` 매개 변수 및 인덱싱에 `$Servers`입니다. 첫째, 둘째,에 대 한 할당을 구분 하는 예 및 세 번째 서버 (인덱스 0, 1 및 2):

    ```PowerShell
    New-Volume -FriendlyName "MyVolume" -Size 100GB -StorageFaultDomainsToUse $Servers[0,1,2]
    ```

### <a name="see-a-delimited-allocation"></a>구분 기호로 분리 된 할당을 참조 하세요.

보려는 어떻게 *MyVolume* 는 사용 하 여 할당 합니다 `Get-VirtualDiskFootprintBySSU.ps1` 스크립트 [부록](#appendix):

```PowerShell
PS C:\> .\Get-VirtualDiskFootprintBySSU.ps1

VirtualDiskFriendlyName TotalFootprint Server1 Server2 Server3 Server4 Server5 Server6
----------------------- -------------- ------- ------- ------- ------- ------- -------
MyVolume                300 GB         100 GB  100 GB  100 GB  0       0       0      
```

Server1, Server2를 및 Server3 포함의 줄임 *MyVolume*합니다.

### <a name="change-a-delimited-allocation"></a>구분 기호로 분리 된 할당을 변경 합니다.

새 `Add-StorageFaultDomain` 고 `Remove-StorageFaultDomain` 할당을 구분 하는 방법을 변경 하기 위한 cmdlet입니다.

예를 들어 이동할 *MyVolume* 서버만 장애 조치 합니다.

1. 지정 하는 네 번째 서버 **수 있습니다** 의 줄임 저장할 *MyVolume*:

    ```PowerShell
    Get-VirtualDisk MyVolume | Add-StorageFaultDomain -StorageFaultDomains $Servers[3]
    ```

2. 지정 하는 첫 번째 서버 **없습니다** 의 줄임 저장할 *MyVolume*:

    ```PowerShell
    Get-VirtualDisk MyVolume | Remove-StorageFaultDomain -StorageFaultDomains $Servers[0]
    ```

3. 변경 내용을 적용 하려면 저장소 풀을 리 밸런스 합니다.

    ```PowerShell
    Get-StoragePool S2D* | Optimize-StoragePool
    ```

![줄임 서버 1, 2 및 3에서에서 집합 2, 3 및 4 서버로 마이그레이션 보여 주는 다이어그램입니다.](media/delimit-volume-allocation/move.gif)

사용 하 여 리 밸런스의 진행률을 모니터링할 수 있습니다 `Get-StorageJob`합니다.

완료 되 면 확인 *MyVolume* 실행 하 여 움직인 `Get-VirtualDiskFootprintBySSU.ps1` 다시 합니다.

```PowerShell
PS C:\> .\Get-VirtualDiskFootprintBySSU.ps1

VirtualDiskFriendlyName TotalFootprint Server1 Server2 Server3 Server4 Server5 Server6
----------------------- -------------- ------- ------- ------- ------- ------- -------
MyVolume                300 GB         0       100 GB  100 GB  100 GB  0       0      
```

Server1에 없는 참고 줄임 *MyVolume* Server04 않습니다 대신 – 더 이상.

## <a name="best-practices"></a>모범 사례

구분 된 볼륨 할당을 사용 하 여 때 따라야 할 모범 사례는 다음과 같습니다.

### <a name="choose-three-servers"></a>세 명의 서버를 선택 합니다.

세 명의 서버에 각 3 방향 미러 볼륨을 더 하지 구분 합니다.

### <a name="balance-storage"></a>분산 저장소

볼륨 크기를 고려 하는 각 서버에 할당할 저장소의 양을 조정 합니다.

### <a name="every-delimited-allocation-unique"></a>고유한 구분 기호로 분리 된 모든 할당

내결함성을 최대화 하려면 고유 하 게 각 볼륨 할당을 공유 하지 않는 의미 *모든* 다른 볼륨 (일부 중복 확인)를 사용 하 여 해당 서버. N 서버를 사용 하 여 가지 고유 조합을 "N 선택 3" – 다음은 몇 가지 일반적인 클러스터 크기에 대 한 의미는:

| (N) 서버의 수 | 고유한 구분 할당 (N 3를 선택 하는 데 사용) |
|-----------------------|-----------------------------------------------------|
| 6                     | 20                                                  |
| 8                     | 56                                                  |
| 12                    | 220                                                 |
| 16                    | 560                                                 |

   > [!TIP]
   > 유용한이 검토는 것이 좋습니다 [combinatorics 표기법 선택한](https://betterexplained.com/articles/easy-permutations-and-combinations/)합니다.

다음은 내결함성을 최대화 하는 예제 – 모든 볼륨에는 고유한 구분 기호로 분리 된 할당 합니다.

![고유한 할당](media/delimit-volume-allocation/unique-allocation.png)

반대로, 다음 예제에서는 처음 세 개의 볼륨 (1, 2 및 3 서버)에 대 한 동일한 구분 기호로 분리 된 할당을 사용 하 고 마지막으로 세 개의 볼륨 (4, 5 및 6 서버)에 대 한 동일한 구분 기호로 분리 된 할당을 사용 합니다. 이 내결함성을 최대화 하지 않습니다: 여러 볼륨 수 오프 라인으로 전환 하 고 한 번에 액세스할 수 없게 세 명의 서버가 실패 하는 경우.

![non-unique-allocation](media/delimit-volume-allocation/non-unique-allocation.png)

## <a name="analysis"></a>분석

이 섹션에서는 볼륨을 온라인 상태이 고 액세스할 수 있는 상태로 유지 된다는 수학 확률 (또는 동등 하 게, 온라인 상태이 고 액세스할 수 있는 상태로 유지 되는 전체 저장소의 예상된 비율) 파생 되는 다양 한 오류 및 클러스터 크기의 함수로.

   > [!NOTE]
   > 이 섹션은 선택 사항 읽기. 수학 합니다 인 경우 계속 읽어주세요. 그러나 그렇지 않은 경우 걱정 하지 마세요. [PowerShell에서 사용 현황](#usage-in-powershell) 하 고 [모범 사례](#best-practices) 구분 기호로 분리 된 할당을 성공적으로 구현 하기만 하면 됩니다.

### <a name="up-to-two-failures-is-always-okay"></a>최대 두 개의 오류 임을 항상

모든 3 방향 미러 볼륨으로 동시에 최대 2 개의 장애를 견딜 수 있습니다 [이 이와](storage-spaces-fault-tolerance.md#examples) 해당 할당에 관계 없이 보여 줍니다. 경우 두 드라이브 실패, 또는 두 서버가 실패 하거나 온라인 상태이 고 일반 할당으로도 액세스할 수 있는 각, 모든 3 방향 미러 볼륨 중 하나에 유지 됩니다.

### <a name="more-than-half-the-cluster-failing-is-never-okay"></a>절반 이상 클러스터 실패 해도 아닙니다.

서버 또는 클러스터 드라이브의 절반에 두 개를 한 번에 실패 하는 극단적인 경우에 반대로 [쿼럼이 손실 된](understand-quorum.md) 오프 라인 상태가 되 모든 3 방향 미러 볼륨 및 해당 할당에 관계 없이 액세스할 수 없게 됩니다.

### <a name="what-about-in-between"></a>어떻습니까 사이?

3 개 이상의 오류가 발생 한 번에 서버 및 드라이브의 최소 절반 이상이 계속 작동은 하지만 온라인 이며 액세스할 수 있는 서버 실패에 따라 구분 기호로 분리 된 할당을 사용 하 여 볼륨 유지 수 있습니다. 정확한 양상이 결정할 숫자를 실행 해 보겠습니다.

간단히 하기 위해 볼륨이 아닌 독립적으로 하며 위의 모범 사례에 따라 동일 하 게 분산된 (IID) 및 해당 충분히 고유 조합이 고유 하 게 모든 볼륨의 할당에 사용할 수를 가정 합니다. 지정 된 볼륨의 생존 가능성이 선형성 기대 수준으로 유지 되는 동안 전체 저장소의 예상된 비율 이기도 합니다. 

지정 된 **N** 서버는 **F** 실패에 할당 된 볼륨 **3** 하 되 오프 라인 이면-및-만-경우에 모든 **3** 합니다 중 **F** 오류가 발생 합니다. 가지 **(N F를 선택 하는 데 사용)** 방법을 **F** 오류는 발생 **(F 3를 선택 하는 데 사용)** 오프 라인으로 전환 및 액세스할 수 없게 되 고 볼륨에서 발생 합니다. 확률으로 표현할 수 있습니다.

![P_offline = Fc3 / NcF](media/delimit-volume-allocation/probability-volume-offline.png)

다른 모든 경우에 볼륨 유지 온라인 상태이 고 액세스할 수 있습니다.

![P_online = 1 – (Fc3 / NcF)](media/delimit-volume-allocation/probability-volume-online.png)

다음 표에서 몇 가지 일반적인 클러스터 크기 및 할당을 구분 기호로 분리 된 것으로 간주 하는 모든 경우에 일반 할당에 비해 내결함성 증가 함을 표시 하는 5 오류 최대 확률을 평가 합니다.

### <a name="with-6-servers"></a>6 대의 서버를 사용 하 여

| 할당                           | 1 실패 극복의 확률 | 2 오류를 극복의 확률 | 3 오류를 극복의 확률 | 4 개의 오류를 극복의 확률 | 5 개의 오류를 극복의 확률 |
|--------------------------------------|------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|
| 일반, 모든 6 대의 서버에 분산 | 100%                               | 100%                                | 0%                                  | 0%                                  | 0%                                  |
| 서버 3 개를 구분합니다.          | 100%                               | 100%                                | 95.0%                               | 0%                                  | 0%                                  |

   > [!NOTE]
   > 총 6 대의 서버에서 3 개 실패 한 후 클러스터 쿼럼을 잃습니다.

### <a name="with-8-servers"></a>8 서버를 사용 하 여

| 할당                           | 1 실패 극복의 확률 | 2 오류를 극복의 확률 | 3 오류를 극복의 확률 | 4 개의 오류를 극복의 확률 | 5 개의 오류를 극복의 확률 |
|--------------------------------------|------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|
| 일반, 모든 8 서버 간에 분산 | 100%                               | 100%                                | 0%                                  | 0%                                  | 0%                                  |
| 서버 3 개를 구분합니다.          | 100%                               | 100%                                | 98.2%                               | 94.3%                               | 0%                                  |

   > [!NOTE]
   > 총 8 개 서버에서 4 개 이상의 실패 한 후 클러스터 쿼럼을 잃습니다.

### <a name="with-12-servers"></a>12 명의 서버를 사용 하 여

| 할당                            | 1 실패 극복의 확률 | 2 오류를 극복의 확률 | 3 오류를 극복의 확률 | 4 개의 오류를 극복의 확률 | 5 개의 오류를 극복의 확률 |
|---------------------------------------|------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|
| 일반, 모든 12 서버 간에 분산 | 100%                               | 100%                                | 0%                                  | 0%                                  | 0%                                  |
| 서버 3 개를 구분합니다.           | 100%                               | 100%                                | 99.5%                               | 99.2%                               | 98.7%                               |

### <a name="with-16-servers"></a>16 대의 서버를 사용 하 여

| 할당                            | 1 실패 극복의 확률 | 2 오류를 극복의 확률 | 3 오류를 극복의 확률 | 4 개의 오류를 극복의 확률 | 5 개의 오류를 극복의 확률 |
|---------------------------------------|------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|
| 일반, 모든 16 서버 간에 분산 | 100%                               | 100%                                | 0%                                  | 0%                                  | 0%                                  |
| 서버 3 개를 구분합니다.           | 100%                               | 100%                                | 99.8%                               | 99.8%                               | 99.8%                               |

## <a name="frequently-asked-questions"></a>질문과 대답

### <a name="can-i-delimit-some-volumes-but-not-others"></a>일부 볼륨 중 반면를 구분할 수 있나요?

예 볼륨에 할당을 구분할 것인지 여부를 선택할 수 있습니다.

### <a name="does-delimited-allocation-change-how-drive-replacement-works"></a>구분 기호로 분리 된 할당 드라이브 교체의 작동 원리를 변경 되나요?

아니요, 일반 할당와 동일 하 게 됩니다.

## <a name="see-also"></a>참조

- [저장소 공간 다이렉트 개요](storage-spaces-direct-overview.md)
- [저장소 공간 다이렉트의 내결함성](storage-spaces-fault-tolerance.md)

## <a name="appendix"></a>부록

이 스크립트에는 볼륨에 할당 되는 방식을 확인할 수 있습니다.

를 사용 하려면 위에서 설명한 대로 복사/붙여넣기 및 다른 이름으로 저장 `Get-VirtualDiskFootprintBySSU.ps1`합니다.

```PowerShell
Function ConvertTo-PrettyCapacity {
    Param (
        [Parameter(
            Mandatory = $True,
            ValueFromPipeline = $True
            )
        ]
    [Int64]$Bytes,
    [Int64]$RoundTo = 0
    )
    If ($Bytes -Gt 0) {
        $Base = 1024
        $Labels = ("bytes", "KB", "MB", "GB", "TB", "PB", "EB", "ZB", "YB")
        $Order = [Math]::Floor( [Math]::Log($Bytes, $Base) )
        $Rounded = [Math]::Round($Bytes/( [Math]::Pow($Base, $Order) ), $RoundTo)
        [String]($Rounded) + " " + $Labels[$Order]
    }
    Else {
        "0"
    }
    Return
}

Function Get-VirtualDiskFootprintByStorageFaultDomain {

    ################################################
    ### Step 1: Gather Configuration Information ###
    ################################################

    Write-Progress -Activity "Get-VirtualDiskFootprintByStorageFaultDomain" -CurrentOperation "Gathering configuration information..." -Status "Step 1/4" -PercentComplete 00

    $ErrorCannotGetCluster = "Cannot proceed because 'Get-Cluster' failed."
    $ErrorNotS2DEnabled = "Cannot proceed because the cluster is not running Storage Spaces Direct."
    $ErrorCannotGetClusterNode = "Cannot proceed because 'Get-ClusterNode' failed."
    $ErrorClusterNodeDown = "Cannot proceed because one or more cluster nodes is not Up."
    $ErrorCannotGetStoragePool = "Cannot proceed because 'Get-StoragePool' failed."
    $ErrorPhysicalDiskFaultDomainAwareness = "Cannot proceed because the storage pool is set to 'PhysicalDisk' fault domain awareness. This cmdlet only supports 'StorageScaleUnit', 'StorageChassis', or 'StorageRack' fault domain awareness."

    Try  {
        $GetCluster = Get-Cluster -ErrorAction Stop
    }
    Catch {
        throw $ErrorCannotGetCluster
    }

    If ($GetCluster.S2DEnabled -Ne 1) {
        throw $ErrorNotS2DEnabled
    }

    Try  {
        $GetClusterNode = Get-ClusterNode -ErrorAction Stop
    }
    Catch {
        throw $ErrorCannotGetClusterNode
    }

    If ($GetClusterNode | Where State -Ne Up) {
        throw $ErrorClusterNodeDown
    }

    Try {
        $GetStoragePool = Get-StoragePool -IsPrimordial $False -ErrorAction Stop
    }
    Catch {
        throw $ErrorCannotGetStoragePool
    }

    If ($GetStoragePool.FaultDomainAwarenessDefault -Eq "PhysicalDisk") {
        throw $ErrorPhysicalDiskFaultDomainAwareness
    }

    ###########################################################
    ### Step 2: Create SfdList[] and PhysicalDiskToSfdMap{} ###
    ###########################################################

    Write-Progress -Activity "Get-VirtualDiskFootprintByStorageFaultDomain" -CurrentOperation "Analyzing physical disk information..." -Status "Step 2/4" -PercentComplete 25

    $SfdList = Get-StorageFaultDomain -Type ($GetStoragePool.FaultDomainAwarenessDefault) | Sort FriendlyName # StorageScaleUnit, StorageChassis, or StorageRack

    $PhysicalDiskToSfdMap = @{} # Map of PhysicalDisk.UniqueId -> StorageFaultDomain.FriendlyName
    $SfdList | ForEach {
        $StorageFaultDomain = $_
        $_ | Get-StorageFaultDomain -Type PhysicalDisk | ForEach {
            $PhysicalDiskToSfdMap[$_.UniqueId] = $StorageFaultDomain.FriendlyName
        }
    }

    ##################################################################################################
    ### Step 3: Create VirtualDisk.FriendlyName -> { StorageFaultDomain.FriendlyName -> Size } Map ###
    ##################################################################################################

    Write-Progress -Activity "Get-VirtualDiskFootprintByStorageFaultDomain" -CurrentOperation "Analyzing virtual disk information..." -Status "Step 3/4" -PercentComplete 50

    $GetVirtualDisk = Get-VirtualDisk | Sort FriendlyName

    $VirtualDiskMap = @{}

    $GetVirtualDisk | ForEach {
        # Map of PhysicalDisk.UniqueId -> Size for THIS virtual disk
        $PhysicalDiskToSizeMap = @{}
        $_ | Get-PhysicalExtent | ForEach {
            $PhysicalDiskToSizeMap[$_.PhysicalDiskUniqueId] += $_.Size
        }
        # Map of StorageFaultDomain.FriendlyName -> Size for THIS virtual disk
        $SfdToSizeMap = @{}
        $PhysicalDiskToSizeMap.keys | ForEach {
            $SfdToSizeMap[$PhysicalDiskToSfdMap[$_]] += $PhysicalDiskToSizeMap[$_]
        }
        # Store
        $VirtualDiskMap[$_.FriendlyName] = $SfdToSizeMap
    }

    #########################
    ### Step 4: Write-Out ###
    #########################

    Write-Progress -Activity "Get-VirtualDiskFootprintByStorageFaultDomain" -CurrentOperation "Formatting output..." -Status "Step 4/4" -PercentComplete 75

    $Output = $GetVirtualDisk | ForEach {
        $Row = [PsCustomObject]@{}

        $VirtualDiskFriendlyName = $_.FriendlyName
        $Row | Add-Member -MemberType NoteProperty "VirtualDiskFriendlyName" $VirtualDiskFriendlyName

        $TotalFootprint = $_.FootprintOnPool | ConvertTo-PrettyCapacity
        $Row | Add-Member -MemberType NoteProperty "TotalFootprint" $TotalFootprint

        $SfdList | ForEach {
            $Size = $VirtualDiskMap[$VirtualDiskFriendlyName][$_.FriendlyName] | ConvertTo-PrettyCapacity
            $Row | Add-Member -MemberType NoteProperty $_.FriendlyName $Size
        }

        $Row
    }

    # Calculate width, in characters, required to Format-Table
    $RequiredWindowWidth = ("TotalFootprint").length + 1 + ("VirtualDiskFriendlyName").length + 1
    $SfdList | ForEach {
        $RequiredWindowWidth += $_.FriendlyName.Length + 1
    }

    $ActualWindowWidth = (Get-Host).UI.RawUI.WindowSize.Width

    If (!($ActualWindowWidth)) {
        # Cannot get window width, probably ISE, Format-List
        Write-Warning "Could not determine window width. For the best experience, use a Powershell window instead of ISE"
        $Output | Format-Table
    }
    ElseIf ($ActualWindowWidth -Lt $RequiredWindowWidth) {
        # Narrower window, Format-List
        Write-Warning "For the best experience, try making your PowerShell window at least $RequiredWindowWidth characters wide. Current width is $ActualWindowWidth characters."
        $Output | Format-List
    }
    Else {
        # Wider window, Format-Table
        $Output | Format-Table
    }
}

Get-VirtualDiskFootprintByStorageFaultDomain
```
