---
title: 가상 컴퓨터에 대 한 성능 기록
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 418ab095f5f0af35f3aa176614ad73f48d727a35
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474690"
---
# <a name="performance-history-for-virtual-machines"></a>가상 컴퓨터에 대 한 성능 기록

> 적용 대상: 시작

[스토리지 공간 다이렉트에 대 한 성능 기록](performance-history.md) 의이 하위 항목에서는 VM (가상 컴퓨터)에 대해 수집 된 성능 기록에 대해 자세히 설명 합니다. 성능 기록은 실행 중인 모든 클러스터 된 VM에 대해 사용할 수 있습니다.

   > [!NOTE]
   > 새로 만들어지거나 이름이 변경 되는 Vm에 대해 수집이 시작 되는 데 몇 분 정도 걸릴 수 있습니다.

## <a name="series-names-and-units"></a>계열 이름 및 단위

이러한 시리즈는 적합 한 모든 VM에 대해 수집 됩니다.

| 계열                            | 단위             |
|-----------------------------------|------------------|
| `vm.cpu.usage`                    | percent          |
| `vm.memory.assigned`              | 바이트            |
| `vm.memory.available`             | 바이트            |
| `vm.memory.maximum`               | 바이트            |
| `vm.memory.minimum`               | 바이트            |
| `vm.memory.pressure`              | -                |
| `vm.memory.startup`               | 바이트            |
| `vm.memory.total`                 | 바이트            |
| `vmnetworkadapter.bandwidth.inbound`  | 초당 비트 수 |
| `vmnetworkadapter.bandwidth.outbound` | 초당 비트 수 |
| `vmnetworkadapter.bandwidth.total`    | 초당 비트 수 |

또한 VM에 연결 된 모든 VHD에 대해와 같은 모든 VHD (가상 하드 디스크) 시리즈를 `vhd.iops.total` 집계 합니다.

## <a name="how-to-interpret"></a>해석 방법


| 계열                            | 설명                                                                                                  |
|-----------------------------------|--------------------------------------------------------------------------------------------------------------|
| `vm.cpu.usage`                    | 가상 컴퓨터가 호스트 서버 프로세서를 사용 하 고 있는 비율입니다.                                   |
| `vm.memory.assigned`              | 가상 컴퓨터에 할당 된 메모리의 양입니다.                                                      |
| `vm.memory.available`             | 할당 된 양에 사용 가능한 상태로 남아 있는 메모리의 양입니다.                                       |
| `vm.memory.maximum`               | 동적 메모리를 사용 하는 경우 가상 컴퓨터에 할당할 수 있는 최대 메모리 양입니다. |
| `vm.memory.minimum`               | 동적 메모리를 사용 하는 경우 가상 컴퓨터에 할당할 수 있는 최소 메모리 양입니다. |
| `vm.memory.pressure`              | 가상 컴퓨터에서 가상 컴퓨터에 할당 된 메모리에 대해 요구 하는 메모리의 비율입니다.            |
| `vm.memory.startup`               | 가상 컴퓨터를 시작 하는 데 필요한 메모리의 양입니다.                                            |
| `vm.memory.total`                 | 총 메모리입니다. |
| `vmnetworkadapter.bandwidth.inbound`  | 가상 컴퓨터가 가상 네트워크 어댑터를 통해 받은 데이터의 요금입니다.                        |
| `vmnetworkadapter.bandwidth.outbound` | 가상 컴퓨터가 가상 네트워크 어댑터를 통해 보낸 데이터의 요금입니다.                            |
| `vmnetworkadapter.bandwidth.total`    | 가상 컴퓨터에서 모든 가상 네트워크 어댑터에 대해 받거나 보낸 데이터의 총 비율입니다.          |

   > [!NOTE]
   > 카운터는 샘플링 되지 않고 전체 간격으로 측정 됩니다. 예를 들어 VM이 9 초 동안 유휴 상태 이지만 10 초 동안 50%의 호스트 CPU를 사용 하도록 급증 하는 경우 `vm.cpu.usage` 이 10 초 간격 동안 평균 5%로 기록 됩니다. 이렇게 하면 성능 기록이 모든 활동을 캡처하고 소음에 대해 강력 하 게 됩니다.

## <a name="usage-in-powershell"></a>PowerShell에서 사용

[GET VM](https://docs.microsoft.com/powershell/module/hyper-v/get-vm) cmdlet을 사용 합니다.

```PowerShell
Get-VM <Name> | Get-ClusterPerf
```

   > [!NOTE]
   > VM cmdlet은 클러스터가 아닌 로컬 (지정 된) 서버의 가상 컴퓨터만 반환 합니다.

## <a name="additional-references"></a>추가 참조

- [스토리지 공간 다이렉트에 대 한 성능 기록](performance-history.md)
