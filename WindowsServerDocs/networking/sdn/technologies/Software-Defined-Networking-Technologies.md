---
title: SDN 기술
description: 이 섹션의에서 항목에서는 개요 및 Windows Server 2016에 포함 된 소프트웨어 정의 네트워킹 기술에 대 한 기술 정보를 제공 합니다.
manager: dougkim
ms.prod: windows-server-threshold
ms.service: virtual-network
ms.technology: networking-sdn
ms.topic: article
ms.assetid: b491089c-5bcb-49d4-95b1-915b7ce69f88
ms.author: pashort
author: shortpatti
ms.date: 02/14/2019
ms.openlocfilehash: acf3e1dc3e5a229c525ba7cad23819640c0d5261
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59891164"
---
# <a name="sdn-technologies"></a>SDN 기술

>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server (반기 채널)

이 섹션의에서 항목에서는 개요 및 Windows Server 2016에 포함 된 소프트웨어 정의 네트워킹 기술에 대 한 기술 정보를 제공 합니다.  

## <a name="network-controllernetwork-controllernetwork-controllermd"></a>[네트워크 컨트롤러](network-controller/Network-Controller.md)

네트워크 컨트롤러는 프로그래밍 가능한 중앙 된 관리, 구성, 모니터링 및 가상 문제를 해결 하는 자동화 및 데이터 센터의 실제 네트워크 인프라를 제공 합니다. 네트워크 컨트롤러를 사용 하 여 네트워크 장치 및 서비스의 수동 구성을 수행 하는 대신 네트워크 인프라 구성을 자동화할 수 있습니다. 

네트워크 컨트롤러는 가용성과 확장성이 높은 서버 하 고 두 개의 Api (응용 프로그래밍 인터페이스)를 제공 합니다.

1. **Southbound API** – 네트워크 컨트롤러가 네트워크와 통신할 수 있습니다.
2. **Northbound API** – 네트워크 컨트롤러와 통신할 수 있습니다.

다음과 같은 실제 및 가상 네트워크 인프라를 관리 하는 Windows PowerShell, REST Representational State Transfer () API 또는 관리 응용 프로그램을 사용할 수 있습니다.

- Hyper-V VM 및 가상 스위치 
- 실제 네트워크 스위치 
- 실제 네트워크 라우터 
- 방화벽 소프트웨어 
- 원격 액세스 서비스 (RAS) 다중 테 넌 트 게이트웨이 포함 하 여 VPN Gateway 
- 부하 분산 장치 
  

  
## <a name="hyper-v-network-virtualizationhyper-v-network-virtualizationhyper-v-network-virtualizationmd"></a>[Hyper-v 네트워크 가상화](hyper-v-network-virtualization/Hyper-V-Network-Virtualization.md)

Hyper-v 네트워크 가상화 (HNV)를 사용 하면 가상 네트워크를 사용 하 여 응용 프로그램 및 실제 네트워크에서 워크 로드를 추상화할 수 있습니다. 가상 네트워크는 공유된 실제 네트워크 패브릭에서 실행되는 동안 필요한 다중 테넌트 격리를 제공하여 리소스 사용률을 높입니다. 작업을 수행할 수 앞으로 기존 투자 하도록 기존 네트워킹 장비에 가상 네트워크를 설정할 수 있습니다. 또한 가상 네트워크는 가상 로컬 영역 네트워크 (Vlan)와 호환 됩니다.   
  
  
## <a name="hyper-v-virtual-switchvirtualizationhyper-v-virtual-switchhyper-v-virtual-switchmd"></a>[Hyper-v 가상 스위치](../../../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md) 

Hyper-v 가상 스위치는 소프트웨어 기반의 계층 2 이더넷 네트워크 스위치를 하이퍼-V 서버 역할을 설치한 후 Hyper-v 관리자에서 사용할 수 있는 합니다. 스위치에는 프로그램 방식으로 관리되며 확장 가능한 기능이 포함되어 있어 가상 시스템을 가상 네트워크와 실제 네트워크에 모두 연결할 수 있습니다. 또한 Hyper-v 가상 스위치는 보안, 격리 및 서비스 수준에 대 한 정책 적용을 제공합니다.
  
또한 팀 SET (Switch Embedded) 및 원격 직접 메모리 액세스 (RDMA)를 사용 하 여 Hyper-v 가상 스위치를 배포할 수 있습니다. 자세한 내용은 섹션을 참조 하세요 [원격 직접 메모리 액세스 (RDMA) 및 스위치 포함 된 팀 (SET)](#bkmk_rdma) 이 항목의 합니다.  

## <a name="internal-dns-service-idns-for-sdnidns-for-sdnmd"></a>[SDN에 대 한 내부 DNS 서비스 (Idn)](Idns-for-Sdn.md)

호스팅된 virtual machines (Vm)와 응용 인터넷에서 외부 리소스와 해당 네트워크 내에서 통신 하는 DNS를 요구 합니다. Idn을 사용 하 여 격리 된, 로컬 네임 스페이스 및 인터넷 리소스에 대 한 DNS 이름 확인 서비스를 사용 하 여 테 넌 트를 제공할 수 있습니다. 
  
## <a name="network-function-virtualizationnetwork-function-virtualizationnetwork-function-virtualizationmd"></a>[네트워크 기능 가상화](network-function-virtualization/Network-Function-Virtualization.md)

부하 분산 장치, 방화벽, 라우터, 스위치 등의 하드웨어 어플라이언스를 점점 더 가상 어플라이언스 점점 합니다. Microsoft는 네트워크, 스위치, 게이트웨이, Nat, 부하 분산 장치 및 방화벽을 가상화 합니다. 이 "네트워크 기능 가상화" 서버 가상화 및 네트워크 가상화의 자연 스러운 진행 됩니다. 가상 어플라이언스는 신속 하 게 새로운 및 새로운 시장 있습니다. 관심을 생성 하 고 업계 동향 가상화 플랫폼 모두에 대 한 권한을 얻는 및 클라우드 서비스를 계속 합니다. 
  
다음과 같은 네트워크 기능 가상화 기술을 사용할 수 있습니다.  
  
-   **소프트웨어 부하 분산 장치 (SLB) 및 네트워크 주소 변환 (NAT)** 합니다. 반환 네트워크 트래픽을 부하 분산 멀티플렉서 무시할 수 Direct Server Return을 지원 하 여 처리량을 개선 합니다. 자세한 내용은 참조 하세요. [SDN에 대 한 소프트웨어 부하 분산 /(SLB/)](network-function-virtualization/software-load-balancing-for-sdn.md)합니다.
  
-   **데이터 센터 방화벽**합니다. VM 인터페이스 수준 또는 서브넷 수준에서 방화벽 정책을 적용할 수 있도록 세분화 된 액세스 제어 목록 (Acl)을 제공 합니다. 자세한 내용은 참조 하세요. [데이터 센터 방화벽 개요](network-function-virtualization/Datacenter-Firewall-Overview.md)합니다.
  
-   **SDN 용 RAS 게이트웨이**합니다. 위치에 관계 없이 실제 네트워크와 VM 네트워크 리소스 간에 네트워크 트래픽을 라우팅하십시오. 동일한 실제 위치 또는 여러 다른 위치에서 네트워크 트래픽을 라우팅할 수 있습니다. 자세한 내용은 참조 하세요. [SDN RAS 게이트웨이](network-function-virtualization/RAS-Gateway-for-SDN.md)합니다.

  
## <a name="remote-direct-memory-access-rdma-and-switch-embedded-teaming-sethttpsdocsmicrosoftcomwindows-servervirtualizationhyper-v-virtual-switchrdma-and-switch-embedded-teaming"></a>[원격 직접 메모리 액세스 (RDMA) 및 스위치 포함 팀 (SET)](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming)  
Windows Server 2016에서 Hyper-v 가상 스위치 또는 없이 스위치 포함 된 팀 (SET)에 바인딩되는 네트워크 어댑터에서 RDMA를 사용할 수 있습니다. 이 집합과 RDMA를 사용 하려는 경우 더 적은 네트워크 어댑터를 사용할 수 있습니다 동시에 합니다.  
  
집합은 Windows Server 2016에 Hyper-v 및 네트워킹 SDN (소프트웨어) 스택을 포함 하는 환경에서 사용할 수 있는 대체 NIC 팀 솔루션. 집합에서 Hyper-v 가상 스위치에 NIC 팀 기능 중 일부를 통합합니다.  
  
집합 하나 및 8 개의 실제 이더넷 네트워크 어댑터 간에 하나 이상의 소프트웨어 기반 가상 네트워크 어댑터에 그룹화 할 수 있습니다. 이 가상 네트워크 어댑터에는 빠른 성능과 네트워크 어댑터 오류 발생 시 내결함성을 제공합니다.  
집합 멤버 네트워크 어댑터 모두 팀에 배치할 수는 동일한 실제 Hyper-v 호스트에 설치 해야 합니다.  
  
또한 데이터 센터 브리징 (DCB)을 사용 하도록 설정, RDMA 가상 NIC (vNIC)를 사용 하 여 Hyper-v 가상 스위치 만들기, vNICs 집합과 RDMA를 사용 하 여 Hyper-v 가상 스위치 만들기를 Windows PowerShell 명령을 사용할 수 있습니다.  

  

## <a name="border-gateway-protocol-bgpremoteremote-accessbgpborder-gateway-protocol-bgpmd"></a>[BGP (Border Gateway Protocol)](../../../remote/remote-access/bgp/Border-Gateway-Protocol-BGP.md)
  
프로토콜 BGP (경계 게이트웨이)는 동적 라우팅 프로토콜 자동으로 사이트 간 VPN 연결을 사용 하는 사이트 간 경로 알아냅니다입니다. 따라서 BGP 라우터를 수동으로 구성을 줄어듭니다.   RAS 게이트웨이 구성 하면 BGP 사용의 테 넌 트의 VM 네트워크와 원격 사이트 간의 네트워크 트래픽 라우팅을 관리할 수 있습니다.  
  
## <a name="software-load-balancing-slb-for-sdnnetwork-function-virtualizationsoftware-load-balancing-for-sdnmd"></a>[소프트웨어 부하 분산 (SLB) SDN에](network-function-virtualization/software-load-balancing-for-sdn.md)
클라우드 서비스 공급자 (Csp) 및 기업 SDN을 배포 하는 테 넌 트 및 가상 네트워크 리소스 간에 테 넌 트 고객 네트워크 트래픽을 균등 하 게 소프트웨어 부하 분산 (SLB)를 사용할 수 있습니다. Windows Server SLB 높은 가용성과 확장성이 같은 작업을 호스트 하는 여러 서버를 수 있습니다. 

## <a name="windows-server-containerscontainerscontainer-networking-overviewmd"></a>[Windows Server 컨테이너](Containers/Container-networking-overview.md)

Windows Server 컨테이너는 동일한 컨테이너 호스트에서 실행 되는 다른 서비스에서 응용 프로그램 또는 서비스를 분리 하는 가벼운 운영 체제 가상화 방법입니다. 각 컨테이너 자체 운영 체제, 프로세스, 파일 시스템, 레지스트리 및 가상 네트워크에 연결할 수 있는 IP 주소에 있습니다. 


## <a name="system-center"></a>System Center  
사용 하 여 SDN 인프라 배포 및 관리 [Virtual Machine Management (VMM)](https://docs.microsoft.com/system-center/vmm/) 하 고 [Operations Manager](https://docs.microsoft.com/system-center/scom/)합니다. VMM을 사용 하 여 프로 비전 하 고 만들기 및 virtual machines 및 서비스를 사설 클라우드에 배포 하는 데 필요한 리소스를 관리 합니다.  Operations Manager를 사용 하 여 기업 전체에서 즉각적인 조치에 대 한 문제를 식별 하 서비스, 장치 및 작업을 모니터링 있습니다. 


---