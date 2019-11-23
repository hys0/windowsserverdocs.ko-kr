---
title: Windows Server 지원 네트워킹 시나리오
description: 이 항목에서는 Windows Server 2016 이상에서 지원 되는 새 네트워킹 시나리오에 대 한 정보를 제공 합니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.date: ''
ms.assetid: 6de4232d-b0b3-4e43-8735-ebae35ae4f9f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f338ddf0a7d3a4fe41277ddbf49b0c3db34ae11b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71395702"
---
# <a name="windows-server-supported-networking-scenarios"></a>Windows Server 지원 네트워킹 시나리오

>적용 대상: Windows Server \(반기 채널\), Windows Server 2016

이 항목 수 또는이 버전의 Windows Server 2016를 사용 하 여 수행할 수 있는 지원 되거나 지원 되지 않는 시나리오에 대 한 정보를 제공 합니다.  
>[!IMPORTANT]
>모든 프로덕션 시나리오에 대 한 original equipment manufacturer에서 서명 된 하드웨어가 최신 드라이버를 사용 하 여 \(OEM\) 또는 독립 하드웨어 공급 업체 \(IHV\)합니다.
  
## <a name="bkmk_supp"></a>지원 되는 네트워킹 시나리오

이 섹션에는 Windows Server 2016 용 지원 되는 네트워킹 시나리오에 대 한 정보를 포함 및 시나리오 범주가 포함 됩니다.  
  
-   [SDN (소프트웨어 정의 네트워킹) 시나리오](#bkmk_sdn)  
  
-   [네트워크 플랫폼 시나리오](#bkmk_netp)  
  
-   [DNS 서버 시나리오](#bkmk_dns)  
  
-   [DHCP 및 DNS를 사용 하는 IPAM 시나리오](#bkmk_ipam)  
  
-   [NIC 팀 시나리오](#bkmk_nicteam)

- [\) 시나리오를 설정 하 \(포함 된 팀 전환](#bkmk_set)
  
### <a name="bkmk_sdn"></a>SDN (소프트웨어 정의 네트워킹) 시나리오
 
Windows Server 2016 SDN 시나리오를 배포 하려면 다음 문서를 사용할 수 있습니다.  
  
  
-   [스크립트를 사용 하 여 소프트웨어 정의 네트워크 인프라 배포](sdn/deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)  
  
자세한 내용은 참조 [소프트웨어 정의 네트워킹 & #40; SDN (& a) #41;](sdn/software-defined-networking.md)합니다.  
  
#### <a name="bkmk_netc"></a>네트워크 컨트롤러 시나리오

네트워크 컨트롤러 시나리오를 수행할 수 있습니다.  
  
-   배포 하 고 네트워크 컨트롤러의 다중 노드 인스턴스를 관리 합니다. 자세한 내용은 참조 [Windows PowerShell을 사용 하 여 네트워크 컨트롤러 배포](sdn/deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)합니다.  
  
-   네트워크 컨트롤러를 사용 하 여 프로그래밍 방식으로 REST Northbound API를 사용 하 여 네트워크 정책을 정의 합니다.  
  
-   네트워크 컨트롤러를 사용 하 여 Hyper-v 네트워크 가상화-NVGRE 또는 VXLAN 캡슐화를 사용 하 여 가상 네트워크 만들기 및 관리 합니다.  
  
자세한 내용은 [네트워크 컨트롤러](sdn/technologies/network-controller/Network-Controller.md)를 참조하세요.  
  
#### <a name="bkmk_netf"></a>네트워크 기능 가상화 (NFV) 시나리오  
NFV 시나리오를 수행할 수 있습니다.  
  
-   배포 하 고 northbound 및 southbound 트래픽을 분산 하기 위해 소프트웨어 부하 분산 장치를 사용 합니다.  
  
-   배포 하 고 Hyper-v 네트워크 가상화를 사용 하 여 만든 가상 네트워크에 대 한 eastbound 및 westbound 트래픽을 분산 하기 위해 소프트웨어 부하 분산 장치를 사용 합니다.  
  
-   배포 하 고 Hyper-v 네트워크 가상화를 사용 하 여 만든 가상 네트워크에 대 한 NAT 소프트웨어 부하 분산 장치를 사용 합니다.  
  
-   배포 하 고 계층 3 전달 게이트웨이 사용 합니다.  
  
-   배포 및 사이트 간 IPsec (IKEv2) 터널에 대한 VPN(가상 사설망) 게이트웨이를 사용합니다.  
  
-   배포 하 고 캡슐화 GRE (Generic Routing) 게이트웨이 사용 합니다.  
  
-   배포 및 동적 라우팅 및 전송 프로토콜 BGP (Border Gateway)를 사용 하 여 사이트 간 라우팅을 구성 합니다.  
  
-   계층 3 및 사이트 간 게이트웨이에 대 한 및 BGP 라우팅에 대 한 M + N 중복성을 구성 합니다.  
  
-   네트워크 컨트롤러를 사용 하 여 가상 네트워크 및 네트워크 인터페이스에 Acl을 지정 합니다.  
  
자세한 내용은 참조 [네트워크 기능 가상화](sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md)합니다.  
  
### <a name="bkmk_netp"></a>네트워크 플랫폼 시나리오

Windows Server 네트워킹이 섹션의 시나리오에 대 한 팀 인증 드라이버는 Windows Server 2016의 사용을 지원 합니다. 네트워크 인터페이스 카드를 확인 하십시오 \(NIC\) 제조업체는 가장 최신 드라이버 업데이트 했는지 확인 하십시오.
  
네트워크 플랫폼 시나리오를 수행할 수 있습니다.  
  
-   수렴 형된 NIC를 사용 하 여 RDMA 및 트래픽 둘 다 이더넷 네트워크 어댑터를 사용 하 여 결합 합니다.  
  
-   패킷 Direct를 Hyper-v 가상 스위치와 단일 네트워크 어댑터에서 활성화를 사용 하 여 지연율이 낮은 데이터 경로를 만듭니다.  
  
-   최대 두 개의 네트워크 어댑터 간에 SMB 다이렉트 및 RDMA 트래픽 흐름을 분산 하는 집합을 구성 합니다.  
  
자세한 내용은 참조 [원격 직접 메모리 액세스 & #40; RDMA & #41; 포함 된 팀 & #40; 전환 집합 & #41;](../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)합니다.  
  
#### <a name="bkmk_switch"></a>Hyper-v 가상 스위치 시나리오

Hyper-v 가상 스위치 등의 시나리오를 수행할 수 있습니다.  
  
-   원격 직접 메모리 액세스 (RDMA) vNIC를 사용 하 여 Hyper-v 가상 스위치 만들기  
  
-   스위치가 포함 된 팀 (설정) 및 RDMA vNICs를 사용 하 여 Hyper-v 가상 스위치 만들기  
  
-   Hyper-v 가상 스위치에서 집합 팀 만들기  
  
-   Windows PowerShell 명령을 사용 하 여 집합 팀을 관리 합니다.  
  
자세한 내용은 참조 [원격 직접 메모리 액세스 & #40; RDMA & #41; 포함 된 팀 & #40; 전환 집합 & #41;](../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)  
  
### <a name="bkmk_dns"></a>DNS 서버 시나리오

DNS 서버 시나리오를 수행할 수 있습니다.  
  
-   지리적 위치 기반 DNS 정책을 사용 하 여 트래픽 관리를 지정 합니다.  
  
-   DNS 정책을 사용 하 여 스플릿 브레인 DNS 구성  
  
-   DNS 정책을 사용 하 여 DNS 쿼리에 필터를 적용 합니다.  
  
-   DNS 정책을 사용 하 여 응용 프로그램 부하 분산 구성  
  
-   하루 중 시간을 기준으로 지능형 DNS 응답 지정  
  
-   DNS 영역 전송 정책 구성  
  
-   DNS 서버 Active Directory 도메인 서비스 (AD DS)에 있는 정책 통합 영역 구성  
  
-   응답 속도 구성 제한  
  
-   명명 된 엔터티 (있는지)의 DNS 기반 인증을 지정 합니다.  
  
-   DNS에서 알 수 없는 레코드에 대 한 지원 구성  
  
자세한 내용은 항목을 참조 하십시오. [Windows Server 2016의 DNS 클라이언트의 새로운](dns/What-s-New-in-DNS-Client.md) 및 [Windows Server 2016에서 DNS 서버에서 새로운](dns/What-s-New-in-DNS-Server.md)합니다.  
  
### <a name="bkmk_ipam"></a>DHCP 및 DNS를 사용 하는 IPAM 시나리오

IPAM 시나리오를 수행할 수 있습니다.  
  
-   검색 하 고 DNS 및 DHCP 서버 및 페더레이션 여러 Active Directory 포리스트에서 IP 주소 관리  
  
-   IPAM을 사용 하 여 영역 및 리소스 레코드를 포함 하 여 DNS 등록 정보를 중앙 집중식으로 관리 합니다.  
  
-   지정한 DNS 속성 집합을 관리 하는 IPAM 사용자 또는 사용자 그룹을 위임 및 세분화 된 역할 기반 액세스 제어 정책을 정의 합니다.  
  
-   IPAM에 대 한 Windows PowerShell 명령을 사용 하 여 DHCP 및 DNS에 대 한 액세스 제어 구성 자동화 합니다.  
  
    자세한 내용은 참조 [IPAM 관리](technologies/ipam/Manage-IPAM.md)합니다.  
  
### <a name="bkmk_nicteam"></a>NIC 팀 시나리오

NIC 팀 등의 시나리오를 수행할 수 있습니다.  
  
-   지원 되는 구성에서 NIC 팀 만들기  
  
-   NIC 팀을 삭제 합니다.  
  
-   지원 되는 구성에서 NIC 팀에 네트워크 어댑터를 추가 합니다.  
  
-   NIC 팀에서 네트워크 어댑터를 제거 합니다.  
  
> [!NOTE]  
> 하지만 Windows Server 2016에서 사용할 수 있습니다 NIC 팀에서 하이퍼-V 일부 경우에 큐 VMQ (가상 컴퓨터) 수 자동으로 사용 하도록 설정 하지 내부 네트워크 어댑터에 NIC 팀을 만들 때. 이 문제가 발생 하는 경우 다음 Windows PowerShell 명령을 사용 하 여 NIC 팀 구성원 어댑터에서 VMQ가 사용 하도록 설정 되었는지 확인할 수 있습니다. `Set-NetAdapterVmq -Name <NetworkAdapterName> -Enable`  

자세한 내용은 참조 [NIC 팀](technologies/nic-teaming/NIC-Teaming.md)합니다. 

### <a name="bkmk_set"></a>\) 시나리오를 설정 하 \(포함 된 팀 전환

집합은 Windows Server 2016에 Hyper-v 및 네트워킹 SDN (소프트웨어) 스택을 포함 하는 환경에서 사용할 수 있는 대체 NIC 팀 솔루션. 일부 NIC 팀 기능은 Hyper-v 가상 스위치에 통합 하는 설정 합니다. 

자세한 내용은 참조 [원격 직접 메모리 액세스 (RDMA) 및 스위치 포함 된 팀 (SET)](https://technet.microsoft.com/windows-server-docs/networking/technologies/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming)
  
 
  
## <a name="bkmk_unsupp"></a>지원 되지 않는 네트워킹 시나리오  
다음과 같은 네트워킹 시나리오는 Windows Server 2016에서 지원 되지 않습니다.  
  
-   VLAN 기반 테 넌 트 가상 네트워크 지원  
  
-   I p v 6 언더레이 또는 오버레이에 지원 되지 않습니다.  
  


