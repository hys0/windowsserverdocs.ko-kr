---
title: 가상 컴퓨터에 대 한 성능 기록
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 09/07/2018
Keywords: Storage Spaces Direct
ms.localizationpriority: medium
ms.openlocfilehash: f8072ab5fc853248f2eedd26019956ec864a891d
ms.sourcegitcommit: d31e266130b3b082372f7af4024e6089cb347d74
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/28/2018
ms.locfileid: "4239220"
---
# 가상 컴퓨터에 대 한 성능 기록

> 적용 대상: Windows Server Insider Preview

이 하위 항목이에서는 [저장소 공간 다이렉트에 대 한 성능 기록](performance-history.md) 의 가상 컴퓨터 (VM)에 대 한 성능 기록을 수집 자세히 설명 합니다. 성능 기록은 모든 실행 클러스터형된 VM에 사용할 수 있습니다.

   > [!NOTE]
   > 컬렉션을 새로 만든 되거나 이름이 바뀐 Vm을 시작 하는 데 몇 분 정도 걸릴 수 있습니다.

## 시리즈 이름과 단위

적합 한 모든 VM에 대 한 이러한 시리즈 수집 됩니다.

| 시리즈                            | Unit             |
|-----------------------------------|------------------|
| `vm.cpu.usage`                    | %          |
| `vm.memory.assigned`              |  바이트            |
| `vm.memory.available`             |  바이트            |
| `vm.memory.maximum`               |  바이트            |
| `vm.memory.minimum`               |  바이트            |
| `vm.memory.pressure`              | -                |
| `vm.memory.startup`               |  바이트            |
| `vm.memory.total`                 |  바이트            |
| `vmnetworkadapter.bandwidth.inbound`  | 초당 비트 |
| `vmnetworkadapter.bandwidth.outbound` | 초당 비트 |
| `vmnetworkadapter.bandwidth.total`    | 초당 비트 |

또한 모든 가상 하드 디스크 (VHD) 시리즈와 같은 `vhd.iops.total`, VM에 연결 된 모든 VHD에 대 한 집계 됩니다.

## 해석 하는 방법


| 시리즈                            | 설명                                                                                                  |
|-----------------------------------|--------------------------------------------------------------------------------------------------------------|
| `vm.cpu.usage`                    | 해당 호스트 서버 프로세서의 백분율 가상 컴퓨터를 사용 합니다.                                   |
| `vm.memory.assigned`              | 가상 컴퓨터에 할당 된 메모리 양입니다.                                                      |
| `vm.memory.available`             | 남아 있는 할당 크기의 사용 가능한 메모리 양입니다.                                       |
| `vm.memory.maximum`               | 동적 메모리를 사용 하는 경우 가상 컴퓨터에 할당 될 수 있는 메모리의 최대 수입니다. |
| `vm.memory.minimum`               | 동적 메모리를 사용 하는 경우 가상 컴퓨터에 할당 될 수 있는 메모리의 최소 수량입니다. |
| `vm.memory.pressure`              | 가상 컴퓨터에 할당 된 메모리를 통해 가상 컴퓨터에서 요구 하는 메모리의 비율입니다.            |
| `vm.memory.startup`               | 시작 하려면 가상 컴퓨터에 필요한 메모리 양입니다.                                            |
| `vm.memory.total`                 | 총 메모리입니다. |
| `vmnetworkadapter.bandwidth.inbound`  | 가상 컴퓨터의 모든 가상 네트워크 어댑터에서 받은 데이터의 속도.                        |
| `vmnetworkadapter.bandwidth.outbound` | 가상 컴퓨터의 모든 가상 네트워크 어댑터에 걸쳐 전송 된 데이터 속도.                            |
| `vmnetworkadapter.bandwidth.total`    | 데이터의 총 속도 수신 하거나 가상 컴퓨터의 모든 가상 네트워크 어댑터에 걸쳐 전송한 합니다.          |

   > [!NOTE]
   > 카운터는 샘플링 하지는 전체 간격을 통해 측정 됩니다. 예를 들어, VM 9 초 하지만 급증 10 초에서 50% 호스트 CPU 사용 하 여 유휴 상태 이면 해당 `vm.cpu.usage` 기록 될 5%로 평균적으로이 10 초 간격 동안 합니다. 이렇게 하면 성능 기록 모든 활동 캡처하고 노이즈 강력 합니다.

## Powershell 사용

[GET-VM](https://docs.microsoft.com/powershell/module/hyper-v/get-vm) cmdlet을 사용 합니다.

```PowerShell
Get-VM <Name> | Get-ClusterPerf
```

   > [!NOTE]
   > GET-VM cmdlet는만 클러스터 전체에서 아니라 로컬 (또는 지정 된) 서버에서 가상 컴퓨터를 반환합니다.

## 참고 항목

- [저장소 공간 다이렉트에 대 한 성능 기록](performance-history.md)
