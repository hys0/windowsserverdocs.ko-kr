---
ms.assetid: 824005ae-c3c1-459b-9baa-1660158918ab
title: 페더레이션 서버를 만들어야 하는 경우
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 91c260dad1bd260a7dad7320fecd15e6472c50a3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407887"
---
# <a name="when-to-create-a-federation-server"></a>페더레이션 서버를 만들어야 하는 경우

Active Directory Federation Services \(AD FS\)에서 페더레이션 serverin 만들 때 조직에서 다음을 수행할 수 있는 방법을 제공 합니다.  
  
-   페더레이션 서버를 하나 이상 포함 하는 다른 조직 \(와 필요한 경우 인터넷\)을 통해 액세스 해야 하는 조직의 직원을 \(하는 다른 조직\)와 \(SSO\)기반 통신에 대 한 웹 single\-sign\-에 참여 합니다.  
  
-   프론트 엔드 서비스가 ID 위임을 사용하여 인프라 서비스에 사용자를 가장. 자세한 내용은 [When to Use Identity Delegation](When-to-Use-Identity-Delegation.md)를 참조하세요.  
  
다음 섹션에서는 하나 이상의 페더레이션 서버를 만들 시기 및 위치를 결정 하기 위한 몇 가지 주요 결정 사항에 대해 설명 합니다.  
  
## <a name="determine-the-organizational-role-for-the-federation-server"></a>페더레이션 서버에 대한 조직 역할 확인  
새 페더레이션 서버를 만들 시기에 대 한 의사 결정을 내리는 데 먼저 서버가 상주할 조직을 결정 해야 합니다. 페더레이션 서버가 조직에서 수행 하는 역할은 계정 파트너 조직 또는 리소스 파트너 조직에 페더레이션 서버를 배치할지 여부에 따라 달라 집니다.  
  
페더레이션 서버가 계정 파트너의 회사 네트워크에 배치 된 경우 해당 역할은 브라우저, 웹 서비스 또는 id 선택기 클라이언트의 사용자 자격 증명을 인증 하 고 클라이언트에 보안 토큰을 보내는 것입니다. 자세한 내용은 참조 [검토 하는 계정 파트너의 페더레이션 서버 역할을](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md)합니다.  
  
페더레이션 서버가 리소스 파트너의 회사 네트워크에 배치 된 경우 해당 역할은 리소스 파트너 조직의 페더레이션 서버에서 발급 한 보안 토큰에 따라 사용자를 인증 하거나, 해당 역할은에서 토큰 요청을 리디렉션하는 것입니다. 클라이언트가 속한 계정 파트너 조직에 웹 응용 프로그램 또는 웹 서비스를 구성 했습니다. 자세한 내용은 [Review the Role of the Federation Server in the Resource Partner](Review-the-Role-of-the-Federation-Server-in-the-Resource-Partner.md)를 참조하세요.  
  
## <a name="determine-which-ad-fs-design-to-deploy"></a>배포할 AD FS 디자인 확인  
다음 AD FS 디자인을 배포 하려는 경우 언제 든 지 조직에서 페더레이션 서버를 만듭니다.  
  
-   [웹 SSO 디자인](Web-SSO-Design.md)  
  
-   [페더레이션된 웹 SSO 디자인](Federated-Web-SSO-Design.md)  
  
필요한 경우 페더레이션된 웹 SSO 디자인을 배포 하는 조직은 계정 파트너 역할과 리소스 파트너 역할 모두에서 작동 하도록 단일 페더레이션 서버를 구성할 수 있습니다. 이 경우 페더레이션 서버는 사용자 계정이 상주 하는 위치에 따라 조직에 대 한 토큰 요청을 다시 라우팅하는 자체 조직의 사용자 계정에 따라 SAML\) 토큰 \(Security Assertion Markup Language 생성할 수 있습니다.  
  
> [!NOTE]  
> 페더레이션된 웹 SSO 디자인의 경우 계정 파트너에 하나 이상의 페더레이션 서버가 있어야 하 고 리소스 파트너에 하나 이상의 페더레이션 서버가 있어야 합니다.  
  
## <a name="differences-between-a-federation-server-and-a-federation-server-proxy"></a>페더레이션 서버와 페더레이션 서버 프록시 간의 차이점  
페더레이션 서버는 페더레이션 서버 프록시를 사용 하는 것과 같은 방식으로, 정책, 인증 및 검색의 서명\-에 대 한 웹 페이지를 제공할 수 있습니다. 페더레이션 서버와 페더레이션 서버 프록시 간의 주요 차이점은 페더레이션 서버가 페더레이션 서버에서 수행할 수 없는 작업을 수행할 수 있는 작업을 수행 해야 합니다.  
  
페더레이션 서버 에서만 수행할 수 있는 작업은 다음과 같습니다.  
  
-   페더레이션 서버는 토큰을 생성 하는 암호화 작업을 수행 합니다. 페더레이션 서버 프록시는 토큰을 생성할 수 없지만 토큰을 클라이언트에 라우트 또는 리디렉션하는 데 사용할 수 있으며, 필요한 경우 페더레이션 서버로 다시 리디렉션할 수 있습니다. 페더레이션 서버를 사용 하는 방법에 대 한 자세한 내용은 [When To Create a Federation Server Proxy](When-to-Create-a-Federation-Server-Proxy.md)항목을 참조 하세요.  
  
-   페더레이션 서버는 회사 네트워크의 클라이언트에 대해 Windows 통합 인증을 사용할 수 있도록 지원 합니다. 페더레이션 서버 프록시는 그렇지 않습니다. 페더레이션 서버에 Windows 통합 인증을 사용 하는 방법에 대 한 자세한 내용은 [When To Create a Federation Server Farm](When-to-Create-a-Federation-Server-Farm.md)항목을 참조 하세요.  
  
> [!CAUTION]  
> 페더레이션 서버와 SQL 서버 구성 데이터베이스, SQL 서버 특성 저장소, 도메인 컨트롤러 및 AD LDS 인스턴스와의 통신은 기본적으로 무결성 또는 기밀성이 보호되지 않습니다. 이를 완화 하려면 IPSEC을 사용 하거나 이러한 서버 간에 물리적으로 안전한 연결을 사용 하 여 이러한 서버 간에 통신 채널을 보호 하는 것이 좋습니다. 페더레이션 서버와 SQL server 간 통신의 경우 연결 문자열에서 SSL 보호를 사용 하는 것이 좋습니다. 페더레이션 서버와 도메인 컨트롤러 간 연결의 경우 Kerberos 서명 및 암호화를 설정 하는 것이 좋습니다. LDAP의 경우 AD LDS\/AD DS에 대해 LDAP\/S이 (가) 지원 되지 않습니다.  
  
## <a name="how-to-create-a-federation-server"></a>페더레이션 서버를 만드는 방법  
페더레이션 서버는 AD FS 페더레이션 서버 구성 마법사나 Fsconfig 명령\-줄 도구를 사용 하 여 만들 수 있습니다. 이러한 도구 중 하나를 사용하는 경우 다음 옵션 중 하나를 선택하여 페더레이션 서버를 만들 수 있습니다.  
  
-   스탠드 만들기\-만 페더레이션 서버  
  
    독립\-단독 페더레이션 서버를 설정 하는 방법에 대 한 자세한 내용은 [독립 실행형 페더레이션 서버 만들기](../../ad-fs/deployment/Create-a-Stand-Alone-Federation-Server.md)를 참조 하세요.  
  
-   페더레이션 서버 팜의 첫 번째 페더레이션 서버 만들기  
  
    첫 번째 페더레이션 서버를 설정 또는 페더레이션 서버 팜에 추가 하는 방법에 대 한 자세한 내용은 참조 하세요. [페더레이션 서버 팜의 첫 번째 페더레이션 서버 만들기](../../ad-fs/deployment/Create-the-First-Federation-Server-in-a-Federation-Server-Farm.md)합니다.  
  
-   페더레이션 서버 팜에 페더레이션 서버 추가  
  
    페더레이션 서버를 팜에 추가하는 방법에 대한 자세한 내용은 [Add a Federation Server to a Federation Server Farm](../../ad-fs/deployment/Add-a-Federation-Server-to-a-Federation-Server-Farm.md)를 참조하세요.  
  
이러한 각 옵션 작업에 대한 자세한 내용은 [The Role of the AD FS Configuration Database](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)를 참조하세요.  
  
페더레이션 서버를 배포하는 데 필요한 모든 필수 구성 요소를 설정하는 방법에 대한 자세한 내용은 [Checklist: Setting Up a Federation Server](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)

