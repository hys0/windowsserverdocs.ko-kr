---
title: 서버에 대 한 성능 기록
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7ed910aba376ba7f78c628d7f47bdd21b366459d
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474740"
---
# <a name="performance-history-for-servers"></a>서버에 대 한 성능 기록

> 적용 대상: 시작

[스토리지 공간 다이렉트에 대 한 성능 기록](performance-history.md) 의이 하위 항목에서는 서버에 대해 수집 된 성능 기록에 대해 자세히 설명 합니다. 성능 기록은 클러스터의 모든 서버에서 사용할 수 있습니다.

   > [!NOTE]
   > 다운 된 서버에 대 한 성능 기록을 수집할 수 없습니다. 서버를 다시 시작 하면 수집이 자동으로 다시 시작 됩니다.

## <a name="series-names-and-units"></a>계열 이름 및 단위

이러한 계열은 모든 적격 서버에 대해 수집 됩니다.

| 계열                           | 단위    |
|----------------------------------|---------|
| `clusternode.cpu.usage`          | percent |
| `clusternode.cpu.usage.guest`    | percent |
| `clusternode.cpu.usage.host`     | percent |
| `clusternode.memory.total`       | 바이트   |
| `clusternode.memory.available`   | 바이트   |
| `clusternode.memory.usage`       | 바이트   |
| `clusternode.memory.usage.guest` | 바이트   |
| `clusternode.memory.usage.host`  | 바이트   |

또한와 같은 드라이브 시리즈 `physicaldisk.size.total` 는 서버에 연결 된 모든 적격 드라이브에 대해 집계 되며와 같은 네트워크 어댑터 시리즈 `networkadapter.bytes.total` 는 서버에 연결 된 모든 적격 네트워크 어댑터에 대해 집계 됩니다.

## <a name="how-to-interpret"></a>해석 방법

| 계열                           | 해석 방법                                                      |
|----------------------------------|-----------------------------------------------------------------------|
| `clusternode.cpu.usage`          | 유휴 상태가 아닌 프로세서 시간 비율입니다.                        |
| `clusternode.cpu.usage.guest`    | 게스트 (가상 컴퓨터) 수요에 사용 되는 프로세서 시간의 비율입니다. |
| `clusternode.cpu.usage.host`     | 호스트 수요에 사용 되는 프로세서 시간의 백분율입니다.                    |
| `clusternode.memory.total`       | 서버의 총 실제 메모리입니다.                              |
| `clusternode.memory.available`   | 서버의 사용 가능한 메모리입니다.                                   |
| `clusternode.memory.usage`       | 서버의 할당 된 (사용할 수 없음) 메모리입니다.                   |
| `clusternode.memory.usage.guest` | 게스트 (가상 컴퓨터) 요청에 할당 된 메모리입니다.               |
| `clusternode.memory.usage.host`  | 호스트 요청에 할당 된 메모리입니다.                                  |

## <a name="where-they-come-from"></a>원본 위치

`cpu.*`이 시리즈는 hyper-v의 설정 여부에 따라 다양 한 성능 카운터에서 수집 됩니다.

Hyper-v를 사용 하는 경우:

| 계열                           | 원본 카운터 |
|----------------------------------|----------------|
| `clusternode.cpu.usage`          | `Hyper-V Hypervisor Logical Processor` > `_Total` > `% Total Run Time`      |
| `clusternode.cpu.usage.guest`    | `Hyper-V Hypervisor Virtual Processor` > `_Total` > `% Total Run Time`      |
| `clusternode.cpu.usage.host`     | `Hyper-V Hypervisor Root Virtual Processor` > `_Total` > `% Total Run Time` |

카운터를 사용 `% Total Run Time` 하면 성능 기록 특성이 모두 사용 됩니다.

Hyper-v를 사용할 수 없는 경우:

| 계열                           | 원본 카운터 |
|----------------------------------|----------------|
| `clusternode.cpu.usage`          | `Processor` > `_Total` > `% Processor Time` |
| `clusternode.cpu.usage.guest`    | *반환* |
| `clusternode.cpu.usage.host`     | *총 사용량과 동일* |

도 불구 아직까지 완벽 synchronization, `clusternode.cpu.usage` 는 항상 `clusternode.cpu.usage.host` + `clusternode.cpu.usage.guest` 입니다.

동일한 주의 사항을 사용 하 여 `clusternode.cpu.usage.guest` 은 항상 `vm.cpu.usage` 호스트 서버에 있는 모든 가상 컴퓨터의 합계입니다.

`memory.*`시리즈는 (출시 예정)입니다.

  > [!NOTE]
  > 카운터는 샘플링 되지 않고 전체 간격으로 측정 됩니다. 예를 들어 서버가 9 초 동안 유휴 상태 이지만 10 초 동안 100% CPU로 급증 하는 경우 `clusternode.cpu.usage` 이 10 초 간격 동안 평균 10%로 기록 됩니다. 이렇게 하면 성능 기록이 모든 활동을 캡처하고 소음에 대해 강력 하 게 됩니다.

## <a name="usage-in-powershell"></a>PowerShell에서 사용

[Start-clusternode](https://docs.microsoft.com/powershell/module/failoverclusters/get-clusternode) cmdlet을 사용 합니다.

```PowerShell
Get-ClusterNode <Name> | Get-ClusterPerf
```

## <a name="additional-references"></a>추가 참조

- [스토리지 공간 다이렉트에 대 한 성능 기록](performance-history.md)
