---
title: AD FS를 사용한 OpenID Connect 단일 로그아웃
author: billmath
ms.author: billmath
manager: femila
ms.date: 11/17/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: fe176af74ebabb5cb56d8aa74d755c4e35ec94a3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857316"
---
#  <a name="single-log-out-for-openid-connect-with-ad-fs"></a>AD FS를 사용한 OpenID Connect 단일 로그아웃

## <a name="overview"></a>개요
Windows Server 2012 r 2에서 AD FS의 초기 Oauth 지원에 따라 AD FS 2016에 Openid connect Connect sign-on 지원이 도입 되었습니다. [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801)를 사용 하면 이제 AD FS 2016에서 openid connect Connect 시나리오에 대 한 단일 로그 아웃을 지원 합니다. 이 문서에서는 Openid connect Connect에 대 한 단일 로그 아웃 시나리오의 개요를 제공 하 고, AD FS의 Openid connect Connect 응용 프로그램에이를 사용 하는 방법에 대 한 지침을 제공 합니다.


## <a name="discovery-doc"></a>검색 문서
Openid connect Connect는 "검색 문서" 라는 JSON 문서를 사용 하 여 구성에 대 한 세부 정보를 제공 합니다.  여기에는 인증, 토큰, userinfo 및 공용 끝점의 Uri가 포함 됩니다.  다음은 검색 문서의 예입니다.

```
{
"issuer":"https://fs.fabidentity.com/adfs",
"authorization_endpoint":"https://fs.fabidentity.com/adfs/oauth2/authorize/",
"token_endpoint":"https://fs.fabidentity.com/adfs/oauth2/token/",
"jwks_uri":"https://fs.fabidentity.com/adfs/discovery/keys",
"token_endpoint_auth_methods_supported":["client_secret_post","client_secret_basic","private_key_jwt","windows_client_authentication"],
"response_types_supported":["code","id_token","code id_token","id_token token","code token","code id_token token"],
"response_modes_supported":["query","fragment","form_post"],
"grant_types_supported":["authorization_code","refresh_token","client_credentials","urn:ietf:params:oauth:grant-type:jwt-bearer","implicit","password","srv_challenge"],
"subject_types_supported":["pairwise"],
"scopes_supported":["allatclaims","email","user_impersonation","logon_cert","aza","profile","vpn_cert","winhello_cert","openid"],
"id_token_signing_alg_values_supported":["RS256"],
"token_endpoint_auth_signing_alg_values_supported":["RS256"],
"access_token_issuer":"http://fs.fabidentity.com/adfs/services/trust",
"claims_supported":["aud","iss","iat","exp","auth_time","nonce","at_hash","c_hash","sub","upn","unique_name","pwd_url","pwd_exp","sid"],
"microsoft_multi_refresh_token":true,
"userinfo_endpoint":"https://fs.fabidentity.com/adfs/userinfo",
"capabilities":[],
"end_session_endpoint":"https://fs.fabidentity.com/adfs/oauth2/logout",
"as_access_token_token_binding_supported":true,
"as_refresh_token_token_binding_supported":true,
"resource_access_token_token_binding_supported":true,
"op_id_token_token_binding_supported":true,
"rp_id_token_token_binding_supported":true,
"frontchannel_logout_supported":true,
"frontchannel_logout_session_supported":true
} 
 
```



프런트 채널 로그 아웃 지원을 나타내는 다음 추가 값을 검색 문서에서 사용할 수 있습니다.

- frontchannel_logout_supported: 값이 ' t r u e '입니다.
- frontchannel_logout_session_supported: 값이 ' t r u e '입니다.
- end_session_endpoint: 클라이언트에서 서버에 대 한 로그 아웃을 시작 하는 데 사용할 수 있는 OAuth 로그 아웃 URI입니다.


## <a name="ad-fs-server-configuration"></a>AD FS 서버 구성
EnableOAuthLogout AD FS 속성은 기본적으로 사용 하도록 설정 됩니다.  이 속성은 클라이언트에서 로그 아웃을 시작 하는 SID를 사용 하 여 URL (LogoutURI)을 검색 하도록 AD FS 서버에 지시 합니다. [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801) 가 설치 되어 있지 않은 경우 다음 PowerShell 명령을 사용할 수 있습니다.

```PowerShell
Set-ADFSProperties -EnableOAuthLogout $true
```

>[!NOTE]
> [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801)를 설치한 후 `EnableOAuthLogout` 매개 변수는 사용 되지 않는 것으로 표시 됩니다. `EnableOAUthLogout`은 항상 true 이며 로그 아웃 기능에 영향을 주지 않습니다.

>[!NOTE]
>frontchannel_logout는 [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801) 의 vcredist 후에 **만** 지원 됩니다.

## <a name="client-configuration"></a>클라이언트 구성
클라이언트는 로그인 한 사용자를 ' 로그 오프 ' 하는 url을 구현 해야 합니다. 관리자는 다음 PowerShell cmdlet을 사용 하 여 클라이언트 구성에서 LogoutUri를 구성할 수 있습니다. 


- `(Add | Set)-AdfsNativeApplication`
- `(Add | Set)-AdfsServerApplication`
- `(Add | Set)-AdfsClient`

```PowerShell
Set-AdfsClient -LogoutUri <url>
```

`LogoutUri`는 AF FS에서 사용자를 "로그 오프" 하는 데 사용 하는 url입니다. `LogoutUri`를 구현 하기 위해 클라이언트는 응용 프로그램에서 사용자의 인증 상태를 지우도록 해야 합니다. 예를 들어, 응용 프로그램에 포함 된 인증 토큰을 삭제할 수 있습니다. AD FS는 해당 URL을 검색 하 고, SID를 쿼리 매개 변수로 사용 하 여 신뢰 당사자/응용 프로그램에 사용자를 로그 오프 하도록 신호를 전달 합니다. 

![](media/ad-fs-logout-openid-connect/adfs_single_logout2.png)


1.  **세션 id가 AD FS 인 oauth 토큰**에는 id_token 토큰 발급 시 oauth 토큰의 세션 id가 포함 됩니다. 이는 나중에 AD FS 하 여 사용자에 대해 정리할 관련 SSO 쿠키를 식별 하는 데 사용 됩니다.
2.  **사용자가 App1에서 로그 아웃 시작**: 사용자는 로그인 한 응용 프로그램에서 로그 아웃을 시작할 수 있습니다. 이 예제 시나리오에서 사용자는 App1에서 로그 아웃을 시작 합니다.
3.  **응용 프로그램에서 AD FS로 로그 아웃 요청을 보냅니다**. 사용자가 로그 아웃을 시작 하면 응용 프로그램은 AD FS의 END_SESSION_ENDPOINT에 GET 요청을 보냅니다. 응용 프로그램은이 요청에 대 한 매개 변수로 id_token_hint를 선택적으로 포함할 수 있습니다. Id_token_hint 있는 경우 AD FS는 세션 ID와 함께 사용 하 여 로그 아웃 (post_logout_redirect_uri) 후에 클라이언트를 리디렉션할 URI를 확인 합니다.  Post_logout_redirect_uri는 RedirectUris 매개 변수를 사용 하 여 AD FS에 등록 된 유효한 uri 여야 합니다.
4.  AD FS는 로그인 된 **클라이언트로 로그 아웃을 보냅니다**. AD FS은 세션 식별자 값을 사용 하 여 사용자가 로그인 한 관련 클라이언트를 찾습니다. 식별 된 클라이언트는 AD FS에 등록 된 LogoutUri에서 요청을 전송 하 여 클라이언트 쪽에서 로그 아웃을 시작 합니다.

## <a name="faqs"></a>FAQ
**Q:** 검색 문서에 frontchannel_logout_supported 및 frontchannel_logout_session_supported 매개 변수가 표시 되지 않습니다.</br>
**A:** 모든 AD FS 서버에 [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801) 이 설치 되어 있는지 확인 합니다. [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801)를 사용 하 여 서버 2016에서 단일 로그 아웃을 참조 하세요.

**Q:** 단일 로그 아웃을 지시 된 대로 구성 했지만 사용자가 다른 클라이언트에 로그인 된 상태를 유지 합니다.</br>
**A:** 사용자가 로그인 한 모든 클라이언트에 대해 `LogoutUri` 설정 되어 있는지 확인 합니다. 또한 AD FS는 등록 된 `LogoutUri`에 대 한 로그 아웃 요청을 전송 하는 데 가장 적합 합니다. 클라이언트는 요청을 처리 하 고 작업을 수행 하 여 응용 프로그램에서 사용자를 로그 아웃 하는 논리를 구현 해야 합니다.</br>

**Q:** 로그 아웃 한 후 클라이언트 중 하나가 유효한 새로 고침 토큰을 사용 하 여 AD FS 다시 이동 하 고 AD FS 액세스 토큰을 발급 합니다.</br>
**A:** 예. 등록 된 `LogoutUri`에서 로그 아웃 요청을 받은 후에는 인증 된 모든 아티팩트를 삭제 하는 것은 클라이언트 응용 프로그램의 책임입니다.


## <a name="next-steps"></a>다음 단계
[AD FS 개발](../../ad-fs/AD-FS-Development.md)  
