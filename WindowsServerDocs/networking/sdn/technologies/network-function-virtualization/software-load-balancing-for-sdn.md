---
title: SDN에 대한 SLB(소프트웨어 부하 분산)
description: 이 항목을 사용 하 여 Windows Server 2016의 소프트웨어 정의 네트워킹에 대 한 소프트웨어 부하 분산에 대해 알아볼 수 있습니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 97abf182-4725-4026-801c-122db96964ed
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 1e7870e045f9af79ed46ec1ad998dbc1f1474afd
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312908"
---
# <a name="software-load-balancing-slb-for-sdn"></a>SDN에 대 한 소프트웨어 부하 분산 \(SLB\)

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목을 사용 하 여 Windows Server 2016의 소프트웨어 정의 네트워킹에 대 한 소프트웨어 부하 분산에 대해 알아볼 수 있습니다.  

클라우드 서비스 공급자 (Csp) 및 엔터프라이즈 네트워킹 SDN (소프트웨어)에서 Windows Server 2016에 배포 하는 테 넌 트 및 테 넌 트 고객 네트워크 트래픽 가상 네트워크 리소스 간에 고르게 배포할 소프트웨어 부하 분산 (SLB)를 사용할 수 있습니다. Windows Server SLB 높은 가용성과 확장성이 같은 작업을 호스트 하는 여러 서버를 수 있습니다.
  
Windows Server SLB는 다음과 같은 기능이 포함 되어 있습니다.  
  
-   ' 북-남 ' 및 ' 동-서 ' TCP/UDP 트래픽을 위한 4 (L4) 부하 분산 서비스 계층.  
  
-   Public 및 내부 네트워크 트래픽 부하를 분산 합니다.  
  
-   Hyper-v 네트워크 가상화를 사용 하 여 만든 가상 네트워크와 가상 로컬 영역 네트워크 (Vlan)에 동적 IP 주소 (Dip)를 지원 합니다.  
  
-   상태 프로브 지원 합니다.  
  
-   이제 확장 기능을 포함 하 여 클라우드 규모와 멀티플렉서 및 호스트 에이전트에 대 한 기능을 강화 합니다.  
  
자세한 내용은 참조 [소프트웨어 부하 분산 기능](#bkmk_features) 이 여기에 있습니다.  
  
> [!NOTE]  
> 그러나 다중 Vlan 네트워크 컨트롤러에서 지원 하지 않는 대 한, 사용할 수 있습니다 Vlan SLB와 서비스 공급자에 대 한 데이터 센터 인프라 및 고밀도 웹 서버 등의 작업을 관리 합니다.  
  
Windows Server SLB를 사용 하 여 부하 분산 기능을 다른 VM 작업에 사용 되는 동일한 Hyper-v 컴퓨팅 서버에서 SLB Vm을 사용 하 여 확장할 수 있습니다. 이 인해 SLB 신속 하 게 생성 및 CSP 작업에 필요한 부하 분산 엔드포인트의 삭제를 지원 합니다. 또한 Windows Server SLB 수십 기가바이트 클러스터당 지원 간단한 프로 비전 모델을 제공 하며 규모 확장 및 감축 하기 쉽습니다.  
  
**SLB 작동 방법**  
  
데이터 센터에 있는 리소스의 클라우드 서비스 집합의 일부인 동적 IP 주소 (Dip)를 가상 IP 주소 (Vip)에 매핑하여 SLB 작동 합니다.  
  
Vip는 분산 Vm 부하의 풀에 대 한 공용 액세스를 제공 하는 단일 IP 주소입니다. 예를 들어, Vip는 테 넌 트 및 테 넌 트 고객 클라우드 데이터 센터의 테 넌 트 리소스에 연결할 수 있도록 인터넷에 노출 되는 IP 주소입니다.  
  
Dip는 멤버 VIP 뒤 부하 분산 된 풀의 Vm의 IP 주소입니다. Dip는 테 넌 트 리소스를 클라우드 인프라 내에서 할당 됩니다.  
  
Vip에는 SLB 멀티플렉서 (MUX)에 있습니다.  하나 이상의 가상 컴퓨터 (Vm)가 MUX 구성 됩니다.  네트워크 컨트롤러는 각 VIP와 각 MUX 및 각 MUX 사용 하 여 프로토콜 BGP (Border Gateway)를 보급 한/32로 실제 네트워크에서 라우터를 각 VIP 제공 경로입니다.  BGP에 실제 네트워크 라우터를 허용합니다.  
  
-   VIP는 각 MUX에서 사용할 수 있는 경우에는 MUXes 3 계층 네트워크의 서로 다른 서브넷에 알아봅니다.  
  
-   각 VIP에 대 한 로드를 같은 비용 다중 경로 (ECMP) 라우팅을 사용 하 여 모든 사용 가능한 MUXes 분산 합니다.  
  
-   자동으로 MUX 실패 또는 노드 제거를 검색 및 실패 한 MUX로 트래픽 전송을 중지 합니다.  
  
-   정상 MUXes 실패 했거나 제거 MUX에서 로드를 분산 합니다.  
  
인터넷에서 공용 트래픽이 도착 하면, SLB MUX를 대상으로 VIP를 포함 하 고 매핑하는 개별 DIP에 도착 하는 트래픽을 다시 작성 하는 트래픽이 검사 합니다. 인바운드 네트워크 트래픽의 경우이 트랜잭션은 MUX 가상 컴퓨터 (Vm)와 대상 DIP 있는 Hyper-v 호스트 간에 분할 하는 2 단계 프로세스에서 수행 됩니다.  
  
-   부하 분산-MUX 사용 하 여 VIP는 DIP를 선택 하는 패킷을 캡슐화 하 고 DIP 있는 Hyper-v 호스트에는 트래픽을 전달 합니다.  
  
-   네트워크 주소 변환 (NAT)-Hyper-v 호스트는 패킷의 캡슐화를 제거, VIP DIP로 변환, 포트, 다시 매핑합니다 및 DIP VM에 패킷을 전달 합니다.  
  
가 MUX 올바른 Dip를 부하 분산 네트워크 컨트롤러를 사용 하 여 정의 하는 정책 때문에 Vip를 매핑하는 방법을 알고 있습니다. 이러한 규칙에는 프로토콜, 포트 프런트 엔드, 백 엔드 포트 및 배포 알고리즘 (5, 3, 또는 2 튜플) 포함 됩니다.  
  
때 Vm에 응답 하는 테 넌 트 및 송신 아웃 바운드 네트워크 트래픽이을 인터넷 이나 원격 테 넌 트 위치 NAT 트래픽 Hyper-v 호스트에서 수행 되기 때문에 MUX를 무시 하 고 Hyper-v 호스트에서 edge 라우터 직접 이동 됩니다. 이 MUX 바이패스 프로세스에 직접 서버 반환 DSR () 호출 됩니다.  
  
및 인바운드 네트워크 트래픽을 구현이 SLB MUX 초기 네트워크 트래픽 흐름이 설정 되 면 완전히 무시 합니다.  
  
다음 그림에서 클라이언트 컴퓨터는 회사 SharePoint 사이트의 IP 주소에 대 한 DNS 쿼리를 수행 합니다 .이 경우에는 가상 회사인 Contoso가 지정 됩니다. 다음 프로세스가 수행 됩니다.  
  
-   DNS 서버는 클라이언트에 107.105.47.60 VIP를 반환합니다.  
  
-   클라이언트는 VIP에 HTTP 요청을 보냅니다.  
  
-   실제 네트워크에 여러 경로가 모든 MUX에 있는 VIP 도달 하기 위해 사용할 수 있습니다.  그 과정에서 각 라우터는 MUX에 도착 하면 요청 될 때까지 경로의 다음 세그먼트를 선택 하 ECMP를 사용 합니다.  
  
-   요청을 받는 MUX 구성 된 정책을 검사 하 고 두 Dip를 사용할 수 10.10.10.5 및 10.10.20.5, 107.105.47.60 VIP로 요청을 처리 하는 가상 네트워크에 있는지 확인  
  
-   가 MUX DIP 10.10.10.5 선택한 VXLAN 것을 보낼 수 있는 호스트를 사용 하 여 DIP를 포함 하는 호스트 실제 네트워크 주소를 사용 하 여 패킷을 캡슐화 합니다.  
  
-   호스트는 캡슐화 된 패킷을 수신 하 고 검사 합니다.  캡슐화를 제거 하 고 대상 VIP 대신 10.10.10.5 DIP는 이제 고 DIP VM에 트래픽을 보내는 패킷을 다시 작성 합니다.  
  
-   이제 요청이 서버 팜 2의 Contoso SharePoint 사이트에 도달 했습니다. 서버 응답을 생성 하 고 원본으로는 자체 IP 주소를 사용 하 여 클라이언트에 보냅니다.  
  
-   호스트는 클라이언트에서 대상 이제 VIP에 원래 요청을 만든 기억 하는 가상 스위치에서 나가는 패킷을 차단 합니다.  호스트 되도록 VIP DIP 주소가 표시 되지 않는 클라이언트에는 패킷 소스를 다시 작성 합니다.  
  
-   호스트에 직접 표준 라우팅 테이블을 사용 하 여 결국 응답을 수신 하는 클라이언트에 전달 하는 실제 네트워크에 대 한 기본 게이트웨이 패킷을 전달 합니다.  
  
![소프트웨어 부하 분산 프로세스](../../../media/Software-Load-Balancing--SLB--for-SDN/slb_process.jpg)  
  
**내부 데이터 센터 트래픽 부하 분산**  
  
동일한 가상 네트워크의 구성원 인 다른 서버에서 실행 하는 테 넌 트 리소스 간의 Vm 연결 되어 있는 Hyper-v 가상 스위치는 NAT. 수행과 같은 경우 부하 분산 네트워크 트래픽을 데이터 센터의 내부  
  
내부 트래픽 부하 분산 된 첫 번째 요청으로 전송 되 고 적절 한 DIP를 선택 하 고 DIP는 트래픽을 라우팅 MUX에서 처리 합니다. 해당 지점에서 설정 된 트래픽 흐름이 MUX를 무시 하 고 VM VM에서 직접 이동 됩니다.  
  
**상태 프로브**  
  
SLB 다음을 포함 하는 네트워크 인프라의 상태를 확인 하려면 상태 검색이 포함 되어 있습니다.  
  
-   포트에 TCP 프로브  
  
-   HTTP 검색 포트 및 URL을 실행  
  
기존 부하 분산 장치 어플라이언스 프로브 기기에서 시작 하 고 DIP로 네트워크를 통해 이동 있는 달리 SLB 프로브 DIP의 위치를 더욱 호스트 간에 작업을 배포 하 고 DIP SLB 호스트 에이전트에서 직접 이동 하는 호스트에서 시작 됩니다.  
  
## <a name="software-load-balancing-infrastructure"></a><a name="bkmk_infrastructure"></a>소프트웨어 부하 분산 인프라  
Windows Server SLB를 배포 하려면 먼저 Windows Server 2016의 네트워크 컨트롤러와 하나 이상의 SLB MUX Vm를 배포 해야 합니다.  
  
또한 SDN 사용이 가능한 Hyper-v 가상 스위치와 함께 Hyper-v 호스트를 구성 하 고 SLB 호스트 에이전트가 실행 되 고 있는지 확인 해야 합니다.  호스트 역할을 하는 라우터 같은 비용 (ECMP) 다중 경로 라우팅 및 프로토콜 BGP (Border Gateway)를 지원 해야 하 고 SLB MUXes에서 BGP 피어 링 요청을 수락 하도록 구성 되어야 합니다.  
  
다음은 SLB 인프라의 개요입니다.  

![소프트웨어 부하 분산 인프라](../../../media/Software-Load-Balancing--SLB--for-SDN/slb_overview1.png)  
  
다음 섹션에서는 SLB 인프라의 이러한 구성 요소에 대 한 자세한 정보를 제공합니다.  
  
### <a name="scvmm"></a>SCVMM  
System Center 2016에서 Windows Server 2016 년까지 SLB 관리자 및 상태 모니터를 포함 하 여 네트워크 컨트롤러를 구성할 수 있습니다. 또한 SLB MUXs를 배포 하 고 Windows Server 2016 및 Hyper-v를 실행 하는 컴퓨터에서 SLB 호스트 에이전트 설치를 System Center를 사용할 수 있습니다.  
  
System Center 2016에 대 한 자세한 내용은 참조 [System Center 2016](https://www.microsoft.com/server-cloud/products/system-center-2016/)합니다.  
  
> [!NOTE]  
> System Center 2016을 사용 하지 않을 경우 설치 하 고 네트워크 컨트롤러 및 기타 SLB 인프라 구성 Windows PowerShell 또는 다른 관리 애플리케이션을 사용할 수 있습니다. 자세한 내용은 참조 [Windows PowerShell을 사용 하 여 네트워크 컨트롤러 배포](../../../sdn/deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)합니다.  
  
### <a name="network-controller"></a>네트워크 컨트롤러  
네트워크 컨트롤러 SLB 관리자를 호스트 하 고 SLB에 대 한 다음 작업을 수행 합니다.  
  
-   Northbound API를 통해 System Center, Windows PowerShell 또는 다른 네트워크 관리 애플리케이션에서 제공 하는 SLB 명령을 처리 합니다.  
  
-   Hyper-v 호스트 및 SLB MUXes 배포에 대 한 정책을 계산합니다.  
  
-   SLB 인프라의 상태를 제공합니다.  
  
### <a name="slb-mux"></a>SLB MUX  
SLB MUX 인바운드 네트워크 트래픽을 처리 하 고 Dip Vip 매핑됩니다 다음 올바른 DIP로 트래픽을 전달 합니다. 또한 각 MUX edge 라우터를 VIP 경로 게시 하려면 BGP를 사용 합니다. BGP Keep Alive MUXes를 활성 MUXes에 기본적으로 부하 분산 장치에 대 한 부하 분산을 제공 하는 MUX 오류가-발생 한 경우 부하를 재배포할 수 있는 한 MUX 실패 하면 알립니다.  
  
### <a name="hosts-that-are-running-hyper-v"></a>Hyper-v를 실행 하는 호스트  
Windows Server 2016 및 Hyper-v를 실행 하는 컴퓨터와 SLB를 사용할 수 있습니다. Hyper-v 호스트의 Vm Hyper-v에서 지 원하는 모든 운영 체제를 실행할 수 있습니다.  
  
### <a name="slb-host-agent"></a>SLB 호스트 에이전트  
SLB를 배포할 때 모든 Hyper-v 호스트 컴퓨터에 SLB 호스트 에이전트를 배포를 System Center, Windows PowerShell 또는 다른 관리 애플리케이션을 사용 해야 합니다. Hyper-v 지원, Nano 서버를 포함 하 여 제공 하는 모든 버전의 Windows Server 2016에서 SLB 호스트 에이전트를 설치할 수 있습니다.  
  
SLB 호스트 에이전트 SLB 정책 업데이트 네트워크 컨트롤러에서 수신 대기합니다. 또한 호스트 에이전트 프로그램은 규칙 SLB에 대 한 SDN 사용이 가능한 Hyper-v 가상 스위치는 로컬 컴퓨터에 구성 되어 있는에 있습니다.  
  
### <a name="sdn-enabled-hyper-v-virtual-switch"></a>SDN은 Hyper-v 가상 스위치를 사용 하도록 설정  
SLB와 호환 되도록 가상 스위치에 스위치를 만들려면 Hyper-v 가상 스위치 관리자 또는 Windows PowerShell 명령을 사용 해야 하 고 가상 스위치에 대 한 가상 필터링 플랫폼 (VFP)을 사용 해야 합니다.  
  
VFP 가상 스위치에서 사용 하도록 설정에 대 한 내용은 Windows PowerShell 명령 참조 [Get-vmsystemswitchextension](https://technet.microsoft.com/library/hh848603.aspx) 및 [사용 VMSwitchExtension](https://technet.microsoft.com/library/hh848541.aspx?f=255&MSPPError=-2147217396)합니다.  
  
SDN Hyper-v 가상 스위치를 사용 하도록 설정 SLB에 대 한 다음 작업을 수행 합니다.  
  
-   SLB에 대 한 데이터 경로 처리합니다.  
  
-   가 MUX에서 인바운드 네트워크 트래픽을 받습니다.  
  
-   DSR를 사용 하 여 라우터를 보내는 아웃 바운드 네트워크 트래픽의 MUX를 무시 합니다.  
  
-   Hyper-v의 Nano 서버 인스턴스를 실행합니다.  
  
### <a name="bgp-enabled-router"></a>BGP 라우터를 사용 하도록 설정  
BGP 라우터 SLB에 대 한 다음 작업을 수행 합니다.  
  
-   ECMP를 사용 하 여 MUX로의 인바운드 트래픽을 경로입니다.  
  
-   아웃 바운드 네트워크 트래픽에 대 한 호스트에서 제공한 경로 사용 합니다.  
  
-   SLB MUX에서 Vip에 대 한 경로 업데이트를 수신합니다.  
  
-   활성 상태로 유지 실패 하면 SLB MUXes SLB 회전에서 제거 합니다.  
  
## <a name="software-load-balancing-features"></a><a name="bkmk_features"></a>소프트웨어 부하 분산 기능  
다음은 일부의 기능 및 SLB의 기능입니다.  
  
**핵심 기능**  
  
-   SLB 계층 4 부하 분산 ' 북-남 ' 및 ' 동-서 ' TCP/UDP 트래픽을 위한 서비스를 제공 합니다.  
  
-   SLB Hyper-v 네트워크 가상화 기반 네트워크에서 사용할 수 있습니다.  
  
-   SDN 활성화 Hyper-v 가상 스위치에 연결 된 vm의 DIP SLB VLAN 기반 네트워크와 함께 사용할 수 있습니다.  
  
-   하나의 SLB 인스턴스가 여러 테 넌 트를 처리할 수 있습니다.  
  
-   SLB 및 DIP 직접 서버 반환 (DSR)에서 구현 되는 확장 가능 하 고 대기 시간이 짧고 반환 경로 지원  
  
-   스위치가 포함 된 팀 (설정) 또는 단일 루트 입출력 가상화 (SR-IOV)도 사용 하는 경우 SLB 함수  
  
-   인터넷 프로토콜 버전 4 (IPv4)를 포함 하는 SLB 지원  
  
-   사이트 간 게이트웨이 시나리오의 경우 SLB는 모든 사이트 간 연결에서 단일 공용 IP를 활용할 수 있도록 NAT 기능을 제공 합니다.  
  
-   전체 호스트 에이전트 및 Windows Server 2016에서 MUX를 포함 하 여 SLB, 핵심 및 Nano 설치를 설치할 수 있습니다.  
  
**크기 조정 및 성능**  
  
-   이제 확장 기능을 포함 하 여 클라우드 규모와 MUXes 및 호스트 에이전트에 대 한 기능을 강화 합니다.  
  
-   하나의 활성 SLB 관리자 네트워크 컨트롤러 모듈 8 MUX 인스턴스를 지원할 수 있습니다.  
  
**고가용성**  
  
-   활성/비활성 구성의 세 개 이상의 노드로 SLB를 배포할 수 있습니다.  
  
-   MUXes는 추가 하 고 SLB 서비스에 영향을 주지 않고 MUX 풀에서 제거할 수 있습니다. SLB 가용성이 유지 때   
    개별 MUXes가 패치 되 고 있습니다.  
  
-   개별 MUX 인스턴스에 99%의 가동 시간  
  
-   상태 모니터링 데이터를 관리 엔터티를 사용할 수  
  
**할당**  
  
-   배포 하 고 SCVMM과 SLB를 구성할 수 있습니다.  
  
-   SLB은 RAS 테 넌 트 게이트웨이, 데이터 센터 방화벽 경로 Reflector와 같은 Microsoft 어플라이언스와 원활 하 게 통합 하 여 다중 테 넌 트 통합된 가장자리를 제공 합니다.  
  

