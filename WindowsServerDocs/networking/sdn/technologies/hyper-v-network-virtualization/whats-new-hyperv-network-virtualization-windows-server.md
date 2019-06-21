---
title: Windows Server 2016의에서 Hyper-v 네트워크 가상화의 새로운 기능
description: 이 항목에서는 Windows Server 2016에서 Hyper-v 네트워크 가상화의 새로운 기능에 대 한 정보를 제공합니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0254275a-0a77-40a9-b68a-1029284c03fe
ms.author: pashort
author: shortpatti
ms.date: 03/19/2018
ms.openlocfilehash: c87ccfba7b9ccc77646f58ade2853766524e67b1
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284036"
---
# <a name="whats-new-in-hyper-v-network-virtualization-in-windows-server-2016"></a>Windows Server 2016의에서 Hyper-v 네트워크 가상화의 새로운 기능

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 Windows Server 2016의 새롭거나 변경 된 Hyper-v 네트워크 가상화 (HNV) 기능을 설명 합니다.  
  
## <a name="BKMK_IPAM2012R2"></a>HNV의 업데이트  
HNV는 다음 영역에서 향상 된 지원을 제공합니다.  
  
|기능|새로운 기능 또는 향상된 기능|설명|  
|--------------------------|-------------------|---------------|  
|[프로그래밍 가능한 Hyper-V 스위치](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#SDN)|단추를 사용하여 새|HNV 정책은 Microsoft 네트워크 컨트롤러를 통해 프로그래밍 가능 합니다.|  
|[VXLAN 캡슐화 지원](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#VXLAN)|단추를 사용하여 새|HNV는 이제 VXLAN 캡슐화를 지원합니다.|  
|[소프트웨어 부하 분산 장치 (SLB) 간의 상호 운용성](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#SLB)|단추를 사용하여 새|HNV는 Microsoft 소프트웨어 부하 분산 장치를 사용 하 여 완벽 하 게 통합 되어 있습니다.|  
|[규격 IEEE 이더넷 헤더](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#L2)|향상된 기능|IEEE 이더넷 표준을 준수|  
  
### <a name="SDN"></a>프로그래밍 가능한 Hyper-V 스위치  
HNV는 Microsoft의 업데이트 된 소프트웨어 정의 네트워킹 (SDN) 솔루션의 기본 빌딩 블록 및 SDN 스택을에 완전히 통합 됩니다.  
  
Microsoft의 새로운 네트워크 컨트롤러에는 HNV 정책으로는 SouthBound 인터페이스 (SBI) 열려 vSwitch 데이터베이스 관리 프로토콜 (OVSDB)를 사용 하 여 각 호스트에서 실행 되는 호스트 에이전트 아래로 푸시합니다. 호스트 에이전트의 사용자 지정을 사용 하 여이 정책을 저장 합니다 [VTEP 스키마](https://github.com/openvswitch/ovs/blob/master/vtep/vtep.ovsschema) 및 Hyper-v 스위치에서 고성능 흐름 엔진에 복잡 한 흐름 규칙 프로그램입니다.  
  
Hyper-v 스위치 내의 흐름 엔진은 Microsoft Azure에서 사용한 동일한 엔진&trade;, 대규모로-Microsoft Azure 공용 클라우드에서 입증 되었습니다. 또한 네트워크 컨트롤러 및 네트워크 리소스 공급자 (자세한 내용은 곧 제공 될 예정)를 통해 전체 SDN 스택을 구성에 일관성이 따라서로 가져와 Microsoft Azure 공용 클라우드의 엔터프라이즈 및 호스팅 서비스에 Microsoft azure 공급자 고객입니다.  
  
> [!NOTE]  
> OVSDB에 대 한 자세한 내용은 참조 하세요. [RFC 7047](https://www.rfc-editor.org/info/rfc7047)합니다.  
  
Hyper-v 스위치는 간단한 'Microsoft 내에서 ' 동작과 일치 흐름 엔진을 기반으로 두 상태 비저장 및 상태 저장 흐름 규칙을 지원 합니다.  
 
![Windows Server 2016 Hyper-v 스위치](../../../media/what-s-new-in-hyper-v-network-virtualization-in-windows-server/HNVOverview.png)  
  
### <a name="VXLAN"></a>VXLAN 캡슐화 지원  
Virtual eXtensible Local Area Network (-VXLAN [RFC 7348](https://www.rfc-editor.org/info/rfc7348)) 프로토콜은 널리 채택 시장에, Cisco, Brocade, Dell, HP 및 다른 사용자와 같은 공급 업체에서 지원 합니다. HNV는 이제 프로그램 매핑에 Microsoft 네트워크 컨트롤러를 통해 MAC 배포 모드를 사용 하 여 테 넌 트 오버레이 네트워크 IP 주소 (고객 주소 또는 CA)를 실제 언더레이 네트워크 IP 주소 (공급자에 대 한이 캡슐화 체계 지원 주소 또는 PA)입니다. NVGRE 및 VXLAN 작업 오프 로드 하는 타사 드라이버를 통해 성능 향상된을 위해 지원 됩니다.  
  
### <a name="SLB"></a>소프트웨어 부하 분산 장치 (SLB) 간의 상호 운용성  
Windows Server 2016 가상 네트워크 트래픽 및 HNV 통해 원활한 상호 작용에 대 한 전체 지원과 소프트웨어 부하 분산 장치 (SLB)를 포함합니다. SLB 데이터 평면 v 스위치의 고성능 흐름 엔진을 통해 구현 되 고 네트워크 컨트롤러에서 제어에 대 한 VIP (가상 IP) / 동적 IP (DIP) 매핑.  
  
### <a name="L2"></a>규격 IEEE 이더넷 헤더  
HNV는 업계 표준 프로토콜에 의존 하는 타사 가상 및 실제 어플라이언스를 사용 하 여 상호 운용성을 보장 하려면 올바른 L2 이더넷 헤더를 구현 합니다. Microsoft이 상호이 운용성을 보장 하려면 모든 필드에 전송 된 모든 패킷이 규격 값 있는지 확인 합니다. 또한 실제 L2 네트워크에서 Jumbo 프레임 (MTU > 1780) 게스트는 HNV 가상 네트워크에 연결 된 가상 컴퓨터를 유지 하면서 캡슐화 프로토콜 (NVGRE, VXLAN) 오버 헤드가 도입 된 패킷에 대 한 계정에 필요한에 대해 지원 된 1514 MTU 합니다.  
  
## <a name="see-also"></a>참조  
  
-   [Hyper-V 네트워크 가상화 개요](hyperv-network-virtualization-overview-windows-server.md)  
  
-   [Hyper-V 네트워크 가상화 기술 세부 정보](hyperv-network-virtualization-technical-details-windows-server.md)  
  
-   [소프트웨어 정의 네트워킹](../../Software-Defined-Networking--SDN-.md)  
  