---
title: AD FS를 사용한 OpenID Connect 단일 로그아웃
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 11/17/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3af10ec139edbc72e75bf80f544ac5b4f1cf9222
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825774"
---
#  <a name="single-log-out-for-openid-connect-with-ad-fs"></a>AD FS를 사용한 OpenID Connect 단일 로그아웃

## <a name="overview"></a>개요
Windows Server 2012 R2의 AD FS에서 초기 Oauth 지원을 토대로, AD FS 2016 OpenId Connect 로그인에 대 한 지원이 도입 되었습니다. 사용 하 여 [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801), 이제 AD FS 2016 OpenId Connect 시나리오에 대 한 단일 로그 아웃을 지원 합니다. 이 문서는 OpenId Connect 시나리오에 대 한 단일 로그 아웃의 개요를 제공 하 고 AD FS에서 OpenId Connect 응용 프로그램에 대 한 사용 방법에 대 한 지침을 제공 합니다.


## <a name="discovery-doc"></a>검색 문서
"검색 문서" 라고 하는 JSON 문서를 사용 하 여 OpenID Connect 구성에 대 한 세부 정보를 제공 합니다.  여기에 인증, 토큰, 사용자, 정보 및 공용 끝점의 Uri입니다.  다음은 검색 문서의 예입니다.

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



다음 추가 값 프런트 채널 로그 아웃에 대 한 지원을 표시 하도록 검색 문서에서 사용할 수 있습니다.

- frontchannel_logout_supported: 값 'true' 됩니다.
- frontchannel_logout_session_supported: 값은 'true' 됩니다.
- end_session_endpoint: OAuth 로그 아웃 클라이언트는 서버에서 로그 아웃을 시작 하는 데 사용할 수 있는 URI입니다.


## <a name="ad-fs-server-configuration"></a>AD FS 서버 구성
AD FS 속성 EnableOAuthLogout 기본적으로 사용 됩니다.  이 속성은 클라이언트에서 로그 아웃을 시작 하는 SID를 사용 하 여 AD FS 서버의 URL (LogoutURI) 찾아볼 수를 나타냅니다. 없는 경우 [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801) 설치 된 다음 PowerShell 명령을 사용할 수 있습니다.

```PowerShell
Set-ADFSProperties -EnableOAuthLogout $true
```

>[!NOTE]
> `EnableOAuthLogout` 매개 변수는 되지 않음으로 표시를 설치한 후 [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801)합니다. `EnableOAUthLogout` 항상 true 여야 하 고 로그 아웃 하는 기능에 영향을 주지 마십시오.

>[!NOTE]
>frontchannel_logout 지원 됩니다 **만** 의 설치 후 [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801)

## <a name="client-configuration"></a>클라이언트 구성
클라이언트에서 기록 하는 ' off' 로그온 된 사용자의 url을 구현 해야 합니다. 관리자는 다음 PowerShell cmdlet을 사용 하 여 클라이언트 구성에는 LogoutUri를 구성할 수 있습니다. 


- `(Add | Set)-AdfsNativeApplication`
- `(Add | Set)-AdfsServerApplication`
- `(Add | Set)-AdfsClient`

```PowerShell
Set-AdfsClient -LogoutUri <url>
```

`LogoutUri` "를 기록 하려면" 사용자 AF FS에서 사용 하는 url입니다. 구현에 대 한는 `LogoutUri`인증 삭제가 있는지를 토큰 예를 들어, 확인 하기 위해 클라이언트에 필요한 응용 프로그램에서 사용자의 인증 상태를 지웁니다. AD FS 신뢰 당사자 신호 쿼리 매개 변수로 SID 사용 하 여 해당 URL로 이동 됩니다 / 로그 오프 사용자 응용 프로그램입니다. 

![](media/ad-fs-logout-openid-connect/adfs_single_logout2.png)


1.  **세션 ID 사용 하 여 OAuth 토큰**: AD FS는 id_token 토큰 발급 시 OAuth 토큰에 세션 id를 포함합니다. 이 나중에 AD FS에서 사용자에 대 한 정리 관련 SSO 쿠키를 식별 하 합니다.
2.  **사용자가 App1에서 로그 아웃 시작**: 사용자를 로그 아웃 로그인 응용 프로그램에서 시작할 수 있습니다. 이 예제 시나리오에서 사용자를 로그 아웃 App1에서 시작합니다.
3.  **응용 프로그램이 AD FS를 로그 아웃 요청을 보내는**: 사용자가 로그 아웃을 시작 후 응용 프로그램 end_session_endpoint의 AD FS에는 GET 요청을 보냅니다. 필요에 따라 응용 프로그램이이 요청에 매개 변수로 id_token_hint를 포함할 수 있습니다. Id_token_hint가 있는 경우 AD FS를 사용 하 여 해당 세션 ID와 함께에서 URI 아웃 클라이언트 리디렉션됩니다 (post_logout_redirect_uri) 로그 아웃 한 후입니다.  post_logout_redirect_uri RedirectUris 매개 변수를 사용 하 여 AD FS를 사용 하 여 등록 된 유효한 uri 여야 합니다.
4.  **AD FS에 로그인 한 클라이언트에 로그 아웃 보냅니다**: AD FS 세션 식별자 값을 사용 하 여 사용자가에 로그인 하는 관련 클라이언트를 찾는. 식별 된 클라이언트는 클라이언트 쪽에는 로그 아웃을 시작 하려면 AD FS를 사용 하 여 등록 LogoutUri에서 요청을 보냈습니다.

## <a name="faqs"></a>FAQ
**Q:** 검색 문서에서 frontchannel_logout_supported 및 frontchannel_logout_session_supported 매개 변수 표시 되지 않습니다.</br>
**A:** 했는지 [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801) 모든 AD FS 서버에 설치 합니다. 서버 2016에서 단일 로그 아웃을 가리킵니다 [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801)합니다.

**Q:** 지시에 따라 단일 로그 아웃을 구성 했습니다 하지만 사용자가 계속에 로그인 한 다른 클라이언트에서.</br>
**A:** 되도록 `LogoutUri` 에 로그인 한 사용자가 모든 클라이언트에 대해 설정 됩니다. 또한 AD FS는 등록 로그 아웃 요청을 보내려고 시도 하는 최상의 `LogoutUri`합니다. 클라이언트 요청을 처리 하 고 응용 프로그램에서 사용자 로그 아웃 작업을 수행 하는 논리를 구현 해야 합니다.</br>

**Q:** 로그 아웃 한 후 클라이언트 중으로 전환 되 면 다시 유효한 새로 고침 토큰을 사용 하 여 AD FS에는 AD FS 액세스 토큰을 발급?</br>
**A:** 예 이 경우 로그 아웃 요청을 수신한 후 인증 된 모든 아티팩트를 삭제 하려면 클라이언트 응용 프로그램에 등록 된 `LogoutUri`합니다.


## <a name="next-steps"></a>다음 단계
[AD FS 개발](../../ad-fs/AD-FS-Development.md)  
