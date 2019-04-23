---
title: 가상 머신에 대 한 성능 기록
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 09/07/2018
Keywords: 저장소 공간 다이렉트
ms.localizationpriority: medium
ms.openlocfilehash: f8072ab5fc853248f2eedd26019956ec864a891d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890874"
---
# <a name="performance-history-for-virtual-machines"></a>가상 머신에 대 한 성능 기록

> 적용 대상: Windows Server Insider Preview

이 하위 항목의 [저장소 공간 다이렉트에 대 한 성능 기록을](performance-history.md) virtual machines (VM)에 대 한 수집 된 성능 기록 세부 정보에 설명 합니다. 성능 기록의 모든 실행, 클러스터 된 VM에 대 한 제품은입니다.

   > [!NOTE]
   > 새로 만든이 또는 이름이 바뀐 vm을 시작 하려면 컬렉션에 대 일 분 정도 걸릴 수 있습니다.

## <a name="series-names-and-units"></a>계열 이름 및 단위

이 시리즈는 적합 한 모든 VM에 대해 수집 됩니다.

| 시리즈                            | 단위             |
|-----------------------------------|------------------|
| `vm.cpu.usage`                    | %          |
| `vm.memory.assigned`              | 바이트            |
| `vm.memory.available`             | 바이트            |
| `vm.memory.maximum`               | 바이트            |
| `vm.memory.minimum`               | 바이트            |
| `vm.memory.pressure`              | -                |
| `vm.memory.startup`               | 바이트            |
| `vm.memory.total`                 | 바이트            |
| `vmnetworkadapter.bandwidth.inbound`  | 비트 / 초 |
| `vmnetworkadapter.bandwidth.outbound` | 비트 / 초 |
| `vmnetworkadapter.bandwidth.total`    | 비트 / 초 |

또한 모든 가상 하드 디스크 (VHD) 시리즈와 같은 `vhd.iops.total`, VM에 연결 된 모든 VHD에 대 한 집계 됩니다.

## <a name="how-to-interpret"></a>해석 하는 방법


| 시리즈                            | 설명                                                                                                  |
|-----------------------------------|--------------------------------------------------------------------------------------------------------------|
| `vm.cpu.usage`                    | 백분율 가상 머신이 해당 호스트 서버의 프로세서의 사용 중입니다.                                   |
| `vm.memory.assigned`              | 가상 컴퓨터에 할당 된 메모리 양입니다.                                                      |
| `vm.memory.available`             | 남아 있는 할당 된 크기의 사용 가능한 메모리 양입니다.                                       |
| `vm.memory.maximum`               | 동적 메모리를 사용 하는 경우 가상 머신에 할당할 수 있는 메모리의 최대 수입니다. |
| `vm.memory.minimum`               | 동적 메모리를 사용 하는 경우 가상 머신에 할당할 수 있는 메모리의 최소 양입니다. |
| `vm.memory.pressure`              | 가상 머신에 할당 된 메모리는 가상 컴퓨터에서 요구 하는 메모리의 비율입니다.            |
| `vm.memory.startup`               | 가상 컴퓨터를 시작 하는 데 필요한 메모리 양입니다.                                            |
| `vm.memory.total`                 | 총 메모리입니다. |
| `vmnetworkadapter.bandwidth.inbound`  | 모든 가상 네트워크 어댑터에서 가상 컴퓨터에서 받은 데이터의 비율입니다.                        |
| `vmnetworkadapter.bandwidth.outbound` | 모든 가상 네트워크 어댑터에서 가상 컴퓨터에서 보낸 데이터의 비율입니다.                            |
| `vmnetworkadapter.bandwidth.total`    | 총 데이터 변동률 받거나 모든 가상 네트워크 어댑터를 통해 가상 컴퓨터에 전송 합니다.          |

   > [!NOTE]
   > 카운터는 샘플링 되지 전체 간격을 측정 됩니다. 예: VM 9 초 하지만 급격히 증가 하는 호스트 CPU의 50%를 사용 하 여 10 초에서 동안 유휴 상태 이면 해당 `vm.cpu.usage` 으로 기록 됩니다 5% 평균 10 초 간격입니다. 이렇게 하면 성능 기록과 모든 활동을 캡처하고 노이즈를 강력 합니다.

## <a name="usage-in-powershell"></a>PowerShell에서 사용

사용 된 [GET-VM](https://docs.microsoft.com/powershell/module/hyper-v/get-vm) cmdlet:

```PowerShell
Get-VM <Name> | Get-ClusterPerf
```

   > [!NOTE]
   > GET-VM cmdlet을 로컬 (또는 지정한) 서버의 가상 컴퓨터 클러스터 전체가 아닌만 반환합니다.

## <a name="see-also"></a>참조

- [저장소 공간 다이렉트에 대 한 성능 기록](performance-history.md)
