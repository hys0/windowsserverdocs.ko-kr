---
ms.assetid: d92731f1-e4d8-4223-9b07-ca1f40bb0e1f
title: 연결되지 않은 네임 스페이스
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0a2e911e889343b05a515c94e615d3648289f2df
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883574"
---
# <a name="disjoint-namespace"></a>연결되지 않은 네임 스페이스

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

비연속 네임 스페이스를 하나 이상의 도메인 구성원 컴퓨터는 컴퓨터를 구성원 인 Active Directory 도메인의 DNS 이름을 일치 하지 않는 기본 서비스 DNS (도메인 이름) 접미사 경우 발생 합니다. 예를 들어 na.corp.fabrikam.com 이라는 Active Directory 도메인에서 corp.fabrikam.com 이라는 주 DNS 접미사를 사용 하는 구성원 컴퓨터는 비연속 네임 스페이스를 사용 하 여 합니다.  
  
비연속 네임 스페이스를 관리, 유지 및 연속 네임 스페이스 보다 문제를 해결 하는 것이 복잡해 집니다. 연속 네임 스페이스, 주 DNS 접미사가 Active Directory 도메인 이름과 일치 합니다. Active Directory 네임 스페이스는 모든 도메인 구성원 컴퓨터에 대 한 주 DNS 접미사와 동일한 것으로 가정 하에 기록 되는 네트워크 응용 프로그램에서 비연속 네임 스페이스를 제대로 작동 하지 않습니다.  
  
## <a name="support-for-disjoint-namespaces"></a>비연속 네임 스페이스에 대 한 지원  
도메인 컨트롤러를 포함 하 여, 도메인 구성원 컴퓨터는 비연속 네임 스페이스에서 작동할 수 있습니다. 도메인 구성원 컴퓨터는 해당 호스트를 등록할 수 있습니다 (A) 리소스 레코드 및 IP 버전 6(ipv6) 호스트 (AAAA) 리소스 레코드 비연속 DNS 네임 스페이스에 있습니다. 이러한 방식으로 해당 리소스 레코드를 등록 하는 도메인 구성원 컴퓨터, 도메인 컨트롤러와 Active Directory 도메인 이름이 동일한 DNS 영역에 전역 및 사이트 관련 서비스 (SRV) 리소스 레코드를 등록 하려면 계속 합니다.  
  
예를 들어 corp.fabrikam.com 이라는 주 DNS 접미사를 사용 하는 na.corp.fabrikam.com 이라는 Active Directory 도메인에 대 한 도메인 컨트롤러 호스트 (A) 및 IPv6 호스트 (AAAA) 리소스 레코드 corp.fabrikam.com 이라는 DNS 영역에 등록 하는 것으로 가정 합니다. 서비스 위치 수 있게 하는 _msdcs.na.corp.fabrikam.com 및 na.corp.fabrikam.com DNS 영역에서 전역 및 사이트 관련 서비스 (SRV) 리소스 레코드를 등록 하려면 도메인 컨트롤러를 계속 합니다.  
  
> [!IMPORTANT]  
> Windows 운영 체제에서 비연속 네임 스페이스를 지원할 수 있지만 주 DNS 접미사가 Active Directory 도메인 접미사와 동일한 것으로 가정 합니다에 작성 된 응용 프로그램이 이러한 환경에서 작동 하지 않습니다. 이러한 이유로 테스트 해야 모든 응용 프로그램 및 해당 운영 체제 신중 하 게 비연속 네임 스페이스를 배포 하기 전에 합니다.  
  
비연속 네임 스페이스를 정상적으로 수행 (및 지원 되는) 다음과 같은 상황에서:  
  
-   여러 Active Directory 도메인이 있는 포리스트를 단일 DNS 네임 스페이스 라고도 DNS 영역을 사용 하는 경우  
  
    이러한 예로 corp.fabrikam.com 같은 단일 DNS 네임 스페이스와 na.corp.fabrikam.com와 sa.corp.fabrikam.com, asia.corp.fabrikam.com 이름의 지역 도메인을 사용 하는 회사입니다.  
  
-   단일 Active Directory 도메인에 별도 DNS 네임 스페이스에 분할 되어 있을 때  
  
    이 예제는 it.corp.contoso.com hr.corp.contoso.com와 production.corp.contoso.com, DNS 영역을 사용 하는 corp.contoso.com의 Active Directory 도메인을 회사입니다.  
  
비연속 네임 스페이스를 제대로 작동 하지 않습니다 (및 지원 되지 않습니다) 다음과 같은 경우:  
  
-   도메인 멤버에서 사용 하는 연결 되지 않은 접미사가 또는 다른 포리스트에 있는 Active Directory 도메인 이름을 찾습니다. 이 Kerberos 이름 접미사 라우팅이 중단 됩니다.  
  
-   다른 포리스트의 동일한 비연속 접미사가 사용 됩니다. 이 포리스트 간에 이러한 접미사를 고유 하 게 라우팅 것을 방지 합니다.  
  
-   변경 되 면 도메인 멤버 인증 기관 (CA) 서버는 정규화 된 도메인 이름 (FQDN) CA 서버를 구성원 도메인의 도메인 컨트롤러에서 사용 되는 동일한 주 DNS 접미사를 사용 하지 않도록 합니다. 이 경우 발급 된 CRL 배포 지점에서 어떤 DNS 이름이 사용 됩니다에 따라 CA 서버 인증서의 유효성을 검사를 할 수 있습니다. 하지만 안정적인 비연속 네임 스페이스에는 CA 서버를 배치 하는 경우 제대로 작동 하 고 지원 됩니다.  
  
## <a name="considerations-for-disjoint-namespaces"></a>비연속 네임 스페이스에 대 한 고려 사항  
다음 고려 사항을 비연속 네임 스페이스를 사용할지 여부를 결정 하는 데 도움이 될 수 있습니다.  
  
### <a name="application-compatibility"></a>응용 프로그램 호환성  
언급 한 대로 비연속 네임 스페이스에는 모든 응용 프로그램 및 컴퓨터의 주 DNS 접미사가 구성원으로 속한 도메인의 이름을 동일한 것으로 가정 합니다에 기록 되는 서비스에 대 한 문제가 발생할 수 있습니다. 비연속 네임 스페이스를 배포 하기 전에 호환성 문제에 대 한 응용 프로그램을 확인 해야 합니다. 또한 분석을 수행할 때 사용 하는 모든 응용 프로그램의 호환성을 확인 해야 합니다. 응용 프로그램에서 Microsoft 및 다른 소프트웨어 개발자가 포함 됩니다.  
  
### <a name="advantages-of-disjoint-namespaces"></a>비연속 네임 스페이스의 장점  
비연속 네임 스페이스를 사용 하 여 다음과 같은 이점을 가질 수 있습니다.  
  
-   컴퓨터의 주 DNS 접미사는 다른 정보를 나타낼 수 있습니다, 때문에 Active Directory 도메인 이름에서 DNS 네임 스페이스를 개별적으로 관리할 수 있습니다.  
  
-   비즈니스 구조 또는 지리적 위치 기반 DNS 네임 스페이스를 구분할 수 있습니다. 예를 들어, 대륙, 국가/지역 또는 빌드 같은 물리적 위치 또는 비즈니스 단위 이름에 따라 네임 스페이스를 구분할 수 있습니다.  
  
### <a name="disadvantages-of-disjoint-namespaces"></a>비연속 네임 스페이스의 단점  
비연속 네임 스페이스를 사용 하 여 다음과 같은 단점이 있습니다 포함할 수 있습니다.  
  
-   만들기 및 각 Active Directory 도메인 포리스트에 있는 비연속 네임 스페이스를 사용 하는 구성원 컴퓨터에 대 한 별도 DNS 영역을 관리 해야 합니다. (즉,이 추가 하 고 더 복잡 한 구성이 필요합니다.)  
  
-   수정 하 고 지정 된, 주 DNS 접미사를 사용 하도록 도메인 구성원이 수 있도록 Active Directory 특성을 관리 하는 수동 단계를 수행 해야 합니다.  
  
-   이름 확인을 최적화 하려면 수정 하 고 대체 주 DNS 접미사를 사용 하 여 구성원 컴퓨터를 구성 하려면 그룹 정책 유지 관리 하는 수동 단계를 수행 해야 합니다.  
  
    > [!NOTE]  
    > 단일 레이블 이름을 확인 하 여 이러한 단점이 오프셋 하는 Windows 인터넷 이름 서비스 WINS ()를 사용할 수 있습니다. WINS에 대 한 자세한 내용은 참조 WINS 기술 참조 ([https://go.microsoft.com/fwlink/?LinkId=102303](https://go.microsoft.com/fwlink/?LinkId=102303)).  
  
-   환경의 여러 주 DNS 접미사를 필요한 경우 포리스트의 모든 Active Directory 도메인에 대 한 DNS 접미사 검색 순서를 적절 하 게 구성 해야 합니다.  
  
    DNS 접미사 검색 순서를 설정 하려면 그룹 정책 개체 또는 동적 호스트 구성 프로토콜 (DHCP) 서버 서비스 매개 변수를 사용할 수 있습니다. 또한 레지스트리를 수정할 수 있습니다.  
  
-   모든 응용 프로그램 호환성 문제에 대해 신중 하 게 테스트 해야 합니다.  
  
수행할 수 있는 단계에 대 한 자세한 정보를 이러한 단점을 해결 하기 위해 만들기 비연속 Namespace 참조 ([https://go.microsoft.com/fwlink/?LinkId=106638](https://go.microsoft.com/fwlink/?LinkId=106638)).  
  
### <a name="planning-a-namespace-transition"></a>네임 스페이스 전환 계획  
네임 스페이스를 수정 하기 전에 전환 비연속 네임 스페이스 (또는 반대)를 연속 네임 스페이스에서 적용할 수 있는 다음 고려 사항을 검토 합니다.  
  
-   수동으로 구성 된 서비스 사용자 이름 (Spn)는 네임 스페이스 변경 된 후 DNS 이름의 더 이상 일치할 수 없습니다. 이 인증 오류가 발생할 수 있습니다.  
  
    자세한 내용은 참조 서비스 로그온 실패로 인해 잘못 설정 된 Spn ([https://go.microsoft.com/fwlink/?LinkId=102304](https://go.microsoft.com/fwlink/?LinkId=102304)).  
  
    -   Windows Server 2003 기반 컴퓨터를 사용 하 여 제한 된 위임을 사용 하는 경우 해당 컴퓨터에는 Spn을 변경 하려면 추가 구성이 필요할 수 있습니다. 자세한 내용은 Microsoft 기술 자료에서 936628 문서를 참조 하세요. ([https://go.microsoft.com/fwlink/?LinkId=102306](https://go.microsoft.com/fwlink/?LinkId=102306)).  
  
    -   하위 관리자에 대 한 Spn을 수정 하는 권한을 위임 하려는 경우 수정 spn 위임 기관 참조 ([https://go.microsoft.com/fwlink/?LinkId=106639](https://go.microsoft.com/fwlink/?LinkId=106639)).  
  
-   도메인 컨트롤러는 비연속 네임 스페이스에 구성 된 배포에서 CA를 사용 하 여 LDAP Lightweight Directory Access Protocol ()를 통해 SSL Secure Sockets Layer () (LDAPS) 사용 하면 적절 한 Active Directory 도메인 이름을 사용 해야 하 고 주 DNS 접미사 LDAPS 인증서를 구성 합니다.  
  
    도메인 컨트롤러에 대 한 인증서 요구 사항에 대 한 자세한 내용은 Microsoft 기술 자료에서 321051 문서를 참조 하세요. ([https://go.microsoft.com/fwlink/?LinkId=102307](https://go.microsoft.com/fwlink/?LinkId=102307)).  
  
    > [!NOTE]  
    > LDAPS 인증서를 사용 하는 도메인 컨트롤러는 해당 인증서를 다시 배포 해야 할 수 있습니다. 이렇게 하면 다시 시작 될 때까지 도메인 컨트롤러 적절 한 인증서를 선택 하지 않을 수 있습니다. Windows Server 2003에 대 한 LDAPS 인증과 관련된 업데이트에 대 한 자세한 내용은 Microsoft 기술 자료에서 932834 문서를 참조 하세요. ([https://go.microsoft.com/fwlink/?LinkId=102308](https://go.microsoft.com/fwlink/?LinkId=102308)).  
  
### <a name="planning-for-disjoint-namespace-deployments"></a>비연속 네임 스페이스 배포 계획  
비연속 네임 스페이스가 있는 환경에서 컴퓨터를 배포 하는 경우 다음 예방 조치를 수행 합니다.  
  
1.  테스트 및 비연속 네임 스페이스를 지원 해야 합니다 비즈니스 사용자를 사용 하 여 수행 하는 모든 소프트웨어 공급 업체를 게 알립니다. 비연속 네임 스페이스를 사용 하는 환경에서 응용 프로그램을 지원 하는지 확인 하도록 요청 합니다.  
  
2.  비연속 네임 스페이스 랩 환경에서 모든 버전의 운영 체제 및 응용 프로그램을 테스트 합니다. 이렇게 하면 이러한 권장 사항을 따르세요.  
  
    1.  환경에 소프트웨어를 배포 하기 전에 모든 소프트웨어 문제를 해결 합니다.  
  
    2.  가능한 경우 운영 체제 및 비연속 네임 스페이스에서 배포 하려는 응용 프로그램의 베타 테스트에 참여 합니다.  
  
3.  관리자 및 지원 센터 직원 비연속 네임 스페이스 및 해당 영향의 인식 되는지 확인 합니다.  
  
4.  수 있도록 하는 수에 대 한 전환 연속 네임 스페이스에 연결 되지 않은 네임 스페이스에서 필요한 경우 계획을 만듭니다.  
  
5.  비연속 네임 스페이스 지원과 운영 체제 및 응용 프로그램 공급자의 중요성을 교육 합니다.  
  


