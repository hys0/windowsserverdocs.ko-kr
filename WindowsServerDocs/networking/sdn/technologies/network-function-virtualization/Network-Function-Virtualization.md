---
title: 네트워크 기능 가상화
description: 이 항목을 사용 하 여 Windows Server 2016의 데이터 센터 방화벽, 다중 테 넌 트 RAS 게이트웨이 및 SLB (소프트웨어 부하 분산)와 같은 가상 네트워킹 어플라이언스를 배포할 수 있도록 하는 네트워크 기능 가상화에 대해 알아볼 수 있습니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 79df3bbe-48fd-4eff-8df6-35f6317566f3
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 338d5a285f2524932a91a66db186554cd0f50e2a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355654"
---
# <a name="network-function-virtualization"></a>네트워크 기능 가상화

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목을 사용 하 여 네트워크 기능 가상화에 대해 자세히 알아볼 수 있습니다 .이를 통해 데이터 센터 방화벽, 다중 테 넌 트 RAS 게이트웨이, 소프트웨어 부하 분산 \(SLB @ no__t-1 멀티플렉서 \(MUX @ no_와 같은 가상 네트워킹 어플라이언스를 배포할 수 있습니다. _t-3.
  
>[!NOTE]  
>이 항목 외에 다음과 같은 네트워크 기능 가상화 설명서를 사용할 수 있습니다.  
> - [데이터 센터 방화벽 개요](../../../sdn/technologies/network-function-virtualization/../../../sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)  
> - [SDN용 RAS 게이트웨이](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)  
> - [SDN에 대한 SLB(소프트웨어 부하 분산)](../../../sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md)  
  
오늘날의 소프트웨어에서 점점 더 가상 어플라이언스로 대 정의 된 데이터 센터, 하드웨어 장비 (예: 부하 분산 장치, 방화벽, 라우터, 스위치 및 등)에서 수행 되는 네트워크 기능 가상화 되 고 됩니다. 이 "네트워크 기능 가상화" 서버 가상화 및 네트워크 가상화의 자연 스러운 진행 됩니다. 가상 어플라이언스는 신속 하 게 새로운 및 새로운 시장 있습니다. 관심을 생성 하 고 업계 동향 가상화 플랫폼 모두에 대 한 권한을 얻는 및 클라우드 서비스를 계속 합니다.  
  
Microsoft은 Windows Server 2012 r 2로 시작 하는 가상 어플라이언스로 독립 실행형 게이트웨이 추가 합니다. 자세한 내용은 [Windows Server 게이트웨이](https://technet.microsoft.com/library/dn313101.aspx)를 참조하세요. 이제 Windows Server 2016 Microsoft 확장 하 고 네트워크 기능 가상화 시장에 대 한 투자를 계속 합니다.  
  
## <a name="virtual-appliance-benefits"></a>가상 어플라이언스 혜택  
가상 어플라이언스 동적 이며 쉽게 미리 작성 된, 사용자 지정 된 가상 컴퓨터는 이기 때문에 변경할 수 있습니다. 패키지, 업데이트 및 하나의 단위로 관리 하나 이상의 가상 컴퓨터 수 있습니다. 소프트웨어와 함께 정의 네트워킹 (SDN), 민첩성 및 오늘날의 클라우드 기반 인프라에 필요한 유연성을 얻게 됩니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  
  
-   SDN 풀링되 고 동적 리소스와 네트워크를 표시합니다.  
  
-   SDN 테 넌 트 격리를 도와줍니다.  
  
-   SDN 규모와 성능 최대화합니다.  
  
-   가상 어플라이언스 원활 하 게 용량 확장 및 작업 부하 이동성을 사용 합니다.  
  
-   가상 어플라이언스 운영 복잡성을 최소화합니다.  
  
-   가상 어플라이언스 쉽게 획득, 배포 및 사전 통합 된 솔루션을 관리 하는 고객을 게 알립니다.  
  
    -   고객 쉽게 이동할 수는 가상 어플라이언스 아무 곳 이나 클라우드.  
  
    -   고객 가상 어플라이언스를 확장할 수 또는 아래로 필요에 따라 동적으로 합니다.  
  
Microsoft SDN에 대 한 자세한 내용은 참조 [소프트웨어 정의 네트워킹](https://technet.microsoft.com/windows-server-docs/networking/sdn/software-defined-networking--sdn-)합니다.  
  
### <a name="what-network-functions-are-being-virtualized"></a>네트워크 기능을 가상화?  
가상화 된 네트워크 기능에 대 한 신속 하 게 증가 합니다. 다음 네트워크 기능을 가상화 합니다.  
  
-   **보안**  
  
    -   방화벽  
  
    -   바이러스 백신  
  
    -   DDoS (분산된 서비스 거부)  
  
    -   IP/ID (침입 방지 시스템/침입 감지 시스템)  
  
-   **Application/WAN 최적화 도구**  
  
-   **테두리**  
  
    -   사이트 간 게이트웨이  
  
    -   L3 게이트웨이  
  
    -   라우터  
  
    -   스위치  
  
    -   NAT  
  
    -   부하 분산 장치 (반드시 지)에  
  
    -   HTTP 프록시  
  
## <a name="why-microsoft-is-a-great-platform-for-virtual-appliances"></a>왜 Microsoft는 가상 장비에 대 한 훌륭한 플랫폼  
![가상 네트워크 스택](../../../media/Network-Function-Virtualization/Microsoft-Network-Function-Virtualization.png)  
  
Microsoft 플랫폼이를 가상 장비 빌드하여 배포 훌륭한 플랫폼으로 설계 되었다는 점입니다. 이유는 다음과 같습니다.  
  
-   Microsoft은 Windows Server 2016 키 가상화 된 네트워크 기능을 제공합니다.  
  
-   사용자가 선택한 공급 업체에서 가상 어플라이언스를 배포할 수 있습니다.  
  
-   배포 하 고, 구성 하 고, 사용자 가상 어플라이언스 Windows Server 2016와 함께 제공 되는 Microsoft 네트워크 컨트롤러를 관리할 수 있습니다. 네트워크 컨트롤러에 대 한 자세한 내용은 참조 [네트워크 컨트롤러](../../../sdn/technologies/network-controller/Network-Controller.md)합니다.  
  
-   Hyper-v는 필요한 상위 게스트 운영 체제를 호스팅할 수 있습니다.  
  
## <a name="network-function-virtualization-in-windows-server-2016"></a>Windows Server 2016에서 네트워크 기능 가상화  
  
### <a name="virtual-appliances-functions-provided-by-microsoft"></a>Microsoft에서 제공 하는 가상 어플라이언스 함수  
Windows Server 2016은 다음 가상 어플라이언스 제공 됩니다.  
  
**소프트웨어 부하 분산 장치**  
  
데이터 센터 대규모로 운영 계층 4 부하 분산 장치입니다. Azure 환경에 대규모로 배포 된 Azure 부하 분산의 유사한 버전입니다. Microsoft 소프트웨어 부하 분산 장치에 대 한 자세한 내용은 참조 [소프트웨어 부하 분산 (SLB) SDN에 대 한](https://technet.microsoft.com/library/mt632286.aspx)합니다. Microsoft Azure 부하 분산 서비스에 대 한 자세한 내용은 참조 [Microsoft Azure 부하 분산 서비스](https://azure.microsoft.com/blog/2014/04/08/microsoft-azure-load-balancing-services/)합니다.  
  
**게이트웨이**합니다. RAS 게이트웨이 모든 조합의 다음 게이트웨이 기능을 제공합니다.  
  
-   **사이트 간 게이트웨이**  
  
    RAS 게이트웨이 프로토콜 BGP (Border Gateway)를 제공 합니다.-테 넌 트가 액세스 하 고 원격 사이트에서 사이트 간 VPN 연결을 통해 자신의 리소스를 관리할 수 있도록 하 고 클라우드 및 테 넌 트의 실제 네트워크의 가상 리소스 간의 네트워크 트래픽 흐름을 허용 하 지원, 다중 테 넌 트 게이트웨이. RAS 게이트웨이에 대 한 자세한 내용은 참조 [RAS 게이트웨이 고가용성](https://technet.microsoft.com/library/mt631692.aspx) 및 [RAS 게이트웨이](https://technet.microsoft.com/library/mt626650.aspx)합니다.  
  
-   **전달 게이트웨이**  
  
    RAS 게이트웨이 가상 네트워크와 호스팅 공급자 실제 네트워크 간에 트래픽을 라우팅합니다. 예를 들어 테 넌 트 하나 이상의 가상 네트워크를 만드는 호스팅 공급자에서 실제 네트워크의 공유 리소스에 액세스 해야 하는 경우 전달 게이트웨이 가상 네트워크와 필요한 서비스를 사용 하 여 가상 네트워크에서 작업 하는 사용자가 제공 하는 실제 네트워크 간에 트래픽을 라우팅할 수 있습니다. 자세한 내용은 참조 [RAS 게이트웨이 고가용성](https://technet.microsoft.com/library/mt631692.aspx) 및 [RAS 게이트웨이](https://technet.microsoft.com/library/mt626650.aspx)합니다.  
  
-   **GRE 터널 게이트웨이**  
  
    GRE 기반의 터널을 사용하면 테넌트 가상 네트워크와 외부 네트워크를 연결할 수 있습니다. GRE 대부분의 네트워크 장치에서 사용할 수 없으면 GRE 프로토콜은 간단 하며 지원, 데이터 암호화 필요 하지 않은 터널링에 이상적인 선택 됩니다. S2S(Site to Site) 터널의 GRE 지원은 다중 테넌트 게이트웨이를 사용하는 테넌트 가상 네트워크와 테넌트 외부 네트워크 간의 전달 문제를 해결합니다. GRE 터널에 대 한 자세한 내용은 참조 [Windows Server 2016에서 GRE 터널링](https://technet.microsoft.com/library/dn765485.aspx)합니다.  
  
**BGP를 사용 하 여 제어 평면 라우팅**  
  
Hyper-v 네트워크 가상화 (HNV) 라우팅을 제어는 모든 고객 주소 평면 경로 전달 하 고 동적으로 학습 하 고, 그런 다음 가상 네트워크에 분산된 RAS 게이트웨이 라우터를 업데이트 하 여 제어 평면에 논리, 중앙 집중화 된 엔터티입니다. 자세한 내용은 참조 [RAS 게이트웨이 고가용성](https://technet.microsoft.com/library/mt631692.aspx) 및 [RAS 게이트웨이](https://technet.microsoft.com/library/mt626650.aspx)합니다.  
  
**분산 다중 테 넌 트 방화벽**  
  
방화벽은 가상 네트워크의 네트워크 계층을 보호합니다. 각 테 넌 트 VM의 SDN vSwitch 포트에 정책이 적용 됩니다. 모든 트래픽 흐름 보호: 동-서 및 북-남 합니다. 테 넌 트 포털을 통해 전달 되는 정책 및 네트워크 컨트롤러 적용 가능한 모든 호스트에 배포 합니다. 분산 된 다중 테 넌 트 방화벽에 대 한 자세한 내용은 참조 [데이터 센터 방화벽 개요](../../../sdn/technologies/network-function-virtualization/../../../sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)합니다.  
  


