---
title: Windows Server 2016의 GRE 터널링
description: Windows Server 2016에서 RAS 게이트웨이에 대 한 캡슐화 GRE (Generic Routing) 터널 기능에 대 한 업데이트의 이해를 갖추기 위해이 항목에서는 사용할 수 있습니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: df2023bf-ba64-481e-b222-6f709edaa5c1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e0ec077ad5e97edd3db7d1dc4e662bb191f7885b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887864"
---
# <a name="gre-tunneling-in-windows-server-2016"></a>Windows Server 2016의 GRE 터널링

>적용 대상: Windows Server (반기 채널), Windows Server 2016

Generic Routing Encapsulation에 업데이트를 제공 하는 Windows Server 2016 \(GRE\) RAS 게이트웨이에 대 한 기능을 터널링 합니다.  
  
GRE는 인터넷 프로토콜 네트워크를 통한 가상 지점 간 연결 내에서 다양한 네트워크 계층 프로토콜을 캡슐화할 수 있는 간단한 터널링 프로토콜입니다. Microsoft GRE 구현에는 IPv4 및 IPv6 캡슐화 할 수 있습니다.  
  
GRE 터널은 많은 시나리오에서 유용 하기 때문에:  
  
-   간단한 및 RFC 2890 규격 다양 한 공급 업체 장치와 상호 운용 가능 하므로  
  
-   경계 게이트웨이 프로토콜을 사용할 수 있습니다 \(BGP\) 동적 라우팅  
  
-   소프트웨어 정의 네트워킹 GRE 다중 테 넌 트 RAS 게이트웨이 사용 하기 위해 구성할 수 있습니다 \(SDN\)
  
-   System Center Virtual Machine Manager 사용 하 여 관리 GRE\-기반 RAS 게이트웨이
  
-   GRE RAS 게이트웨이 서버로 구성 되는 6 코어 가상 머신에서 최대 2.0 중단 없이 32gbps 처리량을 얻을 수 있습니다.
  
-   단일 게이트웨이 여러 연결 모드를 지원합니다.  
  
GRE 기반의 터널을 사용하면 테넌트 가상 네트워크와 외부 네트워크를 연결할 수 있습니다. GRE 프로토콜은 간단 하며 지원 대부분의 네트워크 장치에서 GRE가 되기 이상적인 터널링에 대 한 데이터 암호화 필수가 아닙니다. 

이 항목의 뒷부분에 설명 된 대로 사이트 간 (S2S) 터널의 GRE 지원은 테 넌 트 가상 네트워크 및 다중 테 넌 트 게이트웨이 사용 하 여 테 넌 트 외부 네트워크 간의 전달 문제를 해결 합니다.  
  
GRE 터널 기능은 다음 요구 사항을 충족 하도록 고안 되었습니다.  
  
-   호스팅 공급자의 실제 스위치 구성을 수정 하지 않고 전달에 대 한 가상 네트워크를 만들 수 있어야 합니다.  
  
-   호스팅 공급자는 자신의 인프라 내에서 실제 스위치의 구성을 수정 하지 않고 해당 외부 연결 네트워크에 서브넷을 추가할 수 있어야 합니다.  
GRE 터널 기능을 사용 하거나 Microsoft 기술을 사용 하 여 서비스 제품의 소프트웨어 정의 네트워킹을 구현 하는 서비스 공급자를 호스트 하기 위한 몇 가지 주요 시나리오를 향상 시킵니다.  
  
다음은 몇 가지 예제 시나리오입니다.  
  
-   [실제 네트워크를 테 넌 트를 테 넌 트 가상 네트워크에서 액세스](#BKMK_Access)  
  
-   [고속 연결](#BKMK_Speed)  
  
-   [VLAN 기반 격리를 사용 하 여 통합](#BKMK_Integration)  
  
-   [리소스에 공유 액세스](#BKMK_Shared)  
  
-   [테 넌 트에 타사 장치 서비스](#BKMK_thirdparty)  
  
## <a name="key-scenarios"></a>주요 시나리오

GRE 터널링 기능 주소는 주요 시나리오는 다음과 같습니다.  
  
### <a name="BKMK_Access"></a>실제 네트워크를 테 넌 트를 테 넌 트 가상 네트워크에서 액세스

이 시나리오에서는 테 넌 트 호스팅 서비스 공급자 프레미스에 있는 실제 네트워크에 테 넌 트 가상 네트워크에서 액세스를 제공 하는 확장 가능한 방법입니다. 다중 테 넌 트 게이트웨이에서 GRE 터널 끝점은 설정, 다른 GRE 터널 끝점 실제 네트워크에 타사 장치에서 설정 됩니다. 계층 3 트래픽은 가상 네트워크의 가상 컴퓨터와 실제 네트워크에 제 3 자 장치 간에 라우팅됩니다.  
  
![호스팅 서비스 공급자 실제 네트워크와 테 넌 트 가상 네트워크를 연결 하는 GRE 터널](../../media/gre-tunneling-in-windows-server/GRE_.png)  
  
### <a name="BKMK_Speed"></a>고속 연결

이 시나리오는 확장 가능한 방식으로 테 넌 트 온-프레미스 네트워크를 호스팅 서비스 공급자 네트워크에 있는 가상 네트워크 고속 연결을 제공할 수 있습니다. 테 넌 트 label switching (MPLS) 호스팅 서비스 공급자의 edge router 및 다중 테 넌 트 게이트웨이를 테 넌 트의 가상 네트워크 간에 GRE 터널은 설정 하는 위치를 통해 서비스 공급자 네트워크에 연결 합니다.  
  
![테 넌 트 엔터프라이즈 MPLS 네트워크 및 테 넌 트 가상 네트워크를 연결 하는 GRE 터널](../../media/gre-tunneling-in-windows-server/GRE-.png)  
  
### <a name="BKMK_Integration"></a>VLAN 기반 격리를 사용 하 여 통합

이 시나리오에서는 Hyper-v 네트워크 가상화를 사용 하 여 VLAN 기반 격리를 통합할 수 있습니다. 호스팅 공급자 네트워크에는 실제 네트워크는 VLAN 기반 격리를 사용 하 여 부하 분산 장치를 포함 합니다. 다중 테 넌 트 게이트웨이 실제 네트워크에 부하 분산 장치 및 다중 테 넌 트 가상 네트워크 게이트웨이 간에 GRE 터널을 설정합니다.  
  
원본과 대상 간에 여러 터널을 설정할 수 있습니다 및 터널을 판별 하 GRE 키가 사용 합니다.  
  
![여러 GRE 터널 테 넌 트 가상 네트워크 연결](../../media/gre-tunneling-in-windows-server/GRE-VLANIsolation.png)  
  
### <a name="BKMK_Shared"></a>리소스에 공유 액세스

이 시나리오에서는 호스팅 공급자 네트워크에 있는 실제 네트워크의 공유 리소스에 액세스할 수 있습니다.  
  
여러 테 넌 트 가상 네트워크와 공유 하려는 호스팅 공급자 네트워크에 있는 실제 네트워크에서 서버에 있는 공유 서비스를 할 수 있습니다.  
  
겹치지 않는 서브넷을 사용 하 여 테 넌 트 네트워크 GRE 터널을 통해 공용 네트워크에 액세스 합니다. 단일 테 넌 트 게이트웨이, 따라서 적절 한 테 넌 트 네트워크로 패킷을 라우팅하려면 GRE 터널 간에 라우팅합니다.  
  
이 시나리오에서는 타사 하드웨어 어플라이언스를 통해 단일 테 넌 트 게이트웨이 바꿀 수 있습니다.  
  
![여러 터널을 사용 하 여 여러 가상 네트워크에 연결할 단일 테 넌 트 게이트웨이](../../media/gre-tunneling-in-windows-server/GRE-SharedResource.png)  
  
### <a name="BKMK_thirdparty"></a>테 넌 트에 타사 장치 서비스

이 시나리오에 테 넌 트 가상 네트워크 트래픽 흐름은 타사 장치 (예: 하드웨어 부하 분산 장치)를 통합 하 사용할 수 있습니다. 예를 들어, 엔터프라이즈 사이트에서 시작 된 트래픽을 S2S 터널을 통해 다중 테 넌 트 게이트웨이를 전달 합니다. GRE 터널을 통해 트래픽은 부하 분산 장치에 라우팅됩니다. 부하 분산 장치는 엔터프라이즈의 가상 네트워크의 여러 가상 컴퓨터에 트래픽을 라우팅합니다. 가상 네트워크의 IP 주소를 겹치는 잠재적으로 다른 테 넌 트에 대 한 동일한 상황이 발생 합니다. 네트워크 트래픽을 부하 분산 장치 Vlan을 사용 하 여 격리 된 및 Vlan을 지 원하는 모든 계층 3 장치에 적용 됩니다.  
  
![여러 GRE 터널 타사 장치에 가상 네트워크 연결](../../media/gre-tunneling-in-windows-server/GREThirdParty.png)  
  
## <a name="configuration-and-deployment"></a>구성 및 배포

GRE 터널 추가 프로토콜 S2S 인터페이스 내에서 표시 됩니다. 네트워킹 블로그에서 설명 하는 IPSec S2S 터널와 비슷한 방식으로 구현 됩니다. [Windows Server 2012 R2 사용 하 여 다중 테 넌 트 사이트 및 사이트 간 (S2S) VPN Gateway](https://blogs.technet.com/b/networking/archive/2013/09/29/multi-tenant-site-to-site-s2s-vpn-gateway-with-windows-server-2012-r2.aspx)  
  
GRE 터널 게이트웨이 포함 하 여 게이트웨이 배포 하는 예로 다음 항목을 참조 하십시오.  
  
[스크립트를 사용 하 여 소프트웨어 정의 네트워크 인프라 배포](../../../networking/sdn/deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)
  
## <a name="more-information"></a>자세한 정보

S2S 게이트웨이 배포 하는 방법에 대 한 자세한 내용은 다음 항목을 참조 하세요.  
  
-   [RAS Gateway](RAS-Gateway.md)  
  
-   [경계 게이트웨이 프로토콜 &#40;BGP&#41;](../bgp/Border-Gateway-Protocol-BGP.md)  
  
-   [새로운! Windows Server 2012 R2 RAS 다중 테 넌 트 게이트웨이 배포 가이드](https://blogs.technet.com/b/wsnetdoc/archive/2014/03/26/new-windows-server-2012-r2-RAS-multitenant-gateway-deployment-guide.aspx)  
  
-   [BGP (Border Gateway Protocol) 다중 테 넌 트 RAS 게이트웨이 배포](https://blogs.technet.com/b/wsnetdoc/archive/2014/04/03/deploy-border-gateway-protocol-bgp-with-the-RAS-multitenant-gateway.aspx)  
  


