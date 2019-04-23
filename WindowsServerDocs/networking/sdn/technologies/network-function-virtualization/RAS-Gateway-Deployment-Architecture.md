---
title: RAS 게이트웨이 배포 아키텍처
description: RAS 게이트웨이 풀 RAS 게이트웨이 경로 반영자를 포함 하 여 개별 테 넌 트에 대 한 여러 게이트웨이 배포 및 Windows Server 2016에서 클라우드 서비스 공급자 (CSP) 배포에 대해 자세히 알아보려면이 항목에서는 사용할 수 있습니다.
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
ms.openlocfilehash: a3895e25a2af0437deb9eebe4ad89b110cfc9f2b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870274"
---
# <a name="ras-gateway-deployment-architecture"></a>RAS 게이트웨이 배포 아키텍처

>적용 대상: Windows Server (반기 채널), Windows Server 2016

RAS 게이트웨이 풀 RAS 게이트웨이 경로 반영자를 포함 하 고 개별 테 넌 트에 대 한 여러 게이트웨이 배포의 클라우드 서비스 공급자 (CSP) 배포에 대해 자세히 알아보려면이 항목에서는 사용할 수 있습니다.  
  
다음 섹션에서는 게이트웨이 배포의 디자인에서 이러한 기능을 사용 하는 방법을 이해할 수 있도록 RAS 게이트웨이의 새로운 기능 중 일부에 대 한 간략 한 개요를 제공 합니다.  
  
또한 서버 인증서 배포 예제는 제공 새 테 넌 트, 경로 동기화 및 데이터 평면 라우팅, 게이트웨이 및 경로 Reflector 장애 조치 등을 추가 하는 프로세스에 대 한 정보를 포함 하 여.  
  
이 항목에는 다음 섹션이 수록되어 있습니다.  
  
-   [RAS 게이트웨이의 새로운 기능을 사용 하 여 배포를 디자인 하려면](#bkmk_new)  
  
-   [예제 배포](#bkmk_example)  
  
-   [새 테 넌 트 및 고객 주소 (CA) 공간 EBGP 추가 피어 링](#bkmk_tenant)  
  
-   [경로 동기화 및 데이터 평면 라우팅](#bkmk_route)  
  
-   [RAS 게이트웨이 경로 Reflector 장애 조치를 네트워크 컨트롤러 응답 하는 방법](#bkmk_failover)  
  
-   [새 RAS 게이트웨이 기능을 사용할 때의 장점](#bkmk_advantages)  
  
## <a name="bkmk_new"></a>RAS 게이트웨이의 새로운 기능을 사용 하 여 배포를 디자인 하려면  
RAS 게이트웨이 변경 하 고 게이트웨이 인프라를 데이터 센터에 배포 하는 방식을 개선 하는 여러 새 기능을 포함 합니다.  
  
### <a name="bgp-route-reflector"></a>BGP 경로 Reflector  
프로토콜 BGP (경계 게이트웨이) 경로 Reflector 기능은 이제 RAS 게이트웨이와 포함 되어 있으며 대안을 일반적으로 라우터 간의 경로 동기화에 필요한 BGP 풀 메시 토폴로지를 제공 합니다. 풀 메시 동기화를 수행 하면 모든 BGP 라우터 라우팅 토폴로지에 있는 다른 모든 라우터 연결 해야 합니다. 그러나 경로 Reflector를 사용 하면 경로 Reflector는 연결 된 모든 다른 라우터에, BGP 경로 Reflector 클라이언트, 따라서 간소화 경로 동기화 및 네트워크 트래픽 감소를 호출 하는 유일한 라우터. 경로 Reflector 모든 경로 학습 최상의 경로 계산 하 고 최상의 경로 BGP 클라이언트를 다시 배포 합니다.  
  
자세한 내용은 [RAS 게이트웨이의 새로운](../../../sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md)합니다.  
  
### <a name="bkmk_pools"></a>게이트웨이 풀  
Windows Server 2016에서 서로 다른 형식의 여러 게이트웨이 풀을 만들 수 있습니다. 게이트웨이 풀 RAS 게이트웨이의 여러 인스턴스를 포함 하 고 실제 및 가상 네트워크 간에 네트워크 트래픽을 라우팅합니다.  
  
자세한 내용은 [RAS 게이트웨이의 새로운 기능](../../../sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md) 하 고 [RAS 게이트웨이 고가용성](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md)합니다.  
  
### <a name="bkmk_gps"></a>게이트웨이 풀 확장성  
쉽게 확장할 수 있습니다 게이트웨이 풀 위로 또는 아래로 추가 하거나 풀에서 게이트웨이 Vm을 제거 합니다. 게이트웨이 추가 또는 제거는 풀에서 제공 되는 서비스를 방해 하지 않도록 합니다. 또한 추가 및 게이트웨이 전체 풀을 제거할 수 있습니다.  
  
자세한 내용은 [RAS 게이트웨이의 새로운 기능](../../../sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md) 하 고 [RAS 게이트웨이 고가용성](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md)합니다.  
  
### <a name="bkmk_m"></a>M + N 게이트웨이 풀 중복성  
모든 게이트웨이 풀은 M + N 중복입니다. 즉는 여기 ' 활성 게이트웨이 Vm 수는 ' n ' 수가 대기 게이트웨이 Vm으로 백업 합니다. M + N 중복 RAS 게이트웨이 배포할 때 필요한 안정성 수준을 결정 하는 데 더 많은 융통성을 제공 합니다.  
  
자세한 내용은 [RAS 게이트웨이의 새로운 기능](../../../sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md) 하 고 [RAS 게이트웨이 고가용성](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md)합니다.  
  
## <a name="bkmk_example"></a>예제 배포  
다음 그림에서는 eBGP 두 테 넌 트, Contoso 및 Woodgrove Fabrikam CSP 데이터 센터 간에 구성 하는 사이트 간 VPN 연결을 통해 피어 링을 사용 하 여 예제를 제공 합니다.  
  
![사이트 간 VPN을 통해 피어 링 eBGP](../../../media/RAS-Gateway-Deployment-Architecture/ras_gateway_architecture.png)  
  
이 예에서 Contoso GW2 대신 GW3에서 Contoso Los Angeles 사이트를 종료 하는 게이트웨이 인프라 디자인 결정을 앞에 추가 게이트웨이 대역폭에 필요 합니다. 이 때문에 다른 사이트에서 Contoso VPN 연결에서 두 개의 다른 게이트웨이 CSP 데이터 센터에서 종료합니다.  
  
GW2 및 GW3, 이러한 게이트웨이의 두 개는 첫 번째 RAS 게이트웨이 CSP는 인프라에 Contoso 및 Woodgrove 테 넌 트를 추가 하는 경우 네트워크 컨트롤러에서 구성 합니다. 이 인해 이러한 해당 고객 (또는 테 넌 트)에 대 한 이러한 두 게이트웨이 경로 반영자도 구성 됩니다. GW2 Contoso 경로 Reflector 이며 GW3 Contoso Los Angeles HQ 사이트를 사용 하 여 VPN 연결을 위해 CSP RAS 게이트웨이 종료가 되는 것 외에도 Woodgrove 경로 Reflector-합니다.  
  
> [!NOTE]  
> 하나의 RAS 게이트웨이 하나 백 다른 테 넌 트 각 테 넌 트의 대역폭 요구 사항에 따라 가상 및 실제 네트워크 트래픽을 라우팅할 수 있습니다.  
  
경로 반영자도 GW2 Contoso CA 공간 경로를 네트워크 컨트롤러를 보내고 GW3 Woodgrove CA 공간 경로 네트워크 컨트롤러에 보냅니다.  
  
네트워크 컨트롤러는 Hyper-v 네트워크 가상화 정책을 Contoso 및 Woodgrove 가상 네트워크 뿐만 아니라 RAS 게이트웨이 및 부하 분산 구성 된 소프트웨어 부하 분산 멀티플렉서 (Mux) 하는 정책을 RAS 정책을 푸시합니다 풀입니다.  
  
## <a name="bkmk_tenant"></a>새 테 넌 트 및 CA (고객 주소) 공간 eBGP 추가 피어 링  
새 고객이 로그인 하 고 새 테 넌 트 데이터 센터에서 고객을 추가 하는 경우 네트워크 컨트롤러 및 RAS 게이트웨이 eBGP 라우터에 의해 자동으로 수행 됩니다는 많은 다음 프로세스를 사용할 수 있습니다.  
  
1.  새 가상 네트워크 및 테 넌 트의 요구 사항에 따라 워크 로드를 프로 비전 합니다.  
  
2.  필요한 경우 데이터 센터에서 원격 테 넌 트 엔터프라이즈 사이트와 해당 가상 네트워크 간의 원격 연결을 구성 합니다. 테 넌 트 사이트 간 VPN 연결을 배포할 때 네트워크 컨트롤러 자동으로 사용 가능한 게이트웨이 풀에서 사용할 수 있는 RAS 게이트웨이 VM을 선택 하 고 연결을 구성 합니다.  
  
3.  또한 새 테 넌 트 RAS 게이트웨이 VM을 구성 하는 동안 네트워크 컨트롤러는 RAS 게이트웨이 BGP 라우터를 구성 하 고 테 넌 트에 대 한 경로 Reflector로 지정 합니다. 이 RAS 게이트웨이 사용 되는 게이트웨이 또는 게이트웨이 및 경로 Reflector를 다른 테 넌 트에 대 한 상황에도 적용 합니다.  
  
4.  네트워크 컨트롤러에는 CA 공간 라우팅 구성 되어 있는지 여부를 사용 하 여 정적으로 구성 된 네트워크 또는 BGP 동적 라우팅에 따라 해당 고정 경로, BGP 인접 또는 경로 Reflector RAS 게이트웨이 VM에 둘 다 구성 합니다.  
  
    > [!NOTE]  
    > -   네트워크 컨트롤러를 RAS 게이트웨이 경로 Reflector는 테 넌 트에 대 한에서 구성한 후 될 때마다 동일한 테 넌 트에 필요 새 사이트 간 VPN 연결을이 RAS 게이트웨이 VM에서 사용 가능한 용량에 대 한 네트워크 컨트롤러를 확인 합니다. 원래 게이트웨이 필요한 용량을 처리할 수, 하는 경우 새 네트워크 연결이 동일한 RAS 게이트웨이 VM에도 구성 됩니다. RAS 게이트웨이 VM 추가 용량을 처리할 수 없는 경우 네트워크 컨트롤러 새 사용 가능한 RAS 게이트웨이 VM을 선택 하 고에 새 연결을 구성 합니다. 테 넌 트와 연결 된 새 RAS 게이트웨이 VM이 원래 테 넌 트 RAS 게이트웨이 경로 Reflector 경로 Reflector 클라이언트 됩니다.  
    > -   단일 공용 IP 주소를 가상 IP 주소 (VIP)는 SLBs 하 여 데이터 센터 내부 IP 주소를로 변환 됩니다는 호출을 사용 하 여 각 테 넌 트의 사이트 간 VPN 주소 라는 RAS 게이트웨이 풀 소프트웨어 부하 분산 장치 (SLBs) 뒤 이기 때문에 동적 IP 주소 (DIP)는 엔터프라이즈 테 넌 트에 대 한 트래픽을 라우팅하는 RAS 게이트웨이에 대 한 합니다. 이 공개-개인 IP 주소 매핑을 SLB 하 여 엔터프라이즈 사이트가 CSP RAS 게이트웨이 및 경로 반영자 간의 사이트 간 VPN 터널을 올바르게 설정 되어 있는지 확인 합니다.  
    >   
    >     SLB, Vip 및 Dip에 대 한 자세한 내용은 참조 하세요. [소프트웨어 부하 분산 &#40;SLB&#41; SDN에 대 한](../../../sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md)합니다.  
  
5.  엔터프라이즈 사이트와 새 테 넌 트 RAS 게이트웨이 설정 되는 CSP 데이터 센터 간의 사이트 간 VPN 터널을 후 터널을 사용 하 여 연결 된 고정 경로 자동으로 프로 비전 터널의 양쪽 모두 엔터프라이즈 및 CSP .  
  
6.  CA 공간 BGP 사용 하 여 라우팅, 엔터프라이즈 사이트 및 CSP RAS 게이트웨이 경로 Reflector 간에 피어 링 eBGP은도 설정 됩니다.  
  
## <a name="bkmk_route"></a>경로 동기화 및 데이터 평면 라우팅  
엔터프라이즈 사이트와 CSP RAS 게이트웨이 경로 Reflector 간에 eBGP 피어 링을 설정 하면 경로 Reflector 동적 BGP 라우팅을 사용 하 여 모든 엔터프라이즈 경로 알아냅니다. 모두 동일한 경로 집합으로 구성 되도록 경로 Reflector 모든 경로 Reflector 클라이언트 간의 이러한 경로 동기화 합니다.  
  
또한 경로 Reflector를 네트워크 컨트롤러의 경로 동기화를 사용 하 여 이러한 통합된 경로 업데이트 합니다. 그런 다음 네트워크 컨트롤러는 Hyper-v 네트워크 가상화 정책을 경로 변환 하 고 종단 간 데이터 경로 라우팅 프로 비전 되었는지 확인 하려면 패브릭 네트워크를 구성 합니다. 이 프로세스에서는 테 넌 트 엔터프라이즈 테 넌 트에서 액세스할 수 있는 가상 네트워크 사이트.  
  
데이터 평면 라우팅에 대 한 RAS 게이트웨이 Vm에 도달 하는 패킷은 직접 라우팅됩니다 테 넌 트의 가상 네트워크에 필요한 경로 이제 모든 참여 하는 RAS 게이트웨이 Vm을 사용 하 여 사용할 수 있으므로.  
  
마찬가지로, 현재 위치에서 Hyper-v 네트워크 가상화 정책을 사용 하 여 테 넌 트 가상 네트워크 패킷을 라우팅합니다 (경로 Reflector 알아야 요구) 하지 않고 RAS 게이트웨이 Vm으로 직접 다음 엔터프라이즈 사이트에 사이트 간 VPN 터널을 통해 .  
  
또한. 원격 테 넌 트 엔터프라이즈 사이트는 테 넌 트 가상 네트워크에서 반환 트래픽을 SLBs, 직접 서버 반환 (DSR) 이라는 프로세스를 무시 합니다.  
  
## <a name="bkmk_failover"></a>RAS 게이트웨이 경로 Reflector 장애 조치를 네트워크 컨트롤러 응답 하는 방법  
다음은 두 가지 가능한 장애 조치 시나리오-RAS 게이트웨이 경로 Reflector 클라이언트에 대 한-및 RAS 게이트웨이 경로 반영자 처리 하는 방법을 네트워크 컨트롤러 장애 조치 Vm에 대 한 어떤 구성을 사용 하는 방법에 대 한 정보를 포함 합니다.  
  
### <a name="vm-failure-of-a-ras-gateway-bgp-route-reflector-client"></a>RAS 게이트웨이 BGP 경로 Reflector 클라이언트 VM 실패  
네트워크 컨트롤러 RAS 게이트웨이 경로 Reflector 클라이언트 하지 못하면 다음 작업을 수행 합니다.  
  
> [!NOTE]  
> RAS 게이트웨이 경로 Reflector는 테 넌 트의 BGP 인프라 없는 경우 테 넌 트의 BGP 인프라에서 경로 Reflector 클라이언트입니다.  
  
-   네트워크 컨트롤러는 사용 가능한 대기 RAS 게이트웨이 VM을 선택 하 고 실패 한 RAS 게이트웨이 VM의 구성 사용 하 여 새 RAS 게이트웨이 VM을 프로 비전 합니다.  
  
-   네트워크 컨트롤러 새 RAS 게이트웨이 사용 하 여 실패 한 RAS 게이트웨이를 테 넌 트 사이트에서 사이트 간 VPN 터널을 올바르게 설정 되어 있는지 확인 하는 해당 SLB 구성을 업데이트 합니다.  
  
-   네트워크 컨트롤러는 새 게이트웨이에서 BGP 경로 Reflector 클라이언트를 구성합니다.  
  
-   네트워크 컨트롤러는 활성으로 새 RAS 게이트웨이 BGP 경로 Reflector 클라이언트를 구성합니다. RAS 게이트웨이 라우팅 정보를 공유 하 고 해당 엔터프라이즈 사이트 eBGP 피어 링을 사용 하도록 테 넌 트의 경로 Reflector를 사용 하 여 피어 링을 즉시 시작 합니다.  
  
### <a name="vm-failure-for-a-ras-gateway-bgp-route-reflector"></a>RAS 게이트웨이 BGP 경로 Reflector VM 오류  
네트워크 컨트롤러 RAS 게이트웨이 BGP 경로 Reflector 하지 못하면 다음 작업을 수행 합니다.  
  
-   네트워크 컨트롤러는 사용 가능한 대기 RAS 게이트웨이 VM을 선택 하 고 실패 한 RAS 게이트웨이 VM의 구성 사용 하 여 새 RAS 게이트웨이 VM을 프로 비전 합니다.  
  
-   네트워크 컨트롤러는 새 RAS 게이트웨이 VM에서 경로 Reflector를 구성 하 고 새 VM을 VM 실패 해도 경로 무결성을 제공 하므로 실패 한 VM에서 사용한 동일한 IP 주소를 할당 합니다.  
  
-   네트워크 컨트롤러 새 RAS 게이트웨이 사용 하 여 실패 한 RAS 게이트웨이를 테 넌 트 사이트에서 사이트 간 VPN 터널을 올바르게 설정 되어 있는지 확인 하는 해당 SLB 구성을 업데이트 합니다.  
  
-   네트워크 컨트롤러는 활성으로 새 RAS 게이트웨이 BGP 경로 Reflector VM을 구성합니다.  
  
-   경로 Reflector는 즉시 활성화 됩니다. 엔터프라이즈 사이트 간 VPN 터널이 설정 되 고 경로 Reflector eBGP 피어 링을 사용 하 여 엔터프라이즈 사이트 라우터를 사용 하 여 경로 교환 합니다.  
  
-   BGP 경로 선택 후 RAS 게이트웨이 BGP 경로 Reflector 업데이트 경로 Reflector 클라이언트 데이터 센터에서 테 넌 트 및 테 넌 트 트래픽에 대 한 종단 간 데이터 경로 사용 가능 하 고 네트워크 컨트롤러를 사용 하 여 경로 동기화 합니다.  
  
## <a name="bkmk_advantages"></a>새 RAS 게이트웨이 기능을 사용할 때의 장점  
다음은 RAS 게이트웨이 배포를 디자인할 때 이러한 새 RAS 게이트웨이 기능을 사용 하 여의 장점 중 일부입니다.  
  
**RAS 게이트웨이 확장성**  
  
RAS 게이트웨이 풀에 필요한 만큼 많은 RAS 게이트웨이 Vm을 추가할 수 있으므로 성능 및 용량을 최적화 하기 위해 RAS 게이트웨이 배포를 쉽게 확장할 수 있습니다. 풀에 Vm을 추가 하면 사이트 간 VPN 연결 (IKEv2 L3, GRE), 모든 종류의 중단 시간 없이 사용 하 여 제거 용량 병목 상태를 사용 하 여 이러한 RAS 게이트웨이 구성할 수 있습니다.  
  
**간소화 된 엔터프라이즈 사이트 게이트웨이 관리**  
  
테 넌 트 다중 엔터프라이즈 사이트에 있는 경우 테 넌 트 원격 사이트 간 VPN IP 주소를 사용 하 여 모든 사이트 및 해당 테 넌 트에 대 한 CSP 데이터 센터 RAS 게이트웨이 BGP 경로 Reflector VIP-단일 원격 인접 IP 주소를 구성할 수 있습니다. 이 테 넌 트에 대 한 게이트웨이 관리를 간소화 합니다.  
  
**게이트웨이 오류의 빠른 수정**  
  
신속한 장애 조치 응답을 보장 하려면 edge 경로 짧은 시간 간격을 10 초 보다 작거나 같은 제어 라우터 간의 BGP Keepalive 매개 변수 시간을 구성할 수 있습니다. 이 짧은 연결 유지 간격을 사용 하 여에 지 라우터는 RAS 게이트웨이 BGP 실패 하면 신속 하 게 감지 하 고 네트워크 컨트롤러는 이전 섹션에 나와 있는 단계를 따릅니다. 이러한 이점은 양방향 전달 검색 (BFD) 프로토콜과 같은 별도 오류 검색 프로토콜에 대 한 필요를 줄여 수 있습니다.  
  
 
  


