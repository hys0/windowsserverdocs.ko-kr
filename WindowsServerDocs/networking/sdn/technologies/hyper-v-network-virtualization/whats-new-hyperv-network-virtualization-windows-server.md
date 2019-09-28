---
title: Windows Server 2016에서 제공 되는 Hyper-v 네트워크 가상화의 새로운 기능
description: 이 항목에서는 Windows Server 2016의 Hyper-v 네트워크 가상화의 새로운 기능에 대 한 정보를 제공 합니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0254275a-0a77-40a9-b68a-1029284c03fe
ms.author: pashort
author: shortpatti
ms.date: 03/19/2018
ms.openlocfilehash: 57db82fdd8c7524afb427c61f754e9b8ede8e7b7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355668"
---
# <a name="whats-new-in-hyper-v-network-virtualization-in-windows-server-2016"></a>Windows Server 2016에서 제공 되는 Hyper-v 네트워크 가상화의 새로운 기능

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 Windows Server 2016에서 새로 또는 변경 된 Hyper-v 네트워크 가상화 (HNV) 기능에 대해 설명 합니다.  
  
## <a name="BKMK_IPAM2012R2"></a>HNV의 업데이트  
HNV는 다음 영역에서 향상 된 지원을 제공 합니다.  
  
|기능|새로운 기능 또는 향상된 기능|설명|  
|--------------------------|-------------------|---------------|  
|[프로그래밍 가능 Hyper-v 스위치](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#SDN)|단추를 사용하여 새|HNV 정책은 Microsoft 네트워크 컨트롤러를 통해 프로그래밍할 수 있습니다.|  
|[VXLAN 캡슐화 지원](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#VXLAN)|단추를 사용하여 새|HNV는 이제 VXLAN 캡슐화를 지원 합니다.|  
|[SLB (Software Load Balancer) 상호 운용성](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#SLB)|단추를 사용하여 새|HNV는 Microsoft 소프트웨어 Load Balancer와 완전히 통합 됩니다.|  
|[규격 IEEE 이더넷 헤더](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#L2)|향상된 기능|IEEE 이더넷 표준 준수|  
  
### <a name="SDN"></a>프로그래밍 가능 Hyper-v 스위치  
HNV는 Microsoft의 업데이트 된 SDN (소프트웨어 정의 네트워킹) 솔루션의 기본 빌딩 블록이 며 SDN 스택에 완전히 통합 됩니다.  
  
Microsoft의 새 네트워크 컨트롤러는 SouthBound Interface (SBI)로 Open vSwitch OVSDB (데이터베이스 관리 프로토콜)를 사용 하 여 각 호스트에서 실행 되는 호스트 에이전트로 HNV 정책을 푸시합니다. 호스트 에이전트는 [Vtep 스키마](https://github.com/openvswitch/ovs/blob/master/vtep/vtep.ovsschema) 의 사용자 지정을 사용 하 여이 정책을 저장 하 고 복잡 한 흐름 규칙을 hyper-v 스위치의 성능 흐름 엔진으로 프로그램 합니다.  
  
Hyper-v 스위치 내의 흐름 엔진은 Microsoft Azure @ no__t-0에서 사용 되는 것과 동일한 엔진으로, Microsoft Azure 공용 클라우드의 hyper-v에서 검증 되었습니다. 또한 네트워크 컨트롤러를 통해 전체 SDN 스택과 네트워크 리소스 공급자 (세부 정보 제공 예정)는 Microsoft Azure 일치 하므로 Microsoft Azure 공용 클라우드의 강력한 기능을 엔터프라이즈 및 호스팅 서비스로 활용할 수 있습니다. 공급자 고객.  
  
> [!NOTE]  
> OVSDB에 대 한 자세한 내용은 [RFC 7047](https://www.rfc-editor.org/info/rfc7047)을 참조 하세요.  
  
Hyper-v 스위치는 Microsoft flow 엔진 내의 간단한 ' 일치 작업 '을 기반으로 상태 비저장 및 상태 저장 흐름 규칙을 모두 지원 합니다.  
 
![Windows Server 2016 Hyper-v 스위치](../../../media/what-s-new-in-hyper-v-network-virtualization-in-windows-server/HNVOverview.png)  
  
### <a name="VXLAN"></a>VXLAN 캡슐화 지원  
Cisco, Brocade, Dell, HP 등의 공급 업체에서 지 원하는 기능을 통해 가상의 [7348](https://www.rfc-editor.org/info/rfc7348)VXLAN (확장할 수 있는 로컬 영역 네트워크) 프로토콜은 시장 환경에서 널리 채택 되 고 있습니다. 또한 HNV는 이제 Microsoft 네트워크 컨트롤러를 통해 MAC 배포 모드를 사용 하 여 테 넌 트 오버레이 네트워크 IP 주소 (고객 주소 또는 CA)를 실제 언더레이 네트워크 IP 주소 (공급자)에 대 한 매핑 프로그램을 지원 합니다. 주소 또는 PA). NVGRE 및 VXLAN 작업 오프 로드는 모두 타사 드라이버를 통해 향상 된 성능을 지원 합니다.  
  
### <a name="SLB"></a>SLB (Software Load Balancer) 상호 운용성  
Windows Server 2016에는 가상 네트워크 트래픽 및 HNV와의 원활한 상호 작용을 완벽 하 게 지 원하는 SLB (소프트웨어 부하 분산 장치)가 포함 되어 있습니다. SLB는 데이터 평면 v 스위치의 성능 흐름 엔진을 통해 구현 되 고 VIP (가상 IP)/동적 IP (DIP) 매핑의 네트워크 컨트롤러에 의해 제어 됩니다.  
  
### <a name="L2"></a>규격 IEEE 이더넷 헤더  
HNV는 업계 표준 프로토콜을 사용 하는 타사 가상 및 물리적 어플라이언스와의 상호 운용성을 보장 하기 위해 올바른 L2 이더넷 헤더를 구현 합니다. Microsoft는이 상호 운용성을 보장 하기 위해 모든 전송 된 패킷이 모든 필드에서 호환 값을 갖도록 합니다. 또한 실제 L2 네트워크의 점보 프레임 (MTU > 1780)은 캡슐화 프로토콜 (NVGRE, VXLAN)에 의해 도입 된 패킷 오버 헤드를 고려 하는 데 필요 하며, 게스트 Virtual Machines HNV에 연결 된 상태를 유지 하 Virtual Network 1514 MTU.  
  
## <a name="see-also"></a>참조  
  
-   [Hyper-V 네트워크 가상화 개요](hyperv-network-virtualization-overview-windows-server.md)  
  
-   [Hyper-V 네트워크 가상화 기술 세부 정보](hyperv-network-virtualization-technical-details-windows-server.md)  
  
-   [소프트웨어 정의 네트워킹](../../Software-Defined-Networking--SDN-.md)  
  