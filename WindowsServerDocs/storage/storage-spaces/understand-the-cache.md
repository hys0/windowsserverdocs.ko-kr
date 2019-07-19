---
title: 저장소 공간 다이렉트에서 캐시 이해
ms.assetid: 69b1adc0-ee64-4eed-9732-0fb216777992
ms.prod: windows-server-threshold
ms.author: cosdar
ms.manager: dongill
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 07/17/2019
ms.localizationpriority: medium
ms.openlocfilehash: 0050a8931162e37408895ef664293be2349d1bde
ms.sourcegitcommit: 1bc3c229e9688ac741838005ec4b88e8f9533e8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68315005"
---
# <a name="understanding-the-cache-in-storage-spaces-direct"></a>저장소 공간 다이렉트에서 캐시 이해

>적용 대상: Windows Server 2019, Windows Server 2016

[저장소 공간 다이렉트](storage-spaces-direct-overview.md)에는 서버 쪽 캐시가 기본 제공되어 저장소 성능을 극대화합니다. 대용량 실시간 영구 읽기 *및* 쓰기 캐시입니다. 캐시는 저장소 공간 다이렉트를 사용하면 자동으로 구성됩니다. 대부분의 경우에는 수동 관리가 전혀 필요하지 않습니다.
캐시 작동 방식은 보유한 드라이브 유형에 따라 다릅니다.

다음 동영상은 캐시가 저장소 공간 다이렉트에서 어떻게 작동하는지, 다른 디자인 고려 사항은 무엇인지 자세히 설명합니다.

<strong>스토리지 공간 다이렉트 설계 고려 사항</strong><br>(20분)<br>
<iframe src="https://channel9.msdn.com/Blogs/windowsserver/Design-Considerations-for-Storage-Spaces-Direct/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

## <a name="drive-types-and-deployment-options"></a>드라이브 유형 및 배포 옵션

저장소 공간 다이렉트는 현재 세 가지 유형의 저장 장치에서 작동합니다.

<table>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/NVMe-100px.png">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            NVMe(Non-Volatile Memory Express)
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/SSD-100px.png">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            SATA/SAS SSD(솔리드 스테이트 드라이브)
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/HDD-100px.png">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            HDD(하드 디스크 드라이브)
        </td>
    </tr>
</table>

이를 결합하는 경우의 수는 6가지이며, 여기서는 "플래시 전용"과 "하이브리드"의 2가지 카테고리로 그룹화하고 있습니다.

### <a name="all-flash-deployment-possibilities"></a>플래시 전용 배포 시나리오

모든 플래시 배포는 저장소 성능을 극대화하며 회전 HDD(하드 디스크 드라이브)는 포함되어 있지 않습니다.

![플래시 전용 배포 시나리오](media/understand-the-cache/All-Flash-Deployment-Possibilities.png)

### <a name="hybrid-deployment-possibilities"></a>하이브리드 배포 시나리오

하이브리드 배치는 성능과 용량의 균형을 잡거나 용량을 극대화하려는 것으로 회전 HDD(하드 디스크 드라이브)가 포함되어 있습니다.

![하이브리드 배포 시나리오](media/understand-the-cache/Hybrid-Deployment-Possibilities.png)

## <a name="cache-drives-are-selected-automatically"></a>캐시 드라이브 자동 선택

여러 유형의 드라이브를 통한 배치에서 저장소 공간 다이렉트는 자동적으로 캐싱이 "가장 빠른" 유형의 모든 드라이브를 사용합니다. 나머지 드라이브는 용량에 사용됩니다.

"가장 빠른" 유형은 다음 계층 구조에 따라 결정됩니다.

![드라이브 유형 계층 구조](media/understand-the-cache/Drive-Type-Hierarchy.png)

예를 들어, NVMe와 SSD가 있는 경우 NVMe가 SSD의 캐시를 수행합니다.

SSD와 HDD가 있는 경우 SSD가 HDD의 캐시를 수행합니다.

   >[!NOTE]
   > 캐시 드라이브는 사용할 수 있는 저장소 용량을 제공하지 않습니다. 또한 캐시에 저장된 모든 데이터는 다른 위치에 저장되거나 디스테이징됩니다. 다시 말해 배포의 총 원시 저장소 용량은 용량 드라이브들만 합계를 낸 것입니다.

모든 드라이브가 동일한 유형일 경우 캐시가 자동으로 구성되지 않습니다. 내구성이 높은 드라이브를 수동으로 구성하는 옵션을 통해 동일한 유형이면서 내구성이 낮은 드라이브의 캐시를 수행하도록 할 수 있습니다. 자세한 내용은 [수동 구성](#manual-configuration) 섹션을 참조하세요.

   >[!TIP]
   > 모든 NVMe 또는 모든 SSD 배치에서 특히 규모가 아주 작을 경우, 캐시에 "소모된" 드라이브가 없으면 저장소 효율성을 크게 개선할 수 있습니다.

## <a name="cache-behavior-is-set-automatically"></a>캐시 동작 자동 설정

캐시 동작은 캐시가 수행되는 드라이브 유형에 따라 자동으로 결정됩니다. SSD에 대한 NVMe 캐싱과 같은 솔리드 스테이트 드라이브 캐싱의 경우에는 쓰기에 대해서만 캐시가 수행됩니다. HDD에 대한 SSD 캐싱과 같은 하드 디스크 드라이브 캐싱의 경우에는 읽기 및 쓰기에 대해 모두 캐시가 수행됩니다.

![캐시 읽기 쓰기 동작](media/understand-the-cache/Cache-Read-Write-Behavior.png)

### <a name="write-only-caching-for-all-flash-deployments"></a>플래시 전용 배포에 대한 쓰기 전용 캐싱

NVMe 또는 SSD와 같은 솔리드 스테이트 드라이브 캐싱의 경우에는 쓰기에 대해서만 캐시가 수행됩니다 이 경우 많은 쓰기 및 다시 쓰기가 캐시에서 병합된 다음 필요할 때만 디스테이징을 진행하여 용량 드라이브에 대한 누적 트래픽을 줄이고 수명을 연장할 수 있기 때문에 용량 드라이브의 마모를 감소시킵니다. 그렇기 때문에 캐시에 대해 [내구성이 높고 쓰기에 최적화된](http://whatis.techtarget.com/definition/DWPD-device-drive-writes-per-day) 드라이브 선택을 권장합니다. 용량 드라이브는 쓰기 내구성이 낮은 편이 합리적일 수 있습니다.

읽기는 플래시의 수명에 크게 영향을 미치지 않으며 보편적으로 솔리드 스테이트 드라이브가 제공하는 읽기 대기 시간은 짧기 때문에, 읽기는 캐시가 수행되지 않고 용량 드라이브에서 직접 제공됩니다(데이터가 너무 최근에 작성되어 디스테이징이 아직 진행되지 않은 경우 제외). 이를 통해 캐시를 온전히 쓰기 전용으로 사용할 수 있게 되어 효율성이 극대화됩니다.

그 결과 쓰기 대기 시간과 같은 쓰기 특성은 캐시 드라이브에 의해 결정되고 읽기 특성은 용량 드라이브에 의해 결정됩니다. 양쪽 모두 일관성 있고 예측 가능하며 균일합니다.

### <a name="readwrite-caching-for-hybrid-deployments"></a>하이브리드 배포에 대한 읽기/쓰기 캐싱

HDD(하드 디스크 드라이브) 캐싱의 경우 읽기 *및* 쓰기의 캐시가 모두 수행되어 양쪽 모두 대기 시간이 짧습니다(보통 10배까지 향상). 읽기 캐시는 최근에 사용되었으며 사용 빈도가 높은 읽기 데이터를 저장하여 액세스를 빠르게 하고 HDD에 대한 임의 트래픽을 최소화합니다. (검색 및 회전 지연으로 인해 HDD에 대 한 임의 액세스로 인해 발생 하는 대기 시간 및 손실 된 시간은 매우 큽니다.) 쓰기는 대량을 흡수 하 여 이전 처럼 쓰기를 병합 하 고, 다시 쓰고, 용량 드라이브에 대 한 누적 트래픽을 최소화 하기 위해 캐시 됩니다.

가상 컴퓨터와 같은 작업에서 오는 IO가 실제로는 임의적이어도 순차적으로 보이는 디스크에 IO 패턴을 에뮬레이트하기 위해, 저장소 공간 다이렉트는 디스테이징 전에 쓰기에 대한 임의 지정을 해제하는 알고리즘을 구현합니다. 이로 인해 IOPS는 물론 HDD 처리량이 극대화됩니다.

### <a name="caching-in-deployments-with-drives-of-all-three-types"></a>3가지 유형을 모두 갖춘 드라이브를 통해 배포할 경우의 캐싱

3가지 유형의 드라이브를 모두 보유하고 있을 경우 NVMe 드라이브는 SSD와 HDD 모두에 대한 캐싱을 제공합니다. 동작은 위에서 설명한 바와 같이 SSD의 경우 쓰기만, HDD는 읽기 및 쓰기 모두 캐시가 수행됩니다. HDD에 대한 캐싱의 부담은 캐시 드라이브 간에 고르게 분산됩니다. 

## <a name="summary"></a>요약

이 표는 캐싱에 사용되는 드라이브, 용량에 사용되는 드라이브, 각 배포 시나리오에 대한 캐싱 동작이 요약되어 있습니다.

| 배포     | 캐시 드라이브                        | 용량 드라이브 | 캐시 동작(기본값)  |
| -------------- | ----------------------------------- | --------------- | ------------------------- |
| 모두 NVMe         | 없음(선택 사항: 수동으로 구성) | NVMe            | 쓰기 전용(구성된 경우)  |
| 모두 SSD          | 없음(선택 사항: 수동으로 구성) | SSD             | 쓰기 전용(구성된 경우)  |
| NVMe + SSD       | NVMe                                | SSD             | 쓰기 전용                  |
| NVMe + HDD       | NVMe                                | HDD             | 읽기 + 쓰기                |
| SSD + HDD        | SSD                                 | HDD             | 읽기 + 쓰기                |
| NVMe + SSD + HDD | NVMe                                | SSD + HDD       | HDD(읽기 + 쓰기), SSD(쓰기 전용)  |

## <a name="server-side-architecture"></a>서버 쪽 아키텍처

캐시는 드라이브 수준에서 구현됩니다. 한 서버 내의 개별 캐시 드라이브는 동일한 서버 내의 하나 또는 여러 개의 용량 드라이브에 바인딩됩니다.

캐시는 나머지 Windows 소프트웨어 정의 저장소 스택보다 하위에 있으므로 저장소 공간이나 내결함성과 같은 개념은 인식하지 않아도 됩니다. "하이브리드"(플래시와 디스크의 혼합) 드라이브를 만든 다음 Windows에 표시하는 것으로 이해하면 됩니다. 실제 하이브리드 드라이브와 마찬가지로 실제 미디어의 빠른 부분과 느린 부분 간 핫 데이터와 콜드 데이터의 실시간 이동은 외부에서는 거의 눈에 띄지 않습니다.

저장소 공간 다이렉트에서의 복원력은 서버 수준 이상이라는 사실을 고려할 때(즉, 데이터 복사본은 항상 다른 여러 서버에 기록되고 서버당 최대 하나의 복사본이 있음) 캐시의 데이터는 캐시에 없는 데이터와 동일한 복원력을 누립니다.

![캐시 서버 쪽 아키텍처](media/understand-the-cache/Cache-Server-Side-Architecture.png)

예를 들어, 3방향 미러링을 사용할 때, 모든 데이터에 대해 3개의 복사본이 다른 서버에 기록되고 그곳의 캐시에 연결됩니다. 이후의 디스테이징 여부와 관계없이 3부의 복사본은 항상 존재합니다.

## <a name="drive-bindings-are-dynamic"></a>동적 드라이브 바인딩

캐시 드라이브와 용량 드라이브 간의 바인딩은 1:1에서 최대 1:12 이상에 이르기까지 어떤 비율로든 가능합니다. 규모 확장이나 오류의 경우처럼 드라이브가 추가 또는 제거될 때마다 동적으로 조정됩니다. 즉 캐시 드라이브 또는 용량 드라이브를 언제든 독립적으로 추가할 수 있습니다.

![동적 바인딩](media/understand-the-cache/Dynamic-Binding.gif)

용량 드라이브의 수를 캐시 드라이브 수의 배수가 되도록 대칭시키는 것이 좋습니다. 예를 들어 캐시 드라이브가 4개인 경우 7개나 9개보다는 8개의 용량 드라이브(1:2 비율)를 사용하는 것이 더 일정한 성능을 보일 것입니다.

## <a name="handling-cache-drive-failures"></a>캐시 드라이브 오류 처리

캐시 드라이브에 장애가 발생하면 쓰기가 아직 디스테이징 되지 않은 경우 *로컬 서버에서* 손실됩니다. 즉 다른 서버에 다른 복사본으로만 존재하게 됩니다. 다른 드라이브 장애와 마찬가지로 저장소 공간은 남아 있는 복사본을 참고하여 자동으로 복구가 가능합니다.

손실된 캐시 드라이브에 바인딩된 용량 드라이브는 잠시 동안 비정상으로 표시됩니다. 그러나 캐시 리바인딩이 발생하고(자동) 데이터 복구가 완료되면(자동) 다시 정상으로 표시됩니다.

이러한 시나리오 때문에 성능 유지를 위해 캐시 드라이브가 서버당 최소 2개 이상 필요한 것입니다.

![처리 오류](media/understand-the-cache/Handling-Failure.gif)

이후 다른 드라이브 교체와 마찬가지로 캐시 드라이브를 교체할 수 있습니다.

   >[!NOTE]
   > 추가 기능 카드(AIC) 또는 M.2 폼 팩터인 NVMe를 안전하게 교체하려면 전원을 꺼야 할 수도 있습니다.

## <a name="relationship-to-other-caches"></a>다른 캐시와의 관계

Windows 소프트웨어 정의 저장소 스택에는 관련 없는 다른 캐시가 여러 가지 있습니다. 예를 들면 저장소 공간 나중 쓰기 캐시, CSV(클러스터 공유 볼륨) 메모리 내 읽기 캐시 등이 있습니다.

저장소 공간 다이렉트를 사용하면 저장소 공간 나중 쓰기 캐시를 기본 동작에서 수정하면 안 됩니다. 예를 들어 **New-Volume** cmdlet에서 **-WriteCacheSize**와 같은 매개 변수는 사용하지 않도록 해야 합니다.

CSV 캐시의 사용 여부는 사용자의 결정에 달려 있습니다. 저장소 공간 다이렉트에서는 사용하지 않는 것이 기본값으로 되어 있지만 어떤 방식으로든 이 항목에서 언급한 새로운 캐시와 충돌하지 않습니다. 특정 시나리오에서는 가치 있는 성능 향상이 제공되기도 합니다. 자세한 내용은 [CSV 캐시를 사용하도록 설정하는 방법](../../failover-clustering/failover-cluster-csvs.md#enable-the-csv-cache-for-read-intensive-workloads-optional)을 참조하십시오.

## <a name="manual-configuration"></a>수동 구성

대부분의 배포에서는 수동 구성이 필요하지 않습니다. 필요한 경우 다음 섹션을 참조 하세요. 

설치 후 캐시 장치 모델을 변경 해야 하는 경우 [상태 관리 서비스 개요](../../failover-clustering/health-service-overview.md#supported-components-document)에 설명 된 대로 상태 관리 서비스의 지원 구성 요소 문서를 편집 합니다.

### <a name="specify-cache-drive-model"></a>캐시 드라이브 모델 지정

모두 NVMe 또는 모두 SSD 배포와 같이 모든 드라이브가 동일한 유형인 배포에서는 캐시가 구성되지 않습니다. 동일한 유형의 드라이브 간에 쓰기 내구성과 같은 특성이 자동으로 구분되지 않기 때문입니다.

동일한 유형의 내구성이 낮은 드라이브에 대해 캐시에 내구성이 높은 드라이브를 사용하려면 **Enable-ClusterS2D** cmdlet의 **-CacheDeviceModel** 매개 변수를 통해 사용할 드라이브 모델을 지정하면 됩니다. 저장소 공간 다이렉트를 사용할 수 있게 되면 해당 모델의 모든 드라이브가 캐싱에 사용됩니다.

   >[!TIP]
   > 모델 문자열이 **Get-PhysicalDisk**의 출력에 나타나는 문자열과 정확히 일치하는지 확인하세요.

####  <a name="example"></a>예제

먼저 실제 디스크의 목록을 가져옵니다.

```PowerShell
Get-PhysicalDisk | Group Model -NoElement
```

다음은 몇 가지 출력 예제입니다.

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

PowerShell에서 **Get-PhysicalDisk**를 실행하고 **사용** 속성에 **"저널"** 이 표시되는지 확인하는 방법으로 사용자가 의도한 드라이브가 캐싱에 사용되고 있는지 확인할 수 있습니다.

### <a name="manual-deployment-possibilities"></a>수동 배포 시나리오

수동 구성을 사용하면 다음과 같은 배포 시나리오가 가능해집니다.

![특이한 배포 시나리오](media/understand-the-cache/Exotic-Deployment-Possibilities.png)

### <a name="set-cache-behavior"></a>캐시 동작 지정

캐시의 기본 동작은 재정의가 가능합니다. 예를 들어 심지어 플래시 전용 배포에서도 읽기 캐시가 수행되도록 설정할 수 있습니다. 기본값이 확실하게 사용자의 작업에 맞지 않는 경우를 제외하고는 동작 수정을 권장하지 않습니다.

동작을 재정의 하려면 **ClusterStorageSpacesDirect** cmdlet 및 해당 **-cachemodessd** 및 **-cachemodessd** 매개 변수를 사용 합니다. **CacheModeSSD** 매개 변수는 솔리드 스테이트 드라이브에 대한 캐싱의 경우 캐시 동작을 설정할 수 있습니다. **CacheModeHDD** 매개 변수는 하드 디스크 드라이브에 대한 캐싱의 경우 캐시 동작을 설정합니다. 이 작업은 저장소 공간 다이렉트 사용이 가능해진 후 언제든지 수행할 수 있습니다.

**ClusterStorageSpacesDirect** 를 사용 하 여 동작이 설정 되었는지 확인할 수 있습니다.

#### <a name="example"></a>예제

먼저 스토리지 공간 다이렉트 설정을 가져옵니다.

```PowerShell
Get-ClusterStorageSpacesDirect
```

다음은 몇 가지 출력 예제입니다.

```
CacheModeHDD : ReadWrite
CacheModeSSD : WriteOnly
```

그런 후에 다음을 수행 합니다.

```PowerShell
Set-ClusterStorageSpacesDirect -CacheModeSSD ReadWrite

Get-ClusterS2D
```

다음은 몇 가지 출력 예제입니다.

```
CacheModeHDD : ReadWrite
CacheModeSSD : ReadWrite
```

## <a name="sizing-the-cache"></a>캐시 크기 조정

캐시의 크기는 응용 프로그램과 작업의 작업 집합, 즉, 지정된 시간에 활발하게 읽기와 쓰기를 하는 모든 데이터를 수용할 수 있어야 합니다.

하드 디스크 드라이브를 통한 하이브리드 배포에서는 특히 중요한 사항입니다. 활성 작업 집합이 캐시 크기를 초과하거나 활성 작업 집합이 너무 빨리 이동하면 읽기 캐시 누락이 증가하고 쓰기에 더욱 적극적인 디스테이징이 필요해져서 전반적인 성능이 저하됩니다.

Windows의 기본 제공 성능 모니터(PerfMon.exe) 유틸리티를 사용하여 캐시 누락 비율을 검사할 수 있습니다. 특히 **클러스터 저장소 하이브리드 디스크** 카운터 집합에서 **1초당 캐시 누락 읽기**를 배포의 전체 읽기 IOPS와 비교할 수 있습니다. 각 "하이브리드 디스크"는 하나의 용량 드라이브에 해당합니다.

예를 들어 4개의 용량 드라이브에 연결된 2개의 캐시 드라이브는 서버당 4개의 "하이브리드 디스크" 개체 인스턴스를 생성합니다.

![성능 모니터](media/understand-the-cache/PerfMon.png)

보편적인 규칙은 없지만 읽기에서 캐시가 누락되는 경우가 너무 많으면 크기가 작은 것일 수도 있으므로 캐시 드라이브를 추가하여 캐시를 확장하는 방법을 고려해야 합니다. 캐시 드라이브 또는 용량 드라이브는 언제든 독립적으로 추가할 수 있습니다.

## <a name="see-also"></a>참조

- [드라이브 및 복원 력 유형 선택](choosing-drives.md)
- [내결함성 및 스토리지 효율성](storage-spaces-fault-tolerance.md)
- [하드웨어 요구 사항 스토리지 공간 다이렉트](storage-spaces-direct-hardware-requirements.md)
