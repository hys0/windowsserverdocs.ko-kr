---
title: 저장소 공간 다이렉트에 대 한 중첩 된 복원 력
ms.prod: windows-server-threshold
ms.author: jgerend
ms.manager: dansimp
ms.technology: storagespaces
ms.topic: article
author: cosmosdarwin
ms.date: 11/06/2018
ms.openlocfilehash: 206d5d19ec55774f9055e7265d4c87d276c60590
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879574"
---
# <a name="nested-resiliency-for-storage-spaces-direct"></a>저장소 공간 다이렉트에 대 한 중첩 된 복원 력

> 적용 대상: Windows Server 2019

중첩 된 복원 력은의 새로운 기능 [저장소 공간 다이렉트](storage-spaces-direct-overview.md) 두 서버 클러스터를 저장소 가용성, 따라서 사용자, 앱의 손실 없이 한 번에 여러 하드웨어 오류를 견딜 수 있도록 하는 Windows Server 2019에 및 가상 머신을 계속 중단 없이 실행 합니다. 이 항목에서는 작동 방식을 설명, 가장 자주 묻는 질문 시작 하기 위한 단계별 지침 및 답변을 제공 합니다.

## <a name="prerequisites"></a>사전 요구 사항

### <a name="green-checkmark-iconmedianested-resiliencysupportedpng-consider-nested-resiliency-if"></a>![녹색 확인 표시 아이콘입니다.](media/nested-resiliency/supported.png) 경우에 중첩 된 복원 력을 고려 합니다.

- 클러스터가는 Windows Server 2019; 실행 및
- 클러스터에 정확히 2 개 서버 노드

### <a name="red-x-iconmedianested-resiliencyunsupportedpng-you-cant-use-nested-resiliency-if"></a>![빨간색 X 아이콘입니다.](media/nested-resiliency/unsupported.png) 경우에 중첩 된 복원 력을 사용할 수 없습니다.

- 클러스터가는 Windows Server 2016 실행 또는
- 클러스터에 3 개 이상의 서버 노드

## <a name="why-nested-resiliency"></a>이유는 중첩 된 복원 력

중첩 된 복원 력을 사용 하는 볼륨 수 **동시에 여러 하드웨어 오류가 발생 하는 경우에 온라인 상태이 고 액세스할 수 있는 유지**, 클래식 달리 [양방향 미러링을](storage-spaces-fault-tolerance.md) 복원 력. 예를 들어, 두 드라이브는 동시에 실패 하는 경우, 한 서버가 다운 되 고 드라이브 오류가 발생 하면 중첩 된 복원 력을 사용 하는 볼륨 온라인 하 게 액세스할 수 있는 유지 됩니다. 하이퍼 수렴 형 인프라에 대 한 앱 및 virtual machines;에 대 한 가동 시간 향상 파일 서버 워크 로드의 경우 즉, 사용자에 해당 파일에 중단 없이 액세스할 수 있습니다.

![저장소 가용성](media/nested-resiliency/storage-availability.png)

단점은는 중첩 된 복원 력 **용량 효율성 클래식 양방향 미러링을 보다 낮은**, 즉 약간 적은 범위로 사용 가능한 공간을 확보 합니다. 자세한 내용은 참조는 [용량 효율성](#capacity-efficiency) 아래 섹션.

## <a name="how-it-works"></a>작동 방법

### <a name="inspiration-raid-51"></a>영감: RAID 5 + 1

RAID 5 + 1는 중첩 된 복원 력 이해에 대 한 유용한 배경을 제공 하는 분산된 저장소 복원 력 설정 된 형식입니다. Raid에서 RAID 5에서 제공 하는 각 서버에서 로컬 복원 력 5 + 1 또는 *단일 패리티*단일 드라이브의 손실 로부터 보호 합니다. 그런 다음, 복원 력 RAID-1에서 제공 하는 추가 또는 *양방향 미러링을*, 서버 손실 로부터 보호 하기 위해 두 서버 간에 합니다.

![RAID 5 + 1](media/nested-resiliency/raid-51.png)

### <a name="two-new-resiliency-options"></a>두 가지 새로운 복원 력 옵션

Windows Server 2019에서 저장소 공간 다이렉트는 특수 한 RAID 하드웨어 필요 없이 소프트웨어에 구현 하는 두 가지 새로운 복원 력 옵션을 제공 합니다.

- **중첩 된 양방향 미러입니다.** 각 서버에서 양방향 미러링을에서 지역 복원 력을 제공 하는 두 서버 간에 양방향 미러링을에서 추가 복원 력을 제공 하는 다음을 각 서버에 두 복사본을 사용 하 여 네 방향 미러 기본적으로 것입니다. 중첩 된 양방향 미러링은 인재 성능 제공: 모든 복사본에 쓰기 이동 하 고 모든 복사본에서 읽기를 제공 합니다.

  ![중첩 된 양방향 미러](media/nested-resiliency/nested-two-way-mirror.png)

- **중첩 된 미러 가속 패리티입니다.** 위의에서 양방향 미러링을 결합 중첩 중첩 패리티가 있습니다. 각 서버 내에서 대부분의 데이터에 대 한 로컬 복원 력 단일 제공 됩니다 [산술 비트 패리티](storage-spaces-fault-tolerance.md#parity), 양방향 미러링을 사용 하는 새로운 최신 쓰기를 제외 하 고 있습니다. 그런 다음 추가 서버 간의 양방향 미러링을 통해 모든 데이터에 대 한 복원 력을 제공 됩니다. 패리티 작동 미러 가속에 대 한 자세한 내용은 참조 하세요. [패리티 미러 가속](https://docs.microsoft.com/windows-server/storage/refs/mirror-accelerated-parity)합니다.

  ![중첩 된 미러 가속 패리티](media/nested-resiliency/nested-mirror-accelerated-parity.png)

### <a name="capacity-efficiency"></a>용량 효율성

용량 효율성은 사용 가능한 공간의 비율이 [볼륨 공간](plan-volumes.md#choosing-the-size-of-volumes)입니다. 복원 력으로 높기 때문에 용량 오버 헤드를 설명 하 고 선택 하는 복원 력 옵션에 따라 달라 집니다. 간단한 예로, 양방향 미러링 하는 동안 복원 력 용량이 100% 효율적인 (1TB의 데이터는 실제 저장소 용량을 1TB 등록) 하지 않고 데이터를 저장은 50% 효율적인 (의 데이터는 2TB의 실제 저장소 용량을 1TB)입니다.

- **중첩 된 양방향 미러** 복사본 4 개를 쓰는 모든 항목의 의미를 1TB 데이터를 저장 해야 4TB의 실제 저장소 용량입니다. 간소는 매력적이 긴 하지만 25% 용량 효율성 중첩된 양방향 미러 복원 력 옵션 저장소 공간 다이렉트의 가장 낮은 수준입니다.

- **미러 가속 패리티 중첩** 약 35%-40%, 두 가지 요인에 따라 달라 지는 더 높은 용량 효율성을 달성: 각 서버에 미러 및 패리티 볼륨에 대해 지정한 조합 드라이브 용량의 수입니다. 이 표에서 일반적인 구성에 대 한 조회를 제공 합니다.

  | 서버당 용량 드라이브 | 10% 미러 | 20% 미러 | 30% 미러 |
  |----------------------------|------------|------------|------------|
  | 4                          | 35.7%      | 34.1%      | 32.6%      |
  | 5                          | 37.7%      | 35.7%      | 33.9%      |
  | 6                          | 39.1%      | 36.8%      | 34.7%      |
  | 7+                         | 40.0%      | 37.5%      | 35.3%      |

  > [!NOTE]
  > **원하는 경우, 전체 수학 예가 다음과 같습니다.** 두 서버의 각 6 용량 드라이브 있고 10GB 미러 및 패리티의 90GB 구성 된 하나의 100GB 볼륨을 만들 것을 가정 합니다. 양방향 미러 서버 지역 효율성이 50.0%를 10GB 미러 데이터의 의미 20gb 각 서버에 저장 합니다. 두 서버, 미러는 총 공간은 40GB입니다. 서버 로컬 단일 패리티에이 경우 5/6 = 83.3% 효율적인 패리티 데이터 90GB 의미는 각 서버에 저장할 108 GB입니다. 두 서버, 미러는 총 공간은 216 GB입니다. 총 공간이 따라서 [(10GB / 50.0%) + (90GB / 83.3%)] × 2 = 256 GB, 39.1% 전체에 대 한 용량 효율성입니다.

클래식 2 방향 미러링: (약 50%)의 용량 효율성 미러 가속 패리티를 중첩 된 (최대 40%) 매우 다릅니다. 요구 사항에 따라 약간 낮은 용량 효율성 저장소 가용성을 크게 증가 가치가 수도 있습니다. 중첩 된 복원 력 볼륨과 동일한 클러스터 내의 클래식 양방향 미러 볼륨을 혼합할 수 있으므로 복원 력 볼륨을 선택 합니다.

![균형을 유지](media/nested-resiliency/tradeoff.png)

## <a name="usage-in-powershell"></a>PowerShell에서 사용

중첩 된 복원 력 볼륨을 만들려면 PowerShell에서 친숙 한 저장소 cmdlet을 사용할 수 있습니다.

### <a name="step-1-create-storage-tier-templates"></a>1단계: 저장소 계층 템플릿 만들기

먼저 사용 하 여 새 저장소 계층 템플릿 만들기를 `New-StorageTier` cmdlet. 이 작업을 한 번 수행 해야 하 고 만든 모든 새 볼륨 그런 다음 이러한 템플릿을 참조할 수입니다. 지정는 `-MediaType` 용량 드라이브 및 필요에 따라는 `-FriendlyName` 세요. 다른 매개 변수를 수정 하지 마십시오.

용량 드라이브 하드 디스크 드라이브 (HDD) 인 경우 관리자 권한으로 PowerShell을 시작 하 고 실행 합니다.

```PowerShell 
# For mirror
New-StorageTier -StoragePoolFriendlyName S2D* -FriendlyName NestedMirror -ResiliencySettingName Mirror -MediaType HDD -NumberOfDataCopies 4

# For parity
New-StorageTier -StoragePoolFriendlyName S2D* -FriendlyName NestedParity -ResiliencySettingName Parity -MediaType HDD -NumberOfDataCopies 2 -PhysicalDiskRedundancy 1 -NumberOfGroups 1 -FaultDomainAwareness StorageScaleUnit -ColumnIsolation PhysicalDisk 
``` 

용량 드라이브는 SSD (반도체 드라이브)를 설정 합니다 `-MediaType` 에 `SSD` 대신 합니다. 다른 매개 변수를 수정 하지 마십시오.

> [!TIP]
> 성공적으로 만들어지고 계층 확인 `Get-StorageTier`합니다.

### <a name="step-2-create-volumes"></a>2단계: 볼륨 만들기

다음을 사용 하 여 새 볼륨을 만듭니다는 `New-Volume` cmdlet.

#### <a name="nested-two-way-mirror"></a>중첩 된 양방향 미러

중첩 된 양방향 미러를 사용 하려면 참조는 `NestedMirror` 템플릿 계층 및 크기를 지정 합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.

```PowerShell
New-Volume -StoragePoolFriendlyName S2D* -FriendlyName Volume01 -StorageTierFriendlyNames NestedMirror -StorageTierSizes 500GB
```

#### <a name="nested-mirror-accelerated-parity"></a>중첩 된 미러 가속 패리티

중첩 된 미러 가속 패리티를 사용 하려면 둘 다를 참조 합니다 `NestedMirror` 및 `NestedParity` 템플릿 계층 및 볼륨의 각 부분에 대 한 두 가지 크기를 지정 (미러 먼저 패리티 초)입니다. 예를 들어, 20% 중첩된 양방향 미러 및 80%는 하나의 500GB 볼륨을 만들려면 실행 패리티 중첩 되어 있습니다.

```PowerShell
New-Volume -StoragePoolFriendlyName S2D* -FriendlyName Volume02 -StorageTierFriendlyNames NestedMirror, NestedParity -StorageTierSizes 100GB, 400GB
```

### <a name="step-3-continue-in-windows-admin-center"></a>3단계: Windows Admin Center 진행

중첩 된 복원 력을 사용 하는 볼륨에 나타납니다 [Windows Admin Center](https://docs.microsoft.com/windows-server/manage/windows-admin-center/understand/windows-admin-center) 아래 스크린샷과 같이 명확한 레이블과 함께 합니다. 를 만든 후에 관리 하 고 있는 다른 볼륨에 저장소 공간 다이렉트와 마찬가지로 Windows Admin Center 사용 하 여 모니터링할 수 있습니다.

![](media/nested-resiliency/windows-admin-center.png)

### <a name="optional-extend-to-cache-drives"></a>선택 사항: 캐시 드라이브를 확장 합니다.

해당 기본 설정을 사용 하 여 중첩 된 복원 력, 동시에 여러 용량 드라이브 손실 또는 서버만 및 동시에 단일 용량 드라이브 보호합니다. 이 보호를 확장할 [드라이브 캐시](understand-the-cache.md) 는 추가 고려 사항에: 캐시 드라이브 읽기를 자주 제공 하기 때문에 *쓰고* 에 대 한 캐싱 *여러* 용량 드라이브 를 다른 서버가 다운 된 경우 캐시 드라이브의 손실을 허용할 수 있는 경우 확인 하는 유일한 방법은 단순히 쓰기를 캐시 하지 하도록 이지만 성능에 미치는 영향입니다.

이 시나리오를 해결 하기 위해 자동으로 두 서버 클러스터의 한 서버가 다운 되었거나 때 쓰기 캐싱을 사용 하지 않도록 설정 하 고 다음 서버를 백업 후 쓰기 캐싱을 다시 설정 하는 옵션은 저장소 공간 다이렉트 제공 합니다. 성능 영향을 주지 않고 일상적인 다시 시작을 허용 하려면 30 분에 대 한 서버 다운 될 때까지 캐싱이 비활성화 되지를 작성 합니다.

이 동작 (선택 사항)을 설정 하려면 관리자 권한으로 PowerShell을 시작 하 고 실행 합니다.

```PowerShell
Get-StorageSubSystem Cluster* | Set-StorageHealthSetting -Name "System.Storage.NestedResiliency.DisableWriteCacheOnNodeDown.Enabled" -Value "True"
```

로 설정 되 면 `True`, 캐시 동작:

| 상황                       | 캐시 동작                           | 캐시 드라이브 손실을 허용할 수 있습니까? |
|---------------------------------|------------------------------------------|--------------------------------|
| 두 서버 등록                 | 캐시 읽기 및 쓰기, 전체 성능 | 예                            |
| 서버가 처음 30 분 동안 다운   | 캐시 읽기 및 쓰기, 전체 성능 | 아니요 (일시적)               |
| 첫 번째 30 분 후          | 성능에 영향을 캐시에만 읽기   | 예                            |

## <a name="frequently-asked-questions"></a>질문과 대답

### <a name="can-i-convert-an-existing-volume-between-two-way-mirror-and-nested-resiliency"></a>양방향 미러 복원 력 중첩된 사이의 기존 볼륨을 변환할 수 있나요?

아니요, 볼륨은 복원 력 형식 간에 변환할 수 없습니다. Windows Server 2019에 새 배포에 대 한 요구 사항에 맞는 최상의 복원 력 유형을 미리 결정 합니다. Windows Server 2016에서 업그레이드 하는 경우 중첩 된 복원 력을 사용 하 여 새 볼륨을 만들 수 있습니다, 그리고 데이터 마이그레이션 및 다음 이전 볼륨을 삭제 합니다.

### <a name="can-i-use-nested-resiliency-with-multiple-types-of-capacity-drives"></a>여러 종류의 용량 드라이브를 사용 하 여 중첩 된 복원 력을 사용할 수 있습니까?

예, 지정는 `-MediaType` 각 계층 적절 하 게 하는 동안 [1 단계](#step-1-create-storage-tier-templates) 위에. 예를 들어, NVMe, SSD 및 HDD 동일한 클러스터에서 사용 하 여는 NVMe 캐시 제공 뒤의 두 개 용량을 제공 하는 동안: 설정 합니다 `NestedMirror` 계층 `-MediaType SSD` 및 `NestedParity` 계층을 `-MediaType HDD`입니다. 이 경우에 HDD 드라이브의 수에 따라 달라 집니다 패리티 용량 효율성을 서버당 그 중 4 개 이상 필요한 note 합니다.

### <a name="can-i-use-nested-resiliency-with-3-or-more-servers"></a>3 개 이상의 서버를 사용 하 여 중첩 된 복원 력을 사용할 수 있습니까?

아니요,만 사용 하 여 중첩 된 복원 력 클러스터 정확히 2 개 서버에 있는 경우.

### <a name="how-many-drives-do-i-need-to-use-nested-resiliency"></a>드라이브는 몇 개입니까 중첩 된 복원 력 사용 하나요?

저장소 공간 다이렉트에 대 한 필수 드라이브의 최소 번호가 서버 노드 당 4 용량 드라이브와 서버 노드 (해당 되는 경우) 당 2 캐시 드라이브입니다. 이 Windows Server 2016에서 변경 되지 않습니다. 중첩 된 복원 력에 대 한 추가 요구 사항은 없습니다 및 너무 예약 용량에 권장 되는 변경 되지 않습니다.

### <a name="does-nested-resiliency-change-how-drive-replacement-works"></a>중첩 된 복원 력 드라이브 교체의 작동 원리를 변경 되나요?

아니요.

### <a name="does-nested-resiliency-change-how-server-node-replacement-works"></a>중첩 된 복원 력 서버 노드 교체의 작동 원리를 변경 되나요?

아니요. 서버 노드 및 해당 드라이브를 대체 하려면이 순서를 따릅니다.

1. 보내는 메일 서버에 있는 드라이브를 사용 중지
2. 클러스터에 해당 드라이브를 사용 하 여 새 서버 추가
3. 저장소 풀은 균형 다시 맞추기
4. 보내는 메일 서버와 해당 드라이브가 제거

참조를 [서버를 제거](remove-servers.md) 항목입니다.

## <a name="see-also"></a>참조

- [저장소 공간 다이렉트 개요](storage-spaces-direct-overview.md)
- [저장소 공간 다이렉트의 내결함성 이해](storage-spaces-fault-tolerance.md)
- [저장소 공간 다이렉트 볼륨 계획](plan-volumes.md)
- [저장소 공간 다이렉트에서 볼륨 만들기](create-volumes.md)
