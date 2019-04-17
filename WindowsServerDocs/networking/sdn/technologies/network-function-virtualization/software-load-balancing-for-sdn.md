---
title: 소프트웨어 균형 (SLB) SDN에 대 한
description: Windows Server 2016에 네트워킹 정의 된 소프트웨어에 대 한 부하 분산 소프트웨어가 대 한 자세한 내용은이 항목을 사용할 수 있습니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 97abf182-4725-4026-801c-122db96964ed
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 5e08afddde9c7be8d955a0cfdaf44f0fc31b8155
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="software-load-balancing-slb-for-sdn"></a>소프트웨어 균형 \(SLB\) SDN에 대 한

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

Windows Server 2016에 네트워킹 정의 된 소프트웨어에 대 한 부하 분산 소프트웨어가 대 한 자세한 내용은이 항목을 사용할 수 있습니다.  

(Csp) 클라우드 서비스 공급자와 소프트웨어 정의 네트워킹 (SDN) Windows Server 2016에 배포 하는 기업 테 및 가상 네트워크 리소스 간에 테 고객 네트워크 교통 배포 하 게 하려면 소프트웨어 부하 분산 (SLB)을 사용할 수 있습니다. Windows Server SLB 가용성 우선과 확장성 개최 된 같은 작업을 여러 서버 수 있습니다.
  
Windows Server SLB는 다음과 같은 기능이 포함 되어 있습니다.  
  
-   계층 (L4) 4 부하 분산 서비스 ' 북쪽 사우스 ' 및 TCP/UDP ' 이스트 서쪽 ' 교통 합니다.  
  
-   내부 및 공공 교통 부하 분산 네트워크입니다.  
  
-   네트워크 가상화 Hyper-v를 사용 하 여 만든 가상 네트워크와 가상 영역 로컬 네트워크 (Vlan)에서 동적 IP 주소 (Dip)을 지원 합니다.  
  
-   건강 검사 지원 합니다.  
  
-   이제 확장 기능을 포함 하 여 클라우드 배율와 multiplexers와 호스트 에이전트 기능이를 확대 합니다.  
  
자세한 내용은 참조 [부하 분산 소프트웨어가 기능](#bkmk_features) 이 여기에 있습니다.  
  
> [!NOTE]  
> 그러나 멀티 Vlan 네트워크 컨트롤러에서 지원 하지 않는 대 한 텐/던 가능한 시,를 사용할 수 있습니다 Vlan SLB 서비스 공급자에 대 한 데이터 센터 인프라와 고밀도 웹 서버와 같은 작업을 관리 합니다.  
  
Windows Server SLB를 사용 하 여 균형 SLB Vm를 사용 하 여 다른 사용자 VM 작업에 사용 하는 동일한 Hyper-v 컴퓨팅 서버의 기능 확장할 수 있습니다. 이 인해 SLB 신속 하 게 만들고 삭제 CSP 작업에 필요한 부하 분산 끝점 지원 합니다. 또한 Windows Server SLB g b 클러스터에 따라 수십 지원 간단한 프로 비전 모델을 제공 하며에 및 배율 하기가 쉽습니다.  
  
**SLB의 작동 방식**  
  
IP 주소 가상 (Vip) 리소스 데이터 센터의 클라우드 서비스 집합을의 일부인 동적 IP 주소 (Dip)를 매핑하여 SLB 작동 합니다.  
  
Vip 균형 Vm 공개 로드 풀에 대 한 액세스를 제공 하는 하나 IP 주소 됩니다. 예를 들어, Vip은 IP 주소 테 넌 및 테 고객의 클라우드 데이터 센터에에서 테 리소스에 연결할 수 있도록 인터넷에 노출입니다.  
  
Dip Vm VIP 뒤 부하가 풀의 회원의 IP 주소입니다. Dip은 클라우드 인프라 테 리소스에 내에서 지정 됩니다.  
  
Vip에는 SLB 멀티플렉서 (MUX) 포함 되어 있습니다.  하나 이상의 Vm (가상 컴퓨터)는 MUX 구성 되어 있습니다.  네트워크 컨트롤러와 각 VIP 각 MUX 하 고 각 MUX 결과적를 사용 하 여 테두리 게이트웨이 프로토콜 (BGP)는 / 32로 실제 네트워크 라우터에 각 VIP 광고를 제공 경로 합니다.  BGP 실제 네트워크 라우터를를 수 있습니다.  
  
-   VIP는 각 MUX에서 사용할 수 있는 경우에 있는 MUXes 계층 3 네트워크의 다른 서브넷에 알아보세요.  
  
-   각 VIP에 대 한 비용 같은 다중 경로 (ECMP) 경로 사용 하 여 모든 사용 가능한 MUXes 로드 확산.  
  
-   자동으로 MUX 오류나 제거 검색 및 트래픽을 실패 MUX 보내는 중지 합니다.  
  
-   실패 한 또는 제거 MUX 로드 건강 MUXes 분산 있습니다.  
  
인터넷에서 공개 교통 도착 SLB MUX를 대상으로 VIP 포함 한 지도 개별 담그고에 도착 하는 되도록 교통량을 다시 작성 하는 교통을 검사 합니다. 인바인드 네트워크 교통에 대 한이 거래는 MUX Vm (가상 컴퓨터)과 담그고 대상 있는 Hyper-v 호스트 분할 단계로 수행 됩니다.  
  
-   부하 분산-MUX 사용 하 여 담그고를 선택 하 고 VIP 패킷을, 캡슐화는 담그고 있는 Hyper-v 호스트 하 교통량을 전달 합니다.  
  
-   NAT (주소 변환)-네트워크 Hyper-v 호스트 캡슐화 패킷이에서 제거, 변환 하 여 담그고 VIP, 포트를 다시 매핑하 및 패킷을 담그고 VM 전달 됩니다.  
  
MUX 부하 분산 네트워크 컨트롤러를 사용 하 여 정의 정책으로 인해 올바른 Dip Vip 매핑할 하는 방법을 파악 합니다. 이 규칙 프로토콜, 프런트 엔드 포트, 백 엔드 포트 및 배포 알고리즘 (5 3 일 또는 2gb 튜플) 포함 됩니다.  
  
때 Vm 응답 테 아웃 바운드 보내기 네트워크 및 인터넷 이나 원격 테 위치에 다시 교통 NAT Hyper-v 호스트 교통량에 수행 되므로 MUX 우회 하 고 Hyper-v 호스트에서 지 라우터 직접 이동 됩니다. 이 MUX 우회 프로세스 직접 서버 반환 (DSR) 라고 합니다.  
  
고 인바인드 네트워크 교통 무시 완전히 SLB MUX 초기 네트워크 흐름을 설정 합니다.  
  
다음 그림 클라이언트 컴퓨터 회사 Sharepoint 사이트-이 경우 Contoso 이라는 가상 회사의 IP 주소가 DNS 쿼리를 수행 합니다. 다음 프로세스 발생합니다.  
  
-   DNS 서버가 VIP 107.105.47.60 클라이언트를 반환합니다.  
  
-   클라이언트는 VIP로 HTTP 요청을 보냅니다.  
  
-   실제 네트워크 VIP 모든 MUX에 있는 연결을 사용할 수 있는 여러 경로에 있습니다.  이와 함께 각 라우터 ECMP를 사용 하 여 요청을 MUX에 도착할 때까지 다음 세그먼트 경로 선택.  
  
-   요청을 받은 MUX 정책, 구성 확인 하 고 보 두 Dip 가능한 10.10.10.5 및 10.10.20.5 VIP 107.105.47.60에 대 한 요청을 처리 하기 위한 작업이 가상 네트워크에는  
  
-   MUX 10.10.10.5 담그고 선택한 캡슐화 VXLAN를 보낼 수 있도록 것을 사용 하 여 호스트 담그고 포함 된 호스트 네트워크 실제 주소를 사용 하 여 패킷이 됩니다.  
  
-   호스트는 암호화 된 패킷을 받아서 검사 합니다.  캡슐화를 제거 하 고 대상은 이제 VIP 대신 담그고 10.10.10.5 하 고 교통량 담그고 VM 보냅니다 패킷의 다시 작성 합니다.  
  
-   요청이 서버 농장 2에서 Contoso Sharepoint 사이트에 도달 이제 했습니다. 서버 응답 생성 하 고 원본으로 IP 주소를 사용 하는 클라이언트를 보냅니다.  
  
-   호스트 클라이언트 대상 이제 VIP 수행한 원래 요청 가상 스위치를 기억 하는에서 보내는 패킷 차단 합니다.  호스트 다시 VIP 담그고 주소 표시 되지 않는 클라이언트 하는 경향이 패킷 소스를 작성 합니다.  
  
-   호스트 표준 라우팅 테이블을 사용 하 여 결국 응답을 수신 하는 클라이언트 주로 패킷을 전달 하는 실제 네트워크에 대 한 기본 게이트웨이에 직접 패킷을 전달 됩니다.  
  
![프로세스 부하 분산 소프트웨어가](../../../media/Software-Load-Balancing--SLB--for-SDN/slb_process.jpg)  
  
**균형 조정 내부 datacenter 교통 로드**  
  
Hyper-v 가상 스위치를 Vm 연결 되어 있는 다른 서버에서 실행 되 고 같은 가상 네트워크의 회원는 테 리소스를 간에 NAT. 수행와 같은 데이터 센터의 내부 분산 네트워크 교통 때 로드  
  
내부 교통 부하 분산 첫 번째 요청이 전송 하 고 적절 한 담그고 선택 하 고 담그고 하 고 교통 경로 MUX에 의해 처리가 있습니다. 이 시점에서 기존된 교통 흐름은 MUX 무시 하 고 VM VM에서 직접 이동 됩니다.  
  
**건강 검색**  
  
SLB 건강 조사 다음을 포함 하는 네트워크 인프라 건강 유효성을 검사 하기에 포함 됩니다.  
  
-   포트 TCP 검색  
  
-   HTTP 검색 포트 및 URL  
  
기존의 부하 분산 기기 여 선택기 기기의 시작 하 고는 담그고를 통해 이동 있는 달리 SLB 검사는 담그고의 위치를 추가 하는 작업을 호스트 분산 담그고, 모드로 전환 되는 SLB 호스트 에이전트에서 직접 호스트에 시작 됩니다.  
  
## <a name="bkmk_infrastructure"></a>소프트웨어 부하 분산 인프라  
Windows Server SLB 배포할, Windows Server 2016에 네트워크 컨트롤러 및 하나 또는 여러 개의 SLB MUX Vm 먼저 배포 해야 합니다.  
  
또한 Hyper-v 호스트 SDN 사용 Hyper-v 가상 스위치를 구성 하 고 SLB 호스트 에이전트 실행 되 고 있는지 확인 해야 합니다.  호스트 역할을 하는 라우터에 같은 비용 다중 경로 (ECMP) 경로 및 테두리 게이트웨이 프로토콜 (BGP)를 지원 해야 하 고 SLB MUXes에서 BGP 피어 링 요청을 수락 하도록 설정 해야 합니다.  
  
다음은 SLB 인프라에 대 한 개요입니다.  

![인프라 부하 분산 소프트웨어가](../../../media/Software-Load-Balancing--SLB--for-SDN/slb_overview1.png)  
  
다음 섹션 SLB 인프라 이러한 요소에 대 한 자세한 정보를 제공합니다.  
  
### <a name="scvmm"></a>SCVMM  
시스템 센터 2016 년 Windows Server 2016 SLB 관리자와 의료 모니터를 포함 하 여 네트워크 컨트롤러 구성할 수 있습니다. 또한 SLB MUXs 배포 하 고 SLB 호스트 에이전트 Hyper-v 및 Windows Server 2016을 실행 하는 컴퓨터에 설치 System Center를 사용할 수 있습니다.  
  
시스템 센터 2016에 대 한 자세한 내용은 참조 [시스템 센터 2016](https://www.microsoft.com/en-us/server-cloud/products/system-center-2016/)합니다.  
  
> [!NOTE]  
> 시스템 센터 2016을 사용 하지 않을 경우 설치 하 고 네트워크 컨트롤러 및 기타 SLB 인프라 구성 Windows PowerShell 또는 다른 관리 응용 프로그램을 사용할 수 있습니다. 자세한 내용은 참조 [Windows PowerShell를 사용 하 여 네트워크 컨트롤러 배포](../../../sdn/deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)합니다.  
  
### <a name="network-controller"></a>네트워크 컨트롤러  
네트워크 컨트롤러 SLB 관리자 섬에는 및 SLB에 대 한 다음 작업을 수행 합니다.  
  
-   System Center, Windows PowerShell 또는 다른 네트워크 관리 응용 프로그램에서 Northbound API를 통해 제공 되는 SLB 명령을 처리 합니다.  
  
-   Hyper-v 호스트 및 SLB MUXes 배포에 대 한 정책을 계산합니다.  
  
-   SLB infrastructure의 상태를 제공합니다.  
  
### <a name="slb-mux"></a>SLB MUX  
SLB MUX 인바인드 네트워크 교통 처리 하 고 Vip을 Dip, 지도 다음 올바른 담그고 교통량 전달 합니다. 각 MUX BGP 사용 하 여 edge 라우터에 VIP 경로 게시할 수 있습니다. BGP 활성 상태로 유지 MUXes를 부하 분산 장치에 대 한 부하 분산 기본적으로 제공-MUX 오류가 발생할 경우 로드 재배포 활성 MUXes 수 있는 한 MUX 실패 하면 알립니다.  
  
### <a name="hosts-that-are-running-hyper-v"></a>Hyper-v 실행 되는 호스트  
Hyper-v 및 Windows Server 2016을 실행 하는 컴퓨터와 SLB 사용할 수 있습니다. Hyper-v 호스트 Vm Hyper-v에서 지 원하는 운영 체제를 실행 수 있습니다.  
  
### <a name="slb-host-agent"></a>SLB 호스트 에이전트  
SLB 배포 하는 경우 모든 Hyper-v 호스트 컴퓨터에서 SLB 호스트 에이전트 배포 하는 System Center, Windows PowerShell 또는 다른 관리 응용 프로그램 사용 해야 합니다. SLB 호스트 에이전트 Nano 서버를 포함 하 여 Hyper-v 지원을 제공 하는 모든 버전의 Windows Server 2016에 설치할 수 있습니다.  
  
네트워크 컨트롤러에서 SLB 정책 업데이트는 SLB 호스트 에이전트 수신 대기합니다. 또한 호스트 에이전트 프로그램 규칙 SLB에 대 한 SDN 활성화 Hyper-v 가상 스위치 로컬 컴퓨터에서 구성 된에 있습니다.  
  
### <a name="sdn-enabled-hyper-v-virtual-switch"></a>SDN은 Hyper-v의 가상 스위치를 활성화  
에 대해 가상 스위치를 SLB과 호환 되도록 스위치를 만들 수 Hyper-v 가상 스위치 관리자 또는 Windows PowerShell 명령을 사용 해야 하며 그리고 가상 필터링 플랫폼 (VFP)에 대해 가상 스위치를 사용 해야 합니다.  
  
Windows PowerShell 명령을 보기에 대 한 내용은 VFP 가상 스위치를 활성화 하세요 [Get VMSystemSwitchExtension](https://technet.microsoft.com/en-us/library/hh848603.aspx) 및 [활성화 VMSwitchExtension](https://technet.microsoft.com/en-us/library/hh848541.aspx?f=255&MSPPError=-2147217396)합니다.  
  
SDN Hyper-v 가상 스위치를 활성화 SLB에 대 한 다음 작업을 수행 합니다.  
  
-   SLB에 대 한 데이터 경로 처리합니다.  
  
-   MUX에서 인바인드 네트워크 교통량을 받습니다.  
  
-   DSR를 사용 하 여 라우터에 보내기 아웃 바운드 네트워크 교통량 MUX 무시 합니다.  
  
-   Hyper-v Nano Server 인스턴스에서 실행 됩니다.  
  
### <a name="bgp-enabled-router"></a>BGP 라우터를 사용 하도록 설정  
BGP 라우터 SLB에 대 한 다음 작업을 수행 합니다.  
  
-   ECMP를 사용 하 여 MUX 경로 인바인드 트래픽을 합니다.  
  
-   아웃 바운드 네트워크 교통량 호스트 제공한 경로 사용 합니다.  
  
-   SLB MUX에서 Vip 경로 업데이트를 수신합니다.  
  
-   오류가 발생 하면 활성 상태로 유지 하는 경우 SLB MUXes SLB 회전에서 제거 합니다.  
  
## <a name="bkmk_features"></a>소프트웨어 부하 분산 기능  
다음은 일부의 기능 및 SLB의 기능입니다.  
  
**핵심 기능**  
  
-   SLB 계층 4 부하 분산 ' 북쪽 사우스 ' 및 TCP/UDP ' 이스트 서쪽 ' 교통에 대 한 서비스를 제공 합니다.  
  
-   Hyper-v 네트워크 가상화 기반 네트워크에서 SLB 사용할 수 있는  
  
-   담그고 Vm SDN 활성화 Hyper-v 가상 스위치를에 연결에 대 한 SLB VLAN 기반 네트워크를 사용할 수 있습니다.  
  
-   한 SLB 인스턴스 처리 하는 여러 테 넌  
  
-   SLB 및 담그고 구현 직접 서버 반환 (DSR) 하 여 확장 하 고 낮은 대기 반환 경로 지원  
  
-   스위치 Embedded 팀 (설정) 또는 단일 루트 입력/출력 Virtualization (s R IOV)도 사용 하는 경우 SLB 함수  
  
-   SLB 인터넷 프로토콜 버전 4 (IPv4) 지원이 포함 됩니다.  
  
-   SLB은 사이트 게이트웨이 시나리오에 대해 단일 공개 IP 활용에 대 한 모든 사이트에 연결을 사용 하도록 설정 하려면 NAT 기능을 제공  
  
-   전체 호스트 에이전트와 Windows Server 2016 년에 MUX 포함 하 여 SLB 하며 Nano 설치를 설치할 수 있습니다.  
  
**크기가 조정 및 성능**  
  
-   이제 확장 기능을 포함 하 여 클라우드 배율와 MUXes와 호스트 에이전트 기능이를 확대 합니다.  
  
-   활성 네트워크 컨트롤러 SLB 관리자 모듈 8 MUX 인스턴스를 지원할 수 있습니다  
  
**높은 공급 일**  
  
-   SLB/활성 구성에서 2 개 이상의 노드에 배포할 수 있습니다.  
  
-   MUXes 추가 하 고 SLB 서비스 영향을 주지 않고 MUX 풀에서 제거 될 수 있습니다. 이 유지 SLB 가용성 때   
    개별 MUXes 패치 되 고 됩니다.  
  
-   개별 MUX 인스턴스 있는 99% 시간  
  
-   의료 데이터를 모니터링 관리 기관과에 게 제공 됩니다.  
  
**맞춤**  
  
-   배포 및 SLB SCVMM으로 구성할 수 있습니다.  
  
-   SLB은 RAS 넌 게이트웨이, 데이터 센터 방화벽 경로 반사 기 등 Microsoft 기기와 원활 하 게 통합 하 여 넌 통합된 가장자리를 제공 합니다.  
  

