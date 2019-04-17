---
ms.assetid: d92731f1-e4d8-4223-9b07-ca1f40bb0e1f
title: "연결이 끊긴 Namespace"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ac231dbfbaaeafa39199e29a1744d84d5cec23e8
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="disjoint-namespace"></a>연결이 끊긴 Namespace

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

분리형 네임 하나 이상의 도메인 구성원 컴퓨터의 컴퓨터는 구성원 Active Directory 도메인 DNS 이름을 일치 하지 않는 한 주 서비스 DNS (도메인 이름) 접미사 있는 경우 발생 합니다. 예를 들어, corp.fabrikam.com의 주 DNS 접미사 na.corp.fabrikam.com 라는 Active Directory 도메인에 사용 하는 회원 컴퓨터 이름 공간을 사용 하는 합니다.  
  
이름 공간 관리를 유지 하 고, 보다 연속 네임 스페이스 문제를 해결 하려면 복잡해 집니다. 인접 네임 주 DNS 접미사 Active Directory 도메인 이름을 찾습니다. Active Directory 네임 모든 도메인 회원 컴퓨터에 대 한 기본 DNS 접미사 동일가 하다 고 생각 하 여 작성 된 네트워크 응용 프로그램이 분리형 네임에서 제대로 작동 하지 않습니다.  
  
## <a name="support-for-disjoint-namespaces"></a>연결이 끊긴 네임 스페이스에 대 한 지원  
도메인 회원 컴퓨터에서 도메인 컨트롤러 분리형 네임 스페이스에서 작동할 수 있습니다. 도메인 구성원 컴퓨터의 호스트 등록할 수 리소스 기록 및 IP (IPv6) 버전 6 (는) 호스트 분리 DNS 네임 스페이스에서 (AAAA) 리소스 레코드 합니다. 도메인 구성원 컴퓨터 리소스 레코드 이런 방법으로 등록 도메인 컨트롤러 계속 Active Directory 도메인 이름 동일 하 게 DNS 영역에서 전 세계와 사이트 관련 서비스 (SRV) 리소스 레코드를 등록 합니다.  
  
예를 들어 na.corp.fabrikam.com corp.fabrikam.com의 주 DNS 접미사를 사용 하 라는 Active Directory 도메인에 대 한 도메인 컨트롤러 호스트 (A) 및 IPv6 (AAAA) 호스트 리소스 레코드 corp.fabrikam.com DNS 영역에서 등록을 합니다. 도메인 컨트롤러 계속 등록 리소스 레코드 전 세계와 사이트 관련 서비스 (SRV) _msdcs. na.corp.fabrikam.com 및 na.corp.fabrikam.com DNS 영역에서 위치 서비스를 가능 하 게 하는 합니다.  
  
> [!IMPORTANT]  
> Windows 운영 체제 분리형 네임을 지원할 수 있지만 해당 환경에서 주 DNS 접미사 Active Directory 도메인 접미사 가정는를 작성 된 응용 프로그램이 작동 하지 않습니다. 이러한 이유로 테스트 해야 모든 프로그램과 해당 운영 체제의 신중 하 게 분리형 네임 배포 하기 전에 합니다.  
  
분리형 네임 작동 합니다 (및 지원 되는) 다음과 같은 경우에 다음과 같습니다.  
  
-   여러 Active Directory 도메인와 숲 단일 DNS 네임 DNS 영역 라고도 하는 사용 하는 경우  
  
    이러한 예로 na.corp.fabrikam.com, sa.corp.fabrikam.com asia.corp.fabrikam.com 등 이름으로 지역 도메인을 사용 하 고 단일 DNS 네임 corp.fabrikam.com 등 사용 하는 회사입니다.  
  
-   단일 Active Directory 도메인은 별도 DNS 네임으로 분할 때  
  
    이러한 예로 Active Directory 도메인 corp.contoso.com hr.corp.contoso.com, production.corp.contoso.com it.corp.contoso.com 등 DNS 영역을 사용 하는 회사입니다.  
  
분리형 네임 제대로 작동 하지 않습니다 (및 지원 되지 않습니다) 다음과 같은 경우에 다음과 같습니다.  
  
-   도메인 회원 사용 되는 분리형 접미사 일치 또는 다른 숲 속의 Active Directory 도메인 이름입니다. 이 Kerberos 이름 접미사 경로 중단 됩니다.  
  
-   동일한 분리형 접미사 다른 숲 속의 사용 됩니다. 이 숲 간에 다음이 접미사 고유 하 게 경로 수 없습니다.  
  
-   도메인 회원 인증 기관 (캐나다) 서버 변경을 완벽 하 게 한정 FQDN (도메인 이름) 캘리포니아 서버 회원 되어 있는 도메인 도메인 컨트롤러에서 사용 되는 동일한 기본 DNS 접미사 더 이상 사용할 수 있도록 합니다. 이 경우 인증서의 유효성을 검사 CRL 배포 포인트에서 어떤 DNS 이름을 사용에 따라 발급 캘리포니아 서버를 할 수 있습니다. 그러나 제대로 작동 및 지원 되는 분리형 안정적인 네임 스페이스에서 캘리포니아 서버를 배치 하는 경우 합니다.  
  
## <a name="considerations-for-disjoint-namespaces"></a>연결이 끊긴 네임 스페이스 사항  
다음과 같은 고려 이름 공간을 사용 해야 하는 경우 결정 하는 데 도움이 될 수 있습니다.  
  
### <a name="application-compatibility"></a>응용 프로그램 호환성  
설명한 것 처럼 분리형 네임 스페이스 응용 프로그램 및 컴퓨터 주 DNS 접미사는의 회원은는 도메인 이름 동일으로 작성 된 서비스에 문제가 발생할 수 있습니다. 분리형 네임 배포 하기 전에 응용 프로그램 호환성 문제를 확인 해야 합니다. 또한 분석 수행할 때 사용 하는 모든 응용 프로그램의 호환성을 확인 해야 합니다. Microsoft와 다른 소프트웨어 개발자 응용 프로그램 포함 됩니다.  
  
### <a name="advantages-of-disjoint-namespaces"></a>연결이 끊긴 네임 스페이스의 이점  
이름 공간을 사용 하 여 다음과 같은 이점 가질 수 있습니다.  
  
-   컴퓨터의 기본 DNS 접미사 다른 정보 나타낼 수를 있기 때문에 별도로 된 Active Directory 도메인 이름에서 DNS 네임을 관리할 수 있습니다.  
  
-   비즈니스 구조 또는 지리적 위치를 기반으로 DNS 네임을 구분할 수 있습니다. 예를 들어, 비즈니스 장치 이름을 또는 대륙, 국가/지역 또는 건물 등의 실제 위치를 기반으로 네임을 구분할 수 있습니다.  
  
### <a name="disadvantages-of-disjoint-namespaces"></a>단점 분리형 네임  
이름 공간을 사용 하 여 다음과 같은 단점 가질 수 있습니다.  
  
-   만들기 하 고 각 Active Directory 도메인 이름 공간을 사용 하는 회원 컴퓨터를가지고 있는 숲 속의에 대 한 별도 DNS 영역 관리 해야 합니다. (즉, 필요 더 복잡 한 추가 구성 합니다.)  
  
-   수정 하 고 관리할 도메인 회원 지정한, 기본 DNS 접미사 사용할 수 있도록 Active Directory 특성 수동 단계를 수행 해야 합니다.  
  
-   이름 해상도 최적화 하려면 수정 하 고 기본 대체 DNS 접미사도 구성원 컴퓨터 구성 하려면 그룹 정책 관리 수동 단계를 수행 해야 합니다.  
  
    > [!NOTE]  
    > 단일 레이블 이름을 확인 하 여이 단점은 오프셋 WINS ()는 Windows 인터넷 이름 서비스를 사용할 수 있습니다. WINS에 대 한 자세한 내용은 참조 기술 참조 WINS ([https://go.microsoft.com/fwlink/?LinkId=102303](https://go.microsoft.com/fwlink/?LinkId=102303)).  
  
-   귀하의 환경 필요 여러 기본 DNS 접미사 때 숲에서 DNS 접미사 검색 순서 모든 Active Directory 도메인에 대 한 적절 하 게 구성 해야 합니다.  
  
    DNS 접미사 검색 순서를 설정 하려면 그룹 정책 개체 또는 DHCP(Dynamic Host Configuration Protocol) (DHCP) 서버 서비스 매개 변수를 사용할 수 있습니다. 레지스트리를 수정할 수 있습니다.  
  
-   모든 응용 프로그램 호환성 문제에 대 한 테스트 주의 해야 합니다.  
  
수행할 수 있는 단계에 대 한 자세한 내용은이 단점을 해결 하기 위해 만들기 분리형 Namespace 참조 ([https://go.microsoft.com/fwlink/?LinkId=106638](https://go.microsoft.com/fwlink/?LinkId=106638)).  
  
### <a name="planning-a-namespace-transition"></a>계획 네임 전환  
네임 수정 하기 전에 다음과 같은 고려 연속 네임 분리형 네임 스페이스 (또는 반대)를 전환에 적용할 수 있는 검토 합니다.  
  
-   수동으로 구성 (Spn) 서비스 사용자 이름 수 이상 일치 하지 DNS 이름을 네임 변경 후 합니다. 이 인증 오류를 일으킬 수 있습니다.  
  
    자세한 내용은 참조 서비스 로그온 실패으로 인해 Spn 잘못 설정 ([https://go.microsoft.com/fwlink/?LinkId=102304](https://go.microsoft.com/fwlink/?LinkId=102304)).  
  
    -   제한 된 위임와 Windows Server 2003 기반 컴퓨터를 사용 하는 경우 해당 컴퓨터 Spn 변경 하는 추가 구성이 필요할 수 있습니다. 자세한 내용은 참조는 Microsoft 기술 자료 문서 936628 ([https://go.microsoft.com/fwlink/?LinkId=102306](https://go.microsoft.com/fwlink/?LinkId=102306)).  
  
    -   관리자 하위 Spn 수정할 수 있는 권한을 위임 하려는 경우 참조 수정 Spn 기관에 위임 ([https://go.microsoft.com/fwlink/?LinkId=106639](https://go.microsoft.com/fwlink/?LinkId=106639)).  
  
-   LDAP(Lightweight Directory Access Protocol) (LDAP)을 통해 소켓 SSL (Secure Layer) (LDAPS 라고도 함)에 연결 되지 않은 네임 구성 되어 있는 도메인 컨트롤러에 배포에서 캘리포니아도 사용 하는 경우 LDAPS 인증서를 구성할 때 적절 한 Active Directory 도메인 이름 및 주 DNS 접미사 사용 해야 합니다.  
  
    도메인 컨트롤러 인증서 요구 사항에 대 한 자세한 내용은 참조는 Microsoft 기술 자료 문서 321051 ([https://go.microsoft.com/fwlink/?LinkId=102307](https://go.microsoft.com/fwlink/?LinkId=102307)).  
  
    > [!NOTE]  
    > LDAPS에 인증서를 사용 하는 도메인 컨트롤러의 인증서 재배포 해야 할 수 있습니다. 이렇게 하면 도메인 컨트롤러를는 다시 시작 될 때까지 해당 인증서를 선택 하지 않을 수 있습니다. Windows Server 2003에 대 한 업데이트와 관련 된 LDAPS 인증에 대 한 자세한 내용은 참조는 Microsoft 기술 자료 문서 932834 ([https://go.microsoft.com/fwlink/?LinkId=102308](https://go.microsoft.com/fwlink/?LinkId=102308)).  
  
### <a name="planning-for-disjoint-namespace-deployments"></a>이름 공간 배포를 위해 계획  
컴퓨터에 연결 되지 않은 네임 있는 환경에서 배포 하는 경우 다음 예방 조치를 취하십시오.  
  
1.  테스트 고 분리형 네임 지원 해야 비즈니스를 수행 하는 모든 소프트웨어 공급을 알립니다. 연결이 끊긴 네임 스페이스 사용 하는 환경에서 응용 프로그램을 지원 하는지 확인 하도록 요청 합니다.  
  
2.  연결이 끊긴 네임 랩 환경에서 운영 체제 및 응용 프로그램의 모든 버전을 테스트 합니다. 이렇게 하면 이러한 권장 따르세요.  
  
    1.  귀하의 환경에 소프트웨어를 배포 하기 전에 모든 소프트웨어 문제를 해결 합니다.  
  
    2.  가능 하면 운영 체제 및 분리형 네임에 배포를 계획 하는 응용 프로그램의 베타 테스트에 참여 합니다.  
  
3.  관리자가 및 고객 지원 센터 직원 분리형 네임 및 미치는 영향에 알고 있는지 확인 합니다.  
  
4.  수 있게 해 주는 사용자 전환 연속 네임에 연결 되지 않은 네임에서 필요한 경우 옵션 만들기.  
  
5.  운영 체제와 응용 프로그램 공급자 분리형 네임 지원의 중요성을 배포 합니다.  
  


