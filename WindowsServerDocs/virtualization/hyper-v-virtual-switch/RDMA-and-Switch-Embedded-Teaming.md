---
title: RDMA(원격 직접 메모리 액세스) 및 SET(Switch Embedded Teaming)
description: 이 항목에서는 Windows Server 2016에서 Hyper-v를 사용 하 여 RDMA (원격 직접 메모리 액세스) 인터페이스를 구성 하는 방법 및 스위치 포함 된 팀 (SET)에 대 한 정보를 제공 합니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: 68c35b64-4d24-42be-90c9-184f2b5f19be
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b39cac842f115a1828c666eec52f17f80971510c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365695"
---
# <a name="remote-direct-memory-access-rdma-and-switch-embedded-teaming-set"></a>RDMA\)를 \(원격 직접 메모리 액세스를 설정 하 고 포함 된 팀 \(집합을 전환\)

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 Windows Server 2016에서 Hyper-v를 사용 하 여 RDMA\) 인터페이스 \(원격 직접 메모리 액세스를 구성 하는 방법에 대 한 정보를 제공 하 고,\)집합 \(스위치 포함 팀에 대 한 정보를 제공 합니다.  

> [!NOTE]
> 이 항목 외에 다음 스위치 포함 된 팀 콘텐츠를 사용할 수 있습니다. 
> - TechNet 갤러리 다운로드: [Windows Server 2016 NIC 및 스위치 포함 된 팀 사용자 가이드](https://gallery.technet.microsoft.com/Windows-Server-2016-839cb607?redir=0)

## <a name="bkmk_rdma"></a>Hyper-v를 사용 하 여 RDMA 인터페이스 구성  

Windows Server 2012 r 2에서는 Hyper-v 가상 스위치에 RDMA 서비스를 바인딩할 수 수를 제공 하는 네트워크 어댑터와 동일한 컴퓨터에서 RDMA와 Hyper-v를 사용 합니다. 이렇게 하면 Hyper-v 호스트에 설치 하는 데 필요한 실제 네트워크 어댑터 수가 늘어납니다.

>[!TIP]
>Windows server 2016 이전 버전의 Windows Server에서는 NIC 팀 또는 Hyper-v 가상 스위치에 바인딩된 네트워크 어댑터에서 RDMA를 구성할 수 없습니다. Windows Server 2016에서는 집합을 사용 하거나 사용 하지 않고 Hyper-v 가상 스위치에 바인딩된 네트워크 어댑터에서 RDMA를 사용 하도록 설정할 수 있습니다.

Windows Server 2016 집합 없이 RDMA를 사용 하는 동안 더 적은 수의 네트워크 어댑터를 사용할 수 있습니다.

아래 이미지는 Windows Server 2012 R2 및 Windows Server 2016 간의 소프트웨어 아키텍처 변경 사항을 보여 줍니다.

![아키텍처 자체가 변경](../media/RDMA-and-SET/rdma_over.jpg)

다음 섹션에서는 Windows PowerShell 명령을 사용 하 여 DCB (데이터 센터 브리징)를 사용 하도록 설정 하 고, RDMA 가상 NIC \(vNIC\)를 사용 하 여 Hyper-v 가상 스위치를 만들고, SET 및 RDMA vNICs를 사용 하 여 Hyper-v 가상 스위치를 만드는 방법에 대 한 지침을 제공 합니다.

### <a name="enable-data-center-bridging-dcb"></a>DCB\) \(데이터 센터 브리징 사용

수렴 된 이더넷 \(RoCE\) 버전의 RDMA를 통해 RDMA를 사용 하기 전에 DCB를 사용 하도록 설정 해야 합니다.  인터넷 광역 RDMA 프로토콜 \(iWARP\) 네트워크에는 필요 하지 않지만 테스트는 모든 이더넷 기반 RDMA 기술이 DCB 보다 잘 작동 하는 것으로 확인 되었습니다. 이 때문에 DCB를 사용 하 여 iWARP RDMA 배포에 대해서도 고려해 야 합니다.

다음 Windows PowerShell 예제 명령은 SMB 다이렉트에 대해 DCB를 사용 하도록 설정 하 고 구성 하는 방법을 보여 줍니다.

DCB 설정

    Install-WindowsFeature Data-Center-Bridging

SMB 다이렉트에 대 한 정책을 설정 합니다.

    New-NetQosPolicy "SMB" -NetDirectPortMatchCondition 445 -PriorityValue8021Action 3

SMB에 대 한 흐름 제어를 설정 합니다.

    Enable-NetQosFlowControl  -Priority 3

다른 트래픽에 대해 흐름 제어가 해제 되어 있는지 확인 합니다.

    Disable-NetQosFlowControl  -Priority 0,1,2,4,5,6,7

대상 어댑터에 정책을 적용 합니다.

    Enable-NetAdapterQos  -Name "SLOT 2"

SMB 다이렉트 대역폭의 30%를 최소로 제공:

`New-NetQosTrafficClass "SMB"  -Priority 3  -BandwidthPercentage 30  -Algorithm ETS`  

시스템에 설치 하는 커널 디버거를 사용 하도록 설정한 경우 다음 명령을 실행 하 여 설정 하는 QoS를 허용 하도록 디버거를 구성 해야 합니다.

디버거를 재정의 합니다. 기본적으로 디버거는 NetQos를 차단 합니다.
 
    Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 -Force

### <a name="create-a-hyper-v-virtual-switch-with-an-rdma-vnic"></a>RDMA vNIC를 사용 하 여 Hyper-v 가상 스위치 만들기

배포에 대해 설정이 필요 하지 않은 경우 다음 Windows PowerShell 명령을 사용 하 여 RDMA vNIC를 사용 하 여 Hyper-v 가상 스위치를 만들 수 있습니다.

> [!NOTE]
> RDMA 가능 실제 nic가 있는 집합 팀을 사용 하 여 사용할 vNICs에 RDMA 리소스를 더 제공 합니다.

    New-VMSwitch -Name RDMAswitch -NetAdapterName "SLOT 2"

호스트 vNICs를 추가 하 고 RDMA를 지원할 수 있도록 설정 합니다.

    Add-VMNetworkAdapter -SwitchName RDMAswitch -Name SMB_1
    Enable-NetAdapterRDMA "vEthernet (SMB_1)" "SLOT 2"

RDMA 기능 확인:

    Get-NetAdapterRdma

###  <a name="bkmk_set-rdma"></a>SET 및 RDMA vNICs를 사용 하 여 Hyper-v 가상 스위치 만들기

RDMA 팀을 지 원하는 Hyper-v 가상 스위치에서 vNICs\) \(Hyper-v 호스트 가상 네트워크 어댑터에서 RDMA 크롤러를 사용 하려면 다음 예제 Windows PowerShell 명령을 사용할 수 있습니다.

    New-VMSwitch -Name SETswitch -NetAdapterName "SLOT 2","SLOT 3" -EnableEmbeddedTeaming $true

호스트 vNICs 추가:

    Add-VMNetworkAdapter -SwitchName SETswitch -Name SMB_1 -managementOS
    Add-VMNetworkAdapter -SwitchName SETswitch -Name SMB_2 -managementOS

많은 스위치는 태그가 지정 된 VLAN 트래픽에 대 한 트래픽 클래스 정보를 전달 하지 않으므로 RDMA 용 호스트 어댑터가 Vlan에 있는지 확인 합니다. 이 예제에서는 두 개의 SMB_ * 호스트 가상 어댑터를 VLAN 42에 할당 합니다.
    
    Set-VMNetworkAdapterIsolation -ManagementOS -VMNetworkAdapterName SMB_1  -IsolationMode VLAN -DefaultIsolationID 42
    Set-VMNetworkAdapterIsolation -ManagementOS -VMNetworkAdapterName SMB_2  -IsolationMode VLAN -DefaultIsolationID 42
    

호스트 vNICs에서 RDMA를 사용 하도록 설정 합니다.

    Enable-NetAdapterRDMA "vEthernet (SMB_1)","vEthernet (SMB_2)" "SLOT 2", "SLOT 3"

RDMA 기능 확인 기능이 0이 아닌지 확인 합니다.

    Get-NetAdapterRdma | fl *


## <a name="switch-embedded-teaming-set"></a>스위치가 포함 된 팀 (설정)  

이 섹션에서는 Windows Server 2016의 스위치 포함 된 팀 (집합)에 대해 간략하게 설명 하 고 다음 섹션을 포함 합니다.

- [개요 설정](#bkmk_over)

- [가용성 설정](#bkmk_avail)

- [집합에 지원 되거나 지원 되지 않는 Nic](#bkmk_nics)

- [Windows Server 네트워킹 기술과의 호환성 설정](#bkmk_compat)

- [모드 및 설정 설정](#bkmk_modes)

- [설정 및 가상 머신 큐 (Vmq)](#bkmk_vmq)

- [설정 및 Hyper-v 네트워크 가상화 (HNV)](#bkmk_hnv)

- [설정 및 실시간 마이그레이션](#bkmk_live)

- [전송 된 패킷에 MAC 주소 사용](#bkmk_mac)

- [집합 팀 관리](#bkmk_manage)

## <a name="bkmk_over"></a>개요 설정

SET은 Hyper-v를 포함 하는 환경에서 사용할 수 있는 대체 NIC 팀 솔루션으로, Windows Server 2016에 SDN\) \(SDN이 포함 된 소프트웨어를 정의 합니다. 일부 NIC 팀 기능은 Hyper-v 가상 스위치에 통합 하는 설정 합니다.

집합 하나 및 8 개의 실제 이더넷 네트워크 어댑터 간에 하나 이상의 소프트웨어 기반 가상 네트워크 어댑터에 그룹화 할 수 있습니다. 이 가상 네트워크 어댑터에는 빠른 성능과 네트워크 어댑터 오류 발생 시 내결함성을 제공합니다.

집합 멤버 네트워크 어댑터 모두 팀에 배치할 수는 동일한 실제 Hyper-v 호스트에 설치 해야 합니다.

> [!NOTE]
> 집합의 사용은 Windows Server 2016에서 Hyper-v 가상 스위치에만 지원 됩니다. Windows Server 2012 r 2의 집합을 배포할 수 없습니다.

팀으로 구성 된 Nic를 동일한 물리적 스위치 또는 다른 실제 스위치에 연결할 수 있습니다. 서로 다른 스위치에 Nic를 연결 하는 경우 두 스위치가 모두 동일한 서브넷에 있어야 합니다.

다음 그림은 집합 아키텍처를 보여 줍니다.

![집합 아키텍처](../media/RDMA-and-SET/set_architecture.jpg)

집합은 Hyper-v 가상 스위치에 통합, 가상 컴퓨터 (VM) 내부에서 SET를 사용할 수 없습니다. 그러나 Vm 내에서 NIC 팀을 사용할 수 있습니다.

자세한 내용은 참조 [가상 컴퓨터 (Vm)의 NIC 팀](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nict-vms)합니다.

또한 집합 아키텍처 팀 인터페이스를 노출 하지 않습니다. 대신, Hyper-v 가상 스위치 포트를 구성 해야 합니다.

## <a name="bkmk_avail"></a>가용성 설정

Hyper-v 및 SDN 스택을 포함 하는 모든 버전의 Windows Server 2016에서 제공 됩니다. 또한 도구는 지원 되는 클라이언트 운영 체제를 실행 하는 원격 컴퓨터에서 집합을 관리 하려면 Windows PowerShell 명령 및 원격 데스크톱 연결을 사용할 수 있습니다.

## <a name="bkmk_nics"></a>집합에 대해 지원 되는 Nic

Windows 하드웨어 자격 및 로고가 전달 된 모든 이더넷 NIC를 사용 하 여 Windows Server 2016의 집합 팀에서 WHQL\) 테스트 \(수 있습니다. 을 설정 하려면 집합 팀의 구성원 인 모든 네트워크 어댑터가 동일 해야 합니다. 즉, 동일한 제조업체, 동일한 모델, 동일한 펌웨어 및 드라이버\)\(해야 합니다. 하나 및 8 개의 네트워크 어댑터 팀에서 간에 집합을 지원 합니다.
  
## <a name="bkmk_compat"></a>Windows Server 네트워킹 기술과의 호환성 설정

집합은 Windows Server 2016의 다음 네트워킹 기술은 호환입니다.

- DCB\) \(데이터 센터 브리징
  
- Hyper-v 네트워크 가상화-NV GRE 및 VxLAN는 모두 Windows Server 2016에서 지원 됩니다.  
- 수신 측 체크섬 오프 로드 \(IPv4, IPv6, TCP\)-설정 된 팀 멤버가이를 지 원하는 경우 지원 됩니다.

- RDMA\) \(원격 직접 메모리 액세스

- SR-IOV\) 단일 루트 i/o 가상화 \(

- 전송 측 체크섬 오프 로드 \(IPv4, IPv6, TCP\)-모든 집합의 팀 멤버가 지원 하는 경우 지원 됩니다.

- VMQ\) \(가상 머신 큐

- RSS\) \(가상 수신측 배율

집합은 Windows Server 2016의 다음 네트워킹 기술과 호환 되지 않습니다.

- 802.1 x 인증. 802.1 x Extensible Authentication Protocol \(EAP\) 패킷이 SET 시나리오의\-Hyper-v 가상 스위치에 의해 자동으로 삭제 됩니다.
 
- IPsec 작업 오프 로드는\)에 대 한 \(합니다. 이는 대부분의 네트워크 어댑터에서 지원 되지 않는 레거시 기술 이며, 존재 하는 경우 기본적으로 사용 하지 않도록 설정 됩니다.

- 호스트 또는 네이티브 운영 체제에서\) QoS \(를 사용 합니다. 이러한 QoS 시나리오는 하이퍼\-V 시나리오가 아니므로 기술이 교차 하지 않습니다. 또한 QoS는 사용할 수 있지만 기본적으로 사용 하도록 설정 되어 있지 않습니다. QoS를 의도적으로 사용 하도록 설정 해야 합니다.

- RSC\)\(수신 측 통합. RSC는 하이퍼\-V 가상 스위치에 의해 자동으로 사용 하지 않도록 설정 됩니다.

- RSS\)\(수신 쪽 배율입니다. Hyper-v는 VMQ 및 VMMQ에 대 한 큐를 사용 하기 때문에 가상 스위치를 만들 때 RSS는 항상 사용 하지 않도록 설정 됩니다.

- TCP Chimney 오프 로드. 이 기술은 기본적으로 사용 되지 않습니다.

- 가상 컴퓨터 QoS \(VM-QoS\). VM QoS는 사용할 수 있지만 기본적으로 사용 하지 않도록 설정 되어 있습니다. 집합 환경에서 VM QoS를 구성 하면 QoS 설정으로 인해 예기치 않은 결과가 발생할 수 있습니다.

## <a name="bkmk_modes"></a>모드 및 설정 설정

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

## <a name="bkmk_vmq"></a>설정 및 가상 머신 큐 (Vmq)

VMQ와는 함께 잘 작동 하며 Hyper-v를 사용 하 고을 설정할 때마다 VMQ를 사용 하도록 설정 해야 합니다.

> [!NOTE]
> 팀 멤버를 모두 설정에서 사용할 수 있는 큐의 총 항상 표시를 설정 합니다. NIC 팀에서이 큐의 Sum 모드를 호출 됩니다.

대부분의 네트워크 어댑터에는 RSS\) 또는 VMQ \(수신 측 크기 조정에 사용할 수 있지만 둘 다 동시에 사용할 수 없는 큐가 있습니다.
  
일부 VMQ 설정을 RSS 큐에 대 한 설정을 보이지만 실제로 기능에 따라 RSS 및 VMQ를 모두 사용 하 여 현재 사용 중인 일반 큐에 설정 합니다. 각 NIC에는 고급 속성의 `*RssBaseProcNumber` 및 `*MaxRssProcessors`값이 있습니다.

다음은 시스템 성능을 향상 시키는 몇 가지 VMQ 설정입니다.

- 이상적으로 각 NIC는 `*RssBaseProcNumber` 2 보다 크거나 같은 짝수로 설정 되어야 합니다. 이는 첫 번째 실제 프로세서 인 코어 0 \(논리 프로세서 0 및 1\)는 일반적으로 대부분의 시스템 처리를 수행 하므로이 실제 프로세서에서 네트워크 처리가 조정 됩니다. 

>[!NOTE]
>일부 컴퓨터 아키텍처에는 실제 프로세서 당 2 개의 논리 프로세서가 없으므로 이러한 컴퓨터의 경우 기본 프로세서가 1 보다 크거나 같아야 합니다. 확실 하지 않은 경우 호스트에서 실제 프로세서 아키텍처 당 2 개의 논리적 프로세서를 사용 한다고 가정 합니다.

- 팀 멤버의 프로세서는 실용적이 고 겹치지 않는 범위에 속해야 합니다. 예를 들어 4 코어 호스트 \(8 개의 논리적 프로세서를 사용 하 여 2 개의 10Gbps Nic 팀과\), 기본 프로세서 2를 사용 하 고 4 개 코어를 사용 하도록 첫 번째를 설정할 수 있습니다. 두 번째는 기본 프로세서 6을 사용 하도록 설정 되 고 2 개 코어를 사용 하도록 설정 됩니다.

## <a name="bkmk_hnv"></a>설정 및 Hyper-v 네트워크 가상화 \(HNV\)

집합은 Windows Server 2016에서 Hyper-v 네트워크 가상화와 완전히 호환 됩니다. HNV 관리 시스템에 따라 설정 된 HNV 트래픽을에 최적화 된 방식으로 네트워크 트래픽 부하를 분산 하는 집합 드라이버에 대 한 정보를 제공 합니다.
  
## <a name="bkmk_live"></a>설정 및 실시간 마이그레이션

실시간 마이그레이션는 Windows Server 2016에서 지원 됩니다.

## <a name="bkmk_mac"></a>전송 된 패킷에 MAC 주소 사용

동적 부하 분산을 사용 하 여 집합 팀을 구성 하는 경우 단일 VM\) 같은 단일 원본 \(의 패킷은 동시에 여러 팀 멤버에 게 분산 됩니다. 

스위치가 혼동 되지 않도록 방지 하 고 MAC 플 래핑 경보를 방지 하려면 SET은 원본 MAC 주소를 선호도가 설정 팀 멤버가 아닌 팀 멤버에서 전송 되는 프레임의 다른 MAC 주소로 바꿉니다. 이 때문에 각 팀 멤버에는 다른 MAC 주소를 사용 하 고 MAC 주소 충돌 하지 않는 한 및 오류가 발생할 때까지 실행할 수 없습니다.

기본 NIC에서 오류가 검색 되 면 팀 구성 소프트웨어는 임시 선호도가 설정 팀 \(구성원으로 사용 하도록 선택 된 팀 구성원의 VM MAC 주소를 사용 하기 시작 합니다. 즉, 이제 VM의 인터페이스\)으로 스위치에 표시 됩니다.

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

System Center Virtual Machine Manager \(VMM\)를 사용 하 여 집합 팀을 관리 하는 것이 좋지만 Windows PowerShell을 사용 하 여 집합을 관리할 수도 있습니다. 다음 섹션에서는 Windows PowerShell 명령 집합을 관리 하에 사용할 수 있습니다.

VMM을 사용 하 여 집합 팀을 만드는 방법에 대 한 자세한 내용은 System Center VMM 라이브러리 항목 [논리 스위치 만들기](https://docs.microsoft.com/system-center/vmm/network-switch)의 "논리 스위치 설정" 섹션을 참조 하세요.
  
### <a name="create-a-set-team"></a>집합 팀 만들기

**새-VMSwitch** Windows PowerShell 명령을 사용 하 여 Hyper-v 가상 스위치를 만들 때와 동시에 집합 팀을 만들어야 합니다.

Hyper-v 가상 스위치를 만들 때 명령 구문에 new **EnableEmbeddedTeaming** 매개 변수를 포함 해야 합니다. 다음 예제에서는 포함 된 팀이 포함 된 **Teamedvswitch** 라는 hyper-v 스위치와 두 개의 초기 팀 멤버가 생성 됩니다.
  
```  
New-VMSwitch -Name TeamedvSwitch -NetAdapterName "NIC 1","NIC 2" -EnableEmbeddedTeaming $true  
```  
  
**NetAdapterName** 에 대 한 인수가 단일 Nic 대신 nic 배열인 경우 Windows PowerShell에서 **EnableEmbeddedTeaming** 매개 변수를 가정 합니다. 결과적으로, 다음과 같은 방식으로 이전 명령이 수정할 수 있습니다.

```  
New-VMSwitch -Name TeamedvSwitch -NetAdapterName "NIC 1","NIC 2"  
```  

만들려는 경우 집합을 사용할 수 있는 스위치를 단일 팀 멤버는 나중에 팀 멤버를 추가할 수 있도록 EnableEmbeddedTeaming 매개 변수를 사용 해야 합니다.

```  
New-VMSwitch -Name TeamedvSwitch -NetAdapterName "NIC 1" -EnableEmbeddedTeaming $true  
```  

### <a name="adding-or-removing-a-set-team-member"></a>집합 팀 멤버 추가 또는 제거

**VMSwitchTeam** 명령에는 **NetAdapterName** 옵션이 포함 되어 있습니다. 집합 팀의 팀 멤버를 변경 하려면 원하는 팀 멤버 목록을 **NetAdapterName** 옵션 뒤에 입력 합니다. **Teamedvswitch** 가 원래 nic 1 및 nic 2를 사용 하 여 만들어진 경우 다음 예제 명령은 set 팀 구성원 "nic 2"를 삭제 하 고 새 set 팀 구성원 "nic 3"을 추가 합니다.
  
```  
Set-VMSwitchTeam -Name TeamedvSwitch -NetAdapterName "NIC 1","NIC 3"  
```  

### <a name="removing-a-set-team"></a>집합 팀을 제거합니다.

집합 팀을 포함 하는 Hyper-v 가상 스위치를 제거 하 여 집합 팀만 제거할 수 있습니다.  Hyper-v 가상 스위치를 제거 하는 방법에 대 한 정보는 [-VMSwitch](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/remove-vmswitch) 항목을 참조 하십시오. 다음 예제에서는 **Setvswitch**라는 가상 스위치를 제거 합니다.

```  
Remove-VMSwitch "SETvSwitch"  
```  

### <a name="changing-the-load-distribution-algorithm-for-a-set-team"></a>변경 집합 팀에 대 한 부하 분산 알고리즘

**VMSwitchTeam** cmdlet에는 **LoadBalancingAlgorithm** 옵션이 있습니다. 이 옵션은 다음 두 가지 가능한 값 중 하나를 사용 합니다. **Hypervport** 또는 **Dynamic**. 를 설정 하거나 스위치 포함 된 팀을 위한 부하 분산 알고리즘을 변경 하려면이 옵션을 사용 합니다. 

다음 예제에서 **Teamedvswitch** 라는 VMSwitchTeam는 **동적** 부하 분산 알고리즘을 사용 합니다.  
```  
Set-VMSwitchTeam -Name TeamedvSwitch -LoadBalancingAlgorithm Dynamic  
```  
### <a name="affinitizing-virtual-interfaces-to-physical-team-members"></a>물리적 팀 구성원에 게 가상 인터페이스 한

집합을 사용 하면 가상 인터페이스 \((Hyper-v 가상 스위치 포트\), 팀의 실제 Nic 중 하나) 간에 선호도를 만들 수 있습니다. 

예를 들어 SMB\-에 대해 두 개의 호스트 vNICs를 만들 경우 [설정 및 RDMA vNICs를 사용 하 여 Hyper-v 가상 스위치 만들기](#bkmk_set-rdma)섹션에서와 같이 두 vnics가 서로 다른 팀 구성원을 사용 하는지 확인할 수 있습니다. 

해당 섹션의 스크립트에를 추가 하면 다음 Windows PowerShell 명령을 사용할 수 있습니다.

    Set-VMNetworkAdapterTeamMapping -VMNetworkAdapterName SMB_1 –ManagementOS –PhysicalNetAdapterName “SLOT 2”
    Set-VMNetworkAdapterTeamMapping -VMNetworkAdapterName SMB_2 –ManagementOS –PhysicalNetAdapterName “SLOT 3”

이 항목은 [Windows Server 2016 NIC 및 스위치 포함 된 팀 사용자 가이드](https://gallery.technet.microsoft.com/Windows-Server-2016-839cb607?redir=0)의 4.2.5 섹션에 자세히 설명 되어 있습니다.
