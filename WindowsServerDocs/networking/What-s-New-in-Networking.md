---
title: 네트워킹의 새로운 기능
description: 이 항목에서는 Windows Server 2016의 네트워킹에 대 한 새 기능 및 기술에 대 한 개요 정보 제공
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: get-started-article
ms.assetid: 08fb7563-d319-48a9-b181-ca0ca3032c18
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 43ce6290f6559be7cb078032b79519d1681506d4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829194"
---
# <a name="whats-new-in-networking"></a>네트워킹의 새로운 기능

>적용 대상: Windows Server 2016

다음은 Windows Server 2016의 새로운 기능과 향상 된 네트워킹 기술입니다.  
  이 항목에서는 Upd에는 다음 섹션이 포함 합니다.  
  
-   [새 네트워킹 기능 및 기술](#bkmk_features)  
  
-   [추가 네트워킹 기술에 대 한 새로운 기능](#bkmk_existing)  
  
## <a name="bkmk_features"></a>새 네트워킹 기능 및 기술

네트워킹 소프트웨어 정의 된 데이터 센터 (SDDC) 플랫폼의 기본적인 일부인 및 Windows Server 2016 조직에 대해 완벽 하 게 실현된 SDDC 솔루션으로 이동 하는 데 도움이 하는 새로운 기능과 향상 된 네트워킹 SDN (소프트웨어) 기술을 제공 합니다.  
  
네트워크를 정의 하는 소프트웨어 리소스로 관리 하는 경우 한 번, 응용 프로그램의 인프라 요구 사항에 설명 하 고 다음 선택할 수 있는 응용 프로그램 실행-온-프레미스 또는 클라우드에서 합니다.  이 일관성 즉, 응용 프로그램은 이제 쉽게 확장 하 보안, 성능, 서비스 및 가용성의 품질 주위 같은 안심할 수 있는 응용 프로그램을 어디서 나 원활 하 게 실행할 수 있습니다.  
  
다음 섹션에서는 새로운 기능 및 기술 네트워킹이 대 한 정보입니다.  
  
### <a name="software-defined-networking-infrastructure"></a>소프트웨어 정의 네트워킹 인프라

다음은 새로운 또는 향상 된 SDN 인프라 기술입니다.  
  
-   **네트워크 컨트롤러**합니다. 새로운 네트워크 컨트롤러에서 Windows Server 2016 관리, 구성, 모니터링 및 데이터 센터의 가상 및 실제 네트워크 인프라의 문제를 해결 하는 자동화의 프로그래밍 가능한 중앙된 위치를 제공 합니다. 네트워크 컨트롤러를 사용하여 네트워크 장치 및 서비스를 수동으로 구성하는 대신 네트워크 인프라의 구성을 자동화할 수 있습니다. 자세한 내용은 참조 [네트워크 컨트롤러](sdn/technologies/network-controller/Network-Controller.md) 및 [배포 소프트웨어 정의 네트워크 스크립트를 사용 하 여](https://technet.microsoft.com/library/mt427380.aspx)합니다.  
  
-   **Hyper-v 가상 스위치**합니다. Hyper-v 가상 스위치는 Hyper-v 호스트에서 실행 되 고 분산 전환 및 라우팅, 만들 수 있습니다 이며 정책 적용 계층 있는 정렬 하 고 Microsoft Azure와 호환 됩니다. 자세한 내용은 참조 [Hyper-v 가상 스위치](../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md)합니다.  
  
-   **네트워크 기능 가상화 (NFV)** 합니다. 정의 된 데이터 센터, 하드웨어 장비 (예: 부하 분산 장치, 방화벽, 라우터, 스위치 및 등)에서 수행 되는 네트워크 기능 오늘날의 소프트웨어에서 가상 어플라이언스로 배포 되 고 점점 더 됩니다. 이 "네트워크 기능 가상화" 서버 가상화 및 네트워크 가상화의 자연 스러운 진행 됩니다. 가상 어플라이언스는 신속 하 게 새로운 및 새로운 시장 있습니다. 관심을 생성 하 고 업계 동향 가상화 플랫폼 모두에 대 한 권한을 얻는 및 클라우드 서비스를 계속 합니다. 다음과 같은 NFV 기술을 Windows Server 2016에서 제공 됩니다.  
  
    -   **데이터 센터 방화벽**합니다. 이 분산된 방화벽 VM 인터페이스 수준에서 또는 서브넷 수준에서 방화벽 정책을 적용할 수 있도록 세분화 된 액세스 제어 목록 (Acl)을 제공 합니다.  
  
        자세한 내용은 참조 [데이터 센터 방화벽 개요](sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)합니다.  
  
    -   **RAS 게이트웨이**합니다. 가상 네트워크와 테 넌 트의 원격 사이트에 클라우드 데이터 센터에서 사이트 간 VPN 연결을 비롯 한 실제 네트워크 간에 트래픽 라우팅에 대 한 RAS 게이트웨이 사용할 수 있습니다. 특히, Internet Key Exchange version 2 (IKEv2)를 배포할 수 있습니다 사이트 간 가상 사설망 (Vpn), (L3) 계층 3 VPN 및 캡슐화 GRE (Generic Routing) 게이트웨이. 또한 게이트웨이 풀 및 게이트웨이 M + N 중복 이제 지원 됩니다. 고 프로토콜 BGP (Border Gateway) 경로 Reflector 기능을 가진 모든 게이트웨이 시나리오 (IKEv2 VPN, GRE VPN 및 L3 VPN)에 대 한 네트워크 간의 동적 라우팅을 제공 합니다.  
  
        자세한 내용은 참조  [RAS 게이트웨이의 새로운](sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md) 및 [SDN RAS 게이트웨이](sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)합니다.  
          
    - **소프트웨어 부하 분산 장치 (SLB) 및 네트워크 주소 변환 (NAT)** 합니다. 북-남 및 동-서 계층 4 부하 분산 장치 및 NAT는 반환 되는 네트워크 트래픽이 부하 분산은 멀티플렉서 무시할 수를 직접 서버 반환을 지원 하 여 처리량을 향상 시킵니다.  
       자세한 내용은 참조 [소프트웨어 부하 분산 및 #40; SLB & #41; SDN에 대 한](sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md)합니다.  
  
    자세한 내용은 참조 [네트워크 기능 가상화](sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md)합니다.  
  
-   **프로토콜을 표준화**합니다. 네트워크 컨트롤러 northbound 개체 JSON (JavaScript Notation) 페이로드를 인터페이스에 대해 REPRESENTATIONAL State Transfer ()를 사용합니다. 네트워크 컨트롤러 southbound 인터페이스가 열려 vSwitch 데이터베이스 관리 프로토콜 (OVSDB)를 사용 합니다.  
  
-   **유연한 캡슐화 기술**합니다. 이러한 기술은 데이터 평면에서 작동 하 고 확장 가능한 가상 LAN (VxLAN) 및 네트워크 가상화 캡슐화 NVGRE (Generic Routing)을 모두 지원 합니다. 자세한 내용은 참조 [Windows Server 2016에서 GRE 터널링](../remote/remote-access/ras-gateway/gre-tunneling-windows-server.md)합니다.  
  
SDN에 대 한 자세한 내용은 참조 [소프트웨어 정의 네트워킹 & #40; SDN (& a) #41;](sdn/software-defined-networking.md)합니다.  
  
### <a name="cloud-scale-fundamentals"></a>클라우드 규모 기본 사항
 
다음 클라우드 규모 기본 사항 사용할 수 있습니다.  
  
-   **네트워크 인터페이스 카드 (NIC) 수렴 형**합니다. 수렴 형된 NIC를 사용 하면 관리, 원격 직접 메모리 액세스 RDMA 지원 저장소에 대 한 단일 네트워크 어댑터를 사용 하 고 테 넌 트 트래픽 수 있습니다. 이 서버 당 트래픽 유형의 다양성 관리를 더 적은 네트워크 어댑터에 필요 하기 때문에 각 데이터 센터를 서버와 연결 된 자본 비용을 줄여 줍니다.  
  
-   **패킷 직접**합니다.  패킷 직접 높은 네트워크 트래픽 처리량과 낮은 대기 시간 패킷 처리 인프라를 제공합니다.  
  
-   **스위치 (SET) 팀 포함**합니다.        집합에는 Hyper-v 가상 스위치에 통합 된 NIC 팀 솔루션입니다. 집합은 가용성을 향상 시키고 장애 조치를 제공 하는 단일 집합 팀에 최대 8 개의 실제 NIC 팀 구성 수 있습니다. Windows Server 2016에서 서버 메시지 블록 (SMB) 및 RDMA의 사용을 제한 하는 집합 팀을 만들 수 있습니다. 또한 Hyper-v 네트워크 가상화에 대 한 네트워크 트래픽을 분산 하기 위해 팀 집합을 사용할 수 있습니다. 자세한 내용은 참조 [원격 직접 메모리 액세스 & #40; RDMA & #41; 포함 된 팀 & #40; 전환 집합 & #41;](../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)합니다.  
  
## <a name="bkmk_existing"></a>추가 네트워킹 기술에 대 한 새로운 기능

이 섹션에는 친숙 한 네트워킹 기술에 대 한 새로운 기능에 대 한 정보가 포함 되어 있습니다.
  
## <a name="bkmk_dhcp"></a>DHCP  
DHCP는 프라이빗 인트라넷과 같은 TCP/IP 기반 네트워크에서 호스트를 구성할 때 복잡한 작업 및 관리 부담을 줄일 수 있도록 설계된 IETF(Internet Engineering Task Force) 표준입니다. DHCP 서버 서비스를 사용하면 DHCP 클라이언트에서 TCP/IP를 구성하는 프로세스가 자동으로 수행됩니다.  
  
자세한 내용은 참조 [DHCP의 새로운](technologies/dhcp/What-s-New-in-DHCP.md)합니다.  
  
## <a name="bkmk_dns"></a>DNS  
DNS는 TCP/IP 네트워크에서 컴퓨터 및 네트워크 서비스의 이름을 지정하는 데 사용되는 시스템입니다. DNS 명명 과정에서는 사용자에게 친숙한 이름을 통해 컴퓨터와 서비스를 찾습니다. 사용자가 응용 프로그램에서 DNS 이름을 입력하면 DNS 서비스는 이름과 연결된 다른 정보(IP 주소 등)로 이름을 확인할 수 있습니다.  
  
다음은 DNS 클라이언트와 DNS 서버에 대 한 정보입니다.  
  
### <a name="bkmk_dnsc"></a>DNS 클라이언트  
다음은 새로운 또는 향상 된 DNS 클라이언트 기술입니다.  
  
-   **DNS 클라이언트 서비스 바인딩을**합니다. Windows 10에서 DNS 클라이언트 서비스는 둘 이상의 네트워크 인터페이스를 사용 하 여 컴퓨터에 대 한 향상 된 지원을 제공합니다.  
  
자세한 내용은 참조 하세요. [What's New in Windows Server 2016에서 DNS 클라이언트](dns/What-s-New-in-DNS-Client.md)  
  
### <a name="bkmk_dnss"></a>DNS 서버  
다음은 새로운 또는 향상 된 DNS 서버 기술입니다.  
  
-   **DNS 정책**합니다.  DNS는 DNS 서버 DNS 쿼리에 응답 하는 방법을 지정 하는 정책을 구성할 수 있습니다. DNS 응답을 기반으로 클라이언트 IP 주소 (위치), 시간, 일 및 다른 여러 매개 변수입니다. DNS 정책을 위치 인식 DNS, 트래픽 관리, 부하 분산, 스플릿 브레인 DNS 및 기타 시나리오를 사용 합니다.  
  
-   **Nano 서버에 지원 파일에 대 한 DNS 기반**,   Nano 서버 이미지에 Windows Server 2016에서 DNS 서버를 배포할 수 있습니다. 사용 하는 경우이 배포 옵션은 사용 가능한 파일 기반 DNS입니다. Nano 서버 이미지에 실행 중인 DNS 서버에서 메모리 사용량이 감소와 빠른 부팅, 최소화 된 패치 DNS 서버를 실행할 수 있습니다.  
  
    > [!NOTE]   
    > Active Directory 통합 DNS Nano 서버에 지원 되지 않습니다.  
  
-   **응답 속도 제한 (RRL)** 합니다.  DNS 서버에 대 한 응답 속도 제한 하는 것이 가능 합니다. 이 작업을 수행 하 여 DNS 서버를 사용 하 여 DNS 클라이언트에 서비스 공격 거부를 시작 하는 악의적인 시스템의 가능성을 방지할 수 있습니다.  
  
-   **명명 된 엔터티 (있는지)의 DNS 기반 인증**합니다.   DNS 클라이언트에 어떤 CA (인증 기관)에서 도메인 이름에 대 한 인증서를 기대 해야 상태 정보를 제공 하도록 TLSA (전송 계층 보안 인증) 레코드를 사용할 수 있습니다. 이 방지 중간자 개입 공격 누군가가 수 자신의 웹 사이트를 가리키도록 DNS 캐시를 손상 하 고 다른 CA에서 발급 한 인증서를 제공 합니다.  
  
-   **알 수 없는 레코드 지원**합니다.   
     알 수 없는 레코드 기능을 사용 하 여 Windows DNS 서버에 의해 명시적으로 지원 되지 않는 레코드를 추가할 수 있습니다.  
  
-   **IPv6 루트 힌트**합니다.   
     루트 힌트 지원 IPV6 루트 서버를 사용 하 여 인터넷 이름 확인을 수행 하려면 기본 IPV6를 사용할 수 있습니다.  
  
-   **Windows PowerShell 지원 개선**합니다.   
      새 Windows PowerShell cmdlet은 DNS 서버에 사용할 수 있습니다.  
  
자세한 내용은 참조 하세요. [What's New in Windows Server 2016에서 DNS 서버](dns/What-s-New-in-DNS-Server.md)  
  
## <a name="bkmk_GRE"></a>GRE 터널링  
RAS 게이트웨이 이제 사이트 간 연결 및 게이트웨이 M + N 중복에 대 한 고가용성 캡슐화 GRE (Generic Routing) 터널을 지원합니다. GRE는 인터넷 프로토콜 네트워크를 통한 가상 지점 간 연결 내에서 다양한 네트워크 계층 프로토콜을 캡슐화할 수 있는 간단한 터널링 프로토콜입니다.  
  
자세한 내용은 [Windows Server 2016에서 GRE 터널링](../remote/remote-access/ras-gateway/gre-tunneling-windows-server.md)합니다.  
  
## <a name="HNV"></a>Hyper-v 네트워크 가상화  
Windows Server 2012에 도입 된, Hyper-v 네트워크 가상화 (HNV) 고객 네트워크 공유의 실제 네트워크 인프라의 가상화를 수 있습니다. 실제 네트워크 패브릭에서 필요한 최소한의 변화를 통해 HNV를 통해 서비스 공급자 배포 하 고 세 개의 클라우드에 걸쳐 아무 곳 이나 테 넌 트 작업을 마이그레이션하는 민첩성과: 서비스 공급자 클라우드, 프라이빗 클라우드 또는 Microsoft Azure 공용 클라우드입니다.  
  
자세한 내용은 참조 하세요. [What's New in Windows Server 2016에서 Hyper-v 네트워크 가상화](sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md)  
  
## <a name="bkmk_ipam"></a>IPAM  
IPAM 조직 네트워크의 IP 주소 및 DNS 인프라에 대 한 사용자 정의 가능한 관리 및 모니터링 기능을 제공합니다. IPAM을 사용 하 여 모니터링, 감사 및 동적 호스트 구성 프로토콜 (DHCP) 및 도메인 이름 시스템 (DNS)를 실행 하는 서버를 관리할 수 있습니다.  
  
-   **IP 주소 관리를 향상 된**합니다.  
     IPAM 기능/32 IPv4 및 IPv6 /128 서브넷을 처리 하 고 IP 주소 블록에서 사용 가능한 IP 주소 서브넷 및 범위를 찾는 등의 시나리오에 대 한 개선 되었습니다.  
  
-   **DNS 서비스 관리 향상**합니다.  
     IPAM 두 도메인에 가입 된 Active Directory 통합 및 파일 지원 DNS 서버의 DNS 리소스 레코드, 조건부 전달자 및 DNS 영역 관리를 지원합니다.  
  
-   **통합 된 DNS, DHCP 및 IP 주소 (DDI) 관리**합니다.  
     IP 주소와 관련 된 모든 DNS 리소스 레코드를 시각화와 같은 작업을 사용 하는 몇 가지 새로운 경험 형식 및 통합 된 수명 주기 관리의 DNS 리소스 레코드와 DNS 및 DHCP 작업을 모두에 대 한 IP 주소 수명 주기 관리에 따라 IP 주소 인벤토리를 자동화 합니다.  
  
-   **여러 Active Directory 포리스트 지원**합니다.  
     IPAM 설치 되어 있는 포리스트와 사이의 각 원격 포리스트에 양방향 트러스트 관계가 경우 여러 Active Directory 포리스트 DNS 및 DHCP 서버를 관리 하려면 IPAM을 사용할 수 있습니다.  
  
-   **역할 기반 액세스 제어에 대 한 Windows PowerShell 지원**합니다.  
     IPAM 개체에 대 한 액세스 범위를 설정 하려면 Windows PowerShell을 사용할 수 있습니다.  
  
자세한 내용은 참조 [IPAM의 새로운](technologies/ipam/What-s-New-in-IPAM.md) 및 [IPAM 관리](technologies/ipam/Manage-IPAM.md)합니다.  
  

