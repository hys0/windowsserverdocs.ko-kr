---
title: 스토리지 공간 다이렉트 캐시 이해
ms.assetid: 69b1adc0-ee64-4eed-9732-0fb216777992
ms.prod: windows-server
ms.author: cosdar
manager: dongill
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 07/17/2019
ms.localizationpriority: medium
ms.openlocfilehash: f275e7657fc1e5d9ab982726c5b9b9adee381830
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85473470"
---
# <a name="understanding-the-cache-in-storage-spaces-direct"></a>스토리지 공간 다이렉트 캐시 이해

>적용 대상: Windows Server 2019, Windows Server 2016

[스토리지 공간 다이렉트](storage-spaces-direct-overview.md) 는 저장소 성능을 최대화 하는 기본 제공 서버 쪽 캐시를 제공 합니다. 이는 크고 영구적인 실시간 읽기 */* 쓰기 캐시입니다. 스토리지 공간 다이렉트 사용 하도록 설정 되 면 캐시가 자동으로 구성 됩니다. 대부분의 경우 수동 관리가 필요 하지 않습니다.
캐시 작동 방식은 존재 하는 드라이브의 유형에 따라 달라 집니다.

다음 비디오는 스토리지 공간 다이렉트에 대 한 캐싱 작동 방법 및 기타 디자인 고려 사항에 대해 자세히 설명 합니다.

<strong>스토리지 공간 다이렉트 설계 고려 사항</strong><br>(20 분)<br>
<iframe src="https://channel9.msdn.com/Blogs/windowsserver/Design-Considerations-for-Storage-Spaces-Direct/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

## <a name="drive-types-and-deployment-options"></a>드라이브 유형 및 배포 옵션

현재 스토리지 공간 다이렉트는 다음과 같은 세 가지 유형의 저장 장치에서 작동 합니다.

<table>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/NVMe-100px.png">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            NVMe (비휘발성 메모리 Express)
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/SSD-100px.png">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            SATA/SAS SSD (반도체 드라이브)
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/HDD-100px.png">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            HDD (하드 디스크 드라이브)
        </td>
    </tr>
</table>

이러한 항목은 "모두-플래시" 및 "하이브리드"의 두 가지 범주로 그룹화 하는 6 가지 방법으로 결합 될 수 있습니다.

### <a name="all-flash-deployment-possibilities"></a>모든-플래시 배포 가능성

모든 플래시 배포는 저장소 성능의 극대화를 목표로 하며, HDD (회전 하드 디스크 드라이브)를 포함 하지 않습니다.

![모두-플래시-배포-가능성](media/understand-the-cache/All-Flash-Deployment-Possibilities.png)

### <a name="hybrid-deployment-possibilities"></a>하이브리드 배포 가능성

하이브리드 배포는 성능과 용량의 균형을 유지 하거나 용량을 최대화 하 고, HDD (회전 하드 디스크 드라이브)를 포함 하는 것을 목표로 합니다.

![하이브리드 배포-가능성](media/understand-the-cache/Hybrid-Deployment-Possibilities.png)

## <a name="cache-drives-are-selected-automatically"></a>캐시 드라이브가 자동으로 선택 됩니다.

여러 유형의 드라이브가 포함 된 배포에서 스토리지 공간 다이렉트은 캐싱에 "가장 빠른" 유형의 모든 드라이브를 자동으로 사용 합니다. 나머지 드라이브는 용량에 사용됩니다.

"가장 빠름" 유형은 다음 계층에 따라 결정 됩니다.

![드라이브 유형-계층 구조](media/understand-the-cache/Drive-Type-Hierarchy.png)

예를 들어 NVMe 및 Ssd가 있는 경우 NVMe는 Ssd에 대해 캐시 됩니다.

Ssd 및 Hdd이 있는 경우 Ssd는 Hdd를 캐시 합니다.

   >[!NOTE]
   > 캐시 드라이브는 사용 가능한 저장소 용량에 영향을 주지 않습니다. 캐시에 저장 된 모든 데이터도 다른 곳에 저장 되거나 단계가 취소 됩니다. 즉, 배포의 총 원시 저장소 용량은 용량 드라이브의 합계입니다.

모든 드라이브가 동일한 유형인 경우 자동으로 캐시가 구성 되지 않습니다. Endurance 드라이브를 수동으로 구성 하 여 동일한 유형의 하위 endurance 드라이브에 대해 캐시할 수 있습니다. 자세한 내용은 [수동 구성](#manual-configuration) 섹션을 참조 하세요.

   >[!TIP]
   > 모든 NVMe 또는 모든 SSD 배포에서 특히 매우 작은 규모의 경우 캐시에 "소비한" 드라이브가 없으면 저장소 효율성이 향상 될 수 있습니다.

## <a name="cache-behavior-is-set-automatically"></a>캐시 동작이 자동으로 설정 됨

캐시 동작은에 대해 캐시 되는 드라이브의 유형에 따라 자동으로 결정 됩니다. Ssd의 NVMe 캐싱과 같이 반도체 드라이브에 대해 캐시 하는 경우 쓰기만 캐시 됩니다. 하드 디스크 드라이브 (예: Hdd에 대 한 Ssd 캐싱)를 캐시 하는 경우 읽기와 쓰기가 모두 캐시 됩니다.

![캐시-읽기-쓰기 동작](media/understand-the-cache/Cache-Read-Write-Behavior.png)

### <a name="write-only-caching-for-all-flash-deployments"></a>모든 플래시 배포에 대 한 쓰기 전용 캐싱

NVMe 또는 Ssd (반도체 드라이브)에 대해 캐시 하는 경우 쓰기만 캐시 됩니다. 이렇게 하면 많은 쓰기 및 재작성이 캐시에 병합 될 수 있으며, 필요에 따라 필요에 따라 단계를 취소 하 여 용량 드라이브에 대 한 누적 트래픽을 줄이고 수명을 연장 하므로 용량 드라이브에 대 한 마모를 줄일 수 있습니다. 따라서 캐시에 대해 [더 endurance 쓰기에 최적화](http://whatis.techtarget.com/definition/DWPD-device-drive-writes-per-day) 된 드라이브를 선택 하는 것이 좋습니다. 용량 드라이브는 더 낮은 쓰기 endurance 수 있습니다.

읽기는 플래시의 수명에 크게 영향을 주지 않으며, 반도체 드라이브는 일반적으로 낮은 읽기 대기 시간을 제공 하기 때문에 읽기는 캐시 되지 않습니다. 해당 데이터는 아직 준비 되지 않은 데이터를 기록한 경우를 제외 하 고는 용량 드라이브에서 직접 제공 됩니다. 이렇게 하면 캐시를 전적으로 쓰기 전용으로 설정할 수 있으므로 효과가 극대화 됩니다.

이로 인해 쓰기 대기 시간과 같은 쓰기 특성이 캐시 드라이브에 의해 결정 되는 반면, 읽기 특성은 용량 드라이브에 의해 결정 됩니다. 둘 다 일관적이 고 예측 가능 하며 균일 합니다.

### <a name="readwrite-caching-for-hybrid-deployments"></a>하이브리드 배포에 대 한 읽기/쓰기 캐싱

Hdd (하드 디스크 드라이브)에 대해 캐시 하는 경우 읽기 *와* 쓰기가 모두 캐시 되어 두 가지 모두에 대해 플래시와 같은 대기 시간 (보통 ~ 10 배)을 제공 합니다. 읽기 캐시는 최근 액세스를 위해 최근 및 자주 읽기 데이터를 저장 하 고 Hdd에 대 한 임의 트래픽을 최소화 합니다. (검색 및 회전 지연으로 인해 HDD에 대 한 임의 액세스로 인해 발생 하는 대기 시간 및 손실 된 시간은 매우 큽니다.) 쓰기는 대량을 흡수 하 여 이전 처럼 쓰기를 병합 하 고, 다시 쓰고, 용량 드라이브에 대 한 누적 트래픽을 최소화 하기 위해 캐시 됩니다.

스토리지 공간 다이렉트는 작업 (예: 가상 머신)에서 가져온 실제 IO가 무작위로 수행 되는 경우에도 순차적으로 보이는 디스크에 IO 패턴을 에뮬레이트 하기 위해 준비를 취소 하기 전에 임의화 쓰기를 취소 하는 알고리즘을 구현 합니다. 이렇게 하면 Hdd에 대 한 IOPS 및 처리량이 극대화 됩니다.

### <a name="caching-in-deployments-with-drives-of-all-three-types"></a>세 유형의 드라이브가 있는 배포의 캐싱

세 유형의 드라이브가 모두 있는 경우 NVMe 드라이브는 Ssd 및 Hdd 모두에 대 한 캐싱을 제공 합니다. 이 동작은 위에서 설명한 것과 같습니다. 쓰기 전용은 Ssd에 대해 캐시 되 고 읽기와 쓰기는 모두 Hdd에 대해 캐시 됩니다. Hdd에 대 한 캐싱의 부담이 캐시 드라이브에 고르게 분산 됩니다.

## <a name="summary"></a>요약

이 표에는 캐싱에 사용 되는 드라이브, 용량에 사용 되는 드라이브 및 각 배포 가능성에 대 한 캐싱 동작이 요약 되어 있습니다.

| 배포     | 캐시 드라이브                        | 용량 드라이브 | 캐시 동작 (기본값)  |
| -------------- | ----------------------------------- | --------------- | ------------------------- |
| 모든 NVMe         | 없음 (선택 사항: 수동으로 구성) | NVMe            | 쓰기 전용 (구성 된 경우)  |
| 모든 SSD          | 없음 (선택 사항: 수동으로 구성) | SSD             | 쓰기 전용 (구성 된 경우)  |
| NVMe + SSD       | NVMe                                | SSD             | 쓰기 전용                  |
| NVMe + HDD       | NVMe                                | HDD             | 읽기 + 쓰기                |
| SSD + HDD        | SSD                                 | HDD             | 읽기 + 쓰기                |
| NVMe + SSD + HDD | NVMe                                | SSD + HDD       | HDD의 경우 읽기 + 쓰기, SSD의 경우 쓰기 전용  |

## <a name="server-side-architecture"></a>서버 쪽 아키텍처

캐시는 드라이브 수준에서 구현 됩니다. 한 서버 내의 개별 캐시 드라이브는 동일한 서버 내의 하나 이상의 용량 드라이브에 바인딩됩니다.

캐시는 Windows 소프트웨어 정의 저장소 스택의 나머지 부분에 있으므로 저장소 공간 또는 내결함성과 같은 개념을 인식 하지 않아도 됩니다. Windows에 표시 되는 "하이브리드" (파트 플래시, 파트 디스크) 드라이브를 만드는 것으로 간주할 수 있습니다. 실제 하이브리드 드라이브와 마찬가지로 실제 미디어의 더 빠르고 느린 부분 사이에서 핫 및 콜드 데이터를 실시간으로 이동 하는 것은 외부에 거의 보이지 않습니다.

스토리지 공간 다이렉트의 복원 력이 서버 수준 이상이 면 (데이터 복사본이 항상 다른 서버에 기록 되 고 (서버당 최대 하나의 복사본) 캐시에 있는 데이터는 캐시에 없는 데이터와 동일한 복원 력을 활용할 수 있습니다.

![캐시-서버 측 아키텍처](media/understand-the-cache/Cache-Server-Side-Architecture.png)

예를 들어 3 방향 미러링을 사용 하는 경우 데이터의 복사본 3 개는 캐시에 배치 되는 다른 서버에 기록 됩니다. 나중에 준비 되었는지 여부에 관계 없이 세 개의 복사본이 항상 존재 합니다.

## <a name="drive-bindings-are-dynamic"></a>드라이브 바인딩이 동적입니다.

캐시와 용량 드라이브 간의 바인딩은 1:1 ~ 1:12 이상으로 비율을 가질 수 있습니다. 이는 드라이브를 추가 또는 제거 하는 경우와 같이 드라이브를 추가 또는 제거할 때마다 동적으로 조정 됩니다. 즉, 원할 때마다 캐시 드라이브나 용량 드라이브를 독립적으로 추가할 수 있습니다.

![동적 바인딩](media/understand-the-cache/Dynamic-Binding.gif)

최대 용량을 용량으로 설정 하는 것이 좋습니다. 예를 들어 4 개의 캐시 드라이브가 있는 경우 7 또는 9 보다 8 개의 용량 드라이브 (1:2 비율)를 사용 하 여 훨씬 더 많은 성능을 경험할 수 있습니다.

## <a name="handling-cache-drive-failures"></a>캐시 드라이브 오류 처리

캐시 드라이브에 오류가 발생 하면 아직 준비 되지 않은 모든 쓰기는 *로컬 서버*에서 손실 됩니다. 즉, 다른 서버에 있는 다른 복사본에만 존재 합니다. 다른 드라이브 오류 발생 후와 마찬가지로 저장소 공간은 남아 있는 복사본을 문의 하 여 자동으로 복구할 수 있습니다.

잠시 동안 손실 된 캐시 드라이브에 바인딩된 용량 드라이브가 비정상으로 표시 됩니다. 캐시 리바인딩이 발생 하 고 (자동) 데이터 복구가 완료 된 후 (자동), 정상으로 표시 되는 것이 다시 시작 됩니다.

이 시나리오에서는 성능을 유지 하기 위해 서버당 두 개의 캐시 드라이브가 필요 합니다.

![처리-오류](media/understand-the-cache/Handling-Failure.gif)

이후 다른 드라이브 교체와 마찬가지로 캐시 드라이브를 교체할 수 있습니다.

   >[!NOTE]
   > 추가 기능 카드 (AIC) 또는 M. 2 폼 팩터 인 NVMe를 안전 하 게 교체 하려면이 기능을 해제 해야 할 수 있습니다.

## <a name="relationship-to-other-caches"></a>다른 캐시와의 관계

Windows 소프트웨어 정의 저장소 스택에는 관련이 없는 다른 캐시가 몇 가지 있습니다. 예제에는 저장소 공간 다시 쓰기 캐시 및 클러스터 공유 볼륨 (CSV) 메모리 내 읽기 캐시가 포함 됩니다.

스토리지 공간 다이렉트를 사용 하면 저장소 공간 나중 쓰기 캐시를 기본 동작에서 수정할 수 없습니다. 예를 들어, **새 볼륨** cmdlet의 **-writecachesize** 와 같은 매개 변수는 사용할 수 없습니다.

CSV 캐시를 사용 하도록 선택할 수도 있고 그렇지 않을 수도 있습니다. 스토리지 공간 다이렉트에서는 기본적으로 해제 되어 있지만이 항목에서 설명 하는 새 캐시와 충돌 하지 않습니다. 특정 시나리오에서는 중요 한 성능 향상을 제공할 수 있습니다. 자세한 내용은 [CSV 캐시를 사용 하도록 설정 하는 방법](../../failover-clustering/failover-cluster-csvs.md#enable-the-csv-cache-for-read-intensive-workloads-optional)을 참조 하세요.

## <a name="manual-configuration"></a>수동 구성

대부분의 배포에서는 수동 구성이 필요 하지 않습니다. 필요한 경우 다음 섹션을 참조 하세요.

설치 후 캐시 장치 모델을 변경 해야 하는 경우 [상태 관리 서비스 개요](../../failover-clustering/health-service-overview.md#supported-components-document)에 설명 된 대로 상태 관리 서비스의 지원 구성 요소 문서를 편집 합니다.

### <a name="specify-cache-drive-model"></a>캐시 드라이브 모델 지정

모든 드라이브가 동일한 유형 (예: 모든 드라이브 또는 모든-NVMe 배포)을 배포 하는 경우 Windows에서 write endurance와 같은 특성을 동일한 유형의 드라이브 간에 자동으로 구분할 수 없으므로 캐시가 구성 되지 않습니다.

Endurance 드라이브를 사용 하 여 동일한 유형의 하위 endurance 드라이브에 대해 캐시 하려면 **enable-clusters2d** cmdlet의 **-CacheDeviceModel** 매개 변수와 함께 사용할 드라이브 모델을 지정할 수 있습니다. 스토리지 공간 다이렉트 사용 하도록 설정 되 면 해당 모델의 모든 드라이브가 캐싱에 사용 됩니다.

   >[!TIP]
   > 모델 문자열이 **PhysicalDisk**의 출력에 표시 된 그대로 정확 하 게 일치 하는지 확인 합니다.

####  <a name="example"></a>예제

먼저 실제 디스크의 목록을 가져옵니다.

```PowerShell
Get-PhysicalDisk | Group Model -NoElement
```

다음은 몇 가지 예제 출력입니다.

```
Count Name
----- ----
    8 FABRIKAM NVME-1710
   16 CONTOSO NVME-1520
```

그런 다음 캐시 장치 모델을 지정 하 여 다음 명령을 입력 합니다.

```PowerShell
Enable-ClusterS2D -CacheDeviceModel "FABRIKAM NVME-1710"
```

PowerShell에서 **PhysicalDisk** 를 실행 하 고 **사용** 속성이 **"Journal"** 임을 확인 하 여 의도 한 드라이브가 캐싱에 사용 되는지 확인할 수 있습니다.

### <a name="manual-deployment-possibilities"></a>수동 배포 가능성

수동 구성에서 다음과 같은 배포 가능성을 사용할 수 있습니다.

![Exotic-배포 가능성](media/understand-the-cache/Exotic-Deployment-Possibilities.png)

### <a name="set-cache-behavior"></a>캐시 동작 설정

캐시의 기본 동작을 재정의할 수 있습니다. 예를 들어 모든 플래시 배포 에서도 캐시 읽기로 설정할 수 있습니다. 작업에 적합 하지 않은 것이 확실 하지 않으면 동작을 수정 하지 않는 것이 좋습니다.

동작을 재정의 하려면 **ClusterStorageSpacesDirect** cmdlet 및 해당 **-cachemodessd** 및 **-cachemodessd** 매개 변수를 사용 합니다. **Cachemodessd** 매개 변수는 반도체 드라이브에 대해 캐시할 때 캐시 동작을 설정 합니다. **Cachemodehdd** 매개 변수는 하드 디스크 드라이브에 대해 캐시할 때 캐시 동작을 설정 합니다. 스토리지 공간 다이렉트를 사용 하도록 설정한 후 언제 든 지이 작업을 수행할 수 있습니다.

**ClusterStorageSpacesDirect** 를 사용 하 여 동작이 설정 되었는지 확인할 수 있습니다.

#### <a name="example"></a>예제

먼저 스토리지 공간 다이렉트 설정을 가져옵니다.

```PowerShell
Get-ClusterStorageSpacesDirect
```

다음은 몇 가지 예제 출력입니다.

```
CacheModeHDD : ReadWrite
CacheModeSSD : WriteOnly
```

그런 후 다음을 수행합니다.

```PowerShell
Set-ClusterStorageSpacesDirect -CacheModeSSD ReadWrite

Get-ClusterS2D
```

다음은 몇 가지 예제 출력입니다.

```
CacheModeHDD : ReadWrite
CacheModeSSD : ReadWrite
```

## <a name="sizing-the-cache"></a>캐시 크기 조정

응용 프로그램 및 워크 로드의 작업 집합 (지정 된 시간에 적극적으로 읽거나 작성 되는 데이터)에 맞게 캐시 크기를 조정 해야 합니다.

이는 하드 디스크 드라이브를 사용 하는 하이브리드 배포에서 특히 중요 합니다. 활성 작업 집합이 캐시 크기를 초과 하거나 활성 작업 집합이 너무 빠르게 상태가 경우 읽기 캐시 누락이 증가 하 고 쓰기를 더 적극적으로 취소 해야 합니다. 저하 전반적인 성능이 향상 됩니다.

Windows에서 기본 제공 성능 모니터 (PerfMon.exe) 유틸리티를 사용 하 여 캐시 누락의 속도를 검사할 수 있습니다. 특히 **클러스터 저장소 하이브리드 디스크** 카운터 집합의 **Cache 누락 읽기/초** 를 배포의 전체 읽기 IOPS와 비교할 수 있습니다. 각 "하이브리드 디스크"는 하나의 용량 드라이브에 해당 합니다.

예를 들어 4 개의 용량 드라이브로 바인딩된 2 개의 캐시 드라이브는 서버당 "하이브리드 디스크" 개체 인스턴스 4 개를 생성 합니다.

![성능-모니터](media/understand-the-cache/PerfMon.png)

유니버설 규칙은 없지만 캐시가 너무 많으면 캐시가의 크기가 부족 수 있으며 캐시 드라이브를 추가 하 여 캐시를 확장 하는 것을 고려해 야 합니다. 원할 때마다 캐시 드라이브나 용량 드라이브를 독립적으로 추가할 수 있습니다.

## <a name="additional-references"></a>추가 참조

- [드라이브 및 복원 력 유형 선택](choosing-drives.md)
- [내결함성 및 스토리지 효율성](storage-spaces-fault-tolerance.md)
- [하드웨어 요구 사항 스토리지 공간 다이렉트](storage-spaces-direct-hardware-requirements.md)
