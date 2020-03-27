---
title: Windows Server 2016의 GRE 터널링
description: 이 항목을 사용 하 여 Windows Server 2016의 RAS 게이트웨이에 대 한 GRE (Generic Routing 캡슐화) 터널 기능의 업데이트를 이해할 수 있습니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: df2023bf-ba64-481e-b222-6f709edaa5c1
ms.author: lizross
author: eross-msft
ms.openlocfilehash: d246f0e56681f75e4336ed225d1557a0e05c581b
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80308551"
---
# <a name="gre-tunneling-in-windows-server-2016"></a>Windows Server 2016의 GRE 터널링

>적용 대상: Windows Server(반기 채널), Windows Server 2016

Windows Server 2016에서는 RAS 게이트웨이의 GRE\) 터널 기능 \(일반 라우팅 캡슐화에 대 한 업데이트를 제공 합니다.  
  
GRE는 인터넷 프로토콜 네트워크를 통한 가상 지점 간 연결 내에서 다양한 네트워크 계층 프로토콜을 캡슐화할 수 있는 간단한 터널링 프로토콜입니다. Microsoft GRE 구현은 IPv4 및 IPv6을 캡슐화 할 수 있습니다.  
  
GRE 터널은 다음과 같은 다양 한 시나리오에서 유용 합니다.  
  
-   경량 이며 RFC 2890 호환 되므로 다양 한 공급 업체 장치와 상호 운용할 수 있습니다.  
  
-   Border Gateway Protocol \(BGP\)를 사용 하 여 동적 라우팅을 수행할 수 있습니다.  
  
-   소프트웨어 정의 네트워킹 \(SDN에 사용할 GRE 다중 테 넌 트 RAS 게이트웨이를 구성할 수 있습니다\)
  
-   System Center Virtual Machine Manager를 사용 하 여 GRE\-기반 RAS 게이트웨이를 관리할 수 있습니다.
  
-   GRE RAS 게이트웨이로 구성 된 6 코어 가상 머신에서 최대 2.0 Gbps의 처리량을 달성할 수 있습니다.
  
-   단일 게이트웨이가 여러 연결 모드를 지원 합니다.  
  
GRE 기반의 터널을 사용하면 테넌트 가상 네트워크와 외부 네트워크를 연결할 수 있습니다. GRE 프로토콜은 간단 하 고 대부분의 네트워크 장치에서 GRE를 지원할 수 있기 때문에 데이터 암호화가 필요 하지 않은 터널링에 이상적인 선택이 됩니다. 

S2S (Site to Site) 터널의 GRE 지원은이 항목의 뒷부분에 설명 된 대로 다중 테 넌 트 게이트웨이를 사용 하는 테 넌 트 가상 네트워크와 테 넌 트 외부 네트워크 간의 전달 문제를 해결 합니다.  
  
GRE 터널 기능은 다음 요구 사항을 해결 하도록 설계 되었습니다.  
  
-   호스팅 공급자는 물리적 스위치 구성을 수정 하지 않고 전달할 가상 네트워크를 만들 수 있어야 합니다.  
  
-   호스팅 공급자는 인프라 내에서 물리적 스위치의 구성을 수정 하지 않고도 외부 연결 네트워크에 서브넷을 추가할 수 있어야 합니다.  
GRE 터널 기능은 Microsoft 기술을 사용 하는 서비스 공급자를 호스트 하는 여러 주요 시나리오를 지원 하 고 서비스 제공에서 소프트웨어 정의 네트워킹을 구현 합니다.  
  
다음은 몇 가지 예제 시나리오입니다.  
  
-   [테 넌 트 가상 네트워크에서 테 넌 트 실제 네트워크에 액세스](#BKMK_Access)  
  
-   [고속 연결](#BKMK_Speed)  
  
-   [VLAN 기반 격리와의 통합](#BKMK_Integration)  
  
-   [공유 리소스 액세스](#BKMK_Shared)  
  
-   [테 넌 트에 대 한 타사 장치 서비스](#BKMK_thirdparty)  
  
## <a name="key-scenarios"></a>주요 시나리오

다음은 GRE 터널 기능에서 다루는 주요 시나리오입니다.  
  
### <a name="access-from-tenant-virtual-networks-to-tenant-physical-networks"></a><a name="BKMK_Access"></a>테 넌 트 가상 네트워크에서 테 넌 트 실제 네트워크에 액세스

이 시나리오에서는 테 넌 트 가상 네트워크에서 호스팅 서비스 공급자 온-프레미스에 있는 테 넌 트 실제 네트워크에 액세스할 수 있도록 하는 확장성 있는 방법을 제공 합니다. GRE 터널 끝점은 다중 테 넌 트 게이트웨이에서 설정 되 고 다른 GRE 터널 끝점은 실제 네트워크의 타사 장치에 설정 됩니다. 계층 3 트래픽은 가상 네트워크의 가상 컴퓨터와 실제 네트워크의 타사 장치 간에 라우팅됩니다.  
  
![호스팅 서비스 공급자 실제 네트워크 및 테 넌 트 가상 네트워크를 연결 하는 GRE 터널](../../media/gre-tunneling-in-windows-server/GRE_.png)  
  
### <a name="high-speed-connectivity"></a><a name="BKMK_Speed"></a>고속 연결

이 시나리오에서는 테 넌 트 온-프레미스 네트워크에서 호스팅 서비스 공급자 네트워크에 있는 가상 네트워크로 고속 연결을 제공 하는 확장 가능한 방법을 사용할 수 있습니다. 테 넌 트는 MPLS (멀티 프로토콜 레이블 전환)를 통해 서비스 공급자 네트워크에 연결 합니다. 여기서 GRE 터널은 호스팅 서비스 공급자의에 지 라우터와 다중 테 넌 트 게이트웨이 간에 테 넌 트의 가상 네트워크로 설정 됩니다.  
  
![테 넌 트 엔터프라이즈 MPLS 네트워크 및 테 넌 트 가상 네트워크를 연결 하는 GRE 터널](../../media/gre-tunneling-in-windows-server/GRE-.png)  
  
### <a name="integration-with-vlan-based-isolation"></a><a name="BKMK_Integration"></a>VLAN 기반 격리와의 통합

이 시나리오에서는 VLAN 기반 격리를 Hyper-v 네트워크 가상화와 통합할 수 있습니다. 호스트 공급자 네트워크의 실제 네트워크에는 VLAN 기반 격리를 사용 하는 부하 분산 장치가 있습니다. 다중 테 넌 트 게이트웨이는 실제 네트워크의 부하 분산 장치와 가상 네트워크의 다중 테 넌 트 게이트웨이 간에 GRE 터널을 설정 합니다.  
  
원본 및 대상 간에 여러 터널을 설정할 수 있으며, GRE 키를 사용 하 여 터널을 판별 합니다.  
  
![다중 테 넌 트 가상 네트워크를 연결 하는 다중 GRE 터널](../../media/gre-tunneling-in-windows-server/GRE-VLANIsolation.png)  
  
### <a name="access-shared-resources"></a><a name="BKMK_Shared"></a>공유 리소스 액세스

이 시나리오에서는 호스팅 공급자 네트워크에 있는 실제 네트워크의 공유 리소스에 액세스할 수 있습니다.  
  
여러 테 넌 트 가상 네트워크와 공유 하려는 호스팅 공급자 네트워크에 있는 실제 네트워크의 서버에 공유 서비스가 있을 수 있습니다.  
  
겹치지 않는 서브넷을 사용 하는 테 넌 트 네트워크가 GRE 터널을 통해 공용 네트워크에 액세스 합니다. 단일 테 넌 트 게이트웨이는 GRE 터널 사이에서 경로 하므로 적절 한 테 넌 트 네트워크로 패킷을 라우팅합니다.  
  
이 시나리오에서는 단일 테 넌 트 게이트웨이를 타사 하드웨어 어플라이언스로 교체할 수 있습니다.  
  
![여러 터널을 사용 하 여 여러 가상 네트워크를 연결 하는 단일 테 넌 트 게이트웨이](../../media/gre-tunneling-in-windows-server/GRE-SharedResource.png)  
  
### <a name="services-of-third-party-devices-to-tenants"></a><a name="BKMK_thirdparty"></a>테 넌 트에 대 한 타사 장치 서비스

이 시나리오는 타사 장치 (예: 하드웨어 부하 분산 장치)를 테 넌 트 가상 네트워크 트래픽 흐름에 통합 하는 데 사용할 수 있습니다. 예를 들어 엔터프라이즈 사이트에서 시작 되는 트래픽은 S2S 터널을 통해 다중 테 넌 트 게이트웨이로 전달 됩니다. 트래픽은 GRE 터널을 통해 부하 분산 장치로 라우팅됩니다. 부하 분산 장치는 조직의 가상 네트워크에 있는 여러 가상 컴퓨터로 트래픽을 라우팅합니다. 가상 네트워크에서 잠재적으로 IP 주소가 겹칠 수 있는 다른 테 넌 트의 경우에도 마찬가지입니다. 네트워크 트래픽은 Vlan을 사용 하 여 부하 분산 장치에서 격리 되며 Vlan을 지 원하는 모든 계층 3 장치에 적용 됩니다.  
  
![가상 네트워크를 타사 장치에 연결 하는 여러 GRE 터널](../../media/gre-tunneling-in-windows-server/GREThirdParty.png)  
  
## <a name="configuration-and-deployment"></a>구성 및 배포

GRE 터널은 S2S 인터페이스 내에서 추가 프로토콜로 노출 됩니다. 이는 [Windows Server 2012 r 2를 사용 하 여 다중 테 넌 트 s2s (사이트 간) VPN Gateway](https://blogs.technet.com/b/networking/archive/2013/09/29/multi-tenant-site-to-site-s2s-vpn-gateway-with-windows-server-2012-r2.aspx) 와 비슷한 방식으로 구현 됩니다.  
  
GRE 터널 게이트웨이를 비롯 하 여 게이트웨이를 배포 하는 예제는 다음 항목을 참조 하세요.  
  
[스크립트를 사용 하 여 소프트웨어 정의 네트워크 인프라 배포](../../../networking/sdn/deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)
  
## <a name="more-information"></a>자세한 정보

S2S 게이트웨이를 배포 하는 방법에 대 한 자세한 내용은 다음 항목을 참조 하세요.  
  
-   [RAS 게이트웨이](RAS-Gateway.md)  
  
-   [BGP &#40;Border Gateway Protocol&#41;](../bgp/Border-Gateway-Protocol-BGP.md)  
  
-   [새로운! Windows Server 2012 R2 RAS 다중 테 넌 트 게이트웨이 배포 가이드](https://blogs.technet.com/b/wsnetdoc/archive/2014/03/26/new-windows-server-2012-r2-RAS-multitenant-gateway-deployment-guide.aspx)  
  
-   [RAS 다중 테 넌 트 게이트웨이와 함께 BGP (Border Gateway Protocol) 배포](https://blogs.technet.com/b/wsnetdoc/archive/2014/04/03/deploy-border-gateway-protocol-bgp-with-the-RAS-multitenant-gateway.aspx)  
  


