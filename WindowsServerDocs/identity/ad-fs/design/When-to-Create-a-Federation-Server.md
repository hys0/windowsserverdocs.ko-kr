---
ms.assetid: 824005ae-c3c1-459b-9baa-1660158918ab
title: 페더레이션 서버를 만들어야 하는 경우
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 7e61c734780baa1482670af3f24697c10345b292
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190593"
---
# <a name="when-to-create-a-federation-server"></a>페더레이션 서버를 만들어야 하는 경우

페더레이션 serverin Active Directory Federation Services를 만들면 \(AD FS\), 조직 수 있는 수단을 제공 합니다.  
  
-   웹 단일에서 참여\-기호\-에 \(SSO\)-다른 조직 통신할 기반 \(역시 하나 이상의 페더레이션 서버\) 와 사용 하 여 필요한 경우는 조직에서 직원 \(인터넷을 통해 액세스 해야 하는\)합니다.  
  
-   프론트 엔드 서비스가 ID 위임을 사용하여 인프라 서비스에 사용자를 가장. 자세한 내용은 [When to Use Identity Delegation](When-to-Use-Identity-Delegation.md)를 참조하세요.  
  
다음 섹션에서는 시기 및 하나 이상의 페더레이션 서버를 만들 위치를 결정 하기 위한 주요 결정 사항 중 일부를 설명 합니다.  
  
## <a name="determine-the-organizational-role-for-the-federation-server"></a>페더레이션 서버에 대한 조직 역할 확인  
새 페더레이션 서버를 만들어야 하는 경우에 대 한 합리적된 결정을 하려면 먼저 서버에 있는 어떤 조직에서 결정 해야 합니다. 페더레이션 서버는 조직에서 수행 하는 역할 계정 파트너 조직 또는 리소스 파트너 조직의 페더레이션 서버를 배치 하는지 여부에 따라 달라 집니다.  
  
페더레이션 서버를 계정 파트너의 회사 네트워크에 배치 하면 해당 역할 브라우저, 웹 서비스 또는 id 선택기 클라이언트의 사용자 자격 증명을 인증 하 고 클라이언트에 보안 토큰을 전송 방법은입니다. 자세한 내용은 참조 [검토 하는 계정 파트너의 페더레이션 서버 역할을](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md)합니다.  
  
페더레이션 서버는 리소스 파트너의 회사 네트워크에 배치 하는 경우 그 역할은 사용자, 리소스 파트너 조직의 페더레이션 서버에서 발급 한 보안 토큰 기반 인증 또는 해당 역할의 토큰 요청을 리디렉션하는 것이 웹 응용 프로그램 또는 클라이언트가 속한 계정 파트너 조직에 웹 서비스를 구성 합니다. 자세한 내용은 [Review the Role of the Federation Server in the Resource Partner](Review-the-Role-of-the-Federation-Server-in-the-Resource-Partner.md)를 참조하세요.  
  
## <a name="determine-which-ad-fs-design-to-deploy"></a>배포할 AD FS 디자인 확인  
다음 AD FS 디자인 배포 하려고 할 때마다 조직에서 페더레이션 서버를 만듭니다.  
  
-   [웹 SSO 디자인](Web-SSO-Design.md)  
  
-   [페더레이션된 웹 SSO 디자인](Federated-Web-SSO-Design.md)  
  
필요한 경우 페더레이션된 웹 SSO 디자인을 배포 하는 조직이 리소스 파트너 역할 및 계정 파트너 역할에 둘 다에서 작동할 수 있도록 단일 페더레이션 서버를 구성할 수 있습니다. 이 경우 페더레이션 서버 Security Assertion Markup Language 발생할 \(SAML\) 토큰, 자체 조직 또는 조직에 경로 전환 토큰 요청에서 사용자 계정을 기반으로 사용자 계정이 있는 기준 .  
  
> [!NOTE]  
> 페더레이션된 웹 SSO 디자인에 대 한 계정 파트너에서 하나 이상의 페더레이션 서버 및 리소스 파트너에 페더레이션 서버를 하나 이상 있어야 합니다.  
  
## <a name="differences-between-a-federation-server-and-a-federation-server-proxy"></a>페더레이션 서버와 페더레이션 서버 프록시 간의 차이점  
페더레이션 서버 로그인에 대 한 웹 페이지 사용할 수 있습니다\-에서는 정책, 인증 및 페더레이션 서버 프록시는 동일한 방식으로 검색 합니다. 페더레이션 서버 및 페더레이션 서버 프록시 간의 주요 차이점 작업을 수행 해야 작업을 사용 하 여 페더레이션 서버가 페더레이션 서버 프록시를 수행할 수 없습니다를 수행할 수 있습니다.  
  
다음은 페더레이션 서버 에서만 수행할 수 있는 작업입니다.  
  
-   페더레이션 서버는 토큰을 생성 하는 암호화 작업을 수행 합니다. 페더레이션 서버 프록시는 토큰을 생성할 수 없습니다, 있지만를 라우팅할지 또는 클라이언트를 페더레이션 서버에 필요한 경우 토큰 리디렉션 사용 수 있습니다. 페더레이션 서버를 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [페더레이션 서버 프록시를 만들어야 하는 경우](When-to-Create-a-Federation-Server-Proxy.md)합니다.  
  
-   페더레이션 서버는 회사 네트워크에서 클라이언트에 대 한 Windows 통합 인증 사용을 지원 페더레이션 서버 프록시는 그렇지 않습니다. 페더레이션 서버를 사용 하 여 Windows 통합 인증을 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [페더레이션 서버 팜을 만들어야 하는 경우](When-to-Create-a-Federation-Server-Farm.md)합니다.  
  
> [!CAUTION]  
> 페더레이션 서버와 SQL 서버 구성 데이터베이스, SQL 서버 특성 저장소, 도메인 컨트롤러 및 AD LDS 인스턴스와의 통신은 기본적으로 무결성 또는 기밀성이 보호되지 않습니다. 이 문제를 완화하려면 이러한 모든 서버 간에 IPSEC 또는 물리적인 보안 연결을 사용하여 통신 채널을 보호해 보세요. 페더레이션 서버와 SQL 서버 간 통신의 경우 연결 문자열에서 SSL 보호를 사용해 보세요. 페더레이션 서버와 도메인 컨트롤러 간 연결의 경우 Kerberos 서명 및 암호화를 설정해 보세요. Ldap의 경우 LDAP\/AD LDS가 지원 되지 않습니다\/AD DS 합니다.  
  
## <a name="how-to-create-a-federation-server"></a>페더레이션 서버를 만드는 방법  
AD FS 페더레이션 서버 구성 마법사 또는 Fsconfig.exe 명령을 사용 하 여 페더레이션 서버를 만들 수 있습니다\-명령줄 도구입니다. 이러한 도구 중 하나를 사용하는 경우 다음 옵션 중 하나를 선택하여 페더레이션 서버를 만들 수 있습니다.  
  
-   스탠드 만들기\-만 페더레이션 서버  
  
    대기 모드를 설정 하는 방법에 대 한 자세한 내용은\-만 페더레이션 서버를 참조 하세요 [독립 실행형 페더레이션 서버를 만드는](../../ad-fs/deployment/Create-a-Stand-Alone-Federation-Server.md)합니다.  
  
-   페더레이션 서버 팜의 첫 번째 페더레이션 서버 만들기  
  
    첫 번째 페더레이션 서버를 설정 또는 페더레이션 서버를 팜에 추가하는 방법에 대한 자세한 내용은 [Create the First Federation Server in a Federation Server Farm](../../ad-fs/deployment/Create-the-First-Federation-Server-in-a-Federation-Server-Farm.md)를 참조하세요.  
  
-   페더레이션 서버 팜에 페더레이션 서버 추가  
  
    페더레이션 서버를 팜에 추가하는 방법에 대한 자세한 내용은 [Add a Federation Server to a Federation Server Farm](../../ad-fs/deployment/Add-a-Federation-Server-to-a-Federation-Server-Farm.md)를 참조하세요.  
  
이러한 각 옵션 작업에 대한 자세한 내용은 [The Role of the AD FS Configuration Database](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)를 참조하세요.  
  
페더레이션 서버를 배포 하는 데 필요한 모든 필수 구성 요소를 설정 하는 방법에 대 한 자세한 내용은 참조 하세요. [검사 목록: 페더레이션 서버를 설정할](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md)합니다.  
  
## <a name="see-also"></a>관련 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)

