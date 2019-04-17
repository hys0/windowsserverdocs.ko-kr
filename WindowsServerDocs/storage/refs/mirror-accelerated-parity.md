---
title: "미러-가속 패리티"
ms.prod: windows-server-threshold
ms.author: gawatu
ms.manager: masriniv
ms.technology: storage-file-systems
ms.topic: article
author: gawatu
ms.date: 8/9/2017
ms.assetid: 
ms.openlocfilehash: a94bc4f8251d0f1fb18c3dad95c2915d3346c69a
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="mirror-accelerated-parity"></a>미러-가속 패리티
>적용 대상: Windows Server 2016

저장소 공간은 미러와 패리티라는 두 가지 기본 기술을 사용하여 데이터에 대한 내결함성을 제공할 수 있습니다. [저장소 공간 다이렉트](../storage-spaces/storage-spaces-direct-overview.md)에서 ReFS가 도입한 미러-가속 패리티를 사용하여 미러 및 패러티 복원을 모두 사용하는 볼륨을 만들 수 있습니다. 미러-가속 패리티는 성능 저하 없이 저렴하고 공간 효율적인 저장소를 제공합니다. 

![미러-가속 패리티 볼륨](media/mirror-accelerated-parity/Mirror-Accelerated-Parity-Volume.png)


## <a name="background"></a>배경
미러 및 패리티 복원 체계는 기본적으로 다른 저장소 및 성능 특징을 갖고 있습니다.
- 미러 복원은 사용자가 빠른 쓰기 성능을 확보할 수 있게 하지만 각 복사본의 데이터를 복제하는 것은 공간 효율적이지 않습니다. 
- 한편 패리티는 모든 쓰기에 대해 패리티를 다시 계산해야 하므로 임의 쓰기 성능이 저하됩니다. 그러나 패리티는 사용자가 더 공간 효율적으로 데이터를 저장할 수 있게 합니다. (공간 효율성에 대해 자세히 ![알아보기](../storage-spaces/Storage-Spaces-Fault-Tolerance.md)). 

따라서 패리티는 향상된 저장소 용량 이용률을 제공하는 반면 미러는 성능에 민감한 저장소를 제공하는 경향이 있습니다. 미러-가속 패리티에서 ReFS는 각 복원 유형의 이점을 활용하여 단일 볼륨 내에 두 복원 체계를 모두 결합함으로써 용량 효율적이고 성능에 민감한 저장소를 제공합니다.


## <a name="data-rotation-on-mirror-accelerated-parity"></a>미러-가속 패리티에서 데이터 순환

ReFS는 미러와 패리티 간에 데이터를 실시간으로 순환시킵니다. 이를 통해 들어오는 쓰기가 빠르게 미러에 써진 다음 패리티로 순환되어 효율적으로 저장됩니다. 이 과정에서 들어오는 IO는 미러에서 빠르게 처리되고 콜드 데이터는 패리티에 효율적으로 저장되어 동일한 볼륨 내에서 최적의 성능과 저렴한 저장소를 모두 제공합니다. 

미러와 패리티 간에 데이터를 순환시키기 위해 ReFS는 논리적으로 볼륨을 64 MiB 영역(순환 단위)으로 나눕니다. 아래 이미지는 영역으로 나뉜 미러-가속 패리티 볼륨을 보여 줍니다. 

![저장소 컨테이너가 있는 미러-가속 패리티 볼륨](media/mirror-accelerated-parity/Mirror-Accelerated-Parity-Volume-with-Storage-Containers.png)

미러가 지정한 용량 수준에 도달하면 ReFS가 미러에서 패리티로 전체 영역 순환을 시작합니다. ReFS는 미러에서 패리티로 데이터를 즉시 이동하는 대신, 데이터에 최적의 성능을 계속 제공할 수 있도록 기다렸다가 미러에 데이터를 최대한 오래 보관합니다(아래 “IO 성능” 참조). 

미러에서 패리티로 데이터를 이동할 때 데이터를 읽고 패리티 인코딩을 계산한 다음 해당 데이터를 패리티에 씁니다. 아래 애니메이션에서는 순환 중 삭제 코딩된 영역으로 변환되는 3방향 미러된 영역을 사용하여 이를 보여 줍니다.

![미러-가속 패리티 순환](media/mirror-accelerated-parity/Container-Rotation.gif)

## <a name="io-on-mirror-accelerated-parity"></a>미러-가속 패리티의 IO
### <a name="io-behavior"></a>IO 동작
**쓰기:** ReFS가 세 가지 방식으로 들어오는 쓰기를 처리합니다.
1.  **미러에 쓰기:** 
     - **a.** 들어오는 쓰기가 미러에서 기존 데이터를 수정할 경우 ReFS가 데이터를 바로 수정합니다. 
     - **b.** 들어오는 쓰기가 새로운 쓰기이고 ReFS가 미러에서 이 쓰기를 처리하기에 충분한 여유 공간을 찾을 수 있는 경우 ReFS가 미러에 씁니다. 

![미러에 쓰기](media/mirror-accelerated-parity/Write-to-Mirror.png)

2. **미러에 쓰기, 패리티에서 재할당됨:**
    - **a.** 들어오는 쓰기가 패리티에 있는 데이터를 수정하고 ReFS가 미러에서 들어오는 쓰기를 처리하기에 충분한 여유 공간을 찾을 수 있는 경우 ReFS가 먼저 패리티의 이전 데이터를 무효화한 다음 미러에 씁니다. 이 무효화는 패리티에 대한 쓰기 성능 향상에 도움이 되는 빠르고 저렴한 메타데이터 작업입니다.

![재할당된 쓰기](media/mirror-accelerated-parity/Reallocated-Write.png)

3. **패리티에 쓰기:**
    - **a.** ReFS가 미러에서 충분한 여유 공간을 찾지 못할 경우 ReFS가 패리티에 새 데이터를 쓰거나 패리티의 기존 데이터를 직접 수정합니다. 아래 “성능 최적화” 세션에서는 패리티에 쓰기를 최소화하는 데 도움이 되는 참고 자료를 제공합니다.

![패리티에 쓰기](media/mirror-accelerated-parity/Write-to-Parity.png)

**읽기:** ReFS가 관련 데이터가 들어 있는 계층에서 직접 읽습니다. 패리티가 HDD로 생성된 경우 저장소 공간 다이렉트의 캐시가 이 데이터를 캐시하여 이후 읽기를 가속화합니다. 

> [!NOTE]
> 읽기 때문에 ReFS가 미러 계층으로 데이터를 다시 순환시키지는 않습니다. 

### <a name="io-performance"></a>IO 성능:

**쓰기:** 위에 설명된 쓰기 형식마다 고유의 성능 특징이 있습니다. 대체로 미러 계층에 쓰기가 재할당된 쓰기보다 훨씬 더 빠르며, 재할당된 쓰기는 패리티 계층에 직접 쓰기보다 현저히 더 빠릅니다. 이 관계는 아래의 부등호로 설명됩니다. 


- **미러 계층 > 재할당된 쓰기 >> 패리티 계층**


**읽기:** 패리티에서 읽을 때 의미 있는 부정적인 성능 영향이 없습니다.
- 미러와 패리티가 동일한 미디어 유형으로 생성된 경우 읽기 성능이 같습니다. 
- 미러와 패리티가 미러된 SSD, 패리티 HDD 등 서로 다른 미디어 유형으로 생성되는 경우 [저장소 공간 다이렉트의 캐시](../storage-spaces/understand-the-cache.md)로 핫 데이터를 캐시하여 패리티에서 모든 읽기를 가속화할 수 있습니다.

## <a name="refs-compaction"></a>ReFS 압축
이번 가을의 반기 릴리스에서 ReFS는 90% 이상 찬 미러-가속 패리티 볼륨에 대한 성능을 크게 향상하는 압축을 도입합니다. 

**배경:** 이전에는 미러-가속 패리티 볼륨이 가득 차면 이러한 볼륨의 성능이 저하되기도 했습니다. 볼륨 초과 작업 시간 동안 핫 데이터와 콜드 데이터가 섞이기 때문에 성능이 저하됩니다. 이는 핫 데이터가 사용할 수 있는 미러의 공간을 콜드 데이터가 차지하기 때문에 미러에 더 적은 핫 데이터가 저장될 수 있음을 의미합니다. 미러에 직접 쓰기가 재할당된 쓰기보다 훨씬 더 빠르고 차수가 패리티에 직접 쓰기보다 더 빠르기 때문에 미러에 핫 데이터 저장은 고성능을 유지하는 데 중요합니다. 따라서 미러에 콜드 데이터가 있으면 ReFS가 미러에 직접 쓰기를 만들 가능성이 줄어들기 때문에 성능에 좋지 않습니다. 

ReFS 압축은 미러에 핫 데이터를 위한 여유 공간을 확보하여 이러한 성능 문제를 해결합니다. 압축은 먼저 미러와 패리티의 모든 데이터를 패리티에 통합합니다. 이를 통해 볼륨 내의 조각화가 줄고 미러의 주소 지정 가능한 공간은 늘어납니다. 더 중요한 것은 이 과정을 통해 ReFS가 핫 데이터를 미러로 다시 통합할 수 있다는 것입니다.
-   새 쓰기가 들어오면 미러에서 처리됩니다. 또한 새로 쓴 핫 데이터는 미러에 상주합니다. 
-   패리티의 데이터에 수정 쓰기가 적용될 때 ReFS가 재할당된 쓰기를 만들고 이 쓰기도 미러에서 처리됩니다. 결과적으로 압축 중 패리티로 이동된 핫 데이터가 미러에 다시 재할당됩니다. 

## <a name="performance-optimizations"></a>성능 최적화

>[!IMPORTANT]
>미러-가속 패리티의 Hyper-V 워크로드의 경우 쓰기 작업이 많은 VHD가 여러 디렉터리에 분산될 때 ReFS는 최고의 성능을 제공합니다. 따라서 최적의 성능을 위해서는 동일한 하위 디렉터리에 쓰기 작업이 많은 다수의 VHD를 배치하지 않는 것이 좋습니다.   

### <a name="performance-counters"></a>성능 카운터: 

ReFS는 미러-가속 패리티 성능 평가에 도움이 되도록 성능 카운터를 유지합니다. 
-   패리티에 쓰기에 설명된 것과 같이 ReFS가 미러에서 여유 공간을 찾을 수 없을 때 패리티에 직접 씁니다. 이러한 현상은 대개 ReFS가 패리티에 데이터를 순환시킬 수 있는 것보다 빠르게 미러된 계층이 가득 찰 때 발생합니다. 즉, ReFS 순환이 수집 속도를 따라갈 수 없습니다. 아래의 성능 카운터는 ReFS가 패리티에 직접 쓸 때를 식별합니다.
```
ReFS\Data allocations slow tier/sec
ReFS\Metadata allocations slow tier/sec
```
-   이러한 카운터가 0이 아닐 경우 이는 ReFS가 미러 밖으로 데이터를 충분히 빠르게 순환하고 있지 않음을 나타냅니다. 이를 완화하는 데 도움이 되도록 순환 강도를 변경하거나 미러된 계층의 크기를 늘릴 수 있습니다.

### <a name="rotation-aggressiveness"></a>순환 강도:
미러가 지정한 용량 임계값에 도달하면 ReFS가 데이터 순환을 시작합니다.
-   이 회전 임계값이 높을수록 미러 계층에 데이터가 더 오래 보관됩니다. 핫 데이터를 미러 계층에 두는 것이 성능에 가장 좋지만 ReFS가 더 많은 양의 들어오는 IO를 효과적으로 처리할 수 없습니다. 
-   값이 낮으면 ReFS가 사전에 데이터 준비를 취소하고 들어오는 IO를 더 잘 수집할 수 있습니다. 이는 보관 저장소 등의 수집량이 많은 워크로드에 적용 가능합니다. 그러나 값이 낮으면 범용 워크로드에 대한 성능이 저하됩니다. 미러 계층 밖으로 데이터를 불필요하게 순환하면 성능이 떨어집니다. 

ReFS는 레지스트리 키로 구성 가능한 이 임계값을 조정하기 위해 튜닝할 수 있는 매개 변수를 지정합니다. **저장소 공간 다이렉트 배포의 각 노드**에 이 레지스트리 키를 구성해야 하며 다시 시작해야 변경 내용이 적용됩니다. 
-   **Key:** HKEY_LOCAL_MACHINE\System\CurrentControlSet\Policies
-   **ValueName (DWORD):** DataDestageSsdFillRatioThreshold
-   **ValueType:** Percentage

이 레지스트리 키를 설정하지 않으면 ReFS가 기본값 85%를 사용합니다.  대부분의 배포에 이 기본값이 권장되며 50% 미만의 값은 권장되지 않습니다. 아래의 PowerShell 명령은 75%의 값으로 이 레지스트리 키를 설정하는 방법을 보여줍니다. 
```
Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Policies -Name DataDestageSsdFillRatioThreshold -Value 75
 ```
 저장소 공간 다이렉트 배포의 각 노드에 걸쳐 이 레지스트리 키를 구성하려면 아래와 같은 PowerShell 명령을 사용할 수 있습니다.
 ```
 $Nodes = 'S2D-01', 'S2D-02', 'S2D-03', 'S2D-04'
 Invoke-Command $Nodes {Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Policies -Name DataDestageSsdFillRatioThreshold -Value 75}
 ```

### <a name="increasing-the-size-of-the-mirrored-tier"></a>미러링된 계층의 크기 늘리기: 
미러된 계층의 크기를 늘리면 ReFS가 작업 집합의 더 큰 부분을 미러에 보관할 수 있습니다. 그러면 ReFS가 미러에 직접 쓸 수 있는 가능성이 커지고 성능이 향상됩니다. 아래의 PowerShell cmdlet은 미러링된 계층의 크기를 늘리는 방법을 보여줍니다.
```
Resize-StorageTier -FriendlyName “Performance” -Size 20GB
Resize-StorageTier -InputObject (Get-StorageTier -FriendlyName “Performance”) -Size 20GB
```
>[!TIP]
>**StorageTier**의 크기를 조정한 이후 **파티션** 및 **볼륨**의 크기를 조정해야 합니다. 자세한 내용 및 예제는 [Resize-Volumes](../storage-spaces/resize-volumes.md)를 참조하세요.

## <a name="creating-a-mirror-accelerated-parity-volume"></a>미러-가속 패리티 볼륨 만들기
아래의 PowerShell cmdlet은 대부분의 워크로드에 권장되는 구성인 20:80의 미러:패리티 비율로 미러-가속 패리티 볼륨을 만듭니다. 자세한 내용과 예는 [저장소 공간 다이렉트에서 볼륨 만들기](../storage-spaces/Create-volumes.md)를 참조하세요.

```
New-Volume – FriendlyName “TestVolume” -FileSystem CSVFS_ReFS -StoragePoolFriendlyName “StoragePoolName” -StorageTierFriendlyNames Performance, Capacity -StorageTierSizes 200GB, 800GB
```

## <a name="see-also"></a>참고 항목

-   [ReFS 개요](refs-overview.md)
-   [ReFS 블록 복제](block-cloning.md)
-   [ReFS 무결성 스트림](integrity-streams.md)
-   [저장소 공간 다이렉트 개요](../storage-spaces/storage-spaces-direct-overview.md)
