---
title: RDMA(원격 직접 메모리 액세스) 및 SET(Switch Embedded Teaming)
description: 이 항목에서는 Windows Server 2016의 Hyper-v를 사용 하 여 정보에 대 한 스위치 포함 된 팀 (SET) 외에도 원격 직접 메모리 액세스 (RDMA) 인터페이스를 구성에 정보를 제공 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: 68c35b64-4d24-42be-90c9-184f2b5f19be
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c945144194ac86623bfa8ce60a306f0202df0874
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881664"
---
# <a name="remote-direct-memory-access-rdma-and-switch-embedded-teaming-set"></a>원격 직접 메모리 액세스 \(RDMA\) 포함 된 팀 전환 \(설정\)

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 원격 직접 메모리 액세스를 구성 하는 방법에 설명 \(RDMA\) 스위치 포함 된 팀에 대 한 정보 뿐만 아니라 Windows Server 2016의 Hyper-v와 상호 작용 \(설정\)합니다.  

> [!NOTE]
> 이 항목 외에 다음 스위치 포함 된 팀 콘텐츠는 사용할 수 있습니다. 
> - TechNet 갤러리 다운로드: [Windows Server 2016 NIC 및 스위치 포함 된 팀 사용자 가이드](https://gallery.technet.microsoft.com/Windows-Server-2016-839cb607?redir=0)

## <a name="bkmk_rdma"></a>Hyper-v가 설치 된 구성 RDMA 인터페이스  

Windows Server 2012 r 2에서는 Hyper-v 가상 스위치에 RDMA 서비스를 바인딩할 수 수를 제공 하는 네트워크 어댑터와 동일한 컴퓨터에서 RDMA와 Hyper-v를 사용 합니다. 이렇게 하면 Hyper-v 호스트에 설치 하는 데 필요한 실제 네트워크 어댑터 수가 늘어납니다.

>[!TIP]
>Windows Server 2016 이전의 Windows Server 버전에서는 불가능 NIC 팀에 또는 Hyper-v 가상 스위치에 바인딩된 네트워크 어댑터에서 RDMA를 구성 하려면. Windows Server 2016 집합 없이 Hyper-v 가상 스위치에 바인딩된 네트워크 어댑터에서 RDMA를 사용할 수 있습니다.

Windows Server 2016 집합 없이 RDMA를 사용 하는 동안 더 적은 수의 네트워크 어댑터를 사용할 수 있습니다.

아래 이미지는 Windows Server 2012 R2 및 Windows Server 2016 간의 소프트웨어 아키텍처 변경 사항을 보여 줍니다.

![아키텍처 자체가 변경](../media/RDMA-and-SET/rdma_over.jpg)

다음 섹션에서는 Windows PowerShell 명령을 사용 하 여 데이터 센터 브리징 (DCB)을 사용 하도록 설정, RDMA 가상 NIC를 사용 하 여 Hyper-v 가상 스위치를 만드는 방법에 대 한 지침을 제공 \(vNIC\), 집합을 사용 하 여 Hyper-v 가상 스위치를 만들고 및 RDMA vNICs 합니다.

### <a name="enable-data-center-bridging-dcb"></a>사용 데이터 센터 브리징 \(DCB\)

모든 RDMA over Converged Ethernet 사용 하기 전에 \(RoCE\) 버전 RDMA의 DCB를 사용 해야 합니다.  인터넷 넓은 영역 RDMA 프로토콜에 대 한 필요는 없지만 \(iWARP\) 네트워크 모든 RDMA 이더넷 기반 기술 DCB를 사용 하 여 더 잘 작동 하는지 확인 했습니다 테스트 합니다. 이 때문에 DCB를 사용 하 여 iWARP RDMA 배포에 대해서도 고려해 야 합니다.

다음 Windows PowerShell 예제에서는 명령을 사용 하 여 SMB 다이렉트에 DCB를 구성 하는 방법을 보여 줍니다.

DCB를 켜기

    Install-WindowsFeature Data-Center-Bridging

SMB 다이렉트에 대 한 정책을 설정 합니다.

    New-NetQosPolicy "SMB" -NetDirectPortMatchCondition 445 -PriorityValue8021Action 3

SMB에 대 한 흐름 제어를 켭니다.

    Enable-NetQosFlowControl  -Priority 3

다른 트래픽에 대 한 흐름 제어 꺼져 있는지 확인 합니다.

    Disable-NetQosFlowControl  -Priority 0,1,2,4,5,6,7

정책을 대상 어댑터에 적용 됩니다.

    Enable-NetAdapterQos  -Name "SLOT 2"

SMB 다이렉트 30%의 최소 대역폭을 제공 합니다.

`New-NetQosTrafficClass "SMB"  -Priority 3  -BandwidthPercentage 30  -Algorithm ETS`  

시스템에 설치 하는 커널 디버거를 사용 하도록 설정한 경우 다음 명령을 실행 하 여 설정 하는 QoS를 허용 하도록 디버거를 구성 해야 합니다.

디버거 재정의-기본적으로 디버거는 NetQos를 차단 합니다.
 
    Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 -Force

### <a name="create-a-hyper-v-virtual-switch-with-an-rdma-vnic"></a>RDMA vNIC를 사용 하 여 Hyper-v 가상 스위치 만들기

집합 배포에 필요 하지 않은 경우에 RDMA vNIC를 사용 하 여 Hyper-v 가상 스위치를 만들려면 다음 Windows PowerShell 명령을 사용할 수 있습니다.

> [!NOTE]
> RDMA 가능 실제 nic가 있는 집합 팀을 사용 하 여 사용할 vNICs에 RDMA 리소스를 더 제공 합니다.

    New-VMSwitch -Name RDMAswitch -NetAdapterName "SLOT 2"

호스트 Vnic를 추가 하 고 RDMA 수 있도록 합니다.

    Add-VMNetworkAdapter -SwitchName RDMAswitch -Name SMB_1
    Enable-NetAdapterRDMA "vEthernet (SMB_1)" "SLOT 2"

RDMA 기능을 확인 합니다.

    Get-NetAdapterRdma

###  <a name="bkmk_set-rdma"></a>SET 및 RDMA Vnic를 사용 하 여 Hyper-v 가상 스위치 만들기

RDMA를 활용 하려면 hyper-v 기능을 갖추고 호스트 가상 네트워크 어댑터 \(Vnic\) Hyper-v 가상 스위치를 지 원하는 RDMA 팀에서 이러한 예제에서는 Windows PowerShell 명령을 사용할 수 있습니다.

    New-VMSwitch -Name SETswitch -NetAdapterName "SLOT 2","SLOT 3" -EnableEmbeddedTeaming $true

호스트 Vnic를 추가 합니다.

    Add-VMNetworkAdapter -SwitchName SETswitch -Name SMB_1 -managementOS
    Add-VMNetworkAdapter -SwitchName SETswitch -Name SMB_2 -managementOS

많은 스위치 태그가 지정 되지 않은 VLAN 트래픽을 트래픽 클래스 정보를 전달 won't, 따라서 RDMA에 대 한 호스트 어댑터를 Vlan에 있는지를 확인 합니다. 이 예제에서는 할당 두 SMB_ * 호스트 가상 어댑터를 VLAN 42입니다.
    
    Set-VMNetworkAdapterIsolation -ManagementOS -VMNetworkAdapterName SMB_1  -IsolationMode VLAN -DefaultIsolationID 42
    Set-VMNetworkAdapterIsolation -ManagementOS -VMNetworkAdapterName SMB_2  -IsolationMode VLAN -DefaultIsolationID 42
    

호스트 Vnic에서 RDMA를 사용 하도록 설정 합니다.

    Enable-NetAdapterRDMA "vEthernet (SMB_1)","vEthernet (SMB_2)" "SLOT 2", "SLOT 3"

RDMA 기능 확인 기능은 0이 아닌 위치에 있는지 확인 합니다.

    Get-NetAdapterRdma | fl *


## <a name="bkmk_sswitchembedded"></a>포함 된 팀 (SET) 전환  

이 섹션의 스위치 포함 된 팀 (SET) Windows Server 2016의 개요를 제공 하며 다음과 같은 섹션이 포함 되어 있습니다.

- [설정 개요](#bkmk_over)

- [가용성 집합](#bkmk_avail)

- [집합에 대 한 지원 및 미지원 Nic](#bkmk_nics)

- [Windows Server 네트워킹 기술와의 호환성 설정](#bkmk_compat)

- [집합 모드 및 설정](#bkmk_modes)

- [집합 및 가상 머신 큐 (Vmq)](#bkmk_vmq)

- [Hyper-v 네트워크 가상화 (HNV) 및 집합](#bkmk_hnv)

- [설정 및 실시간 마이그레이션](#bkmk_live)

- [전송 된 패킷에서 MAC 주소 사용](#bkmk_mac)

- [집합 팀 관리](#bkmk_manage)

## <a name="bkmk_over"></a>설정 개요

집합은 Hyper-v 및 소프트웨어 정의 네트워킹을 포함 하는 환경에서 사용할 수 있는 대체 NIC 팀 솔루션 \(SDN\) Windows Server 2016의 스택. 일부 NIC 팀 기능은 Hyper-v 가상 스위치에 통합 하는 설정 합니다.

집합 하나 및 8 개의 실제 이더넷 네트워크 어댑터 간에 하나 이상의 소프트웨어 기반 가상 네트워크 어댑터에 그룹화 할 수 있습니다. 이 가상 네트워크 어댑터에는 빠른 성능과 네트워크 어댑터 오류 발생 시 내결함성을 제공합니다.

집합 멤버 네트워크 어댑터 모두 팀에 배치할 수는 동일한 실제 Hyper-v 호스트에 설치 해야 합니다.

> [!NOTE]
> 집합의 사용은 Windows Server 2016에서 Hyper-v 가상 스위치에만 지원 됩니다. Windows Server 2012 r 2의 집합을 배포할 수 없습니다.

동일한 물리적 스위치 또는 서로 다른 실제 스위치에 그룹화 된 Nic를 연결할 수 있습니다. 서로 다른 스위치에 Nic를 연결 하는 경우 두 스위치가 모두 동일한 서브넷에 있어야 합니다.

다음 그림은 집합 아키텍처를 보여 줍니다.

![집합 아키텍처](../media/RDMA-and-SET/set_architecture.jpg)

집합은 Hyper-v 가상 스위치에 통합, 가상 컴퓨터 (VM) 내부에서 SET를 사용할 수 없습니다. 그러나 Vm 내에서 NIC 팀을 사용할 수 있습니다.

자세한 내용은 참조 [가상 컴퓨터 (Vm)의 NIC 팀](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nict-vms)합니다.

또한 집합 아키텍처 팀 인터페이스를 노출 하지 않습니다. 대신, Hyper-v 가상 스위치 포트를 구성 해야 합니다.

## <a name="bkmk_avail"></a>가용성 집합

Hyper-v 및 SDN 스택을 포함 하는 모든 버전의 Windows Server 2016에서 제공 됩니다. 또한 도구는 지원 되는 클라이언트 운영 체제를 실행 하는 원격 컴퓨터에서 집합을 관리 하려면 Windows PowerShell 명령 및 원격 데스크톱 연결을 사용할 수 있습니다.

## <a name="bkmk_nics"></a>집합에 대 한 지원 되는 Nic

Windows 하드웨어 규정 및 로고 경과 된 NIC를 사용할 수 있습니다 \(WHQL\) Windows Server 2016에서 집합 팀에서 테스트 합니다. 집합 필요 집합 팀의 구성원 인 모든 네트워크 어댑터가 동일 해야 \(즉, 동일한 제조업체, 동일한 모델, 동일한 펌웨어 및 드라이버\)합니다. 하나 및 8 개의 네트워크 어댑터 팀에서 간에 집합을 지원 합니다.
  
## <a name="bkmk_compat"></a>Windows Server 네트워킹 기술와의 호환성 설정

집합은 Windows Server 2016의 다음 네트워킹 기술은 호환입니다.

- 데이터 센터 브리징 \(DCB\)
  
- Hyper-v 네트워크 가상화-NV GRE 및 VxLAN는 모두 Windows Server 2016에서 지원 됩니다.  
- 수신 측 체크섬 오프 로드 \(IPv4, IPv6, TCP\) -이들을 지 원하는 모든 팀 멤버를 설정 하는 경우 이러한가 지원 됩니다.

- 원격 직접 메모리 액세스 \(RDMA\)

- 단일 루트 I/O 가상화 \(SR-IOV\)

- 전송 측 체크섬 오프 로드 \(IPv4, IPv6, TCP\) -지 원하는 모든 팀 멤버를 설정 하는 경우 이러한가 지원 됩니다.

- 가상 머신 큐 \(VMQ\)

- 가상 수신측 배율 \(RSS\)

집합의 Windows Server 2016 다음 네트워킹 기술은와 호환 되지 않습니다.

- 802.1x 인증 합니다. 802.1x Extensible Authentication Protocol \(EAP\) 자동으로에서 패킷을 하이퍼\-집합 시나리오에서 가상 스위치입니다.
 
- IPsec 작업 오프 로드 \(IPsecTO\)합니다. 대부분의 네트워크 어댑터에서 지원 되지 않는 레거시 기술 이며 기본적으로 비활성화 되어 파일이 위치 합니다.

- QoS를 사용 하 여 \(pacer.exe\) 호스트 또는 네이티브 운영 체제입니다. 이러한 QoS 시나리오 하이퍼 없는\-V 시나리오, 기술 교차 하지 않습니다. 또한 QoS를 사용할 수 있지만 기본적으로 사용 안 함-QoS 의도적으로 사용 하도록 설정 해야 합니다.

- 수신 쪽 병합 \(RSC\)합니다. RSC는 하이퍼에서 자동으로 비활성화 됩니다\-V 가상 스위치입니다.

- 수신측 배율 \(RSS\)입니다. Hyper-v에서는 큐 VMQ 및 VMMQ 때문에 가상 스위치를 만들 때 RSS 항상 비활성화 됩니다.

- TCP Chimney 오프 로드 합니다. 이 기술은 기본적으로 비활성화 됩니다.

- 가상 머신 QoS \(VM QoS\)합니다. VM QoS를 사용할 수 있지만 기본적으로 비활성화 합니다. 집합 환경에서 VM QoS를 구성 하는 경우 QoS 설정을 예기치 않은 결과가 발생 하면 됩니다.

## <a name="bkmk_modes"></a>집합 모드 및 설정

NIC 팀을 달리 집합 팀을 만들 때 구성할 수 없습니다 팀 이름입니다. 또한 NIC 팀을에서 지원 되는 대기 중인 어댑터를 사용 하 여 있지만 집합에서 지원 되지 않습니다. 집합을 배포할 때 모든 네트워크 어댑터 활성 상태 이며 대기 모드에 없습니다.

NIC 팀 및 집합 간의 또 다른 주요 차이점은 있는지 NIC 팀 세 개의 서로 다른 팀 구성 모드의 선택 집합만 지원 하지만 **독립 스위치** 모드입니다. 스위치 독립 모드 스위치 또는 스위치를 설정 하는 팀 멤버가 연결 된 집합 팀의 존재를 인식 하지 못합니다 및 팀 멤버를 설정 하는 네트워크 트래픽을 분산 하는 방법을 결정 하지는 않습니다-대신 집합 팀 인바운드 네트워크 트래픽을 분산 팀 멤버를 설정 합니다.

새로운 집합 팀을 만들 때에 다음 팀 속성을 구성 해야 합니다.

- 멤버 어댑터

- 부하 분산 모드

### <a name="member-adapters"></a>멤버 어댑터

집합 팀을 만들 때 집합 팀 구성원 어댑터로 Hyper-v 가상 스위치에 바인딩되는 최대 8 개의 동일한 네트워크 어댑터를 지정 해야 합니다.

### <a name="load-balancing-mode"></a>부하 분산 모드

배포 모드는 부하 분산 집합에 대 한 옵션 팀 **Hyper-v 포트** 및 **동적**합니다.

**Hyper-v 포트**

Vm은 Hyper-v 가상 스위치에서 포트에 연결 됩니다. 집합 팀을 위한 Hyper-v 포트 모드를 사용 하면 Hyper-v 가상 스위치 포트와 연결 된 MAC 주소 집합 팀 구성원 간에 네트워크 트래픽을 분리 하는 데 사용 됩니다.

> [!NOTE]
> 집합 패킷 직접 팀 모드와 함께에서 사용 하는 경우  **독립 스위치** 및 부하 분산 모드 **Hyper-v 포트** 필요 합니다.

인접 스위치가 항상 특정 MAC 주소는 해당된 포트에서을 인식 하기 때문에 스위치에서 MAC 주소가 있는 포트를 수신 부하 (트래픽 스위치에서 호스트에)를 배포 합니다. 특히 유용 가상 컴퓨터 큐 (Vmq)를 사용 하는 큐 트래픽이 도착 하는 데 필요한 특정 NIC에 배치할 수 있으므로 합니다.

그러나 호스트에 몇 가지 Vm만 있는 경우이 모드는 균형이 분포를 달성 하기 위해 충분히 세부적인 아닐 수도 있습니다. 이 모드는 항상 단일 인터페이스에서 사용할 수 있는 대역폭을 단일 VM (즉, 단일 스위치 포트에서 트래픽)를 제한 합니다.

**Dynamic**

이 부하 분산 모드는 다음과 같은 이점이 있습니다.

- 아웃 바운드 로드 TCP 포트 및 IP 주소는 해시에 따라 배포 됩니다.  동적 모드도 다시 부하를 분산 실시간으로 지정 된 아웃 바운드 흐름 집합 팀 구성원 간에 앞뒤로 이동할 수 있도록 합니다.

- 인바운드 로드 Hyper-v 포트 모드와 동일 하 게 배포 됩니다.

이 모드에서는 아웃 바운드 로드는 동적으로 flowlets의 개념에 따라 분산 됩니다. 실제 음성 단어 및 문장 끝에 자연 스러운 나누기가 하는 것 처럼 TCP 흐름 (TCP 통신 스트림을)는 또한 자연스럽 게 발생 나누기를 가집니다. 이러한 두 나누기 사이 TCP 흐름의 부분을 flowlet 라고 합니다.

동적 모드 알고리즘을 flowlet 경계 발생 했습니다.-예를 들어 충분 한 길이의 중단 발생 했을 때 TCP 흐름-에서 감지할 때 알고리즘의 흐름은 해당 하는 경우 다른 팀 멤버 자동으로 변경 합니다.  드문 경우에 따라 알고리즘 흐름 어떤 flowlets를 포함 하지 않는 균형 다시 맞추기 정기적으로 될 수 있습니다. 이 때문에 TCP 흐름 및 팀 멤버 간에 선호도 팀 멤버의 부하를 분산 동적 분산 알고리즘에 따라 언제 든 지 변경할 수 있습니다.

## <a name="bkmk_vmq"></a>집합 및 가상 머신 큐 (Vmq)

VMQ 집합과 함께 잘 작동 하 고 설정 및 Hyper-v를 사용 하는 때마다 VMQ를 사용 하도록 설정 해야 합니다.

> [!NOTE]
> 팀 멤버를 모두 설정에서 사용할 수 있는 큐의 총 항상 표시를 설정 합니다. NIC 팀에서이 큐의 Sum 모드를 호출 됩니다.

대부분의 네트워크 어댑터 중 하나 수신측 배율에 대 한 사용할 수 있는 큐가 있는데 \(RSS\) 또는 VMQ, 하지만, 동시에 둘 다 없습니다.
  
일부 VMQ 설정을 RSS 큐에 대 한 설정을 보이지만 실제로 기능에 따라 RSS 및 VMQ를 모두 사용 하 여 현재 사용 중인 일반 큐에 설정 합니다. 각 NIC에는 고급 속성에 대 한 값 `*RssBaseProcNumber` 고 `*MaxRssProcessors`입니다.

다음은 시스템 성능을 향상 시키는 몇 가지 VMQ 설정입니다.

- 각 NIC 있어야 이상적으로 `*RssBaseProcNumber` 보다 크거나 같음 짝수 설정 2 (2). 왜냐하면 첫 번째 물리적 프로세서 코어 0 \(논리적 프로세서 0과 1\), 일반적으로이 실제 프로세서에서 네트워크 처리를 steered 해야 하므로 시스템 처리 과정의 대부분을 수행 합니다. 

>[!NOTE]
>일부 컴퓨터 아키텍처 없는 없으므로 실제 프로세서당 두 개의 논리 프로세서 1 보다 크거나 같은 경우 이러한 컴퓨터의 기본 프로세서 이어야 합니다. 확실 하지 않은의 경우 호스트는 2 개 논리적 프로세서를 사용 하는 실제 프로세서 아키텍처 당를 가정 합니다.

- 팀 구성원의 프로세서는 하는 것이 실용적이 고 겹치지 않는 이어야 합니다. 4 코어 호스트의 예를 들어 \(논리 프로세서 8\) 의 2 10Gbps Nic 팀을 사용 하 여 첫 번째 2의 기본 프로세서를 사용 하 고 4 개 코어를 사용 하 여 설정할 수 있습니다; 두 번째 6 기본 프로세서를 사용 하 고 2 개의 코어를 사용 하 여 설정 됩니다.

## <a name="bkmk_hnv"></a>집합 및 Hyper-v 네트워크 가상화 \(HNV\)

집합은 Windows Server 2016에서 Hyper-v 네트워크 가상화와 완전히 호환 됩니다. HNV 관리 시스템에 따라 설정 된 HNV 트래픽을에 최적화 된 방식으로 네트워크 트래픽 부하를 분산 하는 집합 드라이버에 대 한 정보를 제공 합니다.
  
## <a name="bkmk_live"></a>설정 및 실시간 마이그레이션

실시간 마이그레이션은 Windows Server 2016에서 지원 됩니다.

## <a name="bkmk_mac"></a>전송 된 패킷에서 MAC 주소 사용

동적 부하 분산을 사용 하면 단일 원본에서 패킷 집합 팀을 구성 하는 경우 \(단일 VM과 같은\) 여러 팀 구성원 간에 동시에 배포 됩니다. 

혼란에서 스위치를 방지 하 고 MAC 날개를 퍼 덕 경보를 방지 하기 위해 설정 하려면 원본을 MAC 주소 선호도 설정 된 팀 멤버가 아닌 팀 멤버를 통해 전송 되는 프레임에서 다른 MAC 주소를 바꿉니다. 이 때문에 각 팀 멤버에는 다른 MAC 주소를 사용 하 고 MAC 주소 충돌 하지 않는 한 및 오류가 발생할 때까지 실행할 수 없습니다.

기본 NIC에는 오류가 감지 되 면 팀 소프트웨어 설정 임시 선호도 설정 된 팀 구성원 역할을 하도록 선택 된 팀 멤버에 VM의 MAC 주소를 사용 하 여 시작 \(, 즉 vm의 스위치에 표시 됩니다 인터페이스\)합니다.

이 변경 된 보내려는 VM의 MAC 주소를 사용 하는 VM의 선호도 설정 된 팀 멤버에 해당 소스로 MAC 주소는 트래픽에 적용 됩니다. 다른 트래픽 어떤 원본 MAC 주소는 오류 전에 사용 되는 것으로 보내야 하는 계속 됩니다.

다음은 팀의 팀을 구성 하는 방법에 따라 MAC 주소 대체 동작 집합을 설명 하는 목록:

- Hyper-v 포트 배포와 함께 스위치 독립 모드

    - 팀 멤버에 모든 vmSwitch 포트 설정 됩니다.
  
    - 포트 설정 됩니다 팀 멤버에 모든 패킷이 전송  
  
    - 소스 MAC 대체 이루어집니다.  
  
- 동적 배포와 함께 스위치 독립 모드
  
    - 팀 멤버에 모든 vmSwitch 포트 설정 됩니다.  
  
    - 모든 ARP/NS 패킷은 전송 하는 포트는 선호도 설정 된 팀 멤버에  
  
    - 선호도 설정 된 팀 멤버는 팀 멤버에 전송 되는 패킷을 소스 수행 하는 MAC 주소 교체  
  
    - 선호도 설정 된 팀 멤버가 아닌 팀 멤버에 전송 되는 패킷을 수행 하는 원본 MAC 주소 교체는  
  
## <a name="bkmk_manage"></a>집합 팀 관리

그러나 System Center Virtual Machine Manager 사용 하는 것이 좋습니다 \(VMM\) 집합을 관리할 팀이, 이용할 수 있습니다 Windows PowerShell 집합을 관리할 수 있습니다. 다음 섹션에서는 Windows PowerShell 명령 집합을 관리 하에 사용할 수 있습니다.

VMM을 사용 하 여 팀 집합을 만드는 방법에 대 한 내용은 System Center VMM 라이브러리 항목의 "논리 스위치 설정" 섹션을 참조 하세요 [논리 스위치를 만들고](https://docs.microsoft.com/system-center/vmm/network-switch)합니다.
  
### <a name="create-a-set-team"></a>집합 팀 만들기

집합 팀을 사용 하 여 Hyper-v 가상 스위치를 만드는 동시에 만들어야 합니다 **New-vmswitch** Windows PowerShell 명령을 합니다.

Hyper-v 가상 스위치를 만들 때 새 포함 해야 합니다 **EnableEmbeddedTeaming** 명령 구문에 대 한 매개 변수입니다. 다음 예제에서는 Hyper-v 스위치 이름이 **TeamedvSwitch** 포함 된 팀 및 두 개의 초기 팀 멤버가 생성 됩니다.
  
```  
New-VMSwitch -Name TeamedvSwitch -NetAdapterName "NIC 1","NIC 2" -EnableEmbeddedTeaming $true  
```  
  
합니다 **EnableEmbeddedTeaming** Windows PowerShell에서 매개 변수로 간주 됩니다 때 인수 **NetAdapterName** 는 단일 nic. 대신 Nic의 배열인 결과적으로, 다음과 같은 방식으로 이전 명령이 수정할 수 있습니다.

```  
New-VMSwitch -Name TeamedvSwitch -NetAdapterName "NIC 1","NIC 2"  
```  

만들려는 경우 집합을 사용할 수 있는 스위치를 단일 팀 멤버는 나중에 팀 멤버를 추가할 수 있도록 EnableEmbeddedTeaming 매개 변수를 사용 해야 합니다.

```  
New-VMSwitch -Name TeamedvSwitch -NetAdapterName "NIC 1" -EnableEmbeddedTeaming $true  
```  

### <a name="adding-or-removing-a-set-team-member"></a>집합 팀 멤버 추가 또는 제거

**집합 VMSwitchTeam** 명령에 포함 된 **NetAdapterName** 옵션입니다. 집합 팀의 팀 멤버를 변경 하려면 원하는 후 팀 멤버 목록을 입력 합니다 **NetAdapterName** 옵션입니다. 하는 경우 **TeamedvSwitch** 집합 팀 구성원 "NIC 2"을 삭제 하 고 새 SET 팀 멤버를 추가 하는 다음 예제 명령은 다음 NIC 1과 NIC 2를 사용 하 여 원래 생성 된 "NIC 3".
  
```  
Set-VMSwitchTeam -Name TeamedvSwitch -NetAdapterName "NIC 1","NIC 3"  
```  

### <a name="removing-a-set-team"></a>집합 팀을 제거합니다.

집합 팀 집합 팀을 포함 하는 Hyper-v 가상 스위치를 제거 해야만 제거할 수 있습니다.  항목을 사용 하 여 [Remove-vmswitch](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/remove-vmswitch) Hyper-v 가상 스위치를 제거 하는 방법에 대 한 정보에 대 한 합니다. 다음 예제에서는 라는 가상 스위치를 제거 **SETvSwitch**합니다.

```  
Remove-VMSwitch "SETvSwitch"  
```  

### <a name="changing-the-load-distribution-algorithm-for-a-set-team"></a>변경 집합 팀에 대 한 부하 분산 알고리즘

합니다 **집합 VMSwitchTeam** cmdlet에는 **LoadBalancingAlgorithm** 옵션입니다. 이 옵션의 두 가지 값 중 하나를 사용 합니다. **HyperVPort** 나 **동적**합니다. 를 설정 하거나 스위치 포함 된 팀을 위한 부하 분산 알고리즘을 변경 하려면이 옵션을 사용 합니다. 

다음 예제는 VMSwitchTeam 이름이 **TeamedvSwitch** 사용 하는 **동적** 부하 분산 알고리즘.  
```  
Set-VMSwitchTeam -Name TeamedvSwitch -LoadBalancingAlgorithm Dynamic  
```  
### <a name="affinitizing-virtual-interfaces-to-physical-team-members"></a>실제 팀 멤버에 해 가상 인터페이스

집합을 사용 하면 가상 인터페이스 간에 선호도 만들 수 있습니다 \(즉, Hyper-v 가상 스위치 포트\) 하 고 팀의 Nic 중 하나입니다. 

예를 들어 만들 경우 두 개의 호스트 Vnic SMB\-섹션과 직접 [SET 및 RDMA Vnic를 사용 하 여 Hyper-v 가상 스위치 만들기](#bkmk_set-rdma), 다른 팀 멤버 두 Vnic에 사용 하는 것을 확인할 수 있습니다. 

해당 섹션의 스크립트를 추가, 다음 Windows PowerShell 명령을 사용할 수 있습니다.

    Set-VMNetworkAdapterTeamMapping -VMNetworkAdapterName SMB_1 –ManagementOS –PhysicalNetAdapterName “SLOT 2”
    Set-VMNetworkAdapterTeamMapping -VMNetworkAdapterName SMB_2 –ManagementOS –PhysicalNetAdapterName “SLOT 3”

이 항목의 4.2.5 섹션에서 자세히 살펴본 합니다 [Windows Server 2016 NIC 및 스위치 포함 팀 사용자 가이드](https://gallery.technet.microsoft.com/Windows-Server-2016-839cb607?redir=0)합니다.
