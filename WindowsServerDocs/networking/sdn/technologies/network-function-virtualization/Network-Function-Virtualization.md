---
title: 네트워크 함수 Virtualization
description: 가상 네트워킹 장비와 같은 Datacenter 방화벽 넌 RAS 게이트웨이 소프트웨어 부하 분산 SLB () Windows Server 2016에 배포할 수 있도록 기능 가상화, 네트워크에 대 한 자세한 내용은이 항목을 사용할 수 있습니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 79df3bbe-48fd-4eff-8df6-35f6317566f3
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7caa9eef42cb7ab95a13d64c1dcd3639b1132eb3
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="network-function-virtualization"></a>네트워크 함수 Virtualization

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

방화벽 Datacenter 넌 RAS 게이트웨이 부하 분산 소프트웨어가 \(SLB\) 등 가상 네트워킹 장비 배포할 수 있도록 기능 가상화, 네트워크에 대 한 자세한 내용은이 항목을 사용할 수 멀티플렉서 \(MUX\) 합니다.
  
>[!NOTE]  
>이 항목 외에 다음과 같은 기능 네트워크 가상화 문서를 사용할 수 있습니다.  
> - [Datacenter 방화벽 개요](../../../sdn/technologies/network-function-virtualization/../../../sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)  
> - [SDN RAS 게이트웨이](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)  
> - [소프트웨어 균형 (SLB) SDN에 대 한](../../../sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md)  
  
하드웨어 기기 (예: 부하 분산, 방화벽, 라우터에, 스위치 및 등)가 수행 하는 네트워크 기능 정의 데이터 센터 오늘 소프트웨어에서 가상 기기도 가상화 되 고 점점 더 됩니다. 이 "네트워크 함수 virtualization" 서버 virtualization 및 네트워크 가상화의 자연 진행입니다. 가상 장비는 신속 하 게 신흥 및 새로운 시장 있습니다. 관심사를 생성 하 고 모두 virtualization 플랫폼에서 운동량 얻고, 클라우드 서비스를 계속 합니다.  
  
Microsoft은 Windows Server 2012 r 2와 시작 가상 기기 같은 독립 실행형 게이트웨이 포함 됩니다. 자세한 내용은 참조 [Windows Server 게이트웨이](https://technet.microsoft.com/library/dn313101.aspx)합니다. 이제 Windows Server 2016 Microsoft 확장 기능 네트워크 가상화 지역/국가에 투자를 계속 합니다.  
  
## <a name="virtual-appliance-benefits"></a>가상 기기 이점  
가상 기기 동적 이며 쉽게 미리 작성, 사용자 지정 된 가상 컴퓨터 있기 때문에 변경할 수 있습니다. 하나 이상의 가상 컴퓨터 패키지, 업데이트 및 단위로 유지 수 있습니다. 소프트웨어와 함께 정의 네트워킹 (SDN), 유연성와 오늘 클라우드 기반 인프라에 필요한 유연 하 게 받을 수 있습니다. 예를 들어:  
  
-   SDN 네트워크 풀 및 동적 리소스를 제공합니다.  
  
-   SDN 테 격리를 수 있습니다.  
  
-   SDN 배율 및 성능을 최대화합니다.  
  
-   가상 기기 원활 하 게 용량 확장 하 고 작업 이동성 사용 하도록 설정 합니다.  
  
-   가상 기기가 작동 복잡성을 최소화 하세요.  
  
-   가상 기기 쉽게 획득, 배포 및 관리 솔루션을 예약 통합된 하는 고객 사용 수 있습니다.  
  
    -   고객 쉽게 이동할 수 가상 기기 어디서 나 클라우드에.  
  
    -   고객 가상 기기 확장할 수 하거나 아래로 동적으로 필요에 따라 합니다.  
  
Microsoft SDN에 대 한 자세한 내용은 [소프트웨어 네트워킹 정의](https://technet.microsoft.com/windows-server-docs/networking/sdn/software-defined-networking--sdn-)합니다.  
  
### <a name="what-network-functions-are-being-virtualized"></a>네트워크 기능은 가상화 되 고 있나요?  
네트워크 가상화 기능에 대 한 마켓플레이스 빠르게 성장 하는 합니다. 다음 네트워크 기능은 가상화 다음과 같습니다.  
  
-   **보안**  
  
    -   방화벽  
  
    -   바이러스 백신  
  
    -   DDoS (배포 된 서비스 거부)  
  
    -   IPS/ID (침입 방지 침입 시스템/감지 시스템)  
  
-   **응용 프로그램/WAN 최적화 프로그램**  
  
-   **Edge**  
  
    -   사이트에 게이트웨이  
  
    -   L 3 게이트웨이  
  
    -   라우터  
  
    -   전환  
  
    -   NAT  
  
    -   부하 분산 (반드시 끝자락)  
  
    -   HTTP 프록시  
  
## <a name="why-microsoft-is-a-great-platform-for-virtual-appliances"></a>Microsoft는 가상 기기에 대 한 멋진 플랫폼 이유  
![가상 네트워크 스택](../../../media/Network-Function-Virtualization/Microsoft-Network-Function-Virtualization.png)  
  
Microsoft 플랫폼 빌드하고 가상 기기 배포 뛰어난 플랫폼을 엔지니어링 되었습니다 했습니다. 다음은 이유 때문이입니다.  
  
-   Microsoft은 Windows Server 2016와 키 가상화 네트워크 기능을 제공합니다.  
  
-   선택 항목의 공급 업체에서 가상 기기를 배포할 수 있습니다.  
  
-   배포을 구성 하 고 Windows Server 2016와 함께 제공 된 Microsoft 네트워크 컨트롤러와 가상 기기가 관리할 수 있습니다. 네트워크 컨트롤러에 대 한 자세한 내용은 참조 [네트워크 컨트롤러](../../../sdn/technologies/network-controller/Network-Controller.md)합니다.  
  
-   Hyper-v 필요한 상위 게스트 운영 체제 호스트할 수 있습니다.  
  
## <a name="network-function-virtualization-in-windows-server-2016"></a>Windows Server 2016에 네트워크 함수 virtualization  
  
### <a name="virtual-appliances-functions-provided-by-microsoft"></a>Microsoft에서 제공한 가상 기기 기능  
Windows Server 2016 다음 가상 기기가 제공 됩니다.  
  
**부하 분산 소프트웨어가**  
  
Datacenter 배율에서 작동 계층 4 부하 분산 합니다. Azure 환경에서 크기로 배포한 Azure의 부하 분산 유사 버전입니다. Microsoft 소프트웨어 부하 분산 장치에 대 한 자세한 내용은 참조 [소프트웨어 부하 분산 SLB () SDN에 대 한](https://technet.microsoft.com/library/mt632286.aspx)합니다. Microsoft Azure 부하 분산 서비스에 대 한 자세한 내용은 참조 [Microsoft Azure 부하 분산 서비스](https://azure.microsoft.com/blog/2014/04/08/microsoft-azure-load-balancing-services/)합니다.  
  
**게이트웨이**합니다. RAS 게이트웨이 모든 조합이 다음 게이트웨이 기능을 제공합니다.  
  
-   **사이트에 게이트웨이**  
  
    RAS 게이트웨이 테두리 게이트웨이 프로토콜 (BGP)를 사용 하면-가능, 넌 게이트웨이 사용자 테 넌 액세스 하 고 원격 사이트에서 VPN 연결에 사이트를 통해 자신의 리소스를 관리할 수 있도록 해 주는 및 가상 리소스는 클라우드와 테 실제 네트워크에서 사이의 교통 흐름 네트워크를 사용할 수 있는 합니다. RAS 게이트웨이 대 한 자세한 내용은 참조 [RAS 게이트웨이 높은 가용성](https://technet.microsoft.com/library/mt631692.aspx) 및 [RAS 게이트웨이](https://technet.microsoft.com/library/mt626650.aspx)합니다.  
  
-   **전달 게이트웨이**  
  
    가상 네트워크와 호스팅 공급자 실제 네트워크 사이의 RAS 게이트웨이 경로 교통 합니다. 예를 들어, 테 넌 만들기 하나 이상의 가상 네트워크 공유 호스팅 공급자에 실제 네트워크 리소스에 액세스 해야 하는 경우 전달 게이트웨이 가상 네트워크 사이의 필요한 서비스를 사용 하 여 가상 네트워크에서 작업 하는 사용자가 제공 하는 실제 네트워크 교통을 경로 수 있습니다. 자세한 내용은 참조 [RAS 게이트웨이 높은 가용성](https://technet.microsoft.com/library/mt631692.aspx) 및 [RAS 게이트웨이](https://technet.microsoft.com/library/mt626650.aspx)합니다.  
  
-   **GRE 터널 게이트웨이**  
  
    GRE 터널 사용 테 가상 네트워크와 외부 네트워크 연결이 기반 으로합니다. GRE 프로토콜 이면 간단 하 고 지원을 GRE은 대부분의 네트워크 디바이스에서 사용할 수 있으므로 해지기에 적합 터널링 데이터가 암호화 필요 하지 않습니다. (S2S) 터널 사이트의에서 지원 GRE 테 가상 네트워크와 테 외부 네트워크를 사용 하 여 여러 테 게이트웨이 사이의 전달의 문제가 해결 되었습니다. GRE 터널에 대 한 자세한 내용은 참조 [GRE Windows Server 2016에 터널링](https://technet.microsoft.com/library/dn765485.aspx)합니다.  
  
**BGP 라우팅 제어 평면**  
  
Hyper-v 네트워크 가상화 (HNV) 경로 컨트롤은 모든 고객이 주소 평면 경로 수행 하 고 학습 동적으로 업데이트 하 고 가상 네트워크에 있는 분산된 RAS 게이트웨이 라우터는 컨트롤 평면에서 논리, 중앙 집중식 엔터티입니다. 자세한 내용은 참조 [RAS 게이트웨이 높은 가용성](https://technet.microsoft.com/library/mt631692.aspx) 및 [RAS 게이트웨이](https://technet.microsoft.com/library/mt626650.aspx)합니다.  
  
**분산된 다중 테 방화벽**  
  
방화벽 가상 네트워크의 네트워크 계층을 보호합니다. 각 테 VM SDN vSwitch 포트에서 정책이 적용 됩니다. 모든 교통 흐름 보호: 이스트 서쪽 및 북쪽 사우스 합니다. 네트워크 컨트롤러 모든 관련 호스트에 배포 하는 정책 테 포털을 통해 전달 되 합니다. 분산된 다중 테 방화벽에 대 한 자세한 내용은 참조 [Datacenter 방화벽 개요](../../../sdn/technologies/network-function-virtualization/../../../sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)합니다.  
  


