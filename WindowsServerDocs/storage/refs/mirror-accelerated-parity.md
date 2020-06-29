---
title: 미러 가속 패리티
ms.prod: windows-server
ms.author: gawatu
manager: masriniv
ms.technology: storage-file-systems
ms.topic: article
author: gawatu
ms.date: 10/17/2018
ms.assetid: ''
ms.openlocfilehash: 3efbc6ae29ddaa4f3a4a4f2a2409bbeb87fec2ed
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475170"
---
# <a name="mirror-accelerated-parity"></a>미러 가속 패리티

>적용 대상: Windows Server 2019, Windows Server 2016

저장소 공간은 미러 및 패리티 라는 두 가지 기본 기술을 사용 하 여 데이터에 대 한 내결함성을 제공할 수 있습니다. [스토리지 공간 다이렉트](../storage-spaces/storage-spaces-direct-overview.md)에서 ReFS는 미러 가속 패리티를 도입 하 여 미러 및 패리티 resiliencies를 모두 사용 하는 볼륨을 만들 수 있습니다. 미러 가속 패리티는 성능 저하 없이 저렴 하 고 공간 효율적인 저장소를 제공 합니다.

![미러-가속-패리티 볼륨](media/mirror-accelerated-parity/Mirror-Accelerated-Parity-Volume.png)

## <a name="background"></a>배경

미러 및 패리티 복원 력 스키마는 근본적으로 다른 저장소 및 성능 특성을 포함 합니다.
- 미러 복원 력을 통해 사용자는 빠른 쓰기 성능을 얻을 수 있지만 각 복사본에 대 한 데이터를 복제 하는 것은 공간 효율성이 크지 않습니다.
- 반면 패리티는 모든 쓰기에 대해 패리티를 다시 계산 해야 하므로 임의 쓰기 성능이 저하 됩니다. 그러나 패리티를 사용 하면 사용자가 더 많은 공간을 효율적으로 데이터를 저장할 수 있습니다. 자세한 내용은 [저장소 공간 내결함성](../storage-spaces/Storage-Spaces-Fault-Tolerance.md)을 참조 하세요.

따라서 패리티는 저장소 용량 사용률을 향상 시킬 수 있는 반면, 성능에 민감한 저장소를 제공 하기 위해 미러가 미리 삭제 됩니다. 미러 가속 패리티에서 ReFS는 각 복원 력 유형의 이점을 활용 하 여 단일 볼륨 내에서 두 복원 체계를 결합 함으로써 용량 효율적이 고 성능이 중요 한 저장소를 모두 제공 합니다.

## <a name="data-rotation-on-mirror-accelerated-parity"></a>미러 가속 패리티의 데이터 회전

ReFS는 실시간으로 미러와 패리티 사이에서 데이터를 적극적으로 회전 합니다. 이렇게 하면 들어오는 쓰기를 빠르게 반영 하 고 패리티에 맞게 회전 하 여 효율적으로 저장할 수 있습니다. 이렇게 하면 들어오는 IO는 미러에서 신속 하 게 처리 되 고 콜드 데이터는 패리티에 효율적으로 저장 되므로 동일한 볼륨 내에서 최적의 성능과 손실 비용 저장소를 모두 제공 합니다.

미러와 패리티 사이에서 데이터를 회전 하기 위해 ReFS는 논리적으로 볼륨을 회전 단위인 64 MiB의 영역으로 나눕니다. 아래 이미지는 지역으로 구분 된 미러 가속 패리티 볼륨을 보여 줍니다.

![미러-가속-패리티-저장소-컨테이너](media/mirror-accelerated-parity/Mirror-Accelerated-Parity-Volume-with-Storage-Containers.png)

미러 계층이 지정 된 용량 수준에 도달 하면 ReFS가 미러에서 패리티로 전체 영역을 회전 하기 시작 합니다. ReFS는 미러에서 패리티로 데이터를 즉시 이동 하는 대신, 가능한 한 오랫동안 데이터를 미러로 대기 하 고 유지 하므로 ReFS는 데이터에 대 한 최적의 성능을 계속 제공할 수 있습니다 (아래의 "IO 성능" 참조).

데이터를 미러에서 패리티로 이동 하는 경우 데이터를 읽고, 패리티 인코딩을 계산 하 고, 해당 데이터를 패리티에 기록 합니다. 아래 애니메이션은 회전 중에 지우기 코딩 된 영역으로 변환 되는 3 방향 미러된 영역을 사용 하 여이를 보여 줍니다.

![미러-가속-패리티-회전](media/mirror-accelerated-parity/Container-Rotation.gif)

## <a name="io-on-mirror-accelerated-parity"></a>미러 가속 패리티의 IO
### <a name="io-behavior"></a>IO 동작
**쓰기:** ReFS 서비스에서 들어오는 쓰기는 다음과 같은 세 가지 방법으로 수행 됩니다.

1.  **미러에 쓰기:**

    - **a.** 들어오는 쓰기가 미러에서 기존 데이터를 수정 하는 경우 ReFS는 현재 위치의 데이터를 수정 합니다.
    - **1b.** 들어오는 쓰기가 새 쓰기가 고 ReFS에서이 쓰기를 처리할 수 있는 충분 한 사용 가능한 공간을 성공적으로 찾으면 ReFS는 미러 서버에 기록 합니다.
    ![쓰기-미러](media/mirror-accelerated-parity/Write-to-Mirror.png)

2. **미러에서 쓰고 패리티에서 다시 할당 합니다.**

    들어오는 쓰기가 패리티 데이터를 수정 하 고 ReFS에서 들어오는 쓰기를 처리할 수 있는 충분 한 사용 가능한 공간을 성공적으로 찾으면 ReFS는 먼저 이전 데이터를 패리티로 무효화 한 다음 미러 서버에 씁니다. 이러한 무효화는 패리티의 쓰기 성능을 의미 있게 향상 시키는 데 도움이 되는 빠르고 저렴 한 메타 데이터 작업입니다.
    ![다시 할당 됨-쓰기](media/mirror-accelerated-parity/Reallocated-Write.png)

3. **패리티에 씁니다.**

    ReFS에서 미러 서버에 충분 한 여유 공간을 찾을 수 없는 경우 ReFS는 패리티에 새 데이터를 쓰거나 패리티의 기존 데이터를 직접 수정 합니다. 아래의 "성능 최적화" 섹션에서는 패리티 쓰기를 최소화 하는 데 도움이 되는 지침을 제공 합니다.
    ![쓰기-패리티](media/mirror-accelerated-parity/Write-to-Parity.png)

**읽기:** ReFS는 관련 데이터를 포함 하는 계층에서 직접 읽습니다. Hdd를 사용 하 여 패리티를 생성 하는 경우 스토리지 공간 다이렉트 캐시는이 데이터를 캐시 하 여 향후 읽기를 가속화 합니다.

> [!NOTE]
> 읽기는 ReFS에서 데이터를 미러 계층으로 다시 회전 시 키 지 않습니다.

### <a name="io-performance"></a>IO 성능

**쓰기:** 위에서 설명한 각 유형의 쓰기에는 고유한 성능 특성이 있습니다. 거의 말하면 미러 계층에 대 한 쓰기는 재할당 된 쓰기 보다 훨씬 빠르지만, 다시 할당 된 쓰기는 패리티 계층에 직접 적용 된 쓰기 보다 훨씬 빠릅니다. 이 관계는 아래와 같지 않습니다.


- **미러 계층 > 다시 할당 쓰기 >> 패리티 계층**


**읽기:** 패리티를 읽을 때에는 의미 있는 부정적인 성능 영향을 주지 않습니다.
- 미러 및 패리티가 동일한 미디어 유형을 사용 하 여 생성 된 경우 읽기 성능은 동일 하 게 됩니다.
- 미러 및 패리티가 다른 미디어 유형 (예: 미러된 Ssd, 패리티 Hdd)을 사용 하 여 생성 된 경우,[스토리지 공간 다이렉트 캐시는](../storage-spaces/understand-the-cache.md) 패리티의 읽기를 가속화 하기 위해 핫 데이터를 캐시 하는 데 도움이 됩니다.

## <a name="refs-compaction"></a>ReFS 압축

이에 해당 하는 반기 릴리스에서 ReFS는 압축을 도입 하 여 90 +% 가득 찬 미러 가속 패리티 볼륨의 성능을 크게 향상 시킵니다.

**배경:** 이전에는 미러 가속 패리티 볼륨이 가득 차서 이러한 볼륨의 성능이 저하 될 수 있습니다. 핫 및 콜드 데이터가 초과 하는 볼륨을 통해 혼합 되어 성능이 저하 됩니다. 즉, 콜드 데이터는 핫 데이터에서 사용할 수 없는 미러의 공간을 차지 하므로 더 작은 핫 데이터를 미러에 저장할 수 있습니다. 미러 서버에 직접 쓰기는 패리티에 직접 기록 하는 것 보다 더 빠르게 다시 할당 된 쓰기와 크기의 순서 보다 훨씬 더 빠르기 때문에 미러 서버에 핫 데이터를 저장 하는 것이 중요 합니다. 따라서 미러에서 콜드 데이터를 사용 하는 것은 ReFS에서 미러에 직접 쓸 수 있는 가능성을 줄여 주므로 성능에 좋지 않습니다.

ReFS 압축은 핫 데이터에 대 한 미러에서 공간을 확보 하 여 이러한 성능 문제를 해결 합니다. 압축은 먼저 미러 및 패리티 모두에서 모든 데이터를 패리티로 통합 합니다. 이를 통해 볼륨 내에서 조각화를 줄이고 미러 서버에서 주소 지정 가능한 공간의 크기를 늘립니다. 보다 중요 한 점은이 프로세스를 통해 ReFS에서 핫 데이터를 다시 미러로 통합할 수 있습니다.
-   새 쓰기가 제공 되는 경우 미러 서버에서 처리 됩니다. 따라서 새로 작성 된 핫 데이터는 미러 서버에 상주 합니다.
-   패리티를 사용 하 여 데이터에 대 한 쓰기를 수정 하는 경우 ReFS는 쓰기를 다시 할당 하므로이 쓰기는 미러 서버 에서도 처리 됩니다. 따라서 압축 중에 패리티로 이동 된 핫 데이터는 다시 미러로 다시 할당 됩니다.

## <a name="performance-optimizations"></a>성능 최적화

>[!IMPORTANT]
> 쓰기 작업이 많은 Vhd를 다른 하위 디렉터리에 배치 하는 것이 좋습니다. ReFS는 디렉터리 및 해당 파일 수준에서 메타 데이터 변경 내용을 작성 하기 때문입니다. 따라서 디렉터리에 쓰기 작업이 많은 파일을 배포 하는 경우 메타 데이터 작업이 더 작고 병렬로 실행 되므로 앱에 대 한 대기 시간이 줄어듭니다.

### <a name="performance-counters"></a>성능 카운터

ReFS는 미러 가속 패리티의 성능을 평가 하는 데 도움이 되는 성능 카운터를 유지 관리 합니다.
- 위의 패리티에 쓰기 섹션에서 설명한 것 처럼 ReFS는 미러에서 사용 가능한 공간을 찾을 수 없을 때 패리티에 직접 기록 합니다. 일반적으로이는 미러된 계층이 ReFS 보다 빠르게 채워질 때 데이터를 패리티로 회전할 수 있는 경우에 발생 합니다. 즉, ReFS 회전은 수집 속도를 유지할 수 없습니다. 아래의 성능 카운터는 ReFS가 패리티에 직접 기록 하는 경우를 식별 합니다.

  ```
  # Windows Server 2016
  ReFS\Data allocations slow tier/sec
  ReFS\Metadata allocations slow tier/sec

  # Windows Server 2019
  ReFS\Allocation of Data Clusters on Slow Tier/sec
  ReFS\Allocation of Metadata Clusters on Slow Tier/sec
  ```

- 이러한 카운터가 0이 아니면 ReFS는 미러 서버에서 데이터를 신속 하 게 회전 하지 않음을 나타냅니다. 이를 줄이기 위해 회전 강도를 변경 하거나 미러된 계층의 크기를 늘릴 수 있습니다.

### <a name="rotation-aggressiveness"></a>회전 강도

미러가 지정 된 용량 임계값에 도달 하면 ReFS에서 데이터를 순환 하기 시작 합니다.
-   이 회전 임계값의 값이 높을수록 ReFS에서 미러 계층의 데이터를 더 오래 보존 합니다. 미러 계층에서 핫 데이터를 유지 하는 것은 성능에 가장 적합 하지만 ReFS는 많은 양의 수신 IO를 효과적으로 처리할 수 없습니다.
-   값이 낮을수록 ReFS에서 데이터를 사전에 디 스테이지 하 고 들어오는 IO를 더 효과적으로 수집할 수 있습니다. 보관 저장소와 같은 수집 집약적 워크 로드에 적용 됩니다. 그러나 값이 낮을수록 범용 작업의 성능이 저하 될 수 있습니다. 미러 계층에서 불필요 하 게 데이터를 회전 하면 성능이 저하 됩니다.

ReFS는 레지스트리 키를 사용 하 여 구성할 수 있는이 임계값을 조정 하기 위해 튜닝할 수 있는 매개 변수를 도입 합니다. 이 레지스트리 키는 **스토리지 공간 다이렉트 배포의 각 노드에서**구성 해야 하며 변경 내용을 적용 하려면 다시 시작 해야 합니다.
-   **키:** HKEY_LOCAL_MACHINE \System\CurrentControlSet\Policies
-   **ValueName (DWORD):** DataDestageSsdFillRatioThreshold
-   **ValueType:** 나타낸

이 레지스트리 키가 설정 되지 않은 경우 ReFS는 기본값 85%를 사용 합니다.  이 기본값은 대부분의 배포에 권장 되며 50% 이하의 값은 권장 되지 않습니다. 아래 PowerShell 명령은 75% 값을 사용 하 여이 레지스트리 키를 설정 하는 방법을 보여 줍니다.
```PowerShell
Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Policies -Name DataDestageSsdFillRatioThreshold -Value 75
 ```
 스토리지 공간 다이렉트 배포의 각 노드에 대해이 레지스트리 키를 구성 하려면 다음 PowerShell 명령을 사용 하면 됩니다.
 ```PowerShell
 $Nodes = 'S2D-01', 'S2D-02', 'S2D-03', 'S2D-04'
 Invoke-Command $Nodes {Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Policies -Name DataDestageSsdFillRatioThreshold -Value 75}
 ```

### <a name="increasing-the-size-of-the-mirrored-tier"></a>미러된 계층의 크기를 늘립니다.

미러된 계층의 크기를 늘리면 ReFS에서 미러에서 작업 집합의 더 큰 부분을 유지할 수 있습니다. 이를 통해 ReFS가 미러에 직접 쓸 수 있는 가능성을 개선 하 여 성능을 향상 시킬 수 있습니다. 아래 PowerShell cmdlet은 미러된 계층의 크기를 늘리는 방법을 보여 줍니다.
```PowerShell
Resize-StorageTier -FriendlyName “Performance” -Size 20GB
Resize-StorageTier -InputObject (Get-StorageTier -FriendlyName “Performance”) -Size 20GB
```
>[!TIP]
>**Storagetier**크기를 조정한 후 **파티션** 및 **볼륨** 의 크기를 조정 해야 합니다. 자세한 내용 및 예제는 [볼륨 크기 조정](../storage-spaces/resize-volumes.md)을 참조 하세요.

## <a name="creating-a-mirror-accelerated-parity-volume"></a>미러 가속 패리티 볼륨 만들기

아래 PowerShell cmdlet은 미러 (패리티 비율 20:80)를 사용 하 여 미러 가속 패리티 볼륨을 만들며, 대부분의 워크 로드에 권장 되는 구성입니다. 자세한 내용 및 예제는 [스토리지 공간 다이렉트에서 볼륨 만들기](../storage-spaces/Create-volumes.md)를 참조 하세요.

```PowerShell
New-Volume – FriendlyName “TestVolume” -FileSystem CSVFS_ReFS -StoragePoolFriendlyName “StoragePoolName” -StorageTierFriendlyNames Performance, Capacity -StorageTierSizes 200GB, 800GB
```

## <a name="additional-references"></a>추가 참조

-   [ReFS 개요](refs-overview.md)
-   [ReFS 블록 복제](block-cloning.md)
-   [ReFS 무결성 스트림](integrity-streams.md)
-   [스토리지 공간 다이렉트 개요](../storage-spaces/storage-spaces-direct-overview.md)
