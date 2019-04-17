---
title: SDN Technologies
description: 이 섹션의 항목 개요 및 Windows Server 2016에 포함 된 소프트웨어 네트워킹 정의 기술에 대 한 기술 정보를 제공 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.service: virtual-network
ms.technology: networking-sdn
ms.topic: article
ms.assetid: b491089c-5bcb-49d4-95b1-915b7ce69f88
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1f842ac0d1a09106c1898374cf8dd1c7823d7dae
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="sdn-technologies"></a>SDN Technologies

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 섹션의 항목 개요 및 Windows Server 2016에 포함 된 소프트웨어 네트워킹 정의 기술에 대 한 기술 정보를 제공 합니다.  
  
> [!NOTE]  
> 추가 소프트웨어 네트워킹 정의 된 문서에 대 한 다음 라이브러리 섹션을 사용할 수 있습니다.  
>   
> - [Plan SDN](../plan/Plan-Software-Defined-Networking.md)
> - [Deploy SDN](../deploy/Deploy-Software-Defined-Networking.md)
> - [Manage SDN](../manage/manage-sdn.md)
> - [Security for SDN](../security/sdn-security-top.md)
> - [Troubleshoot SDN](../troubleshoot/Troubleshoot-Software-Defined-Networking.md)

다음을 포함 한, Microsoft의 소프트웨어 정의 네트워킹 (SDN) 솔루션을 만들기 위해 함께 작동 하는 많은 기술 가지가 있습니다.  
  
-   **[테두리 게이트웨이 프로토콜 & #40; BGP & #41;](../../../remote/remote-access/bgp/Border-Gateway-Protocol-BGP.md)**  
  
    Windows Server 2016 원격 액세스 서비스 (RAS) 게이트웨이의 구성 테두리 게이트웨이 프로토콜 (BGP) 테 넌의 VM 네트워크 사이의 원격 광고주 사이트 네트워크 교통 경로 관리할 수를 제공 합니다. 동적 라우팅 프로토콜 고 자동으로 사이트에서 VPN 연결을 사용 하 여 연결 하는 사이트 간에 경로 학습 있기 때문에 BGP 라우터에 수동 경로 구성에 대 한 필요성을 줄입니다.  
  
-   **[Datacenter 방화벽 개요](../../sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)**  
  
    Datacenter 방화벽은 Windows Server 2016에 포함 된 새로운 서비스입니다. 네트워크 계층, 5 튜플을 (프로토콜, 원본과 대상 포트 번호, IP 주소 원본과 대상), 상태를 넌 방화벽입니다. 배포 서비스 공급자가 서비스를 제공 하는 경우 테 관리자가 설치 하 고 인터넷에서 가져온 원하지 않는 교통에서 가상 네트워크와 인트라넷 네트워크의 보호를 위해 방화벽 정책을 구성 수 있습니다.  
  
  
-   **[Hyper-v 네트워크 가상화](../../sdn/technologies/hyper-v-network-virtualization/Hyper-V-Network-Virtualization.md)**  
  
    Hyper-v 네트워크 가상화 (HNV) 실제 네트워크 공유 infrastructure 위에 고객 네트워크 가상화를 수 있습니다.  
  
- **[내부 DNS 서비스 & #40; Idn & #41; SDN에 대 한](../../sdn/technologies/Idns-for-Sdn.md)**

    가상 컴퓨터 호스팅된 \(VMs\) 및 응용 프로그램 내 네트워크 및 인터넷 외부 리소스와 통신 하도록 DNS 필요 합니다. Idn, 인터넷 리소스 및 자신의 격리, 로컬 이름 공간에 대 한 DNS 이름 해상도 서비스 테 넌을 제공할 수 있습니다.

-   **[네트워크 컨트롤러](../../sdn/technologies/network-controller/Network-Controller.md)**  
  
    네트워크 컨트롤러, 프로그래밍 중앙 집중식 관리, 구성 하 고, 모니터, 데이터 센터에 인프라 가상 및 실제 네트워크 문제를 해결 하려면 자동화 지점의 제공 합니다.  
  
-   **[네트워크 함수 Virtualization](../../sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md)**  
  
    하드웨어 기기 (예: 부하 분산, 방화벽, 라우터에, 스위치 및 등)가 수행 하는 네트워크 기능 가상 기기도 가상화 되 고 점점 더 됩니다.  
  
    네트워크, 전환, 게이트웨이, Nat, 부하 분산 및 방화벽 Microsoft 가상화 했습니다.  

-   **[SDN RAS 게이트웨이](../../sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)**
  
    RAS 게이트웨이 소프트웨어를 기반으로 넌, 테두리 게이트웨이 프로토콜 (BGP) 가능 라우터 (Csp) 클라우드 서비스 공급자 및 네트워크 가상화 Hyper-v를 사용 하 여 여러 테 가상 네트워크 호스트 하는 기업으로 디자인 된 Windows Server 2016에에서는입니다.  
      
- **[원격 직접 메모리 액세스 & #40; RDMA & #41; Embedded 팀 & #40; 전환 설정 & #41;](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)**  
  
    집약된 NIC RDMA 및 이더넷 교통 단일 네트워크 어댑터를 사용 하 여 결합 하 여 사용할 수 있습니다. 집약된 NIC 원격 직접 메모리 액세스 (RDMA) 관리에 대 한 단일 네트워크 어댑터를 사용할 수 있습니다.-테 교통 저장소를 사용 합니다. 다양 한 유형의 교통 서버 관리 적은 네트워크 어댑터 필요 하기 때문에 각 서버에 데이터 센터에와 관련 된 대문자 지출을 줄입니다.  
  
    집합은 NIC 팀 솔루션을 Hyper-v의 가상 스위치에 통합 되어 있습니다. 설정은 가용성 향상 되 고 장애 조치를 제공 하는 하나의 설정 팀으로 8 실제 NIC 팀 수 있게 합니다. Windows Server 2016 블록 SMB (서버 메시지) 및 RDMA의 사용을 제한 된 집합 팀을 만들 수 있습니다.
  

-   **[부하 분산 소프트웨어가 & #40; SLB & #41; SDN에 대 한](../../sdn/technologies/network-function-virtualization/software-load-balancing-for-sdn.md)**  

    (Csp) 클라우드 서비스 공급자와 소프트웨어 정의 네트워킹 (SDN) Windows Server 2016에 배포 하는 기업 테 및 가상 네트워크 리소스 간에 테 고객 네트워크 교통 배포 하 게 하려면 소프트웨어 부하 분산 (SLB)을 사용할 수 있습니다. Windows Server SLB 가용성 우선과 확장성 개최 된 같은 작업을 여러 서버 수 있습니다.
  
-   **[System Center](../../sdn/Sc-Tech-for-Sdn.md)** 시스템 센터 2016 가상 컴퓨터 관리자 VMM () 및 Operations Manager를 배포 및 관리할 네트워크 컨트롤러, 소프트웨어 부하 분산 게이트웨이 등 SDN 인프라를 사용할 수 있습니다. 또한 VMM 중앙 정의 하 고 제어 가상 네트워크 정책 및 응용 프로그램 또는 작업 정책을 연결을 사용할 수 있습니다.
  
- **[Windows 컨테이너](../technologies/Containers/Container-networking-overview.md)**
    
    Windows Server 컨테이너는 동일한 컨테이너 호스트에서 실행 되는 다른 서비스와에서 응용 프로그램 또는 서비스를 분리 하는 데 사용 하는 무게는 가벼우며 운영 체제 virtualization 방법입니다. 이 실현 하기 각 컨테이너 운영 체제, 프로세스, 파일 시스템, 레지스트리 및 IP 주소 고유한 보기를 있습니다. Windows Server 2016 Windows Server 컨테이너 가상 네트워크에 이제 연결할 수 있습니다. Windows 가상 컴퓨터 네트워킹 관련에서 유사 하 게 컨테이너 기능이 합니다. 각 컨테이너 인바인드 및 아웃 바운드 교통 전달 되는 가상 스위치를에 연결 된 가상 네트워크 어댑터를 있습니다. 격리 같은 호스트에 컨테이너 사이 적용 하려면 각 Windows Server, Hyper-v 컨테이너 컨테이너 네트워크 어댑터는 설치에 네트워크 삽입 생성 됩니다. Windows Server 컨테이너 호스트 vNIC를 사용 하 여 가상 스위치를 연결. Hyper-v 컨테이너 합성 VM NIC (유틸리티 VM에 나타나지)를 사용 하 여 가상 스위치를 연결.

