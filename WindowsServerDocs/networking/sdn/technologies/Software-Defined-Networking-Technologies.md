---
title: SDN 기술
description: 이 섹션의 항목에서는 Windows Server 2016에 포함 된 소프트웨어 정의 네트워킹 기술에 대 한 개요 및 기술 정보를 제공 합니다.
manager: dougkim
ms.prod: windows-server
ms.service: virtual-network
ms.technology: networking-sdn
ms.topic: article
ms.assetid: b491089c-5bcb-49d4-95b1-915b7ce69f88
ms.author: pashort
author: shortpatti
ms.date: 02/14/2019
ms.openlocfilehash: b71b17760ec11d7d2ea6a3bfeb118899be9504e7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405952"
---
# <a name="sdn-technologies"></a>SDN 기술

>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server(반기 채널)

이 섹션의 항목에서는 Windows Server 2016에 포함 된 소프트웨어 정의 네트워킹 기술에 대 한 개요 및 기술 정보를 제공 합니다.  

## <a name="network-controllernetwork-controllernetwork-controllermd"></a>[네트워크 컨트롤러](network-controller/Network-Controller.md)

네트워크 컨트롤러는 데이터 센터의 가상 및 실제 네트워크 인프라를 관리, 구성, 모니터링 및 문제를 해결 하기 위한 중앙 집중식의 프로그래밍 가능한 자동화 지점을 제공 합니다. 네트워크 컨트롤러를 사용 하면 네트워크 장치 및 서비스의 수동 구성을 수행 하는 대신 네트워크 인프라의 구성을 자동화할 수 있습니다. 

네트워크 컨트롤러는 항상 사용 가능 하 고 확장 가능한 서버 이며 다음과 같은 두 가지 Api (응용 프로그래밍 인터페이스)를 제공 합니다.

1. **SOUTHBOUND API** – 네트워크 컨트롤러가 네트워크와 통신할 수 있도록 허용 합니다.
2. **NORTHBOUND API** – 네트워크 컨트롤러와 통신할 수 있습니다.

Windows PowerShell, REST (Representational State Transfer) API 또는 관리 응용 프로그램을 사용 하 여 다음과 같은 실제 및 가상 네트워크 인프라를 관리할 수 있습니다.

- Hyper-V VM 및 가상 스위치 
- 실제 네트워크 스위치 
- 실제 네트워크 라우터 
- 방화벽 소프트웨어 
- RAS (원격 액세스 서비스) 다중 테 넌 트 게이트웨이를 포함 한 VPN 게이트웨이 
- 부하 분산 장치 
  
## <a name="hyper-v-network-virtualizationhyper-v-network-virtualizationhyper-v-network-virtualizationmd"></a>[Hyper-v 네트워크 가상화](hyper-v-network-virtualization/Hyper-V-Network-Virtualization.md)

HNV (hyper-v 네트워크 가상화)를 사용 하면 가상 네트워크를 사용 하 여 실제 네트워크에서 응용 프로그램 및 워크 로드를 추상화할 수 있습니다. 가상 네트워크는 공유된 실제 네트워크 패브릭에서 실행되는 동안 필요한 다중 테넌트 격리를 제공하여 리소스 사용률을 높입니다. 기존 투자를 전달할 수 있도록 기존 네트워킹 기어에서 가상 네트워크를 설정할 수 있습니다. 또한 가상 네트워크는 Vlan (virtual Local Area Network)과 호환 됩니다.
  
## <a name="hyper-v-virtual-switchvirtualizationhyper-v-virtual-switchhyper-v-virtual-switchmd"></a>[Hyper-V 가상 스위치](../../../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md) 

Hyper-v 가상 스위치는 hyper-v 서버 역할을 설치한 후 Hyper-v 관리자에서 사용할 수 있는 소프트웨어 기반의 계층 2 이더넷 네트워크 스위치입니다. 스위치에는 프로그램 방식으로 관리되며 확장 가능한 기능이 포함되어 있어 가상 시스템을 가상 네트워크와 실제 네트워크에 모두 연결할 수 있습니다. 또한 Hyper-v 가상 스위치는 보안, 격리 및 서비스 수준에 대 한 정책 적용을 제공 합니다.
  
스위치 포함 된 팀 (설정) 및 RDMA (원격 직접 메모리 액세스)를 사용 하 여 Hyper-v 가상 스위치를 배포할 수도 있습니다. 자세한 내용은이 항목의 [RDMA (원격 직접 메모리 액세스) 및 스위치 포함 된 팀 (SET)](#remote-direct-memory-access-rdma-and-switch-embedded-teaming-set) 섹션을 참조 하십시오.

## <a name="internal-dns-service-idns-for-sdnidns-for-sdnmd"></a>[SDN에 대 한 내부 DNS 서비스 (Idn)](Idns-for-Sdn.md)

호스트 된 Vm (가상 머신) 및 응용 프로그램은 DNS에서 네트워크와 인터넷의 외부 리소스 간에 통신 하는 데 필요 합니다. Idn를 사용 하면 격리 된 로컬 네임 스페이스 및 인터넷 리소스에 대 한 DNS 이름 확인 서비스를 테 넌 트에 제공할 수 있습니다. 
  
## <a name="network-function-virtualizationnetwork-function-virtualizationnetwork-function-virtualizationmd"></a>[네트워크 기능 가상화](network-function-virtualization/Network-Function-Virtualization.md)

부하 분산 장치, 방화벽, 라우터, 스위치 등의 하드웨어 어플라이언스는 점점 더 가상 어플라이언스로 증가 하 고 있습니다. Microsoft는 가상화 된 네트워크, 스위치, 게이트웨이, Nat, 부하 분산 장치 및 방화벽을가지고 있습니다. 이 "네트워크 기능 가상화" 서버 가상화 및 네트워크 가상화의 자연 스러운 진행 됩니다. 가상 어플라이언스는 신속 하 게 새로운 및 새로운 시장 있습니다. 관심을 생성 하 고 업계 동향 가상화 플랫폼 모두에 대 한 권한을 얻는 및 클라우드 서비스를 계속 합니다. 
  
다음 네트워크 기능 가상화 기술을 사용할 수 있습니다.  
  
-   **소프트웨어 부하 분산 장치 (SLB) 및 네트워크 주소 변환 (NAT)** 합니다. 반환 네트워크 트래픽이 부하 분산 멀티플렉서를 무시할 수 있는 Direct Server Return을 지원 하 여 처리량을 향상 시킵니다. 자세한 내용은 [SDN에 대 한 소프트웨어 부하 분산/(SLB/)](network-function-virtualization/software-load-balancing-for-sdn.md)를 참조 하세요.
  
-   **데이터 센터 방화벽**합니다. 세부적인 액세스 제어 목록 (Acl)을 제공 하 여 VM 인터페이스 수준 또는 서브넷 수준에서 방화벽 정책을 적용할 수 있습니다. 자세한 내용은 [데이터 센터 방화벽 개요](network-function-virtualization/Datacenter-Firewall-Overview.md)를 참조 하세요.
  
-   **SDN에 대 한 RAS 게이트웨이**. 위치에 관계 없이 실제 네트워크 리소스와 VM 네트워크 리소스 간에 네트워크 트래픽을 라우팅합니다. 네트워크 트래픽을 동일한 실제 위치 또는 여러 위치에서 라우팅할 수 있습니다. 자세한 내용은 [SDN 용 RAS Gateway](network-function-virtualization/RAS-Gateway-for-SDN.md)를 참조 하세요.

## <a name="remote-direct-memory-access-rdma-and-switch-embedded-teaming-set"></a>RDMA(원격 직접 메모리 액세스) 및 SET(Switch Embedded Teaming)  
Windows Server 2016에서는 스위치 포함 된 팀 (설정)을 사용 하거나 사용 하지 않고 Hyper-v 가상 스위치에 바인딩된 네트워크 어댑터에서 RDMA를 사용 하도록 설정할 수 있습니다. 따라서 RDMA를 사용 하 고 동시에를 설정 하려는 경우 네트워크 어댑터를 줄일 수 있습니다.  
  
집합은 Windows Server 2016에 Hyper-v 및 네트워킹 SDN (소프트웨어) 스택을 포함 하는 환경에서 사용할 수 있는 대체 NIC 팀 솔루션. SET은 일부 NIC 팀 기능을 Hyper-v 가상 스위치에 통합 합니다.  
  
집합 하나 및 8 개의 실제 이더넷 네트워크 어댑터 간에 하나 이상의 소프트웨어 기반 가상 네트워크 어댑터에 그룹화 할 수 있습니다. 이 가상 네트워크 어댑터에는 빠른 성능과 네트워크 어댑터 오류 발생 시 내결함성을 제공합니다.  
집합 멤버 네트워크 어댑터 모두 팀에 배치할 수는 동일한 실제 Hyper-v 호스트에 설치 해야 합니다.  
  
또한 Windows PowerShell 명령을 사용 하 여 DCB (데이터 센터 브리징)를 사용 하도록 설정 하 고, RDMA 가상 NIC (vNIC)를 사용 하 여 Hyper-v 가상 스위치를 만들고, SET 및 RDMA vNICs를 사용 하 여 Hyper-v 가상 스위치를 만들 수 있습니다. 자세한 내용은 [RDMA (원격 직접 메모리 액세스) 및 스위치 포함 된 팀 (SET)](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming.md)을 참조 하세요.

## <a name="border-gateway-protocol-bgpremoteremote-accessbgpborder-gateway-protocol-bgpmd"></a>[BGP(경계 게이트웨이 프로토콜)](../../../remote/remote-access/bgp/Border-Gateway-Protocol-BGP.md)
  
BGP (Border Gateway Protocol)는 사이트 간 VPN 연결을 사용 하는 사이트 간 경로를 자동으로 학습 하는 동적 라우팅 프로토콜입니다. 따라서 BGP는 라우터를 수동으로 구성 하는 것을 줄여 줍니다.   RAS 게이트웨이를 구성 하면 BGP를 사용 하 여 테 넌 트의 VM 네트워크와 원격 사이트 간의 네트워크 트래픽 라우팅을 관리할 수 있습니다.  
  
## <a name="software-load-balancing-slb-for-sdnnetwork-function-virtualizationsoftware-load-balancing-for-sdnmd"></a>[SDN에 대한 SLB(소프트웨어 부하 분산)](network-function-virtualization/software-load-balancing-for-sdn.md)
SDN을 배포 하는 클라우드 서비스 공급자 (Csp) 및 기업은 SLB (소프트웨어 부하 분산)를 사용 하 여 가상 네트워크 리소스 간에 테 넌 트 및 테 넌 트 고객 네트워크 트래픽을 균등 하 게 배포할 수 있습니다. Windows Server SLB 높은 가용성과 확장성이 같은 작업을 호스트 하는 여러 서버를 수 있습니다. 

## <a name="windows-server-containerscontainerscontainer-networking-overviewmd"></a>[Windows Server 컨테이너](Containers/Container-networking-overview.md)

Windows Server 컨테이너는 동일한 컨테이너 호스트에서 실행 되는 다른 서비스와 응용 프로그램 또는 서비스를 구분 하는 간단한 운영 체제 가상화 방법입니다. 각 컨테이너에는 가상 네트워크에 연결할 수 있는 고유한 운영 체제, 프로세스, 파일 시스템, 레지스트리 및 IP 주소가 있습니다. 

## <a name="system-center"></a>System Center

[VMM (가상 컴퓨터 관리](https://docs.microsoft.com/system-center/vmm/) ) 및 [Operations Manager](https://docs.microsoft.com/system-center/scom/)를 사용 하 여 SDN 인프라를 배포 하 고 관리 합니다. VMM을 사용하여 가상 머신을 만들어 프라이빗 클라우드에 배포하는 데 필요한 리소스를 프로비저닝 및 관리합니다.  Operations Manager에서는 기업 전체의 서비스, 디바이스, 작업을 모니터하여 즉각적으로 조치할 수 있게 문제를 식별합니다. 


---