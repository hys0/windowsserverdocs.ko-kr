---
title: RAS 게이트웨이 배포 건축물
description: Windows Server 2016을 포함 하 여 풀 RAS 게이트웨이 경로 반영 하 고 개별 테 넌에 대 한 여러 게이트웨이 배포에서 RAS 게이트웨이의 배포 클라우드 CSP (서비스 공급자)에 대 한 자세한 내용은이 항목을 사용할 수 있습니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d46e4e91-ece0-41da-a812-af8ab153edc4
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 21b101e10dba3d3b9578d6804b4fd92fbbcd2167
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="ras-gateway-deployment-architecture"></a>RAS 게이트웨이 배포 건축물

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

풀 RAS 게이트웨이 경로 반영을 포함 하 고 개별 테 넌에 대 한 여러 게이트웨이 배포 RAS 게이트웨이의 배포 클라우드 CSP (서비스 공급자)에 대 한 자세한 내용은이 항목을 사용할 수 있습니다.  
  
다음 섹션 게이트웨이 배포 디자인에서 이러한 기능을 사용 하는 방법을 이해할 수 있도록 간단한 개요 RAS 게이트웨이 새로운 기능 중 일부를 제공 합니다.  
  
또한 배포 예제 제공 새로운 테 넌, 추가 경로 동기화 및 데이터 평면 경로, 게이트웨이 및 경로 반사 기 장애 조치를 더 프로세스에 대 한 정보를 포함 하 여 합니다.  
  
이 항목 다음 섹션에 포함 되어 있습니다.  
  
-   [배포 디자인 RAS 게이트웨이 새로운 기능을 사용 하 여](#bkmk_new)  
  
-   [예 배포](#bkmk_example)  
  
-   [새 테 넌 및 고객 (캐나다) 주소 공간 EBGP 추가 피어 링](#bkmk_tenant)  
  
-   [경로 평면 경로 동기화 및 데이터](#bkmk_route)  
  
-   [네트워크 컨트롤러 RAS 게이트웨이 및 경로 반사 기 장애 조치에 응답 하는 방법](#bkmk_failover)  
  
-   [새로운 RAS 게이트웨이 기능을 사용할 때의 이점](#bkmk_advantages)  
  
## <a name="bkmk_new"></a>배포 디자인 RAS 게이트웨이 새로운 기능을 사용 하 여  
RAS 게이트웨이 변경 하 고 게이트웨이 인프라를 데이터 센터에 배포 하는 방식을 개선 하는 여러 새로운 기능이 포함 되어 있습니다.  
  
### <a name="bgp-route-reflector"></a>BGP 경로 반사 기  
테두리 게이트웨이 프로토콜 (BGP) 경로 반사 기 기능이 이제는 RAS 게이트웨이 함께 제공 하 고 경로 동기화 라우터 사이 대해 일반적으로 필요 BGP 전체 망 토폴로지 하는 대신 제공 합니다. 전체 망 동기화 라우팅 토폴로지에서 다른 모든 라우터에서 모든 BGP 라우터에 연결 해야 합니다. 그러나 반사 기 경로 사용할 때 경로 반사 기는 모든 BGP 경로 반사 기 클라이언트, 경로 동기화 단순화 하 여 및 네트워크 교통 줄이기 라는 다른 라우터에 연결 하는 유일한 라우터. 경로 반사 기 모든 경로 학습 하 고 최상의 경로 계산 BGP 클라이언트에 최상의 경로 재배포 합니다.  
  
자세한 내용은 참조 [RAS 게이트웨이의 새로운](../../../sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md)합니다.  
  
### <a name="bkmk_pools"></a>게이트웨이 풀  
Windows Server 2016 다른 종류의 많은 게이트웨이 풀 만들 수 있습니다. 게이트웨이 풀 RAS 게이트웨이의 대부분의 경우 포함 하며 사이의 물리적 및 가상 네트워크 네트워크 트래픽을 라우팅하기 합니다.  
  
자세한 내용은 참조 [RAS 게이트웨이의 새로운](../../../sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md) 및 [RAS 게이트웨이 높은 가용성](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md)합니다.  
  
### <a name="bkmk_gps"></a>게이트웨이 풀 확장성  
조정할 수 있습니다 쉽게 게이트웨이 풀을 위나 아래로 추가 하거나 게이트웨이 Vm 풀에서 제거 하 여. 게이트웨이 추가 하거나 제거 풀에서 제공 되는 서비스를 방해 하지 않습니다. 추가 하 고 게이트웨이의 전체 풀 제거 수도 있습니다.  
  
자세한 내용은 참조 [RAS 게이트웨이의 새로운](../../../sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md) 및 [RAS 게이트웨이 높은 가용성](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md)합니다.  
  
### <a name="bkmk_m"></a>게이트웨이 풀 중복 M + N  
모든 게이트웨이 풀 M + N 중복 됩니다. 즉,는 보려고 ' 활성 게이트웨이 Vm 수 대기 게이트웨이 vm'n ' 번호로 백업 됩니다. M + N 중복 안정성 RAS 게이트웨이 배포 하는 경우 필요한 수준을 결정할에 더 많은 유연성 제공 합니다.  
  
자세한 내용은 참조 [RAS 게이트웨이의 새로운](../../../sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md) 및 [RAS 게이트웨이 높은 가용성](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md)합니다.  
  
## <a name="bkmk_example"></a>예 배포  
다음 그림 eBGP 피어 두 테 넌, Contoso 및 Woodgrove, Fabrikam CSP datacenter 간에 구성 사이트에서 VPN 연결을 통해 링 예를 제공 합니다.  
  
![사이트에서 VPN 통해 피어 링 eBGP](../../../media/RAS-Gateway-Deployment-Architecture/ras_gateway_architecture.png)  
  
이 예 Contoso 게이트웨이 infrastructure 디자인 결정 종료 GW2 대신 GW3에 Contoso 르 지역이 사이트를 추가 게이트웨이의 대역폭을 필요 합니다. 이 때문 서로 다른 사이트에서 Contoso VPN 연결에 두 가지 게이트웨이 CSP 데이터 센터에 종료 됩니다.  
  
두 가지 GW2 및 GW3, 이러한 게이트웨이 CSP Contoso 및 Woodgrove 테 넌 인프라에 추가 하는 경우 네트워크 컨트롤러에서 구성 된 첫 번째 RAS 게이트웨이 했습니다. 이 인해 이러한 해당 고객 (또는 테 넌)에 대 한 이러한 두 가지 게이트웨이 경로 반영으로 구성 됩니다. GW2 Contoso 경로 반사 기 이며 GW3-CSP RAS 게이트웨이 종료 지점을 Contoso 르 지역이 HQ 사이트와 VPN 연결에 대 한 될 뿐만 아니라 Woodgrove 경로 반사 기 합니다.  
  
> [!NOTE]  
> 하나 RAS 게이트웨이 각 테 대역폭 요구 사항에 따라 한 백 최대 다른 소유에 대 한 가상 및 실제 네트워크 교통을 경로 설정할 수 있습니다.  
  
경로 반영으로 GW2 Contoso 캘리포니아 공간 경로 네트워크 컨트롤러, 보내고 GW3 Woodgrove 캘리포니아 공간 경로 네트워크 컨트롤러를 보냅니다.  
  
네트워크 컨트롤러 밀어 부하 분산 정책을 소프트웨어 부하 분산 풀으로 구성 된 Multiplexers (MUXes) 하 고 RAS 게이트웨이 RAS 정책을 뿐만 아니라 Contoso 및 Woodgrove 가상 네트워크 Hyper-v 네트워크 가상화 정책을 넣습니다.  
  
## <a name="bkmk_tenant"></a>새 테 넌 및 고객 주소 (캐나다) 공간 eBGP 추가 Peering  
새 고객 서명 하 고 새 거주 고객 데이터 센터에 추가 하는 경우 네트워크 컨트롤러 및 RAS 게이트웨이 eBGP 라우터에서 자동으로 수행 됩니다는 많은 다음 프로세스를 사용할 수 있습니다.  
  
1.  테의 요구 사항에 따라 작업 하 고 새 가상 네트워크 프로 비전 됩니다.  
  
2.  필요한 경우 데이터 센터에 원격 원격 테 엔터프라이즈 사이트와 가상 네트워크 연결이 구성 됩니다. 사이트에서 VPN 연결은 테에 대 한 배포 하는 경우 네트워크 컨트롤러 자동으로 사용할 수 있는 게이트웨이 풀의 사용 가능한 RAS 게이트웨이 VM 선택 하 고 구성 연결 합니다.  
  
3.  또한 새로운 테에 대 한 RAS 게이트웨이 VM를 구성 하는 동안 네트워크 컨트롤러는 BGP 라우터 RAS 게이트웨이 구성 하 고는 테에 대 한 경로 반사 기도 지정 합니다. 이 RAS 게이트웨이 다른 테 넌에 대 한 게이트웨이로 또는 게이트웨이 및 경로 반사 기를 사용 있는 경우에도 적용 합니다.  
  
4.  캘리포니아 공간 경로 구성 되어 있는지 구성 된 고정 사용할 네트워크 또는 동적 BGP 경로 따라 네트워크 컨트롤러와 RAS 게이트웨이 VM 경로 반사 기에 해당 고정 경로 이나 BGP 이웃 구성 합니다.  
  
    > [!NOTE]  
    > -   네트워크 컨트롤러에 구성 요소 RAS 게이트웨이 및 경로 반사 기 테에 대 한 같은 테 네트워크 컨트롤러가 RAS 게이트웨이 VM에서 사용 가능한 용량 확인 새 사이트에 VPN 연결을 필요할 때마다 합니다. 새 네트워크 연결 원래 게이트웨이 필요한 용량을 처리할 수, 동일한 RAS 게이트웨이 VM에서 구성 수도 있습니다. RAS 게이트웨이 VM 추가 용량을 처리할 수 없는 경우 네트워크 컨트롤러 사용할 수 있는 새로운 RAS 게이트웨이 VM 선택 하 고에 새 연결을 구성 합니다. 테와 관련 된 새로운 RAS 게이트웨이 VM이 경로 반사 기 클라이언트의 원래 테 RAS 게이트웨이 경로 반사 기 됩니다.  
    > -   RAS 게이트웨이 풀 하시 부하 분산 소프트웨어가 (SLBs) 뒤, 하기 때문에 테 넌의 사이트에서 VPN 해결 각 사용 단일 공개 IP 주소, 가상 IP 주소를 (VIP)는 엔터프라이즈 테에 대 한 교통량을 경로 RAS 게이트웨이 동적 IP 주소 (담그고) 라고 datacenter 내부 IP 주소를 번역할는 SLBs 하 여 이라고 합니다. 이 공개-IP 주소 매핑 SLB 하 여 사이트에서 VPN 터널 CSP RAS 게이트웨이 엔터프라이즈 사이트 및 경로 반영 간에 올바르게 설정 되어 있는지 확인 합니다.  
    >   
    >     SLB, Vip, Dip에 대 한 자세한 내용은 참조 [부하 분산 소프트웨어가 & #40; SLB & #41; SDN에 대 한](../../../sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md)합니다.  
  
5.  엔터프라이즈 사이트와 RAS 게이트웨이 새 테에 대 한 설정 CSP datacenter 간에 사이트에서 VPN 터널 후 고정 경로 터널와 관련 된은 자동으로 터널의 Enterprise 및 CSP 측면에 구축 됩니다.  
  
6.  캘리포니아 공간이 BGP 경로, Enterprise 사이트와 CSP RAS 게이트웨이 경로 반사 기 간에 피어 링 eBGP도 설정 합니다.  
  
## <a name="bkmk_route"></a>경로 평면 경로 동기화 및 데이터  
엔터프라이즈 사이트와 CSP RAS 게이트웨이 경로 반사 기 간에 eBGP 피어 링 설정 된 후 경로 반사 기 동적 BGP 경로 사용 하 여 모든 엔터프라이즈 경로 학습 합니다. 경로 반사 기 하는 모두 동일한 경로 집합으로 구성 이러한 경로 모든 경로 반사 기 클라이언트 간에 동기화 합니다.  
  
또한 경로 반사 기 경로 동기화 네트워크 컨트롤러를 사용 하 여 이러한 통합된 경로 업데이트 합니다. 네트워크 컨트롤러 경로 Hyper-v 네트워크 가상화 정책으로 변환 그리고 구성 패브릭 네트워크 End-to-End 경로 데이터 연결가 구성 되어 있는지 확인 합니다. 이 프로세스는 테에서는 가상 네트워크 테 기업에서에서 액세스할 수 있는 사이트 합니다.  
  
경로 데이터 평면 설정에 대 한는 RAS 게이트웨이 Vm에 도달 하는 바로 패킷이 테의 가상 네트워크에 필요한 경로 지금 참여 RAS 게이트웨이 Vm의 모든 함께 사용할 수 있으므로 합니다.  
  
마찬가지로, 장소에 Hyper-v 네트워크 가상화 정책을 사용 하 여 테 가상 네트워크 경로 패킷을 (않고도 경로 반사 기에 대해 알아야 할) RAS 게이트웨이 Vm 직접으로 이동한 다음 엔터프라이즈 사이트에 사이트에서 VPN 터널 통해 합니다.  
  
또한. 원격 테 엔터프라이즈 사이트로 테 가상 네트워크에서 반환 교통 직접 서버 반환 (DSR) 이라는 프로세스 SLBs 무시 합니다.  
  
## <a name="bkmk_failover"></a>네트워크 컨트롤러 RAS 게이트웨이 및 경로 반사 기 장애 조치에 응답 하는 방법  
다음 두 가지 가능한 장애 시나리오가-게이트웨이 경로 반사 기 RAS 클라이언트에 대 한-및 RAS 게이트웨이 경로 반영 네트워크 컨트롤러 처리 하는 방법을 장애 조치 Vm에 대 한 구성에 대 한 정보를 포함 합니다.  
  
### <a name="vm-failure-of-a-ras-gateway-bgp-route-reflector-client"></a>게이트웨이 BGP 경로 반사 기 RAS 클라이언트의 VM 실패  
네트워크 컨트롤러 게이트웨이 경로 반사 기 RAS 클라이언트 실패 하면 다음과 같은 작업을 수행 합니다.  
  
> [!NOTE]  
> RAS 게이트웨이 테의 BGP 인프라에 대해 경로 반사 기 충전 되지 않은 경우 경로 반사 기 클라이언트는 테 BGP 인프라에 있습니다.  
  
-   네트워크 컨트롤러 사용 가능한 대기 RAS 게이트웨이 VM 선택 하 고 새 RAS 게이트웨이 VM 실패 RAS 게이트웨이 VM 구성으로 제공 됩니다.  
  
-   네트워크 컨트롤러 새로운 RAS 게이트웨이 실패 RAS 게이트웨이의 테 사이트에서 사이트에서 VPN 터널 올바르게 설정 되어 있는지 확인 하려면 해당 SLB 구성을 업데이트 합니다.  
  
-   네트워크 컨트롤러 새 게이트웨이의 BGP 경로 반사 기 클라이언트를 구성합니다.  
  
-   네트워크 컨트롤러 활성 상태로 새 게이트웨이 BGP 경로 반사 기 RAS 클라이언트를 구성합니다. RAS 게이트웨이 테의 경로 반사 기 라우팅 정보를 공유 하 고 해당 하는 엔터프라이즈 사이트에 대 한 eBGP 피어 링을 사용 하도록 설정 된 피어 링 바로 시작 됩니다.  
  
### <a name="vm-failure-for-a-ras-gateway-bgp-route-reflector"></a>RAS 게이트웨이 BGP 경로 반사 기에 대 한 VM 실패  
네트워크 컨트롤러 RAS 게이트웨이 BGP 경로 반사 기 실패 하면 다음과 같은 작업을 수행 합니다.  
  
-   네트워크 컨트롤러 사용 가능한 대기 RAS 게이트웨이 VM 선택 하 고 새 RAS 게이트웨이 VM 실패 RAS 게이트웨이 VM 구성으로 제공 됩니다.  
  
-   네트워크 컨트롤러 새로운 RAS 게이트웨이 VM에서 경로 반사 기 구성 하 고 새 VM 실패 VM VM 오류 불구 하 고 무결성 경로 제공 하 여 사용한 동일한 IP 주소를 지정 합니다.  
  
-   네트워크 컨트롤러 새로운 RAS 게이트웨이 실패 RAS 게이트웨이의 테 사이트에서 사이트에서 VPN 터널 올바르게 설정 되어 있는지 확인 하려면 해당 SLB 구성을 업데이트 합니다.  
  
-   네트워크 컨트롤러 새로운 RAS 게이트웨이 BGP 경로 반사 기 VM 활성으로 구성 됩니다.  
  
-   즉시 경로 반사 기 활성 상태가 됩니다. 사이트에서 VPN 터널 엔터프라이즈를 설정 하 고 경로 반사 기 eBGP 피어 링을 사용 하는 엔터프라이즈 사이트 라우터 경로 교환.  
  
-   BGP 경로 선택한 후 RAS 게이트웨이 BGP 경로 반사 기 업데이트, 데이터 센터에 경로 반사 기 클라이언트 테 넌 트 및 경로 End-to-End 데이터 경로 테 교통을 사용할 수 있게 네트워크 컨트롤러와 동기화 합니다.  
  
## <a name="bkmk_advantages"></a>새로운 RAS 게이트웨이 기능을 사용할 때의 이점  
장점 RAS 게이트웨이 배포 디자인할 때 RAS 게이트웨이 이러한 새로운 기능을 사용 하는 중 몇 가지는 다음과가 같습니다.  
  
**RAS 게이트웨이 확장성**  
  
많은 RAS 게이트웨이 Vm RAS 게이트웨이 풀을 필요한 만큼를 추가할 수 있으므로 성능과 용량을 최적화 하 여 RAS 게이트웨이 배포 쉽게 조정할 수 있습니다. Vm 풀에 추가 하면 사이트에서 VPN 연결 (IKEv2, l 3, GRE), 어떤 종류의 제거 용량 병목 중단 없이 이러한 RAS 게이트웨이 구성할 수 있습니다.  
  
**간소화 된 엔터프라이즈 사이트 게이트웨이 관리**  
  
사용자 테 여러 엔터프라이즈 사이트에 있는 경우 원격 사이트에서 VPN IP 주소를 사용 하 여 모든 사이트 및 단일 원격 이웃 IP 주소-CSP 센터 RAS 게이트웨이 BGP 경로 반사 기 VIP 해당 테에 대 한는 테 구성할 수 있습니다. 그러면 사용자 테 넌에 대 한 게이트웨이 관리를 간단해 집니다.  
  
**게이트웨이가 장애 패스트 개선**  
  
빠른 장애 응답을 위해, edge 경로 및 제어 라우터 10 초 이하의 등 짧은 시간 간격으로 사이의 BGP Keepalive 매개 시간을 구성할 수 있습니다. 이 짧은 유지 연결 간격으로 RAS 게이트웨이 BGP 지 라우터 실패 하면 신속 하 게 감지 하 고 네트워크 컨트롤러 이전 섹션에 나와 있는 단계를 따릅니다. 이 이용 양방향 전달 감지 (BFD) 프로토콜 등 하는 별도 오류 감지 프로토콜에 대 한 필요성을 줄일 수 있습니다.  
  
 
  


