---
title: 소프트웨어 정의 네트워크에서 HNV 게이트웨이 성능 튜닝
description: 소프트웨어 정의 네트워크에 대 한 HNV 게이트웨이 성능 조정 지침
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: grcusanz; anpaul
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 98b8a50873cf69e96131f98d5d94c386cb30a13d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851626"
---
# <a name="hnv-gateway-performance-tuning-in-software-defined-networks"></a>소프트웨어 정의 네트워크에서 HNV 게이트웨이 성능 튜닝

이 항목에서는 Windows Server 게이트웨이 가상 컴퓨터 (Vm)에 대 한 구성 매개 변수와 함께 Hyper-v를 실행 하 고 Windows Server 게이트웨이 가상 컴퓨터를 호스트 하는 서버에 대 한 하드웨어 사양 및 구성 권장 사항을 제공 합니다. Windows Server 게이트웨이 Vm에서 최상의 성능을 추출 하려면 이러한 지침을 따라야 합니다.
다음 섹션에서는 Windows Server 게이트웨이를 배포할 때의 하드웨어 및 구성 요구 사항을 설명합니다.
1. Hyper-V 하드웨어 권장 사항
2. Hyper-V 호스트 구성
3. Windows Server 게이트웨이 VM 구성

## <a name="hyper-v-hardware-recommendations"></a>Hyper-V 하드웨어 권장 사항

다음은 Windows Server 2016 및 Hyper-v를 실행 하는 각 서버에 권장 되는 최소 하드웨어 구성입니다.

| 서버 구성 요소               | 사양                                                                                                                                                                                                                                                                   |
|--------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| CPU(중앙 처리 장치)  | NUMA (Non-uniform Memory Architecture) 노드: 2 <br> 호스트에 Windows Server 게이트웨이 Vm이 여러 개 있는 경우 최상의 성능을 위해 각 게이트웨이 VM에는 하나의 NUMA 노드에 대 한 모든 권한이 있어야 합니다. 그리고 호스트 실제 어댑터에서 사용 하는 NUMA 노드와 달라 야 합니다. |
| NUMA 노드당 코어 수            | 2                                                                                                                                                                                                                                                                               |
| 하이퍼 스레딩                | 사용 안 함. 하이퍼 스레딩은 Windows Server 게이트웨이의 성능을 향상시키지 않습니다.                                                                                                                                                                                           |
| RAM(Random Access Memory)     | 48GB                                                                                                                                                                                                                                                                           |
| NIC(네트워크 인터페이스 카드) | 2 10 g b Nic, 게이트웨이 성능은 회선 속도에 따라 달라 집니다. 줄 속도가 10Gbps 보다 작은 경우 게이트웨이 터널 처리량 번호도 동일한 배율로 중단 됩니다.                                                                                          |

Windows Server 게이트웨이 VM에 할당된 가상 프로세서 수가 NUMA 노드의 프로세서 수를 초과하지 않는지 확인하십시오. 예를 들어 NUMA 노드에 8개의 코어가 있는 경우 가상 프로세서 수는 8개보다 적거나 같아야 합니다. 최상의 성능을 위해 8 이어야 합니다. NUMA 노드 수와 NUMA 노드당 코어 수를 확인하려면 각 Hyper-V 호스트에서 다음 Windows PowerShell 스크립트를 실행하십시오.

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

각 NUMA 노드에 8 개의 코어가 있는 경우 각 Hyper-v 호스트에 설치할 게이트웨이 vm의 수를 선택 하는 경우 8 개의 가상 프로세서와 8GB 이상의 RAM이 있는 하나의 게이트웨이 VM을 사용 하는 것이 좋습니다. 이 경우 하나의 NUMA 노드가 호스트 컴퓨터 전용입니다.

## <a name="hyper-v-host-configuration"></a>Hyper-v 호스트 구성

다음은 Windows server 2016 및 Hyper-v를 실행 하 고 Windows Server 게이트웨이 Vm을 실행 하는 워크 로드를 실행 하는 각 서버에 권장 되는 구성입니다. 이러한 구성 지침에는 Windows PowerShell 명령의 사용 예가 포함되어 있습니다. 이러한 예에 포함된 자리 표시자는 사용자 환경에서 명령을 실행할 때 실제 값으로 바꿔야 합니다. 예를 들어 네트워크 어댑터 이름 자리 표시자는 "NIC1" 및 "NIC2"입니다. 이러한 자리 표시자를 사용하는 명령을 실행할 때는 자리 표시자를 사용하지 말고 서버에 있는 네트워크 어댑터의 실제 이름을 사용해야 합니다. 그렇지 않으면 명령이 실패합니다.

>[!Note]
> 다음 Windows PowerShell 명령을 실행하려면 Administrators 그룹의 구성원이어야 합니다.

| 구성 항목                          | Windows Powershell 구성                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|---------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 스위치 포함 팀                     | 여러 네트워크 어댑터를 사용 하 여 vswitch를 만들면 자동으로 해당 어댑터에 대 한 포함 된 팀 전환을 사용 하도록 설정 됩니다. <br> ```New-VMSwitch -Name TeamedvSwitch -NetAdapterName "NIC 1","NIC 2"``` <br> LBFO를 통한 기존 팀은 Windows Server 2016의 SDN에서 지원 되지 않습니다. 스위치 포함 팀을 사용 하면 가상 트래픽과 RDMA 트래픽에 대해 동일한 Nic 집합을 사용할 수 있습니다. LBFO을 기반으로 하는 NIC 팀에서는 지원 되지 않습니다.                                                        |
| 실제 NIC의 인터럽트 조절       | 기본 설정을 사용합니다. 구성을 확인 하려면 다음 Windows PowerShell 명령을 사용할 수 있습니다. ```Get-NetAdapterAdvancedProperty```                                                                                                                                                                                                                                                                                                                                                                    |
| 실제 NIC의 수신 버퍼 크기       | ```Get-NetAdapterAdvancedProperty```명령을 실행 하 여 실제 Nic가이 매개 변수의 구성을 지원 하는지 확인할 수 있습니다. 이 매개 변수를 지원 하지 않으면 명령의 출력에 "Receive Buffers" 속성이 포함 되지 않습니다. NIC가 이 매개 변수를 지원하는 경우 다음 Windows PowerShell 명령을 사용하여 수신 버퍼 크기를 설정할 수 있습니다. <br>```Set-NetAdapterAdvancedProperty "NIC1" –DisplayName "Receive Buffers" –DisplayValue 3000``` <br>                          |
| 실제 NIC의 전송 버퍼 크기          | ```Get-NetAdapterAdvancedProperty```명령을 실행 하 여 실제 Nic가이 매개 변수의 구성을 지원 하는지 확인할 수 있습니다. Nic가이 매개 변수를 지원 하지 않으면 명령의 출력에 "송신 버퍼" 속성이 포함 되지 않습니다. NIC가 이 매개 변수를 지원하는 경우 다음 Windows PowerShell 명령을 사용하여 전송 버퍼 크기를 설정할 수 있습니다. <br> ```Set-NetAdapterAdvancedProperty "NIC1" –DisplayName "Transmit Buffers" –DisplayValue 3000``` <br>                           |
| 실제 NIC의 RSS(수신측 배율) | Windows PowerShell 명령 Get-NetAdapterRss를 실행하여 실제 NIC에 RSS가 설정되어 있는지 확인할 수 있습니다. 다음 Windows PowerShell 명령을 사용 하 여 네트워크 어댑터에서 RSS를 사용 하도록 설정 하 고 구성할 수 있습니다. <br> ```Enable-NetAdapterRss "NIC1","NIC2"```<br> ```Set-NetAdapterRss "NIC1","NIC2" –NumberOfReceiveQueues 16 -MaxProcessors``` <br> 참고: VMMQ 또는 VMQ를 사용 하는 경우 실제 네트워크 어댑터에서 RSS를 사용 하도록 설정할 필요가 없습니다. 호스트 가상 네트워크 어댑터에서 사용 하도록 설정할 수 있습니다. |
| VMMQ                                        | VM에 대해 VMMQ를 사용 하도록 설정 하려면 다음 명령을 실행 합니다. <br> ```Set-VmNetworkAdapter -VMName <gateway vm name>,-VrssEnabled $true -VmmqEnabled $true``` <br> 참고: 일부 네트워크 어댑터는 VMMQ을 지원 하지 않습니다. 현재는 Chelsio T5 및 T6, Mellanox CX-3 및 CX-4 및 QLogic 45xxx 시리즈에서 지원 됩니다.                                                                                                                                                                                                                                      |
| NIC 팀의 VMQ(가상 컴퓨터 큐) | 다음 Windows PowerShell 명령을 사용 하 여 집합 팀에서 VMQ를 사용 하도록 설정할 수 있습니다. <br>```Enable-NetAdapterVmq``` <br> 참고:이는 HW가 VMMQ을 지원 하지 않는 경우에만 사용 하도록 설정 해야 합니다. 지원 되는 경우 성능 향상을 위해 VMMQ를 사용 하도록 설정 해야 합니다.                                                                                                                                                                                                                                                               |
>[!Note]
> VMQ 및 vRSS는 VM의 로드가 높고 CPU가 최대한 활용 되는 경우에만 그림으로 제공 됩니다. 그런 다음에만 하나 이상의 프로세서 코어가 최대 출력 됩니다. 그러면 VMQ와 vRSS가 여러 코어에 걸쳐 처리 부하를 분산 하는 데 도움이 됩니다. IPsec 트래픽은 단일 코어로 제한 되므로 IPsec 트래픽에는 적용 되지 않습니다.

## <a name="windows-server-gateway-vm-configuration"></a>Windows Server 게이트웨이 VM 구성

두 Hyper-v 호스트에서 Windows Server 게이트웨이를 사용 하 여 게이트웨이로 구성 된 여러 Vm을 구성할 수 있습니다. 가상 스위치 관리자를 사용하여 Hyper-V 호스트의 NIC 팀에 바인딩된 Hyper-V 가상 스위치를 만들 수 있습니다. 최상의 성능을 위해서는 단일 게이트웨이 VM을 Hyper-v 호스트에 배포 해야 합니다.
다음은 각 Windows Server 게이트웨이 VM에 대한 권장 구성입니다.

| 구성 항목                 | Windows Powershell 구성                                                                                                                                                                                                                                                                                                                                                               |
|------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 메모리                             | 8GB                                                                                                                                                                                                                                                                                                                                                                                           |
| 가상 네트워크 어댑터 수 | 3 Nic: 관리 운영 체제에서 사용 하는 관리의 경우 1, 외부 네트워크에 대 한 액세스를 제공 하는 외부 1, 내부 네트워크에 대 한 액세스만 제공 하는 내부용입니다.                                                                                                                                                            |
| Receive Side Scaling (RSS)         | 관리 NIC에 대 한 기본 RSS 설정을 유지할 수 있습니다. 다음 구성 예는 가상 프로세서가 8개인 VM에 대한 구성입니다. 외부 및 내부 Nic의 경우 다음 Windows PowerShell 명령을 사용 하 여 BaseProcNumber가 0으로 설정 되 고 MaxRssProcessors가 8로 설정 된 RSS를 사용 하도록 설정할 수 있습니다. <br> ```Set-NetAdapterRss "Internal","External" –BaseProcNumber 0 –MaxProcessorNumber 8``` <br> |
| 송신 측 버퍼                   | 관리 NIC의 기본 송신 측 버퍼 설정을 유지할 수 있습니다. 내부 및 외부 Nic 모두에 대해 다음 Windows PowerShell 명령을 사용 하 여 32 MB의 RAM이 있는 송신 측 버퍼를 구성할 수 있습니다. <br> ```Set-NetAdapterAdvancedProperty "Internal","External" –DisplayName "Send Buffer Size" –DisplayValue "32MB"``` <br>                                                       |
| 수신측 버퍼                | 관리 NIC의 기본 수신 측 버퍼 설정을 유지할 수 있습니다. 내부 및 외부 Nic 모두에 대해 다음 Windows PowerShell 명령을 사용 하 여 RAM이 16mb 인 수신측 버퍼를 구성할 수 있습니다. <br> ```Set-NetAdapterAdvancedProperty "Internal","External" –DisplayName "Receive Buffer Size" –DisplayValue "16MB"``` <br>                                            |
| 전달 최적화               | 관리 NIC에 대 한 기본 전달 최적화 설정을 유지할 수 있습니다. 내부 및 외부 Nic 모두에 대해 다음 Windows PowerShell 명령을 사용 하 여 전달 최적화를 사용 하도록 설정할 수 있습니다. <br> ```Set-NetAdapterAdvancedProperty "Internal","External" –DisplayName "Forward Optimization" –DisplayValue "1"``` <br>                                                                      |
