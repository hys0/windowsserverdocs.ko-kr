---
ms.assetid: 824005ae-c3c1-459b-9baa-1660158918ab
title: "Federation 서버 만들어야 하는 경우"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 8013764b88a1061cfcaa3a507466c111bfd59aad
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="when-to-create-a-federation-server"></a>Federation 서버 만들어야 하는 경우

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Federation serverin Active Directory Federation Services \(AD FS\)를 만들 때 조직 수 있는 방법을 제공 합니다.  
  
-   Single\ sign\-켜 짐 웹에서 끼웁니다 \ (SSO\) – 다른 조직과 커뮤니케이션을 기반으로 \ (수도 있는 하나 이상의 federation server\) 및 조직에서 직원와 필요 시 \ (의 Internet\ 통해 누가 필요 액세스).  
  
-   전면 서비스를 사용 하 여 신원을 위임 인프라 서비스에 사용자가 가장 사용 하도록 설정 합니다. 자세한 내용은 참조 [시기를 사용 하 여 신원을 위임](When-to-Use-Identity-Delegation.md)합니다.  
  
다음 섹션에는 몇 가지 주요 결정 시간과 장소 하나 또는 여러 개의 federation 서버를 확인 하기 위한 설명 합니다.  
  
## <a name="determine-the-organizational-role-for-the-federation-server"></a>조직 역할 federation 서버에 대 한 확인  
새 federation 서버 만들어야 하는 경우에 대 한 합리적된 결정을 하려면 먼저 서버에 있는 조직에서 결정 해야 합니다. 조직에서 federation 서버를 수행 하는 역할 리소스 파트너 조직 또는 계정 파트너 조직에서 federation 서버 장소 있는지 여부에 따라 다릅니다.  
  
계정 파트너 회사 네트워크에 federation 서버 있을 때, 브라우저, 웹 서비스 또는 신원 선택기 클라이언트 사용자 자격 증명을 인증 보안 토큰 클라이언트를 전송 하의 역할이입니다. 자세한 내용은 참조 [계정 파트너에 해당 Federation 서버의 역할 검토](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md)합니다.  
  
리소스 파트너 회사 네트워크에 federation 서버 있을 때, 인증 보안 토큰 연합 서버 리소스 파트너 조직에서 발급 한에 따라 사용자의 역할은 또는 역할으로 구성 된 웹 응용 프로그램 또는 웹 서비스의 토큰 요청을 클라이언트 속해 있는 계정 파트너 조직 리디렉션합니다. 자세한 내용은 참조 [리소스 파트너에 해당 Federation 서버의 역할 검토](Review-the-Role-of-the-Federation-Server-in-the-Resource-Partner.md)합니다.  
  
## <a name="determine-which-ad-fs-design-to-deploy"></a>ADFS 디자인 배포 하는 확인  
다음 ADFS 디자인 중 하나에 배포 하려면 때마다 조직에서 federation 서버를 만듭니다.  
  
-   [웹 SSO 디자인](Web-SSO-Design.md)  
  
-   [연결 된 웹 SSO 디자인](Federated-Web-SSO-Design.md)  
  
필요한 경우 하면 두 계정 파트너 역할에서 및 리소스 파트너 역할에서을 작동할 수 있도록 웹 SSO 연방 디자인을 배포 하는 조직 단일 federation 서버를 구성할 수 있습니다. 이 경우 federation 서버 자신의 조직에서 사용자 계정에 따라 보안 설정 Markup Language \(SAML\) 토큰 발생할 수 있습니다 또는 기반으로 사용자의 계정이 있는 경로 조정 토큰 요청 조직에을 합니다.  
  
> [!NOTE]  
> 웹 SSO 연방 디자인에 대 한 계정 파트너의 하나 이상 federation 서버와 리소스 파트너에 하나 이상의 federation 서버 있어야 합니다.  
  
## <a name="differences-between-a-federation-server-and-a-federation-server-proxy"></a>Federation 서버와 federation 서버 프록시 사이의 차이  
Federation 서버 federation 서버 프록시 수행 하는 동일한 방식으로 웹 페이지 sign\에 정책, 인증, 및 검색을 사용할 수 있습니다. Federation 서버와 federation 서버 프록시 있는 주요 차이 연합 어떤 작업을 수행 해야 하는 federation 서버 프록시 수행할 수 없는 서버 수행할 수 있습니다.  
  
다음만 해당 federation 서버 수행할 수 있는 작업은 다음과 같습니다.  
  
-   Federation 서버 암호화 토큰 생성 하는 작업을 수행 합니다. Federation 서버 프록시 토큰을 만들 수 없는, 있지만 클라이언트 및, federation 서버에 다시 필요할 때 토큰 리디렉션합니다 하거나 경로 사용할 수 있습니다. Federation 서버 사용에 대 한 자세한 내용은 참조 [Federation 프록시 서버를 만들 때](When-to-Create-a-Federation-Server-Proxy.md)합니다.  
  
-   Federation 서버 클라이언트 회사의 네트워크에 대 한 통합 인증 Windows의 사용을 지원 federation 서버 프록시 하지 않습니다. Federation 서버와 통합 인증 Windows 사용에 대 한 자세한 내용은 참조 [Federation 서버 팜 만들어야 하는 경우](When-to-Create-a-Federation-Server-Farm.md)합니다.  
  
> [!CAUTION]  
> Federation 서버 및 구성 데이터베이스 SQL Server, SQL Server 특성 저장소, 도메인 컨트롤러 및 광고 LDS 인스턴스 간 통신 무결성 또는 기본적으로 보호 기밀성 아닙니다. 이러한 문제를 해결 하려면 이러한 서버 받는 또는 모든 이러한 서버 사이 물리적 보안 연결을 사용 하 여 간의 통신 채널을 보호 하는 것이 좋습니다. Federation 서버와 SQL server 간 통신에 대 한 연결 문자열에서 SSL 보호를 사용 하는 것이 좋습니다. 도메인 컨트롤러 federation 서버와 연결을 Kerberos 서명 및 암호화를 설정 하는 것이 좋습니다. Ldap, LDAP\/S에 대 한 광고 LDS\/AD DS 지원 되지 않습니다.  
  
## <a name="how-to-create-a-federation-server"></a>Federation 서버를 만드는 방법  
AD FS Federation 서버 구성 마법사 또는 Fsconfig.exe command\ 선 도구를 사용 하 여 federation 서버를 만들 수 있습니다. 이러한 도구를 사용 하면 federation 서버를 만들려면 다음 옵션 중 하나를 선택할 수 있습니다.  
  
-   Stand\만 federation 서버 만들기  
  
    Stand\만 federation 서버를 설정 하는 방법에 대 한 자세한 내용은 참조 [독립 실행형 Federation 서버를 만들](../../ad-fs/deployment/Create-a-Stand-Alone-Federation-Server.md)합니다.  
  
-   첫 번째 federation 서버 federation 서버 팜에서 만들기  
  
    첫 번째 federation server를 설정 하거나 federation 서버 농장을 추가 하는 방법에 대 한 자세한 내용은 참조 [Federation 서버 농장의 첫 번째 Federation 서버를 만들](../../ad-fs/deployment/Create-the-First-Federation-Server-in-a-Federation-Server-Farm.md)합니다.  
  
-   Federation 서버 federation 서버 팜을 추가  
  
    Federation 서버 농장을 추가 하는 방법에 대 한 자세한 내용은 참조 [Federation 서버 Federation 서버 팜을 추가](../../ad-fs/deployment/Add-a-Federation-Server-to-a-Federation-Server-Farm.md)합니다.  
  
자세한 이러한 방법이 효과가 방법에 대 한 정보를 참조 [AD FS 구성 데이터베이스의 The 역할](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)합니다.  
  
Federation 서버를 배포 하는 데 필요한 모든 필수 항목을 설정 하는 방법에 대 한 자세한 내용은 참조 [검사: Federation 서버 설정을](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md)합니다.  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)

