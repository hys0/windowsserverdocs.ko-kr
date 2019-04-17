---
title: Hyper-v 네트워크 가상화 Windows server 2016의에서 새로운 기능
description: 이 항목에서는 Windows Server 2016에 네트워크 가상화 Hyper-v의에서 새로운 기능에 대 한 정보
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0254275a-0a77-40a9-b68a-1029284c03fe
ms.author: pashort
author: shortpatti
ms.date: 03/19/2018
ms.openlocfilehash: 0954768944e44848debfbb7fb752a13ca47031c2
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="whats-new-in-hyper-v-network-virtualization-in-windows-server-2016"></a>Hyper-v 네트워크 가상화 Windows server 2016의에서 새로운 기능

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

새로운 또는 변경 Windows Server 2016에 있는 Hyper-v 네트워크 가상화 (HNV) 기능에 설명 합니다.  
  
## <a name="BKMK_IPAM2012R2"></a>HNV의 업데이트  
HNV는 다음과 같은 지역에서 향상 된 지원을 제공합니다.  
  
|기능/기능|새로운 기능이 나 향상 된|설명|  
|--------------------------|-------------------|---------------|  
|[프로그래밍 Hyper-v 전환](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#SDN)|새로운|HNV 정책이 Microsoft 네트워크 컨트롤러를 통해 프로그래밍 되어 있습니다.|  
|[VXLAN 캡슐화 지원](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#VXLAN)|새로운|이제 HNV VXLAN 캡슐화를 지원합니다.|  
|[소프트웨어 부하 분산 (SLB) 상호 운용성](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#SLB)|새로운|Microsoft 소프트웨어 부하 분산 HNV 완전히 통합 되어 있습니다.|  
|[IEEE 이더넷 머리글 호환](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#L2)|개선|IEEE 이더넷 표준을 준수|  
  
### <a name="SDN"></a>프로그래밍 Hyper-v 전환  
HNV는 Microsoft의 업데이트 된 소프트웨어 정의 네트워킹 (SDN) 솔루션을 기본 구성 요소 이며 SDN 스택에 통합 되어 있습니다.  
  
Microsoft의 새 네트워크 컨트롤러 푸시합니다 HNV 정책으로는 SouthBound 인터페이스 (SBI) 열기 vSwitch 데이터베이스 관리 프로토콜 (OVSDB)를 사용 하 여 각 호스트에서 실행 되는 호스트 에이전트 나타날 때까지 아래로 합니다. 호스트 에이전트 저장의 사용자 지정을 사용 하 여이 정책에서 [VTEP 스키마](https://github.com/openvswitch/ovs/blob/master/vtep/vtep.ovsschema) Hyper-v 스위치에서 가능성 흐름 엔진에 복잡 흐름 규칙 프로그램 및 합니다.  
  
Hyper-v 스위치 내 흐름 엔진은 Microsoft Azure에 사용 되는 동일한 엔진&trade;, 공용 Microsoft Azure 클라우드에서 하이퍼 배율에는 입증 되었습니다. 또한 네트워크 컨트롤러 및 네트워크 리소스 공급자 (자세한 내용은 곧 제공)을 통해 위로 전체 SDN 스택은 Microsoft Azure, 따라서 전원 공개 Microsoft Azure 클라우드 서비스 공급자는 호스팅 고객 및 기업 참가자와 일치 합니다.  
  
> [!NOTE]  
> OVSDB에 대 한 자세한 내용은 참조 [RFC 7047](http://www.rfc-editor.org/info/rfc7047)합니다.  
  
Hyper-v 스위치를 기반으로 'Microsoft 내에서 ' 작업 일치 간단한 흐름 엔진 모두 비저장 및 안정 된 흐름 규칙을 지원 합니다.  
 
![Windows Server 2016 Hyper-v 스위치를](../../../media/what-s-new-in-hyper-v-network-virtualization-in-windows-server/HNVOverview.png)  
  
### <a name="VXLAN"></a>VXLAN 캡슐화 지원  
가상 eXtensible 로컬 영역 네트워크 (VXLAN- [RFC 7348](http://www.rfc-editor.org/info/rfc7348)) 프로토콜 Cisco, Brocade, Dell, HP 등과 같은 공급 업체 로부터 지원 지역/국가 위치에 광범위 하 게 채택 합니다. 또한 이제 HNV 테 오버레이 네트워크에 IP 주소를 (고객 주소 또는 캐나다) 실제 언더레이 네트워크 IP 주소 (공급자 주소 또는 파)에 대 한 Microsoft 네트워크 컨트롤러 프로그램 매핑을 통해 MAC 배포 모드를 사용 하 여이 캡슐화 구성표를 지원 합니다. 제 3 자 드라이버를 통해 성능 향상된을 위해 NVGRE 및 작업 오프 로드 VXLAN 지원 됩니다.  
  
### <a name="SLB"></a>소프트웨어 부하 분산 (SLB) 상호 운용성  
Windows Server 2016 모든 가상 네트워크 교통 지원 HNV와의 상호 작용 원활 하 게 소프트웨어 부하 분산 (SLB)를 포함합니다. SLB 데이터 평면 v 스위치에서 가능성 흐름 engine을 통해 구현 고 가상 IP (VIP)에 대 한 / 동적으로 네트워크 컨트롤러 제어 IP (담그고) 매핑 합니다.  
  
### <a name="L2"></a>IEEE 이더넷 머리글 호환  
HNV 올바른 l 2 이더넷 머리글 산업 표준을 프로토콜에 의존 하는 제 3 자 가상 및 물리적 기기와 상호 운용성을 구현 합니다. Microsoft에 전송 된 모든 패킷이 상호 운용성을 필드를 모두 준수 값이 있다고 보장 합니다. 또한 지원 게스트 HNV 가상 네트워크에 연결 된 모든 가상 컴퓨터 하면서 캡슐화 프로토콜 (NVGRE, VXLAN)가 머리 위로 도입 패킷 고려 하 실제 l 2 네트워크에서 점보 프레임 (MTU > 1780)가 필요에 대 한 유지 1514 MTU 합니다.  
  
## <a name="see-also"></a>참조 하십시오  
  
-   [Hyper-v 네트워크 가상화 개요](hyperv-network-virtualization-overview-windows-server.md)  
  
-   [Hyper-v 네트워크 가상화 기술 세부 정보](hyperv-network-virtualization-technical-details-windows-server.md)  
  
-   [소프트웨어 정의 네트워킹](../../Software-Defined-Networking--SDN-.md)  
  