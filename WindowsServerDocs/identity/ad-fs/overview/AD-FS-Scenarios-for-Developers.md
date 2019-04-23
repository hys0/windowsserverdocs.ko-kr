---
ms.assetid: 8a64545b-16bd-4c13-a664-cdf4c6ff6ea0
title: 개발자를 위한 AD FS 시나리오
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: a2a88608f3989522b1ec1c123f29bd679db7e318
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877944"
---
# <a name="ad-fs-scenarios-for-developers"></a>개발자를 위한 AD FS 시나리오

>적용 대상: Windows Server 2016

Windows Server 2016 [AD FS 2016]에서 AD FS를 사용 하면 업계 표준 OpenID Connect 및 OAuth 2.0 인증 및 권한 부여를 개발 하는 응용 프로그램에 기반을 추가 하 고 AD FS에 대해 직접 사용자를 인증 하는 응용 프로그램이 이러한 수 있습니다.    
  
AD FS 2016에서는 Ws-federation, Ws-trust 및 SAML 프로토콜 및 프로필에서는 지원 되는 이전 버전에서입니다.  이러한 프로토콜에 대 한 개발자 지침에 관심이 있는 경우 문서를 참조 하십시오.  이 문서 사용 되었으며 최신 프로토콜 지원을 활용 하는 방법을 중점적으로 설명 합니다.  
  
## <a name="why-modern-authentication"></a>왜 최신 인증  
사용 하 여 AD FS 로그인에 대 한 Ws-federation과 계속할 수 있지만 Ws-trust 및 SAML 프로토콜 하듯이 가지는 다음과 같은 이점을 얻게 최신 프로토콜을 사용 하기 전에  
  
* **단순 성과 일관성**  
    * Api의 동일한 집합을 사용 하 고 사용 하도록 설정 하는 패턴에 대 한 로그온 합니다.   
        *   여러 종류의 응용 프로그램 (서버, 데스크톱, 모바일, 브라우저)  
        *   여러 플랫폼 (android, iOS, Windows)  
        *   회사 네트워크 내에서 응용 프로그램 또는 클라우드에서 호스팅  
    * 이미 Azure AD에 대해 사용자 인증을 사용할 수 있는 동일한 집합을 사용 하 여  
* **유연성**  
    * 표준 사용자 권한 부여 외에도 더 복잡 한 시나리오와 같은 사용:      
        * ? 하나의 웹 응용 프로그램이 나 다른 웹 응용 프로그램 또는 서비스에 상주 하는 리소스에 액세스 하는 서비스 사용자 권한을 부여 하는 흐름에 3 다리 기호입니다.    
        * ? 중간 계층 서비스를 백 엔드 API를 액세스 하는 서버 간 흐름  
        * ? JavaScript 기반 단일 페이지 응용 프로그램 (SPA)  
* **업계 지원**  
    * OAuth 2.0 및 OpenID Connect 즐길 넓은 사용률 업계 전체에서 이러한 패턴의 정보를 사용 하면 인증 및 권한 부여는 Active Directory 환경 외부에서 사용할 수 있습니다.  
  
## <a name="how-it-works-the-basics"></a>작동 방법: 기본 사항  
AD FS 최신 인증을 사용 하 여 동일한 도구 및 Azure AD에 대해 사용자 인증을 이미 사용할 수 있는 응용 프로그램에 추가할 수 있습니다.   
  
AD FS 시나리오에서 물론 것은 AD FS와 하지 Azure AD id 공급자와 권한 부여 역할을 수행 하는 서버입니다.  그렇지 않으면 개념은 동일 합니다: 사용자는 자격 증명을 제공 하 고 직접 또는 중간 장치 리소스에 대 한 액세스를 통해 토큰을 가져옵니다.  
  
사용자 또는 웹 응용 프로그램에 액세스 하는 브라우저와 상호 작용 "리소스 소유자"의 가장 기본적인 시나리오 구성 됩니다.  
  
![개발자를 위한 AD FS](media/ADFS_DEV_1.png)  
  
웹 응용 프로그램 리소스에 액세스 토큰에 대 한 권한 부여 서버 (AD FS)에 대 한 요청을 시작 하기 때문에 "client" 라고 합니다.  리소스 웹 앱 자체에 의해 호스트 될 또는 웹 API의 임의 위치에서 네트워크 또는 인터넷으로 액세스할 수 있습니다.   사용자 또는 "리소스 소유자" 권한 부여 서버에 자격 증명을 제공 하 여 해당 액세스 토큰을 받는 클라이언트 웹 응용 프로그램에 권한을 부여 합니다.    
  
## <a name="how-it-works-components"></a>방법: 구성 요소  
OAuth 2.0 및 OpenID Connect 시나리오의 경우 AD FS 만들기는 동일한 집합의 도구 및 Azure AD는 id 공급자를 때 사용 해야 하는 라이브러리를 사용 합니다.  이러한 구성 요소는:  
* Active Directory 인증 라이브러리 (ADAL): 클라이언트 라이브러리는 쉽게 사용자 자격 증명을 수집, 만들기 및 토큰 요청을 제출 하 고 결과 토큰을 검색 합니다.    
* OWIN (Open Web Interface for.NET) 미들웨어입니다. OWIN 커뮤니티 기반의 프로젝트인 상태인 Microsoft 만들었습니다 일련의 서버 쪽 라이브러리는 웹 응용 프로그램 및 웹 OpenID Connect 및 OAuth 2.0을 사용 하 여 Api 보호에 대 한  
  
이러한 구성 요소의 역할 아래 다이어그램에 나와 있습니다.  
  
![개발자를 위한 AD FS](media/ADFS_DEV_2.png)  
  
## <a name="modeling-these-scenarios-in-ad-fs-2016"></a>AD FS 2016에서에서 이러한 시나리오의 모델링  
  
### <a name="application-groups"></a>응용 프로그램 그룹  
AD FS 정책에서 이러한 시나리오를 나타내기 위해 응용 프로그램 그룹 이라는 새로운 개념이 도입 되었습니다.  응용 프로그램 그룹은 모든 숫자 및 다음과 같은 기본 유형의 응용 프로그램의 조합을 포함할 수 있습니다.  
  
  
  
응용 프로그램 그룹 / 응용 프로그램 유형  |설명  |역할    
---------|---------|---------  
네이티브 응용 프로그램     |  공용 클라이언트 라고도 함,이 사용자 상호 작용 및 pc 또는 장치에서 실행 되는 클라이언트 앱으로 사용 됩니다.       | 리소스에 대 한 사용자 액세스 권한 부여 서버 (AD FS)의 토큰을 요청 합니다.  HTTP 헤더와 토큰을 사용 하는 보호 된 리소스에 HTTP 요청을 보냅니다.        
서버 응용 프로그램     |   웹 응용 프로그램 서버에서 실행 되며 일반적으로 브라우저를 통해 사용자가 액세스할 수 있습니다.  고유한 클라이언트 '암호' 또는 자격 증명을 유지 관리할 수 있기 때문에 기밀 클라이언트를 라고도 합니다.      | 리소스에 대 한 사용자 액세스 권한 부여 서버 (AD FS)의 토큰을 요청 합니다.  HTTP 헤더와 토큰을 사용 하는 보호 된 리소스에 HTTP 요청을 보냅니다.               
Web API     |  최종 리소스는 사용자에 액세스 합니다. 이러한 "신뢰 당사자"의 새 표현으로 간주 합니다.| 클라이언트에서 얻은 토큰을 사용 합니다.  
  
### <a name="differences-from-ad-fs-2012-r2"></a>AD FS 2012 r 2의 차이점  
응용 프로그램 그룹으로 신뢰 당사자, 클라이언트 및 응용 프로그램 사용 권한을 개별적으로 노출 되는 AD FS 2012 r 2는 신뢰와 권한 부여 요소를 결합 합니다.  
  
다음 표에서는 해당 응용 프로그램 트러스트 개체 만들어집니다 AD FS 2012 r 2에서에서 AD FS 2016 vs 메서드를 비교 합니다.  
  
Windows Server 2012 R2의 AD FS|PowerShell에서|AD FS 관리  
---------|---------|---------  
네이티브 클라이언트 추가|추가 AdfsClient|NA  
클라이언트와 서버 응용 프로그램을 추가 합니다.|추가 AdfsClient|NA  
웹 API를 추가 / 리소스|추가 AdfsRelyingPartyTrust|신뢰 당사자 트러스트 만들기  
  
AD FS 2016|PowerShell에서|AD FS 관리  
---------|---------|---------  
네이티브 클라이언트 추가|추가 AdfsNativeClientApplication|네이티브 응용 프로그램에 그룹 추가  
클라이언트와 서버 응용 프로그램을 추가 합니다.|추가 AdfsServerApplication|서버 응용 프로그램에 그룹 추가  
웹 API를 추가 / 리소스|추가 AdfsWebApiApplication|웹 API 응용 프로그램에 그룹 추가  
  
### <a name="application-permissions-and-consent"></a>응용 프로그램 사용 권한 및 동의  
기본적으로 응용 프로그램 그룹에서 클라이언트는 동일한 그룹의 리소스에 액세스할 수 있습니다.  관리자는 특정 응용 프로그램 사용 권한 구성 하지 않아도 됩니다.  응용 프로그램 그룹에는 또한 openid 또는 user_impersonation 등 허용 범위를 지정 하는 관리자가 허용 됩니다.  아래 시나리오 설명의 범위는 어떤 시나리오에 필요한 정확 하 게 지정 합니다.  
  
AD FS 관리자가 승인의 모델을 사용 하므로 리소스에 액세스할 때 사용자가 동의 필요 하지 않습니다.  응용 프로그램 그룹을 구성 하 여 관리자는 사실 모든 응용 프로그램 사용자를 대신 하 여 동의 제공 합니다.  
  
## <a name="supported-scenarios"></a>지원되는 시나리오  
다음 섹션에서 더 자세하게 지원 등의 시나리오를 설명 합니다.  
  
### <a name="tokens-used"></a>사용 되는 토큰  
이러한 시나리오 확인 세 토큰 형식을 사용 합니다.  
  
* **id_token:** 사용자의 id를 나타내는 데 사용 하는 JWT 토큰입니다. 'Aud' 또는 대상 그룹 클레임은 id_token의 네이티브 또는 서버 응용 프로그램의 클라이언트 ID와 일치합니다.  
* **access_token:** 사용 하는 JWT 토큰에 Oauth 및 OpenID connect 시나리오와 의도 한 리소스에서 사용할 수 있도록 합니다.  이 토큰의 'aud' 또는 대상 그룹 클레임 리소스 또는 웹 API의 식별자를 일치 해야 합니다.  
* **refresh_token:** 이 토큰은 single sign on 환경을 제공 하는 사용자 자격 증명을 수집 하는 대신 전송 됩니다.  이 토큰 발급와 AD FS에서 사용 되 고 클라이언트 또는 리소스에서 읽을 수 없습니다.    
  
### <a name="native-client-to-web-api"></a>웹 API를 네이티브 클라이언트  
이 시나리오에는 AD FS 보호 2016 웹 API를 호출 하는 네이티브 클라이언트 응용 프로그램의 사용자 수 있습니다.  
* 네이티브 클라이언트 응용 프로그램 권한 부여를 ADAL을 사용 하 고 토큰 요청을 AD FS를 필요에 따라 사용자 로부터 자격 증명에 대 한 메시지를 표시 한 다음 보냅니다 웹 API에 대 한 요청에서 HTTP 헤더로 결과 토큰  
* [이 파트는 예시 목적 으로만] 웹 API는 클라이언트에서 보낸 액세스 토큰 생성 되며 클라이언트로 다시 전송 하는 ClaimsPrincipal 개체에서 클레임을 읽습니다.  
  
![프로토콜 흐름 설명](media/ADFS_DEV_3.png)  
  
1.  네이티브 클라이언트 응용 프로그램에서 ADAL 라이브러리에 대 한 호출을 사용 하 여 흐름을 시작합니다.  이 트리거는 브라우저 기반 권한 부여 끝점을 AD FS에 HTTP GET:  
  
**권한 부여 요청:**  
GET https://fs.contoso.com/adfs/oauth2/authorize?  
  
매개 변수|값  
---------|---------  
response_type|"코드"  
resource|응용 프로그램 그룹에서 웹 API의 RP ID (식별자)  
client_id|클라이언트 응용 프로그램 그룹에서 네이티브 응용 프로그램의 Id  
redirect_uri|응용 프로그램 그룹에서 네이티브 응용 프로그램의 리디렉션 URI  
  
**권한 부여 요청 응답:**  
사용자가 로그인 하지 전에 자격 증명에 대 한 메시지가 표시 됩니다.    
AD FS 인증 코드의 redirect_uri의 쿼리 구성 요소에서 "코드" 매개 변수로 반환 하 여 응답 합니다.  예를 들어 다음과 같은 가치를 제공해야 합니다. Http/1.1 302 있음 위치:  **http://redirect_uri:80/?code=&lt; 코드&gt;합니다.**  
  
2.  네이티브 클라이언트 코드와 함께 다음 매개 변수를 AD FS 토큰 끝점에 보냅니다.  
  
**토큰 요청:**  
올리기 https://fs.contoso.com/adfs/oauth2/token  
  
매개 변수|값  
---------|---------  
grant_type|"authorization_code" 
code|1에서 인증 코드  
resource|응용 프로그램 그룹에서 웹 API의 RP ID (식별자)  
client_id|클라이언트 응용 프로그램 그룹에서 네이티브 응용 프로그램의 Id  
redirect_uri|응용 프로그램 그룹에서 네이티브 응용 프로그램의 리디렉션 URI  
  
**토큰 요청 응답:**  
AD FS access_token, refresh_token, 및 id_token 본문에 HTTP 200으로 응답합니다.  
  
3.  네이티브 응용 프로그램을 다음 HTTP 요청에 Authorization 헤더는 위의 응답의 access_token 일부분 웹 API에 보냅니다.  
  
### <a name="single-sign-on-behavior"></a>Single sign-on 동작  
1 시간 (기본적으로) 한 access_token 계속 유효한 캐시에 있으며 새 요청을 AD FS에 대 한 모든 트래픽이 트리거되지 내의 후속 클라이언트 요청 합니다.  한 access_token ADAL에서 캐시에서 자동으로 페치 됩니다.  
  
액세스 토큰이 만료 되 면 ADAL (권한 부여 요청을 자동으로 건너뜁니다) AD FS 토큰 끝점에는 새로 고침 토큰 기반된 요청을 자동으로 보냅니다.  
**토큰 요청을 새로 고칩니다.**  
올리기 https://fs.contoso.com/adfs/oauth2/token
   

매개 변수|값|
---------|---------
grant_type|"refresh_token"|
resource|응용 프로그램 그룹에서 웹 API의 RP ID (식별자)|
client_id|클라이언트 응용 프로그램 그룹에서 네이티브 응용 프로그램의 Id
refresh_token|초기 토큰 요청에 대 한 응답에서 AD FS에서 발급 한 새로 고침 토큰

  
  
**토큰 요청 응답 새로 고침:**  
새로 고침 토큰 < SSO_period > 내에 있으면 새 액세스 토큰을 요청이 됩니다. 사용자 자격 증명에 대해 묻지 않습니다.  SSO 설정 참조에 대 한 자세한 내용은 [AD FS Single Sign에 설정](../../ad-fs/operations/AD-FS-2016-Single-Sign-On-Settings.md)  
  
요청 HTTP 401 오류 "invalid_grant" 및 "error_description"를 사용 하 여 결과 새로 고침 토큰은 만료 된 경우 "MSIS9615: Refresh_token 매개 변수에서 받은 새로 고침 토큰이 만료 되었습니다. "입니다. 이 경우 ADAL 위의 # 1과 같은 새 권한 부여 요청을 자동으로 전송 합니다.    
  
### <a name="web-browser-to-web-app"></a>웹 앱에 웹 브라우저   
이 시나리오에서는 사용자 브라우저와 웹 응용 프로그램에서 호스팅하는 리소스에 액세스 해야 합니다.    
이 작업을 수행 하는 방법은 두 가지 시나리오가 있습니다.  
  
#### <a name="oauth-confidential-client"></a>Oauth 기밀 클라이언트  
이 시나리오는 위와 유사한에 나옵니다. 토큰 exchange에 대 한 코드는 권한 부여 요청 있다는 것입니다.  웹 응용 프로그램 (AD FS에서 서버 응용 프로그램으로 모델링) 브라우저를 통해 권한 부여 요청을 시작 하 고 (직접 연결 하 여 AD FS) 토큰에 대 한 코드를 교환 합니다.  
  
![프로토콜 흐름 설명](media/ADFS_DEV_4.png)  
  
1.  AD FS에 HTTP GET을 전송 하는 브라우저를 통해 권한 부여를 요청 하는 웹 응용 프로그램 시작 권한 부여 끝점  
**권한 부여 요청**:  
GET https://fs.contoso.com/adfs/oauth2/authorize?  
  
매개 변수|값  
---------|---------  
response_type|"코드"  
resource|응용 프로그램 그룹에서 웹 API의 RP ID (식별자)  
client_id|응용 프로그램 그룹에서 네이티브 응용 프로그램의 클라이언트 Id  
redirect_uri|응용 프로그램 그룹에서 웹 응용 프로그램 (서버 응용 프로그램)의 리디렉션 URI  
  
권한 부여 요청 응답:  
사용자가 로그인 하지 전에 자격 증명에 대 한 메시지가 표시 됩니다.  
예를 들어의 redirect_uri의 쿼리 구성 요소에서 "코드" 매개 변수로 권한 부여 코드를 반환 하 여 AD FS 응답: Http/1.1 302 있음 위치: https://webapp.contoso.com/?code=&lt; 코드&gt;합니다.  
  
2.  위의 302 결과로 브라우저 시작 웹 앱에 HTTP GET 예를 들어: 가져올 http://redirect_uri:80/?code=&lt; 코드&gt;합니다.   
  
3.  웹 응용 프로그램에서 코드를 받은 다음 보내는 AD FS 토큰 끝점에 요청을 개시 하는 시점에서  
**토큰 요청:**  
올리기 https://fs.contoso.com/adfs/oauth2/token  
  
매개 변수|값  
---------|---------  
grant_type|"authorization_code"  
code|위의 2에서 인증 코드  
resource|응용 프로그램 그룹에서 웹 API의 RP ID (식별자)  
client_id|응용 프로그램 그룹에서 웹 응용 프로그램 (서버 응용 프로그램)의 클라이언트 Id  
redirect_uri|응용 프로그램 그룹에서 웹 응용 프로그램 (서버 응용 프로그램)의 리디렉션 URI  
client_secret|응용 프로그램 그룹에서 웹 응용 프로그램 (서버 응용 프로그램)의 암호입니다. **참고: 클라이언트의 자격 증명을 client_secret 되도록 필요가 없습니다.  AD FS 인증서 또는 Windows 통합 인증도 사용 하는 기능을 지원 합니다.**  
  
**토큰 요청 응답:**  
AD FS access_token, refresh_token, 및 id_token 본문에 HTTP 200으로 응답합니다.  
클레임  
4.  (경우에는 웹 앱 자체는 리소스를 호스트)는 위의 응답의 access_token 일부분을 사용 하거나 다음 응용 프로그램 이거나 웹으로 HTTP 요청에 Authorization 헤더는 웹 API로 전송 됩니다.  
  
#### <a name="single-sign-on-behavior"></a>Single sign-on 동작  
액세스 토큰은 여전히 유효할 수 기본적으로 1 시간 동안 클라이언트의 캐시에 있는 동안에 두 번째 요청은 작동 하는지 위-네이티브 클라이언트 시나리오에서와 같이 새 요청을 트리거되지 않는다고 AD FS에 대 한 모든 트래픽을 액세스 토큰이 자동으로 인출 되는 캐시에서 ADAL에서으로 생각할 수 있습니다.  그러나 것 고유 권한 부여 및 토큰 요청을 샘플 에서처럼 고유 URL 링크를 통해 이전 웹 앱에 보낼 수 있음을 가능 합니다.  
  
이 경우 AD FS에 자격 증명에 대 한 사용자에 게 확인 하지 않고 새 권한 부여 코드를 실행할 수 있게 해 주는 AD FS 브라우저 SSO 쿠키를입니다. 웹 응용 프로그램이 새 액세스 토큰에 대 한 새 권한 부여 코드를 교환 하도록 AD FS를 호출 합니다.  사용자 자격 증명에 대해 묻지 않습니다.  
  
그렇지 않으면 웹 앱이 경우 스마트 충분히 권한 부여 요청을 건너뛸 수는 사용자가 이미 인증 하는 경우 알 수 및 중 하나:  
* 캐시 된 액세스 토큰이 만료 되지 않은 경우 검색 되어 사용, 또는   
* 아래 설명 된 대로 요청 토큰 기반된 요청을 AD FS 토큰 끝점에 보낼 수  
  
**토큰 요청을 새로 고칩니다.**  
올리기 https://fs.contoso.com/adfs/oauth2/token
   
매개 변수|값  
---------|---------  
grant_type|"refresh_token"  
resource|응용 프로그램 그룹에서 웹 API의 RP ID (식별자)  
client_id|응용 프로그램 그룹에서 웹 응용 프로그램 (서버 응용 프로그램)의 클라이언트 Id  
refresh_token|초기 토큰 요청에 대 한 응답에서 AD FS에서 발급 된 토큰 새로 고침  
client_secret|응용 프로그램 그룹에서 웹 응용 프로그램 (서버 응용 프로그램)의 암호  
  
**토큰 요청 응답 새로 고침:**  
새로 고침 토큰 < SSO_period > 내에 있으면 새 액세스 토큰을 요청이 됩니다. 사용자 자격 증명에 대해 묻지 않습니다. SSO 설정 참조에 대 한 자세한 내용은 [AD FS Single Sign에 설정](../../ad-fs/operations/AD-FS-2016-Single-Sign-On-Settings.md)   
  
요청 HTTP 401 오류 "invalid_grant" 및 "error_description"를 사용 하 여 결과 새로 고침 토큰은 만료 된 경우 "MSIS9615: Refresh_token 매개 변수에서 받은 새로 고침 토큰이 만료 되었습니다. "입니다. 이 경우 ADAL 위의 # 1과 같은 새 권한 부여 요청을 자동으로 전송 합니다.    
  
#### <a name="openid-connect-hybrid-flow"></a>OpenID Connect: 하이브리드 흐름  
이 시나리오는 하에서 위와 비슷한 있습니다 브라우저 리디렉션 및 AD FS 웹 응용 프로그램에서 exchange 토큰에 대 한 코드를 통해 웹 응용 프로그램에 의해 권한 부여 요청 시작 됩니다.  초기 인증 요청 응답의 일부로 AD FS는 id_token을 발급 하는 하는이 시나리오에서는 다릅니다.  
  
![프로토콜 흐름 설명](media/ADFS_DEV_5.png)  
  
1.  AD FS에 HTTP GET을 전송 하는 브라우저를 통해 권한 부여를 요청 하는 웹 응용 프로그램 시작 권한 부여 끝점  
  
**권한 부여 요청:**  
GET https://fs.contoso.com/adfs/oauth2/authorize?  
  
매개 변수|값  
---------|---------  
response_type|"코드 + id_token"  
response_mode|"form_post"  
resource|응용 프로그램 그룹에서 웹 API의 RP ID (식별자)  
client_id|응용 프로그램 그룹에서 웹 응용 프로그램 (서버 응용 프로그램)의 클라이언트 Id  
redirect_uri|응용 프로그램 그룹에서 웹 응용 프로그램 (서버 응용 프로그램)의 리디렉션 URI  
  
**권한 부여 요청 응답:**  
사용자가 로그인 하지 전에 자격 증명에 대 한 메시지가 표시 됩니다.  
AD FS HTTP 200 및 포함 된 폼을 사용 하 여 응답은 아래 숨김으로 요소:  
* 코드: 인증 코드  
* id_token: 사용자 인증을 설명 하는 클레임을 포함 하는 JWT 토큰  
2.  폼에 웹 응용 프로그램 코드와는 id_token 보내기는 웹 앱의 redirect_uri 자동으로 게시 합니다.  
  
3.  웹 응용 프로그램에서 코드를 받은 다음 보내는 AD FS 토큰 끝점에 요청을 개시 하는 시점에서  
  
**토큰 요청:**  
올리기 https://fs.contoso.com/adfs/oauth2/token
  
  
  
매개 변수|값  
---------|---------  
grant_type|"authorization_code"  
code|위쪽에서 인증 코드  
resource|응용 프로그램 그룹에서 웹 API의 RP ID (식별자)  
client_id|응용 프로그램 그룹에서 웹 응용 프로그램 (서버 응용 프로그램)의 클라이언트 Id  
redirect_uri|응용 프로그램 그룹에서 웹 응용 프로그램 (서버 응용 프로그램)의 리디렉션 URI  
client_secret|응용 프로그램 그룹에서 웹 응용 프로그램 (서버 응용 프로그램)의 암호  
  
**토큰 요청 응답:**  
AD FS access_token, refresh_token, 및 id_token 본문에 HTTP 200으로 응답합니다.  
  
4.  (경우에는 웹 앱 자체는 리소스를 호스트)는 위의 응답의 access_token 일부분을 사용 하거나 다음 응용 프로그램 이거나 웹으로 HTTP 요청에 Authorization 헤더는 웹 API로 전송 됩니다.  
  
#### <a name="single-sign-on-behavior"></a>Single Sign-on 동작  
동작에 단일 로그인은 위의 Oauth 2.0 기밀 클라이언트 흐름의 경우와 동일 합니다.  
  
### <a name="on-behalf-of"></a>대신  
이 시나리오에서는 웹 응용 프로그램 사용자 로부터 원래 액세스 토큰을 사용 하 여 요청 하 고 웹 응용 프로그램은 다음으로 최종 사용자에 액세스 하는 다른 웹 API에 대 한 다른 액세스 토큰을 가져옵니다.  이 대신 "의" 흐름을 이라고 합니다.  
  
![프로토콜 흐름 설명](media/ADFS_DEV_6.png)  
  
1 단계와 2 이전 흐름의 3, 4 단계와 마찬가지로 작동합니다.  
3 단계에서에서 주요 요구 사항은 client_id 매개 변수를 2, 웹 응용 프로그램의 클라이언트 ID는 RP ID의 Web API 1. 일치 해야 하는  즉, 새 토큰에 대 한 교환 되는 액세스 토큰의 대상 그룹에 새 토큰을 요청 하는 엔터티의 클라이언트 ID 일치 해야 합니다.  

## <a name="related-content"></a>관련 내용  
참조 [AD FS 개발](../AD-FS-Development.md) 연습 문서 목록은 제공 하는 단계별 지침 관련된 흐름을 사용 합니다. 
