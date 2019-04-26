---
title: HNV 게이트웨이의 성능 조정 소프트웨어 정의 네트워크
description: 소프트웨어 정의 네트워크에 대 한 지침을 조정 하는 HNV 게이트웨이 성능
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: grcusanz; AnPaul
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 217428b84a00b2e2231a15cb3878d0abcec1d9ad
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827324"
---
# <a name="hnv-gateway-performance-tuning-in-software-defined-networks"></a>HNV 게이트웨이의 성능 조정 소프트웨어 정의 네트워크

이 항목에서는 하드웨어 사양 및 Hyper-v를 실행 하 고 Windows Server 게이트웨이 Vm (가상 머신)에 대 한 구성 매개 변수 외에도 Windows Server 게이트웨이 가상 컴퓨터를 호스트 하는 서버에 대 한 구성 권장 사항 . Windows Server 게이트웨이 Vm에서 최상의 성능의 추출 하려면 이러한 지침을 따를 수는 예상 됩니다.
다음 섹션에서는 Windows Server 게이트웨이를 배포할 때의 하드웨어 및 구성 요구 사항을 설명합니다.
1. Hyper-V 하드웨어 권장 사항
2. Hyper-V 호스트 구성
3. Windows Server 게이트웨이 VM 구성

## <a name="hyper-v-hardware-recommendations"></a>Hyper-V 하드웨어 권장 사항

다음은 Windows Server 2016 및 Hyper-v를 실행 하는 각 서버에 대 한 권장된 최소 하드웨어 구성 합니다.

| 서버 구성 요소               | 사양                                                                                                                                                                                                                                                                   |
|--------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| CPU(중앙 처리 장치)  | Non-uniform NUMA (Memory Architecture) 노드: 2 <br> 최상의 성능을 위해 호스트에서 여러 Windows Server 게이트웨이 Vm에 있는 경우 각 게이트웨이 VM NUMA 노드 하나에 대 한 전체 액세스를 해야 합니다. 및 해당 NUMA 노드와 호스트 실제 어댑터에서 사용 하는 달라 야 합니다. |
| NUMA 노드당 코어 수            | 2                                                                                                                                                                                                                                                                               |
| 하이퍼 스레딩                | 사용하지 않도록 설정됩니다. 하이퍼 스레딩은 Windows Server 게이트웨이의 성능을 향상시키지 않습니다.                                                                                                                                                                                           |
| RAM(Random Access Memory)     | 48GB                                                                                                                                                                                                                                                                           |
| NIC(네트워크 인터페이스 카드) | 두 개의 10GB Nic 게이트웨이 성능이 회선 속도에 따라 달라 집니다. 회선 속도 10Gbps 미만인 경우 게이트웨이 터널 처리량 수치도 작동이 중지 될 동일한 비율입니다.                                                                                          |

Windows Server 게이트웨이 VM에 할당된 가상 프로세서 수가 NUMA 노드의 프로세서 수를 초과하지 않는지 확인하십시오. 예를 들어 NUMA 노드에 8개의 코어가 있는 경우 가상 프로세서 수는 8개보다 적거나 같아야 합니다. 최상의 성능을 위해 8 여야 합니다. NUMA 노드 수와 NUMA 노드당 코어 수를 확인하려면 각 Hyper-V 호스트에서 다음 Windows PowerShell 스크립트를 실행하십시오.

```PowerShell
$nodes = [object[]] $(gwmi –Namespace root\virtualization\v2 -Class MSVM_NumaNode)
$cores = ($nodes | Measure-Object NumberOfProcessorCores -sum).Sum
$lps = ($nodes | Measure-Object NumberOfLogicalProcessors -sum).Sum


Write-Host "Number of NUMA Nodes: ", $nodes.count
Write-Host ("Total Number of Cores: ", $cores)
Write-Host ("Total Number of Logical Processors: ", $lps)
```

>[!Important]
> NUMA 노드에서 가상 프로세서를 할당하면 Windows Server 게이트웨이의 성능에 부정적인 영향을 줄 수 있습니다. 각각 하나의 NUMA 노드에서 가상 프로세서가 할당된 여러 VM을 실행하면 모든 가상 프로세서가 단일 VM에 할당된 경우보다 집계 성능이 향상됩니다.

하나의 게이트웨이 VM 8 개의 가상 프로세서 및 8GB 이상 RAM 사용 하 여 각 NUMA 노드에 8 개의 코어가 있는 경우 각 Hyper-v 호스트에 설치 하려면 게이트웨이 Vm 수를 선택 하는 경우 좋습니다. 이 경우 이상의 NUMA 노드가 호스트 컴퓨터에 전용 됩니다.

## <a name="hyper-v-host-configuration"></a>Hyper-v 호스트 구성

다음은 Windows Server 2016 및 Hyper-v 및 해당 실행 하는 각 서버에 대 한 권장된 구성 작업 Windows Server 게이트웨이 Vm을 실행 하는 것입니다. 이러한 구성 지침에는 Windows PowerShell 명령의 사용 예가 포함되어 있습니다. 이러한 예에 포함된 자리 표시자는 사용자 환경에서 명령을 실행할 때 실제 값으로 바꿔야 합니다. 예를 들어 네트워크 어댑터 이름 자리 표시자는 "NIC1? 및 "NIC2? 이러한 자리 표시자를 사용하는 명령을 실행할 때는 자리 표시자를 사용하지 말고 서버에 있는 네트워크 어댑터의 실제 이름을 사용해야 합니다. 그렇지 않으면 명령이 실패합니다.

>[!Note]
> 다음 Windows PowerShell 명령을 실행하려면 Administrators 그룹의 구성원이어야 합니다.

| 구성 항목                          | Windows Powershell 구성                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|---------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 스위치 포함 팀                     | 여러 네트워크 어댑터를 사용 하 여 vswitch를 만들면 해당 어댑터 팀 구성 스위치 포함 된 자동으로 설정 합니다. <br> ```New-VMSwitch -Name TeamedvSwitch -NetAdapterName "NIC 1","NIC 2"``` <br> Windows Server 2016에서 SDN을 사용 하 여 기존 팀 LBFO 통해 지원 되지 않습니다. 스위치 포함 된 팀에 가상 트래픽 및 RDMA 트래픽 Nic의 동일한 집합을 사용할 수 있습니다. LBFO에 따라 NIC 팀과 함께 지원 되지 않았습니다.                                                        |
| 실제 NIC의 인터럽트 조절       | 기본 설정을 사용합니다. 구성을 확인 하려면 다음 Windows PowerShell 명령을 사용할 수 있습니다. ```Get-NetAdapterAdvancedProperty```                                                                                                                                                                                                                                                                                                                                                                    |
| 실제 NIC의 수신 버퍼 크기       | 명령을 실행 하 여 실제 nic가이 매개 변수 구성을 지원 하는지 여부를 확인할 수 있습니다 ```Get-NetAdapterAdvancedProperty```합니다. 명령의 출력은 속성을 포함 하지 않는이 매개 변수를 지원 하지 않는 경우 "수신 버퍼? NIC가 이 매개 변수를 지원하는 경우 다음 Windows PowerShell 명령을 사용하여 수신 버퍼 크기를 설정할 수 있습니다. <br>```Set-NetAdapterAdvancedProperty “NIC1�? –DisplayName “Receive Buffers�? –DisplayValue 3000``` <br>                          |
| 실제 NIC의 전송 버퍼 크기          | 명령을 실행 하 여 실제 nic가이 매개 변수 구성을 지원 하는지 여부를 확인할 수 있습니다 ```Get-NetAdapterAdvancedProperty```합니다. 명령의 출력은 속성을 포함 하지 않는 Nic를이 매개 변수를 지원 하지 않는 경우 "Send Buffers? NIC가 이 매개 변수를 지원하는 경우 다음 Windows PowerShell 명령을 사용하여 전송 버퍼 크기를 설정할 수 있습니다. <br> ```Set-NetAdapterAdvancedProperty “NIC1�? –DisplayName “Transmit Buffers�? –DisplayValue 3000``` <br>                           |
| 실제 NIC의 RSS(수신측 배율) | 실제 Nic에 RSS가 Get-netadapterrss Windows PowerShell 명령을 실행 하 여 설정 되어 있는지 여부를 확인할 수 있습니다. 사용 하도록 설정 하 고 네트워크 어댑터에서 RSS를 구성 하려면 다음 Windows PowerShell 명령을 사용할 수 있습니다. <br> ```Enable-NetAdapterRss “NIC1�?,�?NIC2�?```<br> ```Set-NetAdapterRss “NIC1�?,�?NIC2�? –NumberOfReceiveQueues 16 -MaxProcessors``` <br> 참고: VMMQ 또는 VMQ를 사용 하는 경우에 RSS를 실제 네트워크 어댑터에서 사용 하도록 설정 하지 않아도 합니다. 호스트 가상 네트워크 어댑터에 설정할 수 있습니다. |
| VMMQ                                        | VMMQ vm을 사용 하려면 다음 명령을 실행 합니다. <br> ```Set-VmNetworkAdapter -VMName <gateway vm name>,-VrssEnabled $true -VmmqEnabled $true``` <br> 참고: 일부 네트워크 어댑터 VMMQ를 지원합니다. 현재 Chelsio T5 및 T6, Mellanox CX 3 및 CX-4, QLogic 45xxx 시리즈에서 지원 됩니다.                                                                                                                                                                                                                                      |
| NIC 팀의 VMQ(가상 컴퓨터 큐) | 다음 Windows PowerShell 명령을 사용 하 여 집합 팀의 VMQ를 사용할 수 있습니다. <br>```Enable-NetAdapterVmq``` <br> 참고: HW VMMQ를 지원 하지 않는 경우에이 사용 해야 합니다. 지원 되는 경우 VMMQ 성능 향상을 위해 설정 되어야 합니다.                                                                                                                                                                                                                                                               |
>[!Note]
> VMQ 및 vRSS VM에서 부하가 높으면 및 최대 CPU 사용 되는 경우에 그림으로 제공 됩니다. 그런 후에는 하나 이상의 프로세서 핵심 max 아웃 합니다. 그러면 VMQ 및 vRSS 다중 코어 처리 부하를 분산 하는 데 도움이 됩니다. 이 단일 코어를 IPsec 트래픽에 제한으로 IPsec 트래픽에 적용 되지 않습니다.

## <a name="windows-server-gateway-vm-configuration"></a>Windows Server 게이트웨이 VM 구성

두 Hyper-v 호스트에서 Windows Server 게이트웨이 사용 하 여 게이트웨이로 구성 된 여러 Vm을 구성할 수 있습니다. 가상 스위치 관리자를 사용하여 Hyper-V 호스트의 NIC 팀에 바인딩된 Hyper-V 가상 스위치를 만들 수 있습니다. 최상의 성능을 위해 단일 게이트웨이 VM에서 Hyper-v 호스트에 배포 해야 하는 참고 합니다.
다음은 각 Windows Server 게이트웨이 VM에 대한 권장 구성입니다.

| 구성 항목                 | Windows Powershell 구성                                                                                                                                                                                                                                                                                                                                                               |
|------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 메모리                             | 8GB                                                                                                                                                                                                                                                                                                                                                                                           |
| 가상 네트워크 어댑터 수 | 다음과 같은 특정을 사용 하 여 3 개의 Nic를 사용 합니다. 관리 운영 체제, 외부 네트워크, 내부 네트워크에 대 한 액세스를 제공 하는 내부 1에 대 한 액세스를 제공 하는 1 외부에서 사용 되는 관리에 대 한 1입니다.                                                                                                                                                            |
| Receive Side Scaling (RSS)         | 기본 관리 NIC에 대 한 RSS 설정을 유지할 수 있습니다. 다음 구성 예는 가상 프로세서가 8개인 VM에 대한 구성입니다. 외부 및 내부 Nic의 경우 0과 다음 Windows PowerShell 명령을 사용 하 여 8로 MaxRssProcessors BaseProcNumber 사용 하 여 RSS를 사용할 수 있습니다. <br> ```Set-NetAdapterRss “Internal�?,�?External�? –BaseProcNumber 0 –MaxProcessorNumber 8``` <br> |
| 전송측 버퍼                   | 기본 관리 NIC에 대 한 설정을 전송측 버퍼를 유지할 수 있습니다. 내부 nic와 외부 Nic 모두에 대 한 다음 Windows PowerShell 명령을 사용 하 여 ram이 32MB 인 전송측 버퍼를 구성할 수 있습니다. <br> ```Set-NetAdapterAdvancedProperty “Internal�?,�?External�? –DisplayName “Send Buffer Size�? –DisplayValue “32MB�?``` <br>                                                       |
| 수신측 버퍼                | 기본 관리 NIC에 대 한 설정을 수신측 버퍼를 유지할 수 있습니다. 내부와 외부 Nic 모두에 대 한 다음 Windows PowerShell 명령을 사용 하 여 ram이 16mb 수신측 버퍼를 구성할 수 있습니다. <br> ```Set-NetAdapterAdvancedProperty “Internal�?,�?External�? –DisplayName “Receive Buffer Size�? –DisplayValue “16MB�?``` <br>                                            |
| 전달 최적화               | 기본 관리 NIC에 대 한 전달 최적화 설정을 유지할 수 있습니다. 내부와 외부 Nic 모두에 대 한 다음 Windows PowerShell 명령을 사용 하 여 전달 최적화를 사용할 수 있습니다. <br> ```Set-NetAdapterAdvancedProperty “Internal�?,�?External�? –DisplayName “Forward Optimization�? –DisplayValue “1�?``` <br>                                                                      |
