---
title: 서버에 대 한 성능 기록
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/0s/2018
Keywords: Storage Spaces Direct
ms.localizationpriority: medium
ms.openlocfilehash: 33fd62376e9769c23fc6b00eefde9a9b95eb4650
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/01/2018
ms.locfileid: "1894252"
---
# <a name="performance-history-for-servers"></a>서버에 대 한 성능 기록

> Windows Server 내부 인 미리 보기에 적용 됩니다.

이 하위 항목 [저장소 공간 직접에 대 한 성능 기록](performance-history.md) 의 서버에 대 한 수집 된 성능 기록 자세하게에서 설명 합니다. 성능 기록은 클러스터의 모든 서버에 대해 사용할 수 있습니다.

   > [!NOTE]
   > 아래에 있는 서버에 대 한 성능 기록을 수집할 수 없습니다. 서버가 다시 시작 되 면 컬렉션을 자동으로 재개 합니다.

## <a name="series-names-and-units"></a>계열 이름 및 단위

이러한 시리즈 가능한 모든 서버에 대 한 수집 됩니다.

| 시리즈                           | Unit    |
|----------------------------------|---------|
| `clusternode.cpu.usage`          | % |
| `clusternode.cpu.usage.guest`    | % |
| `clusternode.cpu.usage.host`     | % |
| `clusternode.memory.total`       |  바이트   |
| `clusternode.memory.available`   |  바이트   |
| `clusternode.memory.usage`       |  바이트   |
| `clusternode.memory.usage.guest` |  바이트   |
| `clusternode.memory.usage.host`  |  바이트   |

또한 시리즈를와 같은 드라이브 `physicaldisk.size.total` 서버 및와 같은 네트워크 어댑터 시리즈에 연결 된 모든 가능한 드라이브에 대해 집계 된 `networkadapter.bytes.total` 은 서버에 연결 하는 모든 적합 한 네트워크 어댑터에 대해 집계 됩니다.

## <a name="how-to-interpret"></a>해석 하는 방법

| 시리즈                           | 해석 하는 방법                                                      |
|----------------------------------|-----------------------------------------------------------------------|
| `clusternode.cpu.usage`          | 유휴 하지 않은 프로세서 시간의 백분율입니다.                        |
| `clusternode.cpu.usage.guest`    | 게스트 (가상 컴퓨터) 제안에 사용 되는 프로세서 시간의 백분율입니다. |
| `clusternode.cpu.usage.host`     | 호스트 제안에 사용 되는 프로세서 시간의 백분율입니다.                    |
| `clusternode.memory.total`       | 서버의 총 실제 메모리입니다.                              |
| `clusternode.memory.available`   | 서버에 사용 가능한 메모리                                   |
| `clusternode.memory.usage`       | 서버 (사용할 수 없음) 할당 된 메모리입니다.                   |
| `clusternode.memory.usage.guest` | 게스트 (가상 컴퓨터) 제안에 할당 된 메모리입니다.               |
| `clusternode.memory.usage.host`  | 호스트 제안에 할당 된 메모리입니다.                                  |

## <a name="where-they-come-from"></a>가져올 위치

`cpu.*` 시리즈 Hyper-v 사용 하도록 설정 여부에 따라 다른 성능 카운터를 수집 합니다.

Hyper-v 사용 하는 경우:

| 시리즈                           | 원본 카운터 |
|----------------------------------|----------------|
| `clusternode.cpu.usage`          | `Hyper-V Hypervisor Logical Processor` > `_Total` > `% Total Run Time`      |
| `clusternode.cpu.usage.guest`    | `Hyper-V Hypervisor Virtual Processor` > `_Total` > `% Total Run Time`      |
| `clusternode.cpu.usage.host`     | `Hyper-V Hypervisor Root Virtual Processor` > `_Total` > `% Total Run Time` |

사용 하는 `% Total Run Time` 카운터 성능 기록 모든 사용 현황 특성을 보장 합니다.

Hyper-v 사용 하지 않는 경우:

| 시리즈                           | 원본 카운터 |
|----------------------------------|----------------|
| `clusternode.cpu.usage`          | `Processor` > `_Total` > `% Processor Time` |
| `clusternode.cpu.usage.guest`    | *0* |
| `clusternode.cpu.usage.host`     | *총 사용 현황와 동일* |

불완전 한 동기화도 불구 하 고 `clusternode.cpu.usage` 는 항상 `clusternode.cpu.usage.host` plus `clusternode.cpu.usage.guest`합니다.

같은 주의와 `clusternode.cpu.usage.guest` 의 합은 항상 `vm.cpu.usage` 호스트 서버에 있는 모든 가상 컴퓨터에 대 한 합니다.

`memory.*` 시리즈는 (출시 예정).

  > [!NOTE]
  > 카운터 하지 샘플링 하는 전체 간격을 통해 측정 됩니다. 예: 서버 유휴 상태에 대 한 경우 9 초 하지만 급격히 증가 하는 100 %CPU 10 초에서 해당 `clusternode.cpu.usage` 기록 되는 10%로 평균이 10 초 간격 중입니다. 이렇게 하면 해당 성능 기록 모든 활동 캡처하고 소음을 강력한 합니다.

## <a name="usage-in-powershell"></a>PowerShell에서 사용 현황

[Get-clusternode](https://docs.microsoft.com/powershell/module/failoverclusters/get-clusternode) cmdlet을 사용 하십시오.

```PowerShell
Get-ClusterNode <Name> | Get-ClusterPerf
```

## <a name="see-also"></a>참고 항목

- [저장소 공간 직접에 대 한 성능 기록](performance-history.md)
