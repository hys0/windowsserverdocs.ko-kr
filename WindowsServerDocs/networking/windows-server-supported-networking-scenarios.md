---
title: Windows Server 네트워킹 시나리오를 지원
description: 이 항목에서는 Windows Server 2016에 하 고 나중에 새로운 지원된 네트워킹 시나리오에 대 한 정보
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.date: ''
ms.assetid: 6de4232d-b0b3-4e43-8735-ebae35ae4f9f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 70198f97c4ec39de4b78de28ab196dc3e86a684c
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="windows-server-supported-networking-scenarios"></a>Windows Server 네트워킹 시나리오를 지원

>적용 대상: Windows Server \(Semi-Annual Channel\), Windows Server 2016

이 항목에서는이 버전의 Windows Server 2016 수행할 수 없는 또는 수 있는 지원 되 고 지원 되지 않는 시나리오에 대 한 정보를 제공 합니다.  
>[!IMPORTANT]
>모든 프로덕션 시나리오에 대해 original equipment 제조업체에서 최신 서명 된 하드웨어 드라이버를 사용 하 여 \(OEM\) 또는 하드웨어 공급 업체 \(IHV\) 합니다.
  
## <a name="bkmk_supp"></a>지원 되는 네트워킹 시나리오

이 섹션 Windows Server 2016 대 한 지원 되는 네트워킹 시나리오에 대 한 정보를 포함 하며 다음과 같은 시나리오 범주를 포함 합니다.  
  
-   [소프트웨어 정의 네트워킹 (SDN) 시나리오](#bkmk_sdn)  
  
-   [네트워크 플랫폼 시나리오](#bkmk_netp)  
  
-   [DNS 서버 시나리오](#bkmk_dns)  
  
-   [DHCP에서 DNS와 IPAM 시나리오](#bkmk_ipam)  
  
-   [NIC 팀 시나리오](#bkmk_nicteam)

- [Embedded 팀 \(SET\) 시나리오 전환](#bkmk_set)
  
### <a name="bkmk_sdn"></a>소프트웨어 정의 네트워킹 (SDN) 시나리오
 
이 문서 배포 된 Windows Server 2016 SDN 시나리오를 사용할 수 있습니다.  
  
  
-   [스크립트를 사용 하는 소프트웨어 정의 네트워크 인프라 배포](sdn/deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)  
  
자세한 내용은 참조 [소프트웨어 네트워킹 정의 & #40; SDN & #41;](sdn/software-defined-networking.md).  
  
#### <a name="bkmk_netc"></a>네트워크 컨트롤러 시나리오

네트워크 컨트롤러 시나리오를 수행할 수 있습니다.  
  
-   배포 하 고 네트워크 컨트롤러의 여러 노드 인스턴스를 관리 합니다. 자세한 내용은 참조 [Windows PowerShell를 사용 하 여 네트워크 컨트롤러 배포](sdn/deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)합니다.  
  
-   네트워크 컨트롤러를 사용 하 여 Northbound REST API를 사용 하 여 네트워크 정책 프로그래밍 방식으로 정의 됩니다.  
  
-   네트워크 컨트롤러를 사용 하 여 작성 및 NVGRE 또는 VXLAN 캡슐화 사용 하 여 네트워크 가상화-Hyper-v를 사용 하 여 가상 네트워크 관리 합니다.  
  
자세한 내용은 참조 [네트워크 컨트롤러](sdn/technologies/network-controller/Network-Controller.md)합니다.  
  
#### <a name="bkmk_netf"></a>네트워크 가상화 (NFV 기능) 시나리오  
NFV 시나리오를 수행할 수 있습니다.  
  
-   배포 및 배포 northbound 및 southbound 교통 소프트웨어 부하 분산 사용 합니다.  
  
-   배포 및 소프트웨어 부하 분산 eastbound 및 westbound 교통 네트워크 가상화 Hyper-v를 사용 하 여 만든 가상 네트워크에 대 한 배포를 사용 합니다.  
  
-   배포 및 가상 네트워크 네트워크 가상화 Hyper-v를 사용 하 여 만든 NAT 소프트웨어 부하 분산을 사용 합니다.  
  
-   배포 및 계층 3 전달 게이트웨이 사용  
  
-   배포 및 가상 개인 네트워크 (VPN) 게이트웨이 대 한 인 사이트 (IKEv2) IPsec 터널 사용  
  
-   배포 및 게이트웨이 일반 경로 캡슐화 (GRE)를 사용 합니다.  
  
-   배포 및 동적 경로 및 교통 테두리 게이트웨이 프로토콜 (BGP)를 사용 하는 사이트 간의 경로 구성 합니다.  
  
-   M + N 중복 BGP 경로 및 계층 3, 게이트웨이, 인 사이트에 대 한 구성 합니다.  
  
-   네트워크 컨트롤러를 사용 하 여 가상 네트워크 및 한 네트워크 인터페이스 Acl 지정할 수 있습니다.  
  
자세한 내용은 참조 [기능 네트워크 가상화](sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md)합니다.  
  
### <a name="bkmk_netp"></a>네트워크 플랫폼 시나리오

Windows Server 네트워킹이 섹션의 시나리오에 대 한 팀에서는 모든 Windows Server 2016 인증 드라이버의 사용 합니다. 최신 드라이버 업데이트가 있는지 확인 하 여 네트워크 인터페이스 카드 \(NIC\) 제조업체에 확인 하세요.
  
네트워크 플랫폼 시나리오를 수행할 수 있습니다.  
  
-   집약된 NIC RDMA 및 이더넷 교통 단일 네트워크 어댑터를 사용 하 여 결합 하 여 사용 합니다.  
  
-   사용 패킷 Direct Hyper-v 가상 스위치와 단일 네트워크 어댑터에서 사용 하 여 저 대기 데이터 경로를 만듭니다.  
  
-   네트워크 어댑터 최대 두 개의 사이의 SMB 직접 및 RDMA 교통 흐름 손가락을 펼치고로 설정을 구성 합니다.  
  
자세한 내용은 참조 [원격 직접 메모리 액세스 & #40; RDMA & #41; Embedded 팀 & #40; 전환 설정 & #41;](../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md).  
  
#### <a name="bkmk_switch"></a>Hyper-v 가상 스위치를 시나리오

Hyper-v 가상 스위치를 시나리오를 수행할 수 있습니다.  
  
-   Hyper-v 가상 스위치를 원격 직접 메모리 액세스 (RDMA) vNIC를 사용 하 여 만들기  
  
-   Hyper-v 가상 스위치를 전환 Embedded 팀 (설정) 및 RDMA vNICs를 사용 하 여 만들기  
  
-   Hyper-v 가상 스위치를에서 설정 팀 만들기  
  
-   Windows PowerShell 명령을 사용 하 여 설정 팀 관리  
  
자세한 내용은 참조 [원격 직접 메모리 액세스 & #40; RDMA & #41; Embedded 팀 & #40; 전환 설정 & #41;](../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)  
  
### <a name="bkmk_dns"></a>DNS 서버 시나리오

DNS 서버 시나리오를 수행할 수 있습니다.  
  
-   지리적 위치 기반 교통 관리 DNS 정책을 사용 하 여 지정  
  
-   DNS 정책을 사용 하 여 split-brain DNS 구성  
  
-   DNS 정책을 사용 하 여 DNS 쿼리에 필터를 적용  
  
-   DNS 정책을 사용 하 여 응용 프로그램 부하 분산 구성  
  
-   지능형 DNS 응답 하루 중 시간에 따라 지정합니다  
  
-   DNS 영역 전송 정책을 구성합니다  
  
-   DNS 서버 정책 Active Directory Domain Services (AD DS) 통합 영역에서 구성  
  
-   응답 속도 구성 제한  
  
-   (있는지) 명명 엔터티의 DNS 기반 인증을 지정  
  
-   Dns에서 알 수 없는 레코드에 대 한 지원을 구성합니다  
  
자세한 내용은 참조 항목 [DNS Windows Server 2016 클라이언트의 새로운](dns/What-s-New-in-DNS-Client.md) 및 [DNS 서버를 Windows Server 2016의 새로운](dns/What-s-New-in-DNS-Server.md)합니다.  
  
### <a name="bkmk_ipam"></a>DHCP에서 DNS와 IPAM 시나리오

IPAM 시나리오를 수행할 수 있습니다.  
  
-   검색 및 관리 하 고 DHCP DNS 서버 및 IP 주소 전체 여러 연결 된 Active Directory 숲  
  
-   IPAM 영역 및 리소스 레코드를 포함 하 여 DNS 속성의 중앙 집중식된 관리를 위해 사용 합니다.  
  
-   세밀 역할 기반 액세스 제어 정책이 정의 및 위임 IPAM 사용자 또는 사용자 그룹 DNS 속성 지정 하는 설정 관리 합니다.  
  
-   DHCP와 DNS에 대 한 액세스를 제어 구성을 자동화 IPAM에 대 한 Windows PowerShell 명령을 사용 합니다.  
  
    자세한 내용은 참조 [관리 IPAM](technologies/ipam/Manage-IPAM.md)합니다.  
  
### <a name="bkmk_nicteam"></a>NIC 팀 시나리오

NIC 팀 시나리오를 수행할 수 있습니다.  
  
-   NIC 팀에서 지원 되는 구성 만들기  
  
-   NIC 팀 삭제  
  
-   네트워크 어댑터에서 지원 되는 구성 NIC 팀에 추가  
  
-   NIC 팀에서 네트워크 어댑터를 제거  
  
> [!NOTE]  
> 그러나 Windows Server 2016 사용할 수 있습니다 NIC 팀 Hyper-v에서 경우에 따라 큐 (VMQ 가상 컴퓨터) 수 자동으로 사용 되지 기본 네트워크 어댑터에 NIC 팀을 만들 때. 이 문제가 발생 하면 VMQ NIC 팀 멤버 어댑터에서 활성화 되어 있는지 확인 하려면 다음 Windows PowerShell 명령을 사용할 수 있습니다. `Set-NetAdapterVmq -Name <NetworkAdapterName> -Enable`  

자세한 내용은 참조 [NIC 팀](technologies/nic-teaming/NIC-Teaming.md)합니다. 

### <a name="bkmk_set"></a>Embedded 팀 \(SET\) 시나리오 전환

집합은 있는 다른 NIC 팀 솔루션 Hyper-v 및 소프트웨어 정의 네트워킹 (SDN) 스택 Windows Server 2016에 포함 된 환경에서 사용할 수 있습니다. NIC 팀 기능을 일부 Hyper-v의 가상 스위치에 통합 하는 설정 합니다. 

자세한 내용은 참조 [원격 직접 메모리 액세스 (RDMA) 및 스위치 Embedded 팀 (설정)](https://technet.microsoft.com/windows-server-docs/networking/technologies/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming)
  
 
  
## <a name="bkmk_unsupp"></a>지원 되지 않는 네트워킹 시나리오  
Windows Server 2016에는 다음과 같은 네트워킹 시나리오를 지원 되지 않습니다.  
  
-   테 VLAN 기반 가상 네트워크입니다.  
  
-   IPv6은 언더레이 또는 오버레이에서 지원 되지 않습니다.  
  


