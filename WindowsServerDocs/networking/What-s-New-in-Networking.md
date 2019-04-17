---
title: 네트워크의 새로운 기능
description: 이 항목에서는 Windows Server 2016에는 네트워크에 대 한 새 기능 및 기술에 대 한 개요 정보 제공
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: get-started-article
ms.assetid: 08fb7563-d319-48a9-b181-ca0ca3032c18
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 85b1a573e8ac724a2a9e22863f890db668423cad
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="whats-new-in-networking"></a>네트워크의 새로운 기능

>Windows Server 2016 적용 됩니다.

다음은 Windows Server 2016의 새로운 기능이 나 향상 된 네트워킹 기술입니다.  
  
이 항목 다음 섹션에 포함 되어 있습니다.  
  
-   [새 네트워크 기능 및 기술](#bkmk_features)  
  
-   [추가 네트워킹 기술에 대 한 새로운 기능](#bkmk_existing)  
  
## <a name="bkmk_features"></a>새 네트워크 기능 및 기술

네트워킹 소프트웨어 정의 데이터 센터 (SDDC) 플랫폼의 기본 일부인 및 Windows Server 2016 새 기술과 향상 된 소프트웨어 정의 네트워킹 (SDN) 조직에 대 한 완벽 하 게 인식된 SDDC 솔루션으로 이동 하는 데 도움이 되는 제공 합니다.  
  
네트워크 정의 소프트웨어 리소스를 관리 하는 경우 한 번 응용 프로그램의 인프라 요구 사항에 설명 하 고 다음 선택할 수 있는 응용 프로그램을 실행-또는 클라우드 온-프레미스 합니다.  이 일관성 응용 프로그램은 배율 쉽게 이제 보안, 성능, 서비스 및 공급 일 품질 주위 같은 신뢰도와 응용 프로그램을 어디서 나을 실행 원활 하 게 의미 합니다.  
  
다음 섹션에서는 새로운 기능 및 기술 네트워킹이 대 한 정보를 포함 합니다.  
  
### <a name="software-defined-networking-infrastructure"></a>소프트웨어 정의 네트워킹 Infrastructure

새로운 기능이 나 향상 된 SDN 인프라 기술은 다음과가 같습니다.  
  
-   **네트워크 컨트롤러**합니다. 새로운 Windows Server 2016 네트워크 컨트롤러, 프로그래밍 중앙 집중식 관리, 구성 하 고, 모니터, 데이터 센터에 인프라 가상 및 실제 네트워크 문제를 해결 하려면 자동화 지점의 제공 합니다. 네트워크 컨트롤러를 사용 하 여 네트워크 디바이스 및 서비스를 수동으로 구성 수행 하는 대신 네트워크 infrastructure 구성을 자동 수 있습니다. 자세한 내용은 참조 [네트워크 컨트롤러](sdn/technologies/network-controller/Network-Controller.md) 및 [배포 소프트웨어 정의 사용 하 여 네트워크 스크립트](https://technet.microsoft.com/library/mt427380.aspx)합니다.  
  
-   **Hyper-v 가상 스위치**합니다. Hyper-v 가상 스위치 Hyper-v 호스트에서 실행 되 고 분산 전환한 경로 만들 수 있도록 이며 정책이 적용 계층 하는 정렬 하 고 Microsoft Azure과 호환 수 있습니다. 자세한 내용은 참조 [Hyper-v의 가상 스위치](../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md)합니다.  
  
-   **함수 가상화 (NFV) 네트워크**합니다. 하드웨어 기기 (예: 부하 분산, 방화벽, 라우터에, 스위치 및 등)가 수행 하는 네트워크 기능 정의 데이터 센터 오늘 소프트웨어에서 가상 기기도 배포 되 고 점점 더 됩니다. 이 "네트워크 함수 virtualization" 서버 virtualization 및 네트워크 가상화의 자연 진행입니다. 가상 장비는 신속 하 게 신흥 및 새로운 시장 있습니다. 관심사를 생성 하 고 모두 virtualization 플랫폼에서 운동량 얻고, 클라우드 서비스를 계속 합니다. Windows Server 2016에는 다음 NFV 기술 사용할 수 있습니다.  
  
    -   **Datacenter 방화벽**합니다. 이 분산된 방화벽은 세밀 액세스 제어 (Acl 목록), 방화벽 정책을 VM 인터페이스 수준에서 나 서브넷 수준 적용할 수 있도록 합니다.  
  
        자세한 내용은 참조 [Datacenter 방화벽 개요](sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)합니다.  
  
    -   **RAS 게이트웨이**합니다. 가상 네트워크와 프로그램 테 넌 원격 사이트로 클라우드 데이터 센터의 사이트-VPN 연결을 포함 하 여 실제 네트워크 사이의 트래픽을 라우팅하기 RAS 게이트웨이 사용할 수 있습니다. 특히, 인터넷 키 교환 버전 (IKEv2) 2 배포할 수 있습니다 사이트에서 Vpn 가상 사설망 (), 계층 3 (l 3) VPN 일반 경로 캡슐화 (GRE) 게이트웨이 하 고 있습니다. 또한 게이트웨이 풀 및 게이트웨이의 M + N 중복 이제 지원 됩니다. 테두리 게이트웨이 프로토콜 (BGP) 경로 반사 기 기능에 대 한 모든 시나리오 (IKEv2 VPN, GRE VPN 및 l 3 VPN) 네트워크 사이의 동적 경로 제공 합니다.  
  
        자세한 내용은 참조 [RAS 게이트웨이의 새로운](sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md) 및 [SDN RAS 게이트웨이](sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)합니다.  
          
    - **부하 분산 소프트웨어가 (SLB) 및 네트워크 (NAT 변환) 주소**합니다. 북쪽 사우스 및 동쪽 서쪽 계층 4 부하 분산 및 NAT는 처리량 지원 직접 서버 반환 함께 반환 네트워크 교통은 부하 분산 멀티플렉서 무시할 수 있습니다.  
       자세한 내용은 참조 [부하 분산 소프트웨어가 & #40; SLB & #41; SDN에 대 한](sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md)합니다.  
  
    자세한 내용은 참조 [기능 네트워크 가상화](sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md)합니다.  
  
-   **프로토콜 표준화**합니다. 네트워크 컨트롤러와 JavaScript 개체 표기법 (JSON) 페이로드 northbound 인터페이스에서 표시 상태 전송 (REST)를 사용합니다. 네트워크 컨트롤러 southbound 인터페이스 열기 vSwitch 데이터베이스 관리 프로토콜 (OVSDB)를 사용합니다.  
  
-   **유연한 캡슐화 기술**합니다. 이러한 기술을 데이터 평면에서 작동 하 고 가상 Extensible LAN (VxLAN) 및 네트워크 가상화 일반 경로 캡슐화 (NVGRE)을 지원 합니다. 자세한 내용은 참조 [GRE Windows Server 2016에 터널링](../remote/remote-access/ras-gateway/gre-tunneling-windows-server.md)합니다.  
  
SDN에 대 한 자세한 내용은 참조 [소프트웨어 네트워킹 정의 & #40; SDN & #41; ](sdn/software-defined-networking.md).  
  
### <a name="cloud-scale-fundamentals"></a>클라우드에 배율이 기본 사항
 
다음 클라우드 조정 기본 사항 사용할 수 있습니다.  
  
-   **(NIC) 네트워크 인터페이스 카드 수렴**합니다. 집약된 NIC 원격 직접 메모리 액세스 (RDMA) 관리에 대 한 단일 네트워크 어댑터를 사용할 수 있습니다.-테 교통 저장소를 사용 합니다. 다양 한 유형의 교통 서버 관리 적은 네트워크 어댑터 필요 하기 때문에 각 서버에 데이터 센터에와 관련 된 대문자 지출을 줄입니다.  
  
-   **패킷 직접**합니다.  패킷 직접 높은 네트워크 교통 처리량 및 저 대기 패킷 처리 인프라를 제공합니다.  
  
-   **(설정) 팀 스위치를 포함**합니다.        집합은 NIC 팀 솔루션을 Hyper-v의 가상 스위치에 통합 되어 있습니다. 설정은 가용성 향상 되 고 장애 조치를 제공 하는 하나의 설정 팀으로 8 실제 NIC 팀 수 있게 합니다. Windows Server 2016에 블록 SMB (서버 메시지) 및 RDMA의 사용을 제한 하는 설정 팀을 만들 수 있습니다. 또한, 네트워크 교통 Hyper-v 네트워크 가상화에 게 배포할 설정 팀을 사용할 수 있습니다. 자세한 내용은 참조 [원격 직접 메모리 액세스 & #40; RDMA & #41; Embedded 팀 & #40; 전환 설정 & #41;](../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md).  
  
## <a name="bkmk_existing"></a>추가 네트워킹 기술에 대 한 새로운 기능

이 섹션에는 익숙한 네트워킹 기술에 대 한 새로운 기능에 대 한 정보가 포함 됩니다.
  
## <a name="bkmk_dhcp"></a>DHCP  
DHCP는 인터넷 엔지니어링 작업 포스 (IETF) 표준 관리 부담와 같은 개인 인트라넷 TCP 기반 네트워크 호스트 구성 복잡성 줄이기 하도록 설계 됩니다. DHCP 서버 서비스를 사용 하 여 DHCP 클라이언트에서 TCP/IP를 구성 하는 과정은 자동 합니다.  
  
자세한 내용은 참조 [DHCP의 새로운](technologies/dhcp/What-s-New-in-DHCP.md)합니다.  
  
## <a name="bkmk_dns"></a>DNS  
DNS는 TCP/IP 네트워크에서 이름 컴퓨터 및 네트워크 서비스에 사용 되는 시스템입니다. DNS 명명 컴퓨터와 서비스를 사용자에 게 친숙 이름 찾습니다. 응용 프로그램에서 DNS 이름을 입력 하는 경우 DNS 서비스 이름을 IP 주소와 같이 이름와 연결 된 기타 정보를 확인할 수 있습니다.  
  
다음은 DNS 클라이언트 및 DNS 서버에 대 한 정보입니다.  
  
### <a name="bkmk_dnsc"></a>DNS 클라이언트  
DNS 클라이언트 새로운 기능이 나 향상 된 기술이 다음과가 같습니다.  
  
-   **DNS 클라이언트 서비스 구속력**합니다. Windows 10에서 DNS 클라이언트 서비스는 하나 이상의 네트워크 인터페이스 된 컴퓨터에 대 한 향상 된 지원을 제공합니다.  
  
자세한 내용은 참조 [DNS Windows Server 2016 클라이언트의 새로운](dns/What-s-New-in-DNS-Client.md)  
  
### <a name="bkmk_dnss"></a>DNS 서버  
DNS 서버 새로운 기능이 나 향상 된 기술이 다음과가 같습니다.  
  
-   **DNS 정책**합니다.  DNS 서버가 DNS 쿼리에 응답 하는 방법을 지정 DNS 정책 구성할 수 있습니다. DNS 응답 클라이언트 IP 주소 (위치)에 따라 수 요일과 여러 매개 변수 시간 합니다. DNS 정책을 위치 인식 DNS, 교통 관리, 부하 분산, split-brain DNS 및 기타 시나리오 사용 합니다.  
  
-   **파일에 대 한 지원을 Nano 서버 기반 DNS**, DNS 서버 Windows Server 2016에 Nano 서버 이미지에 배포할 수 있습니다. 이 배포 옵션을 사용 하는 경우를 사용할 수 있는 파일 DNS 기반으로 합니다. Nano 서버 이미지에서 DNS 서버를 실행 하 여 감소 발자국, 빠른 부팅을 및 최소화 패치 DNS 서버를 실행할 수 있습니다.  
  
    > [!NOTE]   
    > 통합 DNS active Directory Nano 서버에서 지원 되지 않습니다.  
  
-   **응답 평가 제한 (RRL)**합니다.  DNS 서버에 응답 속도 제한 사용할 수 있습니다. 이 작업을 수행 하 여 가능성을 서비스 거부 공격이 DNS 클라이언트를 시작 하려면 DNS 서버를 사용 하 여 악성 시스템을 방지할 수 있습니다.  
  
-   **(있는지) 명명 엔터티의 DNS 기반 인증**합니다.   DNS 클라이언트 국립 어떤 인증 기관에서 도메인 이름에 대 한 인증서 기대 해야 하는 정보를 제공 하기 위해 (Transport Layer Security 인증) TLSA 기록을 사용할 수 있습니다. 이렇게 하면 남자 중간 공격 사람이 수 DNS 캐시 성공한 해당 웹 사이트를 가리키도록 손상 하 고 다른 캘리포니아에서 발급 한 인증서를 제공 합니다.  
  
-   **알 수 없는 기록 지원**합니다.   
     알 수 없는 녹화 기능을 사용 하 여 Windows DNS 서버에서 명시적으로 지원 되지 않는 기록에 추가할 수 있습니다.  
  
-   **IPv6 루트 힌트**합니다.   
     기본 IPV6 루트 힌트 지원 IPV6 루트 서버를 사용 하 여 인터넷 이름을 확인 하는 데 사용할 수 있습니다.  
  
-   **개선 된 Windows PowerShell 지원을**합니다.   
      새로운 Windows PowerShell cmdlet DNS 서버를 사용할 수 있습니다.  
  
자세한 내용은 참조 [DNS 서버를 Windows Server 2016의 새로운](dns/What-s-New-in-DNS-Server.md)  
  
## <a name="bkmk_GRE"></a>GRE 터널링  
이제 RAS 게이트웨이 사이트 연결 및 게이트웨이의 M + N 중복 높은 가용성 일반 경로 캡슐화 (GRE) 터널을 지원합니다. GRE은는 인터넷 프로토콜 네트워크 연결을 통해 네트워크 연결이 가상 내 계층 프로토콜의 다양 한 캡슐화 할 수 있는 간단한 터널링 프로토콜 합니다.  
  
자세한 내용은 참조 [GRE Windows Server 2016에 터널링](../remote/remote-access/ras-gateway/gre-tunneling-windows-server.md)합니다.  
  
## <a name="HNV"></a>Hyper-v 네트워크 가상화  
Windows Server 2012에 소개 된, Hyper-v 네트워크 가상화 (HNV) 실제 네트워크 공유 infrastructure 위에 고객 네트워크 가상화를 수 있습니다. 실제 네트워크 패브릭에 필요한 변경 최소화, HNV 제공 서비스 공급자는 유연성 배포 하 고 세 구름에서 아무 곳 이나 테 작업 마이그레이션하: 클라우드 서비스 공급자, 개인 클라우드 나 공개 Microsoft Azure 클라우드.  
  
자세한 내용은 참조 [Hyper-v 네트워크 가상화 Windows Server 2016의에서 새로운](sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md)  
  
## <a name="bkmk_ipam"></a>IPAM  
IPAM은 조직의 네트워크에 IP 주소와 DNS 인프라에 대해 매우 사용자 지정 가능한 관리 및 모니터링 기능을 제공 합니다. IPAM를 사용 하 여 모니터링 감사를 고 DHCP Dynamic Host Configuration Protocol () 및 시스템 DNS (도메인 이름)을 실행 하는 서버 관리할 수 있습니다.  
  
-   **IP 주소 관리를 향상**합니다.  
     I p v 4/32 및 IPv6 /128 서브넷 처리, IP 주소 블록에서 무료 IP 주소 서브넷 및 범위를 찾는 등 시나리오에 대해 IPAM 기능이 개선 되었습니다.  
  
-   **고급 DNS 서비스 관리**합니다.  
     IPAM은 리소스 DNS 레코드, 조건부 전달자 및 DNS 영역 관리 모두 도메인에 가입 Active Directory 통합 하 고 파일 백업 DNS 서버를 지원합니다.  
  
-   **DNS, DHCP 및 IP 주소 (DDI) 관리 통합**합니다.  
     몇 가지 새로운 환경과 통합된 수명 주기 관리 IP 주소와 관련 된 모든 DNS 리소스 레코드 시각화와 같은 작업을 활성화 인벤토리 DNS 리소스 기록과 IP 주소 수명 주기 관리 DNS 및 DHCP 작업에 대 한에 따라 IP 주소를 자동으로 합니다.  
  
-   **여러 Active Directory 숲 지원**합니다.  
     IPAM 양방향 신뢰 IPAM 설치 되어 있는 숲와 각각 원격 숲 관계 있을 때의 여러 Active Directory 숲 DNS 및 DHCP 서버 관리에 사용할 수 있습니다.  
  
-   **역할 액세스 제어 기반에 대 한 지원이 Windows PowerShell**합니다.  
     Windows PowerShell IPAM 개체에 대 한 액세스 범위를 설정 하려면 사용할 수 있습니다.  
  
자세한 내용은 참조 [IPAM의 새로운](technologies/ipam/What-s-New-in-IPAM.md) 및 [관리 IPAM](technologies/ipam/Manage-IPAM.md)합니다.  
  

