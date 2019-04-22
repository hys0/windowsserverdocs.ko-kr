---
title: 서버에 대 한 성능 기록
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/0s/2018
Keywords: 저장소 공간 다이렉트
ms.localizationpriority: medium
ms.openlocfilehash: 33fd62376e9769c23fc6b00eefde9a9b95eb4650
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820594"
---
# <a name="performance-history-for-servers"></a>서버에 대 한 성능 기록

> 적용 대상: Windows Server Insider Preview

이 하위 항목의 [저장소 공간 다이렉트에 대 한 성능 기록을](performance-history.md) 서버에 대 한 수집 된 성능 기록 세부 정보에 설명 합니다. 성능 기록은 클러스터의 모든 서버에 대해 사용할 수 있습니다.

   > [!NOTE]
   > 성능 기록 아래에 있는 서버에 대해 수집할 수 없습니다. 컬렉션을 고 서버가 다시 시작 되 면 자동으로 재개 합니다.

## <a name="series-names-and-units"></a>계열 이름 및 단위

이 시리즈는 적격 한 모든 서버에 대 한 수집 됩니다.

| 시리즈                           | 단위    |
|----------------------------------|---------|
| `clusternode.cpu.usage`          | % |
| `clusternode.cpu.usage.guest`    | % |
| `clusternode.cpu.usage.host`     | % |
| `clusternode.memory.total`       | 바이트   |
| `clusternode.memory.available`   | 바이트   |
| `clusternode.memory.usage`       | 바이트   |
| `clusternode.memory.usage.guest` | 바이트   |
| `clusternode.memory.usage.host`  | 바이트   |

또한 시리즈와 같은 드라이브 `physicaldisk.size.total` 는 서버 및 네트워크 어댑터 시리즈와 같은 연결 된 모든 적격 드라이브에 대해 집계 된 `networkadapter.bytes.total` 서버에 연결 하는 모든 적합 한 네트워크 어댑터에 대해 집계 됩니다.

## <a name="how-to-interpret"></a>해석 하는 방법

| 시리즈                           | 해석 하는 방법                                                      |
|----------------------------------|-----------------------------------------------------------------------|
| `clusternode.cpu.usage`          | 유휴 상태가 아닌 프로세서 시간의 백분율입니다.                        |
| `clusternode.cpu.usage.guest`    | 게스트 (가상 머신) 요청에 사용 되는 프로세서 시간 비율입니다. |
| `clusternode.cpu.usage.host`     | 호스트 요청에 사용 되는 프로세서 시간 비율입니다.                    |
| `clusternode.memory.total`       | 서버의 총 실제 메모리입니다.                              |
| `clusternode.memory.available`   | 서버의 사용 가능한 메모리입니다.                                   |
| `clusternode.memory.usage`       | 서버 (사용할 수 없음) 할당 된 메모리입니다.                   |
| `clusternode.memory.usage.guest` | 게스트 (가상 머신) 요청에 할당 된 메모리입니다.               |
| `clusternode.memory.usage.host`  | 호스트 요청에 할당 된 메모리입니다.                                  |

## <a name="where-they-come-from"></a>어디에서 생겨날

`cpu.*` 시리즈 Hyper-v 사용 하도록 설정할지 여부에 따라 다양 한 성능 카운터에서 수집 됩니다.

Hyper-v 사용 하는 경우:

| 시리즈                           | 원본 카운터 |
|----------------------------------|----------------|
| `clusternode.cpu.usage`          | `Hyper-V Hypervisor Logical Processor` > `_Total` > `% Total Run Time`      |
| `clusternode.cpu.usage.guest`    | `Hyper-V Hypervisor Virtual Processor` > `_Total` > `% Total Run Time`      |
| `clusternode.cpu.usage.host`     | `Hyper-V Hypervisor Root Virtual Processor` > `_Total` > `% Total Run Time` |

사용 하는 `% Total Run Time` 카운터 성능 기록 특성 모든 사용량을 확인 합니다.

Hyper-v 사용 하지 않는 경우:

| 시리즈                           | 원본 카운터 |
|----------------------------------|----------------|
| `clusternode.cpu.usage`          | `Processor` > `_Total` > `% Processor Time` |
| `clusternode.cpu.usage.guest`    | *zero* |
| `clusternode.cpu.usage.host`     | *총 사용량 동일* |

불완전 한 동기화도 불구 하 고 `clusternode.cpu.usage` 은 항상 `clusternode.cpu.usage.host` plus `clusternode.cpu.usage.guest`합니다.

와 동일한 주의 사항이 `clusternode.cpu.usage.guest` 의 합계는 항상 `vm.cpu.usage` 호스트 서버의 모든 가상 머신에 대 한 합니다.

`memory.*` 시리즈는 (출시 예정).

  > [!NOTE]
  > 카운터는 샘플링 되지 전체 간격을 측정 됩니다. 예를 들어 서버 유휴 상태인 경우 9 초 있지만 100 %cpu 스파이크를 10 초에서 해당 `clusternode.cpu.usage` 으로 기록 됩니다 10% 평균 10 초 간격입니다. 이렇게 하면 성능 기록과 모든 활동을 캡처하고 노이즈를 강력 합니다.

## <a name="usage-in-powershell"></a>PowerShell에서 사용

사용 된 [Get-clusternode](https://docs.microsoft.com/powershell/module/failoverclusters/get-clusternode) cmdlet:

```PowerShell
Get-ClusterNode <Name> | Get-ClusterPerf
```

## <a name="see-also"></a>참조

- [저장소 공간 다이렉트에 대 한 성능 기록](performance-history.md)
