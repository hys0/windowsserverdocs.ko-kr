---
title: 소프트웨어 정의 네트워킹 (SDN)
description: Windows Server, System Center 및 Microsoft Azure에서 제공 되는 소프트웨어 정의 네트워킹 (SDN) 기술에 대 한 자세한 내용은이 항목을 사용할 수 있습니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 9a1ea73c-20cd-42c5-95ad-b003b9cc6d64
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 33351ccfa1466f667ef9351768c89b373734075d
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="software-defined-networking-sdn"></a>소프트웨어 정의 네트워킹 (SDN)

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

Microsoft Azure, 시스템 센터 2016 및 Windows Server Datacenter edition에서 제공 되는 소프트웨어 정의 네트워킹 (SDN) 기술에 대 한 자세한 내용은이 항목을 사용할 수 있습니다.  
  
> [!NOTE]
> 이 항목 외에 다음과 같은 SDN 콘텐츠를 사용할 수 있습니다.
> 
> - [Windows Server에 대 한 SDN의 새로운 기능](sdn-whats-new.md)
> - [Introduction to SDN in Windows Server Datacenter](sdn-intro.md)
> - [SDN Technologies](technologies/Software-Defined-Networking-Technologies.md)  
> - [Plan SDN](plan/Plan-Software-Defined-Networking.md) 
> - [Deploy SDN](deploy/Deploy-Software-Defined-Networking.md)  
> - [Manage SDN](manage/manage-sdn.md)
> - [Security for SDN](security/sdn-security-top.md)
> - [Troubleshoot SDN](troubleshoot/Troubleshoot-Software-Defined-Networking.md)
> - [System Center Technologies for SDN](Sc-Tech-for-Sdn.md)
> - [Microsoft Azure and SDN](Azure_and_Sdn.md)
> - [Datacenter 및 클라우드 네트워킹 팀에 문의](contact-sdn-team.md)
  
## <a name="bkmk_sdn"></a>소프트웨어 정의 네트워킹 개요

소프트웨어 네트워킹 정의 \(SDN\) 중앙 구성 하 고 라우터와 스위치, 데이터 센터 게이트웨이가 등의 실제 및 가상 네트워크 디바이스를 관리 하는 방법을 제공 합니다. Hyper-v 가상 스위치, Hyper-v 네트워크 가상화 RAS 게이트웨이 등 가상 네트워크 요소는 SDN 인프라 가장 중요 한 요소 되도록 디자인 되었습니다.

>[!NOTE]
>Hyper-v 호스트와 같은 네트워크 컨트롤러 및 부하 분산 소프트웨어가 노드 SDN 인프라 서버 실행 가상 컴퓨터 \(VMs\) Datacenter edition Windows Server 2016을 설치 해야 합니다. Hyper-v 호스트의 테 작업 SDN\ 제어 네트워크에 연결 된 Vm를 포함 하는 경우 Windows Server 2016 Standard edition을 실행할 수 있습니다.

기존 물리적 스위치를, 라우터 및 기타 하드웨어 디바이스도 사용할 수 있지만, 이러한 디바이스 소프트웨어 정의 네트워킹와의 호환성을 위해 설계 된 가상 네트워크 실제 네트워크와 보다 긴밀 한 통합을 얻을 수 있습니다.  
  
네트워크 비행기 기능 관리, 컨트롤 및 데이터 비행기-자체 네트워크 디바이스에 더 이상 바인딩된 있지만 시스템 센터 2016 같은 datacenter 관리 소프트웨어 등의 기타 기관과에서 사용할 수 있도록 추상화는 때문에 SDN 불가능 합니다.  
  
SDN 동적으로 자동화, 중앙 집중식 응용 프로그램 및 작업의 요구 사항을 충족 하는 방법을 제공 하 여 datacenter 네트워크 관리할 수 있습니다. 소프트웨어 정의 네트워킹 다음과 같은 기능을 제공합니다.  
  
-   추상 응용 프로그램 및 네트워크 가상화 하면 기본 실제 네트워크에서 작업 하는 기능입니다. Hyper-v를 사용 하 여 서버 가상화와 마찬가지로 추상화는 일관 되 고 직장 응용 프로그램 및 작업 중단 없는 방식에서입니다. 예를 들어, 정의 소프트웨어 네트워킹 IP 주소, 스위치를 부하 분산 등 사용자 실제 네트워크 요소에 대 한 가상 추상화 제공합니다.  
  
-   중앙 정의 하는 기능 및 물리적 및 가상 네트워크 교통 체증 등을 제어 하는 제어 정책 두 네트워크 유형 간에 이동 합니다.  
  
-   새로운 작업 배포 또는 가상 또는 실제 네트워크 작업 움직입니다 때에, 크기로 일관 된 방식 네트워크 정책 구현할 수 있습니다.  
  
## <a name="bkmk_ws"></a>소프트웨어에 대 한 Windows Server 기술 정의 네트워킹  
Windows Server에 다음과 같은 정의 소프트웨어 네트워킹 기술이 포함 되어 있습니다.  

### <a name="bkmk_nc"></a>네트워크 컨트롤러

새로운 Windows Server 2016 네트워크 컨트롤러 관리를 구성 하 고, 모니터, 모두 가상 문제를 해결 하려면 자동화 및 사용자 데이터 센터에 실제 네트워크 인프라 중앙 집중식, 프로그래밍 포인트를 제공 합니다. 네트워크 컨트롤러를 사용 하 여 네트워크 디바이스 및 서비스를 수동으로 구성 수행 하는 대신 네트워크 infrastructure 구성을 자동 수 있습니다.  
  
네트워크 컨트롤러는 많이 사용 가능 하 고 확장 가능 하도록 만들기 서버 역할을 하 고 특정 응용 프로그램 프로그래밍 인터페이스 (API)-Southbound API-네트워크와 통신 하도록 네트워크 컨트롤러 수 있도록 해 주는 및 네트워크 컨트롤러와 통신할 수 있도록 두 번째 API-Northbound API-를 제공 합니다.  
  
Windows PowerShell, 표시 상태가 전송 (REST) API 또는 응용 프로그램을 관리를 사용 하 여 네트워크 컨트롤러 다음 실제 및 가상 네트워크 infrastructure 관리에 사용할 수 있습니다.  
  
-   Hyper-v Vm 및 가상 스위치  
  
-   실제 네트워크 스위치가  
  
-   실제 네트워크 라우터  
  
-   방화벽 소프트웨어로  
  
-   VPN 게이트웨이, 넌 게이트웨이 원격 액세스 서비스 (RAS)를 포함 하 여  
  
-   부하 분산  
  
자세한 내용은 참조 [네트워크 컨트롤러](../sdn/technologies/network-controller/Network-Controller.md)합니다.  
  
### <a name="bkmk_hv"></a>Hyper-v 네트워크 가상화

네트워크 가상화 Hyper-v 가상 네트워크를 사용 하 여 응용 프로그램 및 실제 네트워크에서 작업 추상 수 있습니다. 가상 네트워크 리소스 사용량을 되므로 운전 실제 네트워크 공유 패브릭에서 실행 하면서 필요한 넌 격리를 제공 합니다. 수행할 수 앞으로 기존 투자 하도록 가상 네트워킹 기존 기어 네트워크를 설정할 수 있습니다. 또한, 가상 네트워크 가상 영역 로컬 네트워크 (Vlan)과 호환 됩니다.  
  
자세한 내용은 참조 [Hyper-v 네트워크 가상화](../sdn/technologies/hyper-v-network-virtualization/Hyper-V-Network-Virtualization.md)합니다.  
  
### <a name="bkmk_switch"></a>Hyper-v 가상 스위치를

Hyper-v 가상 스위치 소프트웨어 기반 2 계층 이더넷 네트워크 스위치 Hyper-v 서버 역할을 설치한 후 Hyper-v 관리자에서 사용할 수 있는입니다. 스위치 가상 컴퓨터 가상 네트워크와는 실제 네트워크에 연결 하려면 프로그래밍 방식으로 관리 하 고 확장 가능 기능이 포함 되어 있습니다. 또한, Hyper-v의 가상 스위치 보안, 격리 및 수준 서비스에 대 한 정책을 적용을 제공합니다.  
  
Windows Server 2016에 Hyper-v 가상 스위치를 전환 Embedded 팀 (설정) 및 원격 직접 메모리 액세스 (RDMA)을 배포할 수도 있습니다. 자세한 내용은 섹션을 참조 [원격 직접 메모리 액세스 (RDMA) 및 스위치 Embedded 팀 (설정)](#bkmk_rdma) 이 여기에 있습니다.  
  
Hyper-v 가상 스위치를에 대 한 자세한 내용은 참조 [Hyper-v의 가상 스위치](../../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md)합니다.

### <a name="bkmk_idns"></a>내부 DNS 서비스 & #40; Idn & #41;

가상 컴퓨터 호스팅된 \(VMs\) 및 응용 프로그램 내 네트워크 및 인터넷 외부 리소스와 통신 하도록 DNS 필요 합니다. Idn, 인터넷 리소스 및 자신의 격리, 로컬 이름 공간에 대 한 DNS 이름 해상도 서비스 테 넌을 제공할 수 있습니다.

자세한 내용은 참조 [내부 DNS 서비스 & #40; Idn & #41; SDN에 대 한](technologies/Idns-for-Sdn.md)합니다.
  
### <a name="bkmk_nfv"></a>네트워크 함수 Virtualization

하드웨어 기기 (예: 부하 분산, 방화벽, 라우터에, 스위치 및 등)가 수행 하는 네트워크 기능 정의 데이터 센터 오늘 소프트웨어에서 가상 기기도 가상화 되 고 점점 더 됩니다. 이 "네트워크 함수 virtualization" 서버 virtualization 및 네트워크 가상화의 자연 진행입니다. 가상 장비는 신속 하 게 신흥 및 새로운 시장 있습니다. 관심사를 생성 하 고 모두 virtualization 플랫폼에서 운동량 얻고, 클라우드 서비스를 계속 합니다.  
  
다음과 같은 기능 네트워크 가상화 기술이 사용할 수 있습니다.  
  
-   **부하 분산 소프트웨어가 (SLB) 및 네트워크 (NAT 변환) 주소**합니다. 북쪽 사우스 및 동쪽 서쪽 계층 4 부하 분산 및 NAT는 처리량 지원 직접 서버 반환 함께 반환 네트워크 교통은 부하 분산 멀티플렉서 무시할 수 있습니다. 자세한 내용은 참조 [소프트웨어 부하 분산 SLB () SDN에 대 한](technologies/network-function-virtualization/software-load-balancing-for-sdn.md)합니다.  
  
-   **Datacenter 방화벽**합니다. 이 분산된 방화벽은 세밀 액세스 제어 (Acl 목록), 방화벽 정책을 VM 인터페이스 수준에서 나 서브넷 수준 적용할 수 있도록 합니다.  
  
    자세한 내용은 참조 [Datacenter 방화벽 개요](../sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)합니다.  
  
-   **RAS 게이트웨이**합니다. 가상 네트워크 가상화 비 네트워크 등 사이의 교통 브리지 게이트웨이 사용할 수 있습니다. 특히, 사이트에서 VPN 게이트웨이, 전달 게이트웨이 및 일반 경로 캡슐화 (GRE) 게이트웨이 배포할 수 있습니다. 또한 M + N 게이트웨이 중복 지원 됩니다. 자세한 내용은 참조 [SDN RAS 게이트웨이](technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)합니다.
  
자세한 내용은 참조 [기능 네트워크 가상화](technologies/network-function-virtualization/Network-Function-Virtualization.md)합니다.  
  
### <a name="bkmk_rdma"></a>원격 직접 메모리 액세스 (RDMA) 스위치를 포함 됩니다 (설정) 팀  
Windows Server 2016 RDMA Hyper-v 가상 스위치와 또는 없이 스위치 Embedded 팀 (설정)에 연결 된 네트워크 어댑터에 사용할 수 있습니다. 이렇게 하면 RDMA 및 설정 사용 하려는 경우 더 적은 네트워크 어댑터를 사용 하 여 동시에 있습니다.  
  
집합은 있는 다른 NIC 팀 솔루션 Hyper-v 및 소프트웨어 정의 네트워킹 (SDN) 스택 Windows Server 2016에 포함 된 환경에서 사용할 수 있습니다. 설정은 Hyper-v의 가상 스위치를 NIC 팀 기능 중 일부를 통합 합니다.  
  
설정 한 하 고 8 물리적 이더넷 네트워크 어댑터에 하나 이상의 소프트웨어 기반 가상 네트워크 어댑터를 그룹화 수 있습니다. 이러한 가상 네트워크 어댑터 빠른 성능 및 네트워크 어댑터 오류가 발생할 경우 오류 허용 제공합니다.  
설정 회원 네트워크 어댑터가 모두 팀에 동일한 실제 Hyper-v 호스트도 설치 합니다.  
  
또한, 데이터 센터 브리지 (DCB)를 사용 하도록 설정 Hyper-v 가상 스위치를 RDMA 가상 NIC (vNIC)를 만들고 일련 및 RDMA vNICs Hyper-v 가상 스위치를 사용 하 Windows PowerShell 명령을 사용할 수 있습니다.  
  
자세한 내용은 참조 [원격 직접 메모리 액세스 (RDMA) 및 스위치 Embedded 팀 (설정)](https://technet.microsoft.com/library/mt403349.aspx)합니다.  
  
### <a name="bkmk_rras"></a>SDN RAS 게이트웨이  
RAS 게이트웨이 소프트웨어를 기반으로 넌, 테두리 게이트웨이 프로토콜 (BGP) 가능 라우터 (Csp) 클라우드 서비스 공급자 및 네트워크 가상화 Hyper-v를 사용 하 여 여러 테 가상 네트워크 호스트 하는 기업으로 디자인 된 Windows Server 2016에에서는입니다.  
  
RAS 게이트웨이 게이트웨이 풀, M + N 중복, 여러 종류의 하 고 BGP 경로 반사 기 게이트웨이 인프라에 대해 유연한 디자인 옵션이 제공 하기 위해 사이트에서 VPN 연결을 제공 합니다.  
  
자세한 내용은 참조 [RAS 게이트웨이 SDN에 대 한](technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)  
  
### <a name="bkmk_slb"></a>소프트웨어 부하 분산 (SLB)  
(Csp) 클라우드 서비스 공급자와 소프트웨어 정의 네트워킹 (SDN) Windows Server 2016에 배포 하는 기업 테 및 가상 네트워크 리소스 간에 테 고객 네트워크 교통 배포 하 게 하려면 소프트웨어 부하 분산 (SLB)을 사용할 수 있습니다. Windows Server SLB 가용성 우선과 확장성 개최 된 같은 작업을 여러 서버 수 있습니다.  
  
자세한 내용은 참조 [부하 분산 소프트웨어가 & #40; SLB & #41; SDN에 대 한](../sdn/technologies/network-function-virtualization/software-load-balancing-for-sdn.md)합니다.

### <a name="windows-server-containers"></a>Windows Server 컨테이너

Windows Server 컨테이너는 동일한 컨테이너 호스트에서 실행 되는 다른 서비스와에서 응용 프로그램 또는 서비스를 분리 하는 데 사용 하는 무게는 가벼우며 운영 체제 virtualization 방법입니다. 이 실현 하기 각 컨테이너 운영 체제, 프로세스, 파일 시스템, 레지스트리 및 IP 주소 고유한 보기를 있습니다. Windows Server 2016 Windows Server 컨테이너 가상 네트워크에 이제 연결할 수 있습니다. 자세한 내용은 참조 [Windows Server 컨테이너](technologies/containers/Container-networking-overview.md)합니다.

### <a name="contact-the-datacenter-and-cloud-networking-product-team"></a>데이터 센터 네트워킹 클라우드 및 제품 팀에 문의

다양 한 방법으로 만들기에 대 한 가지 SDN 기술 Microsoft 또는 다른 SDN 고객에 설명에 관심이 있는 경우 연락처 합니다.

자세한 내용은 참조 [Datacenter 및 클라우드 네트워킹 팀에 문의](contact-sdn-team.md)합니다.
