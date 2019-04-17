---
ms.assetid: 8a64545b-16bd-4c13-a664-cdf4c6ff6ea0
title: "개발자를 위해 광고 FS 시나리오"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 753b2b235cb1d73ab47588f8f229410c1f81db40
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="ad-fs-scenarios-for-developers"></a>개발자를 위해 광고 FS 시나리오

>Windows Server 2016 적용 됩니다.

Windows Server 2016 [AD FS 2016]에 ADFS 표준 OpenID 연결 및 OAuth 2.0 기반 응용 프로그램을 개발 하는 인증과 업계 추가 하 고 해당 응용 프로그램을 사용자 Adfs에 대해 직접 인증 수 있습니다.    
  
광고 FS 2016 WS-연합, Ws-trust도 지원 하 고 SAML 프로토콜 우리 프로필 이전 버전에서 지원 했습니다.  이러한 프로토콜에 대 한 개발자 지침 관심 있는 경우 문서를 여기 참조 합니다.  이 문서는 사용 및 최신 프로토콜 지원 활용 하는 방법에 집중 합니다.  
  
## <a name="why-modern-authentication"></a>왜 최신 인증  
사용 ADFS 로그인에 대 한에 WS Federation를 계속 Ws-trust, 및 그대로 SAML 프로토콜 받게 이점은 새 프로토콜을 사용 하기 전에 다음과 같습니다.  
  
* **간단 하 고 일관성**  
    * 동일한 집합이 Api 사용 하 여 및 패턴을 사용 하도록 설정에 대 한에 로그인을 하면 다음과 같습니다.   
        *   여러 종류의 응용 프로그램 (예: 서버, 바탕 화면, 모바일, 브라우저)  
        *   여러 플랫폼 (iOS, android, Windows)  
        *   회사의 네트워크 안에 응용 프로그램 또는 클라우드에서 호스트  
    * 이미 사용자에 게 Azure AD에 대해 인증을 사용할 수 있습니다 라이브러리의 같은 집합을 사용  
* **유연성**  
    * 표준 사용자 승인 뿐만 아니라 더 복잡 한 시나리오를와 같은 사용:      
        * ? 3 다리 기호 사용자 인증 하나 흐름에서 웹 응용 프로그램 또는 서비스와 웹 앱 이나 서비스에서 다른 있는 리소스에 액세스할 수 있습니다.    
        * ? 다중 계층 서비스 백 엔드 API 액세스 하는 서버에 흐름  
        * ? JavaScript 기반 단일 페이지 응용 프로그램 (SPA)  
* **업계 지원**  
    * OAuth 2.0 및 OpenID 연결 다양 한 활용도 에서도 음향을 즐길 수는 산업 하므로 기술 이러한 패턴을 사용 하도록 설정 된 Active Directory 환경 외 인증과 데 도움이 됩니다.  
  
## <a name="how-it-works-the-basics"></a>작동 방식: 기본 사항  
ADFS 최신 인증을 사용 하 여 동일한 도구 및 이미 사용자에 게 Azure AD에 대해 인증을 사용할 수 있습니다 라이브러리 응용 프로그램에 추가할 수 있습니다.   
  
ADFS 시나리오에서 물론, 것 이며 ADFS id 공급자와 인증 역할을 수행 하지 Azure AD 서버 합니다.  그렇지 않으면 개념 동일: 사용자가 자격 증명을 제공 하 고 직접 또는 중간 장치 리소스에 대 한 액세스를 통해 토큰을 가져오는 합니다.  
  
기본 가장 시나리오 사용자 또는 웹 응용 프로그램에 액세스 하는 브라우저와 상호 작용 "리소스 소유자" 구성 되어 있습니다.  
  
![개발자를 위한 ADFS](media/ADFS_DEV_1.png)  
  
웹 응용 프로그램에서이 리소스에 액세스 토큰 (ADFS) 권한 서버에 요청을 시작 하기 때문에 "클라이언트" 라고 합니다.  리소스 웹 앱 자체에 의해 호스트 될 또는 웹 API 어딘가에 네트워크 또는 인터넷에 액세스할 수 있습니다.   사용자 또는 "리소스 소유자" 권한 서버 자격 증명을 제공 하 여 해당 액세스 토큰 받으려면 클라이언트 웹 앱에 권한을 부여 합니다.    
  
## <a name="how-it-works-components"></a>작동 방식: 구성 요소가  
OAuth 2.0 및 OpenID 연결 시나리오를 ADFS 제조업체의 도구와 라이브러리 Azure AD 신원을 공급자가 사용 하 여 동일한 설정 사용 합니다.  이러한 구성 요소는 다음과 같습니다.  
* Active Directory 인증 라이브러리 (ADAL): 클라이언트 라이브러리를 쉽게 사용자 자격 증명을 수집, 만들기 및 토큰 요청을 제출 하 고 검색 결과 토큰 합니다.    
* (.NET에 대해 열고 웹 인터페이스) OWIN 미들웨어: 동안 OWIN는 기반 커뮤니티 프로젝트, Microsoft는 만들었습니다 일련의 서버 쪽 라이브러리를 보호 하기 위해 웹 응용 프로그램 및 Api OpenID 연결 OAuth 2.0와 웹  
  
이러한 구성 요소 역할 다이어그램 아래에 표시 됩니다.  
  
![개발자를 위한 ADFS](media/ADFS_DEV_2.png)  
  
## <a name="modeling-these-scenarios-in-ad-fs-2016"></a>광고 FS 2016에 모델링 이러한 시나리오  
  
### <a name="application-groups"></a>응용 프로그램 그룹  
ADFS 정책에서 이러한 시나리오를 대표 하 응용 프로그램 그룹 라는 새로운 개념이 도입 했습니다.  응용 프로그램 그룹 번호와 응용 프로그램의 다음 기본 형식의 조합 포함 될 수 있습니다.  
  
  
  
응용 프로그램 그룹 응용 프로그램에 입력 /  |설명  |역할    
---------|---------|---------  
기본 응용 프로그램     |  공용 클라이언트 라고도 합니다이 사용자 상호 작용할 된 pc 또는 디바이스에서 실행 되는 클라이언트 앱으로 사용 됩니다.       | 사용자 액세스 권한 서버 (ADFS)에서 토큰 리소스를 요청 합니다.  토큰을 사용 하 여 탐지도 보호 된 리소스에 HTTP 요청을 보냅니다.        
서버 응용 프로그램     |   웹 응용 프로그램 서버에서 실행 되는 일반적으로 브라우저를 통해 사용자가 액세스할 수 있습니다.  해당 클라이언트 '비밀' 또는 자격 증명 유지 관리할 수 있기 때문에 기밀 클라이언트를 라고도 합니다.      | 사용자 액세스 권한 서버 (ADFS)에서 토큰 리소스를 요청 합니다.  토큰을 사용 하 여 탐지도 보호 된 리소스에 HTTP 요청을 보냅니다.               
웹 API     |  사용자의 최종 리소스에 액세스 합니다. "신뢰 당사자"의 새 표현으로 중 이라고 생각 합니다.| 토큰 클라이언트에서 얻은 사용  
  
### <a name="differences-from-ad-fs-2012-r2"></a>광고 FS 2012 r 2의 차이  
응용 프로그램 그룹 광고 FS 2012 r 2 신뢰 당사자, 클라이언트 및 응용 프로그램 사용 권한으로 별도로 노출 신뢰 하 고 승인 요소 결합 합니다.  
  
다음 표에서 비교 하 여 해당 응용 프로그램 신뢰 개체 만들어집니다 광고 FS 2012 r 2에 vs FS 2016 AD 방법:  
  
Windows Server 2012 r 2 ADFS|PowerShell의|AD FS 관리  
---------|---------|---------  
기본 클라이언트 추가|추가 AdfsClient|나  
서버 응용 프로그램 클라이언트로 추가|추가 AdfsClient|나  
웹 API 추가 / 리소스|추가 AdfsRelyingPartyTrust|신뢰 당사자 신뢰 만들기  
  
ADFS 2016|PowerShell의|AD FS 관리  
---------|---------|---------  
기본 클라이언트 추가|추가 AdfsNativeClientApplication|기본 응용 프로그램에 그룹 추가  
서버 응용 프로그램 클라이언트로 추가|추가 AdfsServerApplication|서버 응용 프로그램에 그룹 추가  
웹 API 추가 / 리소스|추가 AdfsWebApiApplication|웹 API 응용 프로그램에 그룹 추가  
  
### <a name="application-permissions-and-consent"></a>응용 프로그램 사용 권한 및 동의  
기본적으로 클라이언트 응용 프로그램 그룹에 같은 그룹에 리소스에 액세스할 수 있습니다.  관리자 특정 응용 프로그램 사용 권한을 구성 필요가 없습니다.  응용 프로그램 그룹은 또한 openid user_impersonation 등 허용 범위를 지정 하려면 관리자 수 있습니다.  아래 시나리오 설명을 범위는 어떤 시나리오에 대 한 필요 정확 하 게 지정 합니다.  
  
Adfs의 관리자 동의 모델을 사용 하므로 리소스에 액세스할 때 사용자가 동의 필요 하지 않습니다.  응용 프로그램을 구성 하 여 관리자 적용 응용 프로그램의 모든 사용자를 대신 하 여 동의 제공 합니다.  
  
## <a name="supported-scenarios"></a>지원 되는 경우  
다음 섹션 자세히 지원 시나리오에 설명 합니다.  
  
### <a name="tokens-used"></a>토큰  
이러한 시나리오 확인 세 가지 토큰 종류의 사용:  
  
* **id_token:** A JWT 토큰 사용자의 id를 대표 하는 데 사용 합니다. 'Aud' 또는 대상은 id_token 클레임에 서버 또는 기본 응용 프로그램의 클라이언트 ID를 찾습니다.  
* **access_token:** 사용 되는 A JWT 토큰 Oauth 및 OpenID에서 연결 시나리오 및 리소스에 의해 소모 될 수 있습니다.  이 토큰의 'aud' 또는 대상 클레임 리소스 또는 웹 API의 식별자를 일치 해야 합니다.  
* **refresh_token:** 이 토큰 경험에 단일 로그인을 제공 하기 위해 사용자 자격 증명을 수집 하는 대신 전송 됩니다.  이 토큰 발행와 Adfs에 사용 되 고 클라이언트 또는 리소스 읽을 수 없습니다.    
  
### <a name="native-client-to-web-api"></a>웹 API를 기본 클라이언트  
이 경우 ADFS 보호 2016 웹 API 호출 기본 클라이언트 응용 프로그램의 하면 수 있습니다.  
* 기본 클라이언트 응용 프로그램 ADAL 인증을 사용 하 여 및 토큰 필요에 따라 사용자의 자격에 대 한 라는 ADFS 하도록 요청 다음 전송 HTTP 헤더 웹 API에 대 한 요청에으로 결과 토큰  
* [데모 목적 으로만이 이곳은] 웹 API 클레임은 클라이언트에서 보낸 액세스 토큰의 결과 클라이언트도 다시 보냅니다 ClaimsPrincipal 개체의 읽습니다.  
  
![프로토콜 흐름의 설명](media/ADFS_DEV_3.png)  
  
1.  기본 클라이언트 응용 프로그램 ADAL 라이브러리에 전화를 사용 하 여 흐름을 시작합니다.  브라우저 기반 트리거하이 끝점 HTTP는 Adfs에 액세스할 권한을 부여 합니다.  
  
**권한 요청 합니다.**  
GET https://fs.contoso.com/adfs/oauth2/authorize?  
  
매개|값  
---------|---------  
response_type|"코드"  
리소스|웹 응용 프로그램 그룹 API의 RP ID (식별자)  
client_id|클라이언트 응용 프로그램 그룹에서 기본 응용 프로그램의 Id  
redirect_uri|응용 프로그램 그룹에서 기본 응용 프로그램의 URI 이동  
  
**권한 요청 응답:**  
사용자가 로그인 하지 자격 증명에 대해 묻는 전에 합니다.    
Adfs의는 redirect_uri 쿼리 구성에서 "code" 매개는 인증 코드가 반환 하 여 응답 합니다.  예: 302/1.1 찾을 위치: **http://redirect_uri:80 /? 코드 =&lt;코드&gt;합니다.**  
  
2.  기본 클라이언트 ADFS 토큰 끝점 다음 매개 코드를 보냅니다.  
  
**토큰 요청 합니다.**  
POST https://fs.contoso.com/adfs/oauth2/token  
  
매개|값  
---------|---------  
grant_type|"authorization_code" 
코드|인증 코드가 1  
리소스|웹 응용 프로그램 그룹 API의 RP ID (식별자)  
client_id|클라이언트 응용 프로그램 그룹에서 기본 응용 프로그램의 Id  
redirect_uri|응용 프로그램 그룹에서 기본 응용 프로그램의 URI 이동  
  
**토큰 요청 응답:**  
Adfs는 access_token, refresh_token, 및 본문에서 id_token HTTP 200를 사용 하 여 응답 합니다.  
  
3.  그러면 기본 응용 프로그램 HTTP 요청에서 인증 헤더 위의 응답 access_token 부분을 웹 API 보냅니다.  
  
### <a name="single-sign-on-behavior"></a>동작에 단일 기호  
기본적으로 1 시간은 access_token 여전히 유효한 캐시에 않으며 새 요청은 모든 ADFS 트래픽이 트리거되지 이후 클라이언트 내 요청 합니다.  access_token ADAL 하 여 캐시에서 자동으로 가져올 됩니다.  
  
액세스 토큰 만료 되 면 ADAL을 (를 건너뛰는 것이 요청은 자동으로) ADFS 토큰 끝점 새로 고침 토큰 기반된 요청을 자동으로 보냅니다.  
**토큰 요청 새로 고침 다음과 같습니다.**  
POST https://fs.contoso.com/adfs/oauth2/token
   

매개|값|
---------|---------
grant_type|"refresh_token"|
리소스|웹 응용 프로그램 그룹 API의 RP ID (식별자)|
client_id|클라이언트 응용 프로그램 그룹에서 기본 응용 프로그램의 Id
refresh_token|Adfs의 초기 토큰 요청에 응답 하 여 발급 새로 고침 토큰

  
  
**토큰 요청 응답 새로 고침:**  
새로 고침 토큰 < SSO_period > 내에 있으면 요청 새 액세스 토큰 발생 합니다. 자격 증명을 사용자를 묻지 않습니다.  에 대 한 자세한 내용은 SSO 설정 확인 [광고 FS 단일 로그인에서 설정](../../ad-fs/operations/AD-FS-2016-Single-Sign-On-Settings.md)  
  
요청 오류 "invalid_grant"와 "error_description" HTTP 401 결과 새로 고침 토큰 만료 되 면 "MSIS9615: 만료 refresh_token 매개 받은 새로 고침 토큰"입니다. 이 경우 ADAL 위의 1 처럼 보이는 새 권한 요청을 자동으로 전송 합니다.    
  
### <a name="web-browser-to-web-app"></a>웹 브라우저에 웹 응용 프로그램   
이 경우 브라우저를 통해 사용자 웹 응용 프로그램에서 주최한 리소스에 액세스 해야 합니다.    
이렇게 두 가지 경우도 있습니다.  
  
#### <a name="oauth-confidential-client"></a>Oauth 기밀 클라이언트  
이 시나리오는 비슷한 위의에 요청을 토큰 거래소에 대 한 코드 옵니다.  웹 응용 프로그램 (adfs에서 서버 응용 프로그램으로 모델링) 브라우저를 통해 권한 요청을 시작 하 고 Adfs에 직접 연결) (함으로써 토큰에 대 한 코드를 교환  
  
![프로토콜 흐름의 설명](media/ADFS_DEV_4.png)  
  
1.  웹 응용 프로그램 시작 하 고 ADFS HTTP 다운로드를 전송 하는 브라우저를 통해 다른 인증 요청 끝점 승인  
**권한 요청**:  
GET https://fs.contoso.com/adfs/oauth2/authorize?  
  
매개|값  
---------|---------  
response_type|"코드"  
리소스|웹 응용 프로그램 그룹 API의 RP ID (식별자)  
client_id|응용 프로그램 그룹에서 기본 응용 프로그램의 클라이언트 Id  
redirect_uri|URI 응용 프로그램 그룹의 (서버 응용 프로그램) 웹 앱을 이동합니다  
  
권한 요청 응답:  
사용자가 로그인 하지 자격 증명에 대해 묻는 전에 합니다.  
예를 들어 쿼리 구성 요소는 redirect_uri에서 "code" 매개도 인증 코드가 반환 하 여 ADFS 응답: / 1.1 302 찾을 위치: https://webapp.contoso.com/?code=&lt;코드&gt;합니다.  
  
2.  위의 302로 인해 브라우저가 시작 웹 앱을 다운로드 HTTP 예: 다운로드 http://redirect_uri:80 /? 코드 =&lt;코드&gt;합니다.   
  
3.  이 시점에서 코드를 수신 하는 데 웹 앱을 시작 ADFS 토큰 끝점 다음 전송에 대 한 요청  
**토큰 요청 합니다.**  
POST https://fs.contoso.com/adfs/oauth2/token  
  
매개|값  
---------|---------  
grant_type|"authorization_code"  
코드|인증 코드가 위의 2에서  
리소스|웹 응용 프로그램 그룹 API의 RP ID (식별자)  
client_id|응용 프로그램의 웹 응용 프로그램 (서버 응용 프로그램) 클라이언트 Id  
redirect_uri|URI 응용 프로그램 그룹의 (서버 응용 프로그램) 웹 앱을 이동합니다  
client_secret|시크릿 응용 프로그램의 웹 응용 프로그램 (서버 응용 프로그램). **참고: 클라이언트의 자격 증명을 client_secret 되도록 필요가 없습니다.  Adfs도 Windows 통합 인증 되거나 인증서를 사용 하는 기능을 지원 합니다.**  
  
**토큰 요청 응답:**  
Adfs는 access_token, refresh_token, 및 본문에서 id_token HTTP 200를 사용 하 여 응답 합니다.  
클레임  
4.  웹 응용 프로그램 (있는 경우에는 웹 앱 자체 리소스를 호스트 하는) 위의 응답 access_token 부분을 사용 하거나 다음 되었거나 인증 헤더 HTTP 요청에으로 웹 API로 보냅니다.  
  
#### <a name="single-sign-on-behavior"></a>동작에 단일 기호  
액세스 토큰은 여전히 되어 유효한 기본적으로 1 시간에 대 한 클라이언트의 캐시를 동안 두 번째 요청이 작동 하는지 위의-네이티브 클라이언트 시나리오 새 요청을 액세스 토큰을 자동으로 불러 캐시에서 ADAL 하 여으로 ADFS 하 든 교통 발생 하지는 생각할 수 있습니다.  고유한 인증과 토큰 요청 웹 앱 보내는 수, 샘플 처럼 고유한 URL를 통해 이전 연결에 불가능 합니다.  
  
이 경우 ADFS 자격 증명을 입력 하지 않고도 새 인증 코드를 실행할 수 있도록 ADFS 브라우저 SSO 쿠키입니다. 다음 웹 앱 전화 ADFS 새 액세스 토큰에 대 한 새로운 인증 코드를 교환 하려면 연락처를 합니다.  자격 증명을 사용자를 묻지 않습니다.  
  
그렇지 않은 경우 웹 앱을 하는 경우 스마트 부여 요청을 건너뛸 수 있는 사용자가 이미 인증 하는 경우를 알아야 충분 한 및 중 다음과 같습니다.  
* 캐시 된 액세스, 만료 되지 않은 경우는 검색 토큰과 사용 하는 또는   
* 아래에 설명 된 대로 ADFS 토큰 endpoint을 보낼 수 요청 토큰 기반된 요청  
  
**토큰 요청 새로 고침 다음과 같습니다.**  
POST https://fs.contoso.com/adfs/oauth2/token
   
매개|값  
---------|---------  
grant_type|"refresh_token"  
리소스|웹 응용 프로그램 그룹 API의 RP ID (식별자)  
client_id|응용 프로그램의 웹 응용 프로그램 (서버 응용 프로그램) 클라이언트 Id  
refresh_token|Adfs의 초기 토큰 요청에 응답 하 여 발급 토큰 새로 고침  
client_secret|시크릿 응용 프로그램의 웹 응용 프로그램 (서버 응용 프로그램)  
  
**토큰 요청 응답 새로 고침:**  
새로 고침 토큰 < SSO_period > 내에 있으면 요청 새 액세스 토큰 발생 합니다. 자격 증명을 사용자를 묻지 않습니다. 에 대 한 자세한 내용은 SSO 설정 확인 [광고 FS 단일 로그인에서 설정](../../ad-fs/operations/AD-FS-2016-Single-Sign-On-Settings.md)   
  
요청 오류 "invalid_grant"와 "error_description" HTTP 401 결과 새로 고침 토큰 만료 되 면 "MSIS9615: 만료 refresh_token 매개 받은 새로 고침 토큰"입니다. 이 경우 ADAL 위의 1 처럼 보이는 새 권한 요청을 자동으로 전송 합니다.    
  
#### <a name="openid-connect-hybrid-flow"></a>하이브리드 흐름 OpenID 연결:  
이 시나리오는에 위의 비슷한 있는 브라우저로 이동 하 고 ADFS 웹 응용 프로그램에서 토큰 exchange 코드를 통해 웹 응용 프로그램에서 권한 요청 시작 됩니다.  이 경우 차이점 ADFS 초기 권한 요청 응답의 일환으로 한 id_token 문제는입니다.  
  
![프로토콜 흐름의 설명](media/ADFS_DEV_5.png)  
  
1.  웹 응용 프로그램 시작 하 고 ADFS HTTP 다운로드를 전송 하는 브라우저를 통해 다른 인증 요청 끝점 승인  
  
**권한 요청 합니다.**  
GET https://fs.contoso.com/adfs/oauth2/authorize?  
  
매개|값  
---------|---------  
response_type|"코드 + id_token"  
response_mode|"form_post"  
리소스|웹 응용 프로그램 그룹 API의 RP ID (식별자)  
client_id|응용 프로그램의 웹 응용 프로그램 (서버 응용 프로그램) 클라이언트 Id  
redirect_uri|웹 응용 프로그램의 응용 프로그램 그룹에서 (서버 응용 프로그램)의 URI 이동  
  
**권한 요청 응답:**  
사용자가 로그인 하지 자격 증명에 대해 묻는 전에 합니다.  
ADFS 응답 HTTP 200 및 폼을 포함 하는 아래와 숨겨진 요소 다음과 같습니다.  
* 코드: 인증 코드  
* id_token: 클레임 사용자 인증을 설명 하는 포함 된 JWT 토큰  
2.  양식 자동으로 웹 앱을 코드 및는 id_token 전송을 웹 앱을 redirect_uri에 게시 됩니다.  
  
3.  이 시점에서 코드를 수신 하는 데 웹 앱을 시작 ADFS 토큰 끝점 다음 전송에 대 한 요청  
  
**토큰 요청 합니다.**  
POST https://fs.contoso.com/adfs/oauth2/token
  
  
  
매개|값  
---------|---------  
grant_type|"authorization_code"  
코드|인증 코드가 위쪽에서  
리소스|웹 응용 프로그램 그룹 API의 RP ID (식별자)  
client_id|응용 프로그램의 웹 응용 프로그램 (서버 응용 프로그램) 클라이언트 Id  
redirect_uri|URI 응용 프로그램 그룹의 (서버 응용 프로그램) 웹 앱을 이동합니다  
client_secret|시크릿 응용 프로그램의 웹 응용 프로그램 (서버 응용 프로그램)  
  
**토큰 요청 응답:**  
Adfs는 access_token, refresh_token, 및 본문에서 id_token HTTP 200를 사용 하 여 응답 합니다.  
  
4.  웹 응용 프로그램 (있는 경우에는 웹 앱 자체 리소스를 호스트 하는) 위의 응답 access_token 부분을 사용 하거나 다음 되었거나 인증 헤더 HTTP 요청에으로 웹 API로 보냅니다.  
  
#### <a name="single-sign-on-behavior"></a>동작에 단일 기호  
동작에 단일 로그인 위의 Oauth 2.0 기밀 클라이언트 흐름와 같습니다.  
  
### <a name="on-behalf-of"></a>대신 하 여  
이 시나리오 웹 앱을 요청 하 고 최종 사용자와 웹 앱은 다음 액세스 하는 다른 웹 API에 대 한 또 다른 액세스 토큰 얻을에서는 사용자에 게 원래 액세스 토큰을 사용 합니다.  이 대신 "의" 흐름을 라고 합니다.  
  
![프로토콜 흐름의 설명](media/ADFS_DEV_6.png)  
  
3 단계와 4 이전 흐름에서 처럼 1, 2 단계 작동 합니다.  
3 단계에서에서 중요 한 요구 사항 웹 앱 2, 클라이언트 ID client_id 매개 RP ID의 웹 API 대답: 일치 해야 한다는 즉, 되 고 새로운 토큰 교환할 액세스 토큰 관객 요청 하는 새 토큰 엔터티의 클라이언트 ID 일치 해야 합니다.  

## <a name="related-content"></a>관련된 내용  
참조 [광고 FS 개발](../AD-FS-Development.md) 단계별 지침 관련된 흐름을 사용 하 여에 제공 하는 단계 문서의 전체 목록은 합니다. 
