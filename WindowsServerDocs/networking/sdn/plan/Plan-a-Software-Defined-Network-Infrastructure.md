---
title: 소프트웨어 정의 된 네트워크 Infrastructure 계획
description: 이 항목 소프트웨어 정의 네트워크 (SDN) infrastructure 배포를 계획 하는 방법에 대해 설명 합니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.service: virtual-network
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ea7e53c8-11ec-410b-b287-897c7aaafb13
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bb3b9313996637fa5ee7367c538fe04d7cbefea9
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="plan-a-software-defined-network-infrastructure"></a>소프트웨어 정의 된 네트워크 Infrastructure 계획

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

다음 정보를 소프트웨어 정의 네트워크 (SDN) infrastructure 배포를 계획 하는 데 도움이 검토 합니다. 이 정보를 검토 한 후 참조 [소프트웨어 정의 네트워크 인프라 배포](../deploy/Deploy-a-Software-Defined-Network-Infrastructure.md) 배포 정보에 대 한 합니다.

>[!NOTE]
>이 항목 외에 다음과 같은 SDN 계획 콘텐츠를 사용할 수 있습니다.  
>
> - [설치 및 네트워크 컨트롤러 배포 하기 위한 준비 요구 사항](Installation-and-Preparation-Requirements-for-Deploying-Network-Controller.md)  

에 대 한 Hyper-v 네트워크 가상화 (HNV), 가상화 Microsoft SDN 배포에서 네트워크를 사용할 수 있는 정보를 참조 하세요. [Hyper-v 네트워크 가상화](../technologies/hyper-v-network-virtualization/Hyper-V-Network-Virtualization.md)합니다.  

## <a name="prerequisites"></a>필수
이 번호를 포함 하 여 하드웨어 및 소프트웨어 필수 설명 합니다.

-   **실제 네트워크**  
    RDMA 기술을 사용 하는 경우 Vlan, 라우팅, BGP, 데이터 센터 브리지 (ETS) 구성 실제 네트워크 장치에 액세스 해야 하 고 데이터 센터 브리지 (PFC) 사용 하 여 RoCE 경우 RDMA 기술을 기반으로 합니다. 이 항목에서는 BGP 피어 링 뿐만 아니라 수동 스위치 구성 계층 3 스위치 / 라우터 또는 액세스 원격 서버 (RRAS) 및 라우팅 가상 컴퓨터 합니다.   

-   **실제 컴퓨팅 호스트**  
이러한 호스트 Hyper-v 실행 하 고 호스트 SDN 인프라와 테 가상 컴퓨터 필요 합니다.  최상의 성능을 나중에 설명 된 이러한 호스트에서 특정 네트워크 하드웨어가 필요는 **네트워크 하드웨어** 섹션.  
      
  
## <a name="physical-network-configuration"></a>실제 네트워크 구성

각 실제 컴퓨팅 호스트 실제 스위치 포트에 연결 하는 하나 이상의 네트워크 어댑터를 통해 네트워크 연결이 필요 합니다. 네트워크는 계층 2로 필요에 따라 지원 여러 논리 네트워크 단위로 분리 [VLAN](https://en.wikipedia.org/wiki/Virtual_LAN)합니다. IP 서브넷 접두사 및 아래에 표시 된 VLAN Id 예는 네트워크 관리자에 게에서 지침에 따라 귀하의 환경에 대 한 사용자 지정 해야 합니다. 논리 네트워크 중 하나 tagged 수 없거나 액세스 모드에서를 사용 하 여 VLAN ID 0 이러한 네트워크에 대 한 논리 서브넷 System Center 가상 컴퓨터 Manager 또는 PowerShell 스크립트 구성 파일 구성할 때 합니다.

>[!IMPORTANT]
>Windows Server 2016 소프트웨어 네트워킹 정의 언더레이 및 오버레이 IPv4 주소를 지원 합니다. IPv6 지원 되지 않습니다.
  
### <a name="management-and-hnv-provider-logical-networks"></a>관리 및 HNV 공급자 논리 네트워크

모든 물리적 호스트 관리 논리 네트워크와 HNV 공급자 논리 네트워크에 액세스할 수 있는 필요가 계산 해야 합니다. 논리 네트워크 Vlan를 사용 하는 경우 물리적 컴퓨팅 호스트 이러한 Vlan에 액세스할 수 있는 스위치를 trunked 포트에 연결 해야 합니다. 마찬가지로, 컴퓨팅 호스트 실제 네트워크 어댑터 사용할 수 없습니다 활성화 VLAN 필터링. Switch-Embedded 팀 (설정)를 사용 하는 여러 NIC 팀 멤버 (즉, 네트워크 어댑터) 컴퓨팅 호스트에 있는 경우 모든 NIC 팀 멤버 해당 호스트 같은 2 계층 브로드캐스트 도메인에 연결 해야 합니다.  
  
IP 주소가 계획을 위해 각 실제 컴퓨팅 호스트 관리 논리 네트워크에서 지정 하나 이상 IP 주소가 있어야 합니다. 네트워크 컨트롤러 HNV 공급자 논리 네트워크에서 두 개의 정확 하 게 IP 주소를 자동으로 할당합니다. 실제 컴퓨팅 호스트 추가 인프라 가상 컴퓨터 (예를 들어 네트워크 컨트롤러, SLB/MUX 또는 게이트웨이)을 실행 중인 경우 해당 호스트 각 인프라 가상 컴퓨터를 호스팅할 관리 논리 네트워크에서 지정 추가 IP 주소가 있어야 합니다.   
  
또한 각 SLB/MUX 인프라 가상 컴퓨터 HNV 공급자 논리 네트워크에서 예약 된 IP 주소가 있어야 합니다. 

>[!IMPORTANT]
>이러한 SLB/MUX IP 주소 IP 주소 풀 HNV 공급자 논리 네트워크에 대 한 구성 된 외부에서 할당 되어야 합니다. 이렇게 하려면 네트워크에서 중복 된 IP 주소 될 수 있습니다. 

네트워크 컨트롤러 역할을 나머지 IP 주소를 관리 네트워크에서 예약 된 주소가 필요 합니다. 수동으로 만들어야 호스트 A 기록 dns에서 나머지 IP 주소가 합니다.  
  
DHCP 서버 관리 네트워크의 IP 주소를 자동으로 할당 수 있는 또는 수동으로 고정 IP 주소를 지정할 수 있습니다. SDN 스택 개별 Hyper-v 호스트 IP 풀 통해 지정 하 고 관리 하는 네트워크 컨트롤러에서에서에 대 한 HNV 공급자 네트워크에 대 한 IP 주소를 자동으로 할당 합니다.   
  
패브릭 관리자 정적 사용 하는 PowerShell 스크립트를 통해 SLB/MUX 또는 VMM HNV 공급자 IP 주소를 지정 합니다. 네트워크 컨트롤러 네트워크 컨트롤러 호스트 에이전트 특정 테 가상 컴퓨터에 대 한 정책을 네트워크를 받은 후에 물리적 컴퓨팅 호스트 HNV 공급자 IP 주소를 지정 합니다.  
  
#### <a name="sample-network-topology"></a>샘플 네트워크 토폴로지

서브넷 접두사, VLAN Id 및 네트워크 관리자의 지침에 따라 게이트웨이 IP 주소를 사용자 지정 합니다.  
  
네트워크 이름|서브넷|가 면|트렁크에 VLAN ID|게이트웨이|예약<br />(예)  
----------------|----------|--------|--------------------|-----------|-----------------------------  
|**관리**|10.184.108.0|24|7|10.184.108.1|라우터 10.184.108.1-<br /><br />네트워크 컨트롤러 10.184.108.4-<br /><br />10.184.108.10-컴퓨팅 호스트 1<br /><br />10.184.108.11-컴퓨팅 호스트 2<br /><br />10.184.108.X-컴퓨팅 호스트 X  
|**HNV 공급자**|10.10.56.0|23|11|10.10.56.1|라우터 10.10.56.1-<br /><br />10.10.56.2-SLB/MUX1  
  
### <a name="logical-networks-for-gateways-and-the-software-load-balancer"></a>게이트웨이 및 부하 분산 소프트웨어가 대 한 논리 네트워크
  
추가 논리 네트워크 만들고 게이트웨이 및 SLB 사용을 위해 제공 해야 합니다. 다시 한 번 네트워크 얻으려면 관리자에 올바른 IP 접두사, VLAN Id 및 이러한 네트워크에 대 한 게이트웨이 IP 주소를 사용 해야 할 수도 있습니다.

#### <a name="transit-logical-network"></a>교통 논리 네트워크
  
RAS 게이트웨이 및 SLB/MUX BGP 피어 링 정보와 북쪽/사우스 (외부 내부) 테 교통 교환 하려면 연락처 교통 논리 네트워크를 사용 합니다. 이 서브넷 크기 일반적으로 다른 보다 작은 됩니다 합니다. RAS 게이트웨이 또는 SLB/MUX 가상 컴퓨터를 실행 하는 물리적 컴퓨팅 호스트만 필요 네트워크 어댑터는 컴퓨팅 호스트 연결 되어 있는 스위치 포트에서 이러한 Vlan trunked 하 고 액세스할 수 있는이 서브넷에 연결 합니다. 각 SLB/MUX 또는 RAS 게이트웨이 가상 컴퓨터 하나의 IP 주소 교통 논리 네트워크에서 할당 정적 됩니다.

#### <a name="public-vip-logical-network"></a>공용 VIP 논리 네트워크  
  
공용 VIP 논리 네트워크는 클라우드 환경을 (일반적으로 경로 조정 가능 인터넷) 경로 조정 가능 IP 서브넷 접두사가 필요 합니다.  이러한 사이트에 게이트웨이 대 한 전면 종료 VIP를 포함 하 여 가상 네트워크 리소스에 액세스할 클라이언트 외부에서 사용 되는 프런트 IP 주소 됩니다.

#### <a name="private-vip-logical-network"></a>개인 VIP 논리 네트워크
  
개인 VIP 논리 네트워크만 내부 클라우드 클라이언트 SLB 관리자 또는 개인 서비스에서에서 액세스할 수 있는 Vip에 사용 되는 외부 클라우드 경로 조정 가능 되도록 필요 하지 않습니다.
  
#### <a name="gre-vip-logical-network"></a>GRE VIP 논리 네트워크

GRE VIP 네트워크 S2S GRE 연결 형식 여 SDN 패브릭에서 실행 중인 게이트웨이 가상 컴퓨터에 할당 된 Vip 정의 하는 용도로 있는 서브넷입니다. 이 네트워크 실제 스위치 나 라우터에서 미리 구성 해야 할를 할당 VLAN 없는 필요 없습니다.   

### <a name="sample-network-topology"></a>샘플 네트워크 토폴로지

서브넷 접두사, VLAN Id 및 네트워크 관리자의 지침에 따라 게이트웨이 IP 주소를 사용자 지정 합니다.  
  
네트워크 이름|서브넷|가 면|트렁크에 VLAN ID|게이트웨이|예약<br />(예)  
----------------|----------|--------|--------------------|-----------|-----------------------------  
|**교통**|10.10.10.0|24|10|10.10.10.1|10.10.10.1-라우터  
|**공용 VIP**|41.40.40.0|27|나|41.40.40.1|41.40.40.1-라우터<br /> 41.40.40.2-SLB/MUX VIP<br />41.40.40.3-IPSec S2S VPN VIP  
|**개인 VIP**|20.20.20.0|27|나|20.20.20.1|20.20.20.1-기본 GW (라우터)  
|**GRE VIP**|31.30.30.0|24|나|31.30.30.1|기본 GW 31.30.30.1-|  
  
### <a name="logical-networks-required-for-rdma-based-storage"></a>필요한 RDMA 기반 저장소에 대 한 논리 네트워크  
  
우면 RDMA를 사용 하 여 저장소를 기반으로 다음 컴퓨팅 및 저장소 호스트의 VLAN 및 서브넷 각 실제 어댑터용를 정의 필요 합니다. 일반적으로 두 개의 실제 어댑터가 노드가이 구성에 따라 해야 합니다.  
  
> [!IMPORTANT]  
> 가장 실제 스위치 서비스 품질 설정 올바르게 적용 되도록 하기 위해에서 tagged VLAN 보낼 RDMA 교통이 필요 합니다.  태그가 VLAN 또는 물리적 액세스 모드 포트에서 RDMA 교통을 두지 않습니다.  
  
네트워크 이름  |서브넷  |가 면  |트렁크에 VLAN ID  |게이트웨이  |예약<br />(예)    
---------|---------|---------|---------|---------|---------  
**Storage1**     |    10.60.36.0     | 25        |   8      |  10.60.36.1       |  10.60.36.1-라우터<br />10.60.36.x-컴퓨팅 호스트 x<br />10.60.36.y-컴퓨팅 호스트 y<br />10.60.36.v-계산 클러스터<br />10.60.36.w-저장소 클러스터  
|**Storage2**|10.60.36.128|25|9|10.60.36.129|10.60.36.129-라우터<br />10.60.36.x-컴퓨팅 호스트 x<br />10.60.36.y-컴퓨팅 호스트 y<br />10.60.36.v-계산 클러스터<br />10.60.36.w-저장소 클러스터  
  
스위치 구성에 대 한 자세한 내용은 참조는 **구성 예** 섹션.  
  
## <a name="routing-infrastructure"></a>라우팅 infrastructure  
  
스크립트를 사용 하 여 SDN 인프라를 배포 하는 경우에 실제 네트워크를 서로 경로 조정 가능 관리, HNV 공급자, 교통, 및 VIP 서브넷 해야 합니다.     
  
라우팅 정보 \ (예: 다음 hop\)에 대 한 VIP 서브넷 알리는 SLB/MUX 및 RAS 게이트웨이 BGP 피어 내부 링을 사용 하 여 실제 네트워크에 있습니다. VIP 논리 네트워크 할당 VLAN 하지 않은 2 계층 스위치 (예: 랙 위에 스위치)에서 미리 구성 된 하지 않습니다.  
  
경로 SLB/MUXes 및 RAS 게이트웨이 광고 VIP 논리 네트워크에 대 한 받으려는 SDN 인프라에 사용 되는 경우 라우터에서 BGP 피어 만들 해야 합니다. (출처: SLB/MUX 또는 외부 BGP 피어 RAS 게이트웨이) 방법 중 하나를 하기만 BGP 피어 링 있습니다.  하지만 사용자의 첫 번째 layer 위의 사용할 수 있으며 고정 경로 OSPF 같은 다른 동적 라우팅 프로토콜, 이전에 명시 된에서는 IP 서브넷 접두사 VIP 논리 네트워크에 대 한 외부 BGP 피어 실제 네트워크에서 경로 조정 가능 수행 해야 합니다.   
  
BGP 피어 링 관리 스위치 나 라우터가 네트워크 인프라의 일환으로에서 일반적으로 구성 됩니다. 원격 서버 (RAS 액세스) 역할이 경로 전용 모드에 설치 된 BGP 피어 Windows Server에서 구성할 수도 수 있습니다. 이 BGP 라우터 피어 네트워크 인프라에는 자체 ASN 있고 SDN 구성 요소에 할당 된 ASN에서 피어 링 허용 하도록 구성 해야 \ (SLB/MUX 및 RAS Gateways\). 실제 라우터 또는 해당 라우터를 제어 하는 네트워크 관리자에서 다음과 같은 정보를 받아야 합니다.

- 라우터 ASN  
- 라우터의 IP 주소  
- (어떤 수 AS 개인 ASN 범위에서) SDN 구성에서 사용할 수 있도록 ASN

>[!NOTE]
>네 바이트 ASNs SLB/MUX에서 지원 되지 않습니다. 두 개의 바이트 ASNs SLB/MUX와 라우터에 할당 해야 연결 하는 wo 합니다. 4 바이트 ASNs 귀하의 환경에 다른 곳에서 사용할 수 있습니다.  
  
또는 네트워크 관리자 RAS 게이트웨이 및 SLB/MUXes를 사용 하는 논리 교통 네트워크 서브넷 주소나 ASN 및 IP 주소에서 연결을 수락 하도록 BGP 라우터 피어를 구성 해야 합니다.
  
자세한 내용은 참조 [테두리 게이트웨이 프로토콜 & #40; BGP & #41;](../../../remote/remote-access/bgp/Border-Gateway-Protocol-BGP.md).
  
## <a name="default-gateways"></a>기본 게이트웨이

실제 호스트 게이트웨이 가상 컴퓨터 등 여러 네트워크에 연결 하도록 구성 된 컴퓨터 에서만 기본 게이트웨이 구성 되어 있어야 합니다. 기본 게이트웨이 인터넷 끝에 도달 하는 데 사용 되는 어댑터에서 일반적으로 구성 됩니다.

가상 컴퓨터에 대 한 다음 규칙 사용 하 여 기본 게이트웨이으로 사용 하 여 네트워크를 결정 합니다.

1. 가상 컴퓨터를 통과 네트워크에 연결 되어 있는 경우 또는 하 고 교통 및 기타 네트워크 다중 홈가 있는 경우 기본 게이트웨이으로 전송 네트워크를 사용 합니다.  
2. 가상 컴퓨터 관리 네트워크에만 연결 되어 있는 경우 기본 게이트웨이으로 관리 네트워크를 사용 합니다.  
3.  기본 게이트웨이 HNV 공급자 네트워크 사용 하면 안 됩니다. 이 네트워크에 연결 하는 유일한 가상 컴퓨터의 SLB/MUXes 및 RAS 게이트웨이 됩니다.  
4.  가상 컴퓨터 Storage1, Storage2, 공용 VIP 또는 개인 VIP 네트워크에 직접 연결 되지 않습니다.  
  
Hyper-v 호스트 및 저장 노드에 대 한 기본 게이트웨이으로 관리 네트워크를 사용 합니다.  저장소 네트워크 절대 할당 기본 게이트웨이 있어야 합니다.
  
## <a name="network-hardware"></a>네트워크 하드웨어

다음 섹션 네트워크 하드웨어 배포 계획을 사용할 수 있습니다.

### <a name="network-interface-cards-nics"></a>인터페이스 Nic (네트워크 카드)

최고의 성능을 얻으려면, 특정 기능 Hyper-v 호스트 및 저장소 호스트에 사용 하 여 네트워크 인터페이스 카드 사용 해야 합니다.  
 
원격 직접 메모리 액세스 (RDMA)을 커널을 호스트 CPU를 않고도 많은 양의 데이터를 전송할 수 있도록 해 주는 기술을 알림을 무시할입니다. 네트워크 어댑터에 DMA 엔진 전송 하기 때문에 CPU 메모리 동작에 대 한 사용 되지 않습니다.  다른 작업을 수행할 수 있는 CPU를 해제 합니다.  

스위치 Embedded 팀 (설정) NIC 팀 솔루션 Hyper-v 및 소프트웨어 정의 네트워킹 (SDN) 스택 Windows Server 2016에 포함 된 환경에서 사용할 수 있는 다른 방법입니다. NIC 팀 기능을 일부 Hyper-v의 가상 스위치에 통합 하는 설정 합니다.

자세한 내용은 참조 [원격 직접 메모리 액세스 & #40; RDMA & #41; Embedded 팀 & #40; 전환 설정 & #41;](../../../virtualization//hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md).  

테 가상 네트워크 교통 VXLAN 또는 NVGRE 캡슐화 머리글 인해 오버에 맞도록 2 계층 패브릭 네트워크 (스위치와 호스트)의 MTU 설정 해야에 보다 크거나 1674 바이트 \ (2 계층 이더넷 headers\ 포함). 새 지원 Nic *EncapOverhead* 고급 어댑터 키워드 MTU 호스트 에이전트 네트워크 컨트롤러를 통해 자동으로 설정 됩니다. 새 지원 하지 않는 Nic *EncapOverhead* 키워드를 사용 하 여 각 실제 호스트 수동으로 MTU 크기를 설정 해야 할는 *JumboPacket* \(or equivalent\) 키워드 합니다.

### <a name="switches"></a>전환
  
실제 스위치와 귀하의 환경에 대 한 라우터를 선택 하 않도록 하는 경우 다음과 같은 기능 집합을 지원 합니다.  

- Switchport MTU 설정 \(required\)  
- MTU 설정 > 1674 바이트 = \ (l 2 이더넷 Header\ 포함)  
- 프로토콜 \(required\) l 3  
- ECMP  
- BGP \(IETF RFC 4271\)\-based ECMP

구현 해야 문을 다음 IETF 표준을에서 지원 해야 합니다.

- 2545 RFC: "BGP 4 멀티 프로토콜 확장 IPv6 도메인 간 라우팅"  
- 4760 RFC: 멀티 프로토콜 "확장" BGP 4  
- 4893 RFC: "4 옥텟 AS에 대 한 지원을 BGP 번호 공간"  
- 4456 RFC: "BGP 경로 비친 풍경: 전체 하는 대신 Mesh 내부 BGP (IBGP)"  
- 4724 RFC: "BGP 정상적으로 다시 시작 메커니즘"  

태그 지정 프로토콜은 필요 합니다.

- 다양 한 유형의 트래픽 분리 VLAN
- 802.1 q 트렁크

다음과 같은 항목이 Link 컨트롤을 제공합니다.

- 서비스 품질 \ (PFC RoCE\ 사용 하는 경우에 필요)
- 교통 향상 된 선택 항목이 \(802.1Qaz\)
- 우선 순위 부여 기반 흐름 제어 \ (802.1 p/Q 및 802.1Qbb\)

다음 항목 사용 가능 시간 및 중복 제공합니다.

- 전환 하 여 가용성 (필수).
- 가용성 라우터 게이트웨이 기능을 수행 해야 합니다. 다중 섀시 switch\ 라우터 또는 VRRP 같은 기술을 사용 하 여이 수행할 수 있습니다.
        
다음과 같은 항목이 관리 기능을 제공합니다.

**모니터링**

- SNMP v1 또는 SNMP v2 (네트워크 컨트롤러를 사용 하 여 실제 스위치를 모니터링 하는 경우 필요)  
- SNMP Mib \ (물리적 스위치 monitoring\에 대 한 네트워크 컨트롤러를 사용 하는 경우 필요)  
- 설명 되어 (1213 RFC), LLDP, MIB IF MIB \(RFC 2863\) IP MIB, IP-앞-MIB, Q-다리-MIB, 다리 MIB, LLDB MIB, 엔터티 MIB, IEEE8023-지연-MIB 인터페이스  
  
다음 다이어그램 샘플 네 노드 설치를 보여 줍니다. 선명도 목적을 위해 처음 그림의 네트워크 컨트롤러, 네트워크 컨트롤러 및 소프트웨어 부하 분산 표시 하 고 세 번째 다이어그램 네트워크 컨트롤러, 소프트웨어 부하 분산와 게이트웨이 보여 줍니다.  
  
저장소 네트워크와 vNICs 이러한 다이어그램 shonwn 되지 않습니다. SMB 기반 저장소를 사용 하려는 경우 필요한은 다음과 같습니다.    
  
모든 물리적 컴퓨팅 호스트 (올바른 논리 네트워크에 대 한 정확한 네트워크 연결이 있는지 경우) 간에 인프라와 테 가상 컴퓨터 재배포할 수 있습니다.  
  
### <a name="network-controller-deployment"></a>네트워크 컨트롤러 배포

네트워크 컨트롤러를 배포 하기 전에 설치 및 소프트웨어 요구 사항으로 구성 보안 그룹 동적 DNS 등록 검토 해야 합니다. 자세한 내용은 참조 [설치 및 배포 네트워크 컨트롤러 위한 준비 요구 사항](Installation-and-Preparation-Requirements-for-Deploying-Network-Controller.md)합니다.

가상 컴퓨터에서 구성 된 세 네트워크 컨트롤러 노드 설치 매우 사용할 수입니다. 도 표시 두 가상 서브넷 나뉩니다 테 2 가상 네트워크 테 넌 웹 계층 및 데이터베이스 계층 시뮬레이트에 두 가지입니다.  

![SDN NC 계획](../../media/Plan-a-Software-Defined-Network-Infrastructure/SDN-NC-Planning.png)

### <a name="network-controller-and-software-load-balancer-deployment"></a>네트워크 컨트롤러 및 소프트웨어 부하 분산 배포

높은 가용성 두 개 이상의 SLB/MUX 노드 있습니다.
   
![SDN NC 계획](../../media/Plan-a-Software-Defined-Network-Infrastructure/SDN-SLB-Deployment.png)
  
### <a name="network-controller-software-load-balancer-and-ras-gateway-deployment"></a>네트워크 컨트롤러, 소프트웨어 부하 분산 및 RAS 게이트웨이 배포

세 가지 게이트웨이 가상 컴퓨터가; 두 개의 활성 상태 이며 하나 중복 됩니다.

![SDN NC 계획](../../media/Plan-a-Software-Defined-Network-Infrastructure/SDN-GW-Deployment.png)  
  
  
  
배포 TP5 기반 자동화, Active Directory 하 고 이러한 서브넷에서 사용할 수 있어야 합니다. Active Directory에 대 한 자세한 내용은 참조 [Active Directory Domain Services 개요](https://technet.microsoft.com/en-us/library/mt703721.aspx)합니다.  
  
>[!IMPORTANT] 
>VMM를 사용 하 여 배포 하는 경우 되도록 인프라 가상 컴퓨터 (VMM 서버, 광고/DNS SQL Server, 등) 다이어그램에 네 가지 호스트 중 하나에 호스팅된 되지 않습니다.  
  
## <a name="switch-configuration-examples"></a>구성 예 전환  
  
실제 스위치 나 라우터에서 구성을 위해 샘플 구성에 대 한 파일 스위치 모델 및 공급 업체의 다양 한 설정에서 사용할 수 있는 [Microsoft SDN Github 저장소](https://github.com/microsoft/SDN/tree/master/SwitchConfigExamples)합니다. 자세한 정보 및 특정 스위치가 대 한 테스트 명령줄 인터페이스 (CLI) 명령 제공 됩니다.         
  
  
## <a name="compute"></a>계산  
모든 Hyper-v 호스트 Windows Server 2016 설치 되어 있어야 하 고 Hyper-v를 사용 하도록 설정 물리적 어댑터를 사용 하 여 만든 외부 Hyper-v 가상 스위치 관리 논리 네트워크에 연결 합니다. 호스트 관리 호스트 vNIC에 지정 된 관리 IP 주소를 통해 연결할 수 있어야 합니다.  
  
Hyper-v, 공유 또는 로컬와 호환 되는 모든 저장소 입력을 사용할 수 있습니다.   
  
> [!TIP]  
> 필수입니다. 하지만 폴더가 모든 가상 스위치를 사용 하는 경우 유용 합니다. 스크립트를 사용 하 여 배포를 계획 하는 경우 참조와 관련 된 메모에서 `vSwitchName`config.psd1 파일에서 가변 합니다.  
  
**호스트 컴퓨팅 요구 사항**  
다음 표에서 배포 예제에에서 사용 되는 4 물리적 호스트에 대 한 최소 하드웨어 및 소프트웨어 요구 사항이 나와 있습니다.  
  
호스트|하드웨어 요구 사항|소프트웨어 요구 사항|  
--------|-------------------------|-------------------------  
|실제 hyper-v 호스트|4 코어 2.66 g h z CPU<br /><br />32GB의 RAM<br /><br />300 g B 디스크 공간<br /><br />1gb/s (또는 빠르게) 실제 네트워크 어댑터|운영 체제: Windows Server 2016<br /><br />Hyper-v 역할이 설치|  
  
  
**SDN 인프라 가상 컴퓨터 역할 요구 사항**  
  
역할|vCPU 요구 사항|메모리 요구 사항|디스크 요구 사항|  
--------|---------------------|-----------------------|---------------------  
|네트워크 컨트롤러 (세 노드)|4 vCPUs|4 g B 분 (8GB 권장)|OS 드라이브에 대 한 75 g B  
|SLB/MUX (세 노드)|8 vCPUs|권장 8GB|OS 드라이브에 대 한 75 g B  
|RAS 게이트웨이<br /><br />(세 개의 노드 게이트웨이, 두 활성, 수동 하나 하나의 풀)|8 vCPUs|권장 8GB|OS 드라이브에 대 한 75 g B  
|RAS 게이트웨이 BGP 라우터에 관한 SLB/MUX 피어 링<br /><br />(또는 사용 하 여에 스위치 BGP 라우터로)|2 vCPUs|2GB|OS 드라이브에 대 한 75 g B|  
  
  
배포에 대 한 VMM를 사용 하는 경우 추가 인프라 가상 컴퓨터 리소스는 VMM 및 기타 SDN 비 인프라에 대해 필요 합니다. 자세한 내용은 참조 [최소 시스템 센터 Technical Preview에 대 한 하드웨어 권장 합니다.](https://technet.microsoft.com/library/dn997303.aspx)  
  
## <a name="extending-your-infrastructure"></a>인프라를 확장합니다.  
인프라에 대 한 크기 조정 및 리소스 요구 사항을 개최 된 하려는 테 작업 가상 컴퓨터에 따라 달라 집니다. CPU, 메모리 및 디스크 요구 인프라 가상 컴퓨터에 대 한 (예: 네트워크 컨트롤러, SLB, 게이트웨이, 등)은 위의 표에 나열 됩니다. 필요에 따라 확장할 수 이러한 인프라 가상 컴퓨터의 추가할 수 있습니다. 그러나 Hyper-v 호스트에서 실행 중인 모든 테 가상 컴퓨터 자신의 CPU, 메모리 및 디스크 요구 고려해 야 하는 했습니다.   
  
테 작업 가상 컴퓨터 실제 Hyper-v 호스트에서 너무 많이 리소스를 사용 하는 시작, 추가 실제 호스트 추가 하 여 인프라를 확장할 수 있습니다. 가상 컴퓨터 관리자와 또는 (배포한 방식에 따라 처음에 인프라) PowerShell 스크립트를 사용 하 여 이렇게 네트워크 컨트롤러를 통해 새로운 서버 리소스 만들 수 있습니다. HNV 공급자 네트워크에 대 한 추가 IP 주소를 추가 해야 하는 경우 (해당 IP 풀)와 호스트 사용할 수 있는 새로운 논리 서브넷 만들 수 있습니다.  
  
  
## <a name="see-also"></a>참조 하십시오  
[설치 및 네트워크 컨트롤러 배포 하기 위한 준비 요구 사항](Installation-and-Preparation-Requirements-for-Deploying-Network-Controller.md)  
[소프트웨어 정의 네트워킹 및 #40; SDN & #41;](../Software-Defined-Networking--SDN-.md)  
  


