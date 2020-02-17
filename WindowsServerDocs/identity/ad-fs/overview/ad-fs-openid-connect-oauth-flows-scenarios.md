---
ms.assetid: 8a64545b-16bd-4c13-a664-cdf4c6ff6ea0
title: AD FS OpenID Connect/OAuth 흐름 및 애플리케이션 시나리오
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: e1e0235e50945fadd09fe9dd5ffeaf6d7119e482
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385597"
---
# <a name="ad-fs-openid-connectoauth-flows-and-application-scenarios"></a>AD FS OpenID Connect/OAuth 흐름 및 애플리케이션 시나리오
적용 대상: AD FS 2016 이상


|시나리오|시나리오 연습에 사용되는 샘플|OAuth 2.0 흐름/권한 부여|클라이언트 유형|
|-----|-----|-----|-----|
|단일 페이지 앱</br> | &bull; [ADAL 사용 샘플](../development/Single-Page-Application-with-AD-FS.md)|[암시적](#implicit-grant-flow)|공용| 
|사용자를 로그인하는 웹앱</br> | &bull; [OWIN 사용 샘플](../development/enabling-openid-connect-with-ad-fs.md)|[권한 부여 코드](#authorization-code-grant-flow)|퍼블릭, 비밀|  
|웹 API를 호출하는 네이티브 앱</br>|&bull; [MSAL 사용 샘플](../development/msal/adfs-msal-native-app-web-api.md)</br>&bull; [ADAL 사용 샘플](../development/native-client-with-ad-fs.md)|[권한 부여 코드](#authorization-code-grant-flow)|공용|   
|웹 API를 호출하는 웹앱</br>|&bull; [MSAL 사용 샘플](../development/msal/adfs-msal-web-app-web-api.md)</br>&bull; [ADAL 사용 샘플](../development/enabling-oauth-confidential-clients-with-ad-fs.md)|[권한 부여 코드](#authorization-code-grant-flow)|비밀| 
|사용자를 대신하여(OBO) 다른 웹 API를 호출하는 웹 API</br>|&bull; [MSAL 사용 샘플](../development/msal/adfs-msal-web-api-web-api.md)</br>&bull; [ADAL 사용 샘플](../development/ad-fs-on-behalf-of-authentication-in-windows-server.md)|[On-Behalf-Of](#on-behalf-of-flow)|비밀 역할을 하는 웹앱| 
|웹 API를 호출하는 디먼 앱||[클라이언트 자격 증명](#client-credentials-grant-flow)|비밀| 
|사용자 자격 증명을 사용하여 웹 API를 호출하는 웹앱||[리소스 소유자 암호 자격 증명](#resource-owner-password-credentials-grant-flow-not-recommended)|퍼블릭, 비밀| 
|웹 API를 호출하는 브라우저 없는 앱||[디바이스 코드](#device-code-flow)|퍼블릭, 비밀| 

## <a name="implicit-grant-flow"></a>암시적 권한 부여 흐름 
 
단일 페이지 애플리케이션(AngularJS, Ember.js, React.js 등)의 경우 AD FS는 OAuth 2.0 암시적 권한 부여 흐름을 지원합니다. 암시적 흐름은  [OAuth 2.0 사양](https://tools.ietf.org/html/rfc6749#section-4.2)에서 설명하고 있습니다. 주요 이점은 백 엔드 서버 자격 증명 교환을 수행하지 않고도 앱에서 AD FS로부터 토큰을 가져올 수 있다는 이 있습니다. 이렇게 하면 앱에서 사용자를 로그인하고, 세션을 유지 관리하며, 클라이언트 JavaScript 코드 내에서 토큰을 다른 웹 API에 가져올 수 있습니다. 특히 [클라이언트](https://tools.ietf.org/html/rfc6749#section-10.3)를 기준으로 암시적 흐름을 사용하는 경우 고려해야 할 몇 가지 중요한 보안 고려 사항이 있습니다.  
 
암시적 흐름과 AD FS를 사용하여 인증을 JavaScript 앱에 추가하려면 아래의 일반 단계를 따릅니다.  
  
### <a name="protocol-diagram"></a>프로토콜 다이어그램

다음 다이어그램에서는 전체적인 암시적 로그인 흐름을 보여 주며, 이어지는 섹션에서 각 단계에 대해 자세히 설명합니다.  

![암시적 로그인](media/adfs-scenarios-for-developers/implicit.png)

### <a name="request-id-token-and-access-token"></a>요청 ID 토큰 및 액세스 토큰 
 
처음에 사용자를 앱에 로그인하려면 OpenID Connect 인증 요청을 보내고 AD FS 엔드포인트에서 id_token 및 액세스 토큰을 가져올 수 있습니다.  
 
```
// Line breaks for legibility only 
 
https://adfs.contoso.com/adfs/oauth2/authorize? 
client_id=6731de76-14a6-49ae-97bc-6eba6914391e 
&response_type=id_token+token 
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F 
&scope=openid 
&response_mode=fragment 
&state=12345 
```


|매개 변수|필수/선택|설명| 
|-----|-----|-----|
|client_id|필수|AD FS에서 앱에 할당한 애플리케이션(클라이언트) ID입니다.| 
|response_type|필수|OpenID Connect 로그인에 대한 `id_token` 을 포함해야 합니다.  `token` response_type도 포함할 수 있습니다. 여기서 토큰을 사용하면 앱에서 토큰 엔드포인트에 대한 두 번째 요청을 수행하지 않고도 권한 부여 엔드포인트에서 액세스 토큰을 즉시 받을 수 있습니다.| 
|redirect_uri|필수|앱에서 인증 응답을 보내고 받을 수 있는 앱의 redirect_uri입니다. AD FS에서 구성한 redirect_uri 중 하나와 정확히 일치해야 합니다.| 
|nonce|필수|앱에서 생성하여 요청에 포함된 값이며, 결과 id_token에 클레임으로 포함됩니다. 그러면 앱에서 이 값을 확인하여 토큰 재생 공격을 완화할 수 있습니다. 이 값은 일반적으로 요청의 출처를 식별하는 데 사용할 수 있는 임의의 고유 문자열입니다. id_token이 요청된 경우에만 필요합니다.|
|scope|선택적|공백으로 구분된 범위의 목록입니다. OpenID Connect의 경우 `openid` 범위를 포함해야 합니다.|
|리소스|선택적|웹 API의 URL입니다.</br>참고 - MSAL 클라이언트 라이브러리를 사용하는 경우 리소스 매개 변수를 보내지 않습니다. 대신 리소스 URL을 범위 매개 변수(`scope = [resource url]//[scope values e.g., openid]`)의 일부로 보냅니다.</br>리소스가 여기 또는 범위에 전달되지 않으면 ADFS에서 기본 urn:microsoft:userinfo 리소스를 사용합니다. MFA, 발급 또는 권한 부여 정책과 같은 userinfo 리소스 정책은 사용자 지정할 수 없습니다.| 
|response_mode|선택적| 결과 토큰을 앱으로 다시 보내는 데 사용해야 하는 메서드를 지정합니다. 기본값은 `fragment`입니다.| 
|state|선택적|토큰 응답에도 반환되는 요청에 포함된 값입니다. 원하는 콘텐츠의 문자열일 수 있습니다. 임의로 생성된 고유 값은 일반적으로 사이트 간 요청 위조 공격을 방지하는 데 사용됩니다. 또한 state는 인증 요청이 발생하기 전에 앱에서 사용자 상태에 대한 정보(예: 페이지 또는 보기)를 인코딩하는 데 사용됩니다.| 
|prompt|선택적|필요한 사용자 상호 작용 유형을 나타냅니다. 현재 유일하게 유효한 값은 login 및 none입니다.</br>- `prompt=login` 은 사용자가 해당 요청에 대한 자격 증명을 입력하도록 하여 Single Sign-On을 부정합니다. </br>- `prompt=none` 은 반대의 경우로, 사용자에게 대화형 프롬프트가 표시되지 않습니다. Single Sign-On을 통해 요청을 자동으로 완료할 수 없으면 AD FS에서 interaction_required 오류를 반환합니다.| 
|login_hint|선택적|사용자 이름을 미리 알고 있는 경우 사용자 로그인 페이지의 사용자 이름/이메일 주소 필드를 미리 채우는 데 사용할 수 있습니다. 앱에서 다시 인증하는 동안 이 매개 변수를 사용하는 경우가 많으며, `id_token`의  `upn` 클레임을 사용하여 이전 로그인에서 사용자 이름을 이미 추출했습니다.| 
|domain_hint|선택적|포함되는 경우 사용자가 로그인 페이지에서 수행하는 도메인 기반 검색 프로세스를 건너뛰어 약간 더 간소화된 사용자 환경을 제공합니다.| 

이 시점에서 사용자에게 자격 증명을 입력하고 인증을 완료하라는 메시지가 표시됩니다. 사용자가 인증되면 AD FS 권한 부여 엔드포인트에서 response_mode 매개 변수에 지정된 메서드를 사용하여 표시된 redirect_uri에서 앱에 대한 응답을 반환합니다.  
 
### <a name="successful-response"></a>성공적인 응답 
 
 `response_mode=fragment and response_type=id_token+token` 을 사용한 성공적인 응답은 다음과 같습니다.  
 
```
// Line breaks for legibility only 
 
GET https://localhost/myapp/# 
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZEstZnl0aEV... 
&token_type=Bearer 
&expires_in=3599 
&scope=openid  
&id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZstZnl0aEV1Q... 
&state=12345 
```


|매개 변수|설명| 
|-----|-----|
|access_token|response_type에 `token`이 포함된 경우 포함됩니다.|
|token_type|response_type에 `token`이 포함된 경우 포함됩니다. 항상 Bearer입니다.| 
|expires_in| response_type에 `token`이 포함된 경우 포함됩니다. 캐싱을 위해 토큰이 유효한 시간(초)을 나타냅니다.| 
|scope| access_token이 유효한 범위를 나타냅니다.|  
|id_token|response_type에 `id_token`이 포함된 경우 포함됩니다. 서명된 JWT(JSON 웹 토큰)입니다. 앱에서 이 토큰의 세그먼트를 디코딩하여 로그인한 사용자에 대한 정보를 요청할 수 있습니다. 앱에서 값을 캐시하고 표시할 수 있지만, 권한 부여 또는 보안 경계에 이러한 값을 사용하지 않아야 합니다.| 
|state|state 매개 변수가 요청에 포함된 경우 동일한 값이 응답에 표시됩니다. 앱은 요청 및 응답의 state 값이 동일한지 확인해야 합니다.|

### <a name="refresh-tokens"></a>새로 고침 토큰 
암시적 권한 부여는 새로 고침 토큰을 제공하지 않습니다.  `id_tokens`및  `access_tokens`는 모두 짧은 시간 후에 만료되므로 앱에서 이러한 토큰을 주기적으로 새로 고칠 수 있도록 준비해야 합니다. 토큰 형식 중 하나를 새로 고치려면 `prompt=none`  매개 변수를 통해 위와 동일한 숨겨진 iframe 요청을 수행하여 ID 플랫폼의 동작을 제어할 수 있습니다. `new id_token`을 받으려면 `response_type=id_token`을 사용해야 합니다. 

## <a name="authorization-code-grant-flow"></a>인증 코드 부여 흐름 
 
웹앱에서 OAuth 2.0 인증 코드 부여를 사용하여 웹 API와 같은 보호된 리소스에 액세스할 수 있습니다. OAuth 2.0 인증 코드 흐름은 [OAuth 2.0 사양의 4.1 섹션](https://tools.ietf.org/html/rfc6749)에서 설명하고 있습니다. 웹앱 및 기본적으로 설치된 앱을 포함하여 대부분의 앱 유형에서 인증 및 권한 부여를 수행하는 데 사용됩니다. 이 흐름을 통해 앱에서 AD FS를 신뢰하는 리소스에 액세스하는 데 사용할 수 있는 access_token을 안전하게 획득할 수 있습니다.  
 
### <a name="protocol-diagram"></a>프로토콜 다이어그램 
 
네이티브 애플리케이션의 인증 흐름은 개략적으로 다음과 같습니다.

![인증 코드 부여 흐름](media/adfs-scenarios-for-developers/authorization.png)

### <a name="request-an-authorization-code"></a>인증 코드 요청 
 
인증 코드 흐름은 클라이언트에서 사용자를 /authorization 엔드포인트에 연결하면서 시작됩니다. 이 요청에서 클라이언트는 사용자로부터 획득해야 하는 권한을 나타냅니다. 
 
```
// Line breaks for legibility only 
 
https://adfs.contoso.com/adfs/oauth2/authorize? 
client_id=6731de76-14a6-49ae-97bc-6eba6914391e 
&response_type=code 
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F 
&response_mode=query 
&resource=https://webapi.com/ 
&scope=openid 
&state=12345 
```

|매개 변수|필수/선택|설명|
|-----|-----|-----| 
|client_id|필수|AD FS에서 앱에 할당한 애플리케이션(클라이언트) ID입니다.|  
|response_type|필수| 인증 코드 흐름에 대한 코드를 포함해야 합니다.| 
|redirect_uri|필수|앱에서 인증 응답을 보내고 받을 수 있는 앱의 `redirect_uri`입니다. AD FS에서 클라이언트에 대해 등록한 redirect_uri 중 하나와 정확히 일치해야 합니다.|  
|리소스|선택적|웹 API의 URL입니다.</br>참고 - MSAL 클라이언트 라이브러리를 사용하는 경우 리소스 매개 변수를 보내지 않습니다. 대신 리소스 URL을 범위 매개 변수(`scope = [resource url]//[scope values e.g., openid]`)의 일부로 보냅니다.</br>리소스가 여기 또는 범위에 전달되지 않으면 ADFS에서 기본 urn:microsoft:userinfo 리소스를 사용합니다. MFA, 발급 또는 권한 부여 정책과 같은 userinfo 리소스 정책은 사용자 지정할 수 없습니다.| 
|scope|선택적|공백으로 구분된 범위 목록입니다.|
|response_mode|선택적|결과 토큰을 앱으로 다시 보내는 데 사용해야 하는 메서드를 지정합니다. 다음 중 하나일 수 있습니다. </br>- query </br>- fragment </br>- form_post</br>`query` 는 코드를 리디렉션 URI에 대한 쿼리 문자열 매개 변수로 제공합니다. 코드를 요청하는 경우 쿼리, 조각 또는 form_post를 사용할 수 있습니다. `form_post` 는 리디렉션 URI에 대한 코드가 포함된 POST를 실행합니다.|
|state|선택적|토큰 응답에도 반환되는 요청에 포함된 값입니다. 원하는 콘텐츠의 문자열일 수 있습니다. 임의로 생성된 고유 값은 일반적으로 사이트 간 요청 위조 공격을 방지하는 데 사용됩니다. 또한 이 값은 인증 요청이 발생하기 전에 앱에서 사용자 상태에 대한 정보(예: 페이지 또는 보기)를 인코딩할 수도 있습니다.|
|prompt|선택적|필요한 사용자 상호 작용 유형을 나타냅니다. 현재 유일하게 유효한 값은 login 및 none입니다.</br>- `prompt=login` 은 사용자가 해당 요청에 대한 자격 증명을 입력하도록 하여 Single Sign-On을 부정합니다. </br>- `prompt=none` 은 반대의 경우로, 사용자에게 대화형 프롬프트가 표시되지 않습니다. Single Sign-On을 통해 요청을 자동으로 완료할 수 없으면 AD FS에서 interaction_required 오류를 반환합니다.|
|login_hint|선택적|사용자 이름을 미리 알고 있는 경우 사용자 로그인 페이지의 사용자 이름/이메일 주소 필드를 미리 채우는 데 사용할 수 있습니다. 앱에서 다시 인증하는 동안 이 매개 변수를 사용하는 경우가 많으며, `id_token`의 `upn` 클레임을 사용하여 이전 로그인에서 사용자 이름을 이미 추출했습니다.|
|domain_hint|선택적|포함되는 경우 사용자가 로그인 페이지에서 수행하는 도메인 기반 검색 프로세스를 건너뛰어 약간 더 간소화된 사용자 환경을 제공합니다.|
|code_challenge_method|선택적|code_challenge 매개 변수의 code_verifier를 인코딩하는 데 사용되는 메서드입니다. 다음 값 중 하나일 수 있습니다. </br>- plain </br>- S256 </br>제외되는 경우 `code_challenge` 가 포함되면 code_challenge는일반 텍스트로 간주됩니다. AD FS는 일반 및 S256을 모두 지원합니다. 자세한 내용은  [PKCE RFC](https://tools.ietf.org/html/rfc7636)를 참조하세요.|
|code_challenge|선택적| 네이티브 클라이언트에서 PKCE(코드 교환용 증명 키)를 통해 인증 코드 부여를 보호하는 데 사용됩니다.  `code_challenge_method` 가 포함되는 경우 필수입니다. 자세한 내용은  [PKCE RFC](https://tools.ietf.org/html/rfc7636)를 참조하세요.|

이 시점에서 사용자에게 자격 증명을 입력하고 인증을 완료하라는 메시지가 표시됩니다. 사용자가 인증되면 AD FS에서 `response_mode`  매개 변수에 지정된 메서드를 사용하여 표시된 `redirect_uri`에서 앱에 대한 응답을 반환합니다.  
 
### <a name="successful-response"></a>성공적인 응답 
 
response_mode=query를 사용한 성공적인 응답은 다음과 같습니다. 
 
```
GET https://adfs.contoso.com/common/oauth2/nativeclient? 
code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq... 
&state=12345  
```


|매개 변수|설명|
|-----|-----|
|code|앱에서 요청한 `authorization_code`입니다. 앱에서 권한 부여 코드를 사용하여 대상 리소스에 대한 액세스 토큰을 요청할 수 있습니다. authorization_code는 수명이 짧으며, 일반적으로 약 10분 후에 만료됩니다.|
|state|`state` 매개 변수가 요청에 포함된 경우 동일한 값이 응답에 표시됩니다. 앱은 요청 및 응답의 state 값이 동일한지 확인해야 합니다.|

### <a name="request-an-access-token"></a>액세스 토큰 요청 
 
이제 `authorization_code`를 획득하고 사용자가 권한을 부여했으므로 `access_token` 에 대한 코드를 원하는 리소스로 사용할 수 있습니다. 이렇게 하려면 POST 요청을 /token 엔드포인트에 보냅니다.  
 
```
// Line breaks for legibility only 
 
POST /adfs/oauth2/token HTTP/1.1 
Host: https://adfs.contoso.com/ 
Content-Type: application/x-www-form-urlencoded 
 
client_id=6731de76-14a6-49ae-97bc-6eba6914391e 
&code=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq3n8b2JRLk4OxVXr... 
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F 
&grant_type=authorization_code 
&client_secret=JqQX2PNo9bpM0uEihUPzyrh    // NOTE: Only required for confidential clients (web apps)  
```

|매개 변수|필수/선택|설명|
|-----|-----|-----| 
|client_id|필수|AD FS에서 앱에 할당한 애플리케이션(클라이언트) ID입니다.| 
|grant_type|필수|인증 코드 흐름에 대해 `authorization_code` 여야 합니다.| 
|code|필수|흐름의 첫 번째 레그에서 획득한 `authorization_code`입니다.| 
|redirect_uri|필수|`authorization_code`를 획득하는 데 사용된 것과 동일한 `redirect_uri` 값입니다.| 
|client_secret|웹앱의 경우 필수|AD FS에서 앱을 등록하는 동안 만든 애플리케이션 비밀입니다. client_secret을 디바이스에 안정적으로 저장할 수 없으므로 네이티브 앱에서 애플리케이션 비밀을 사용하면 안 됩니다. client_secret을 서버 쪽에 안전하게 저장할 수 있는 웹앱 및 웹 API에 필요합니다. 클라이언트 암호는 보내기 전에 URL로 인코딩해야 합니다. 이러한 앱은 JWT에 서명하고 이를 client_assertion 매개 변수로 추가하여 키 기반 인증을 사용할 수도 있습니다.| 
|code_verifier|선택적|authorization_code를 가져오는 데 사용된 것과 동일한 `code_verifier`입니다. PKCE를 인증 코드 부여 요청에 사용한 경우에 필요합니다. 자세한 내용은  [PKCE RFC](https://tools.ietf.org/html/rfc7636)를 참조하세요.</br>참고 – AD FS 2019 이상에 적용됩니다.| 

### <a name="successful-response"></a>성공적인 응답 
 
성공적인 토큰 응답은 다음과 같습니다. 
 
```
{ 
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...", 
    "token_type": "Bearer", 
    "expires_in": 3599, 
    "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4...", 
    "refresh_token_expires_in": 28800, 
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctOD...", 
} 
```


|매개 변수|설명| 
|-----|-----|
|access_token|요청된 액세스 토큰입니다. 앱에서 이 토큰을 사용하여 보안 리소스(웹 API)를 인증할 수 있습니다.| 
|token_type|토큰 형식 값을 나타냅니다. AD FS에서 지원하는 유일한 형식은 Bearer입니다.
|expires_in|액세스 토큰의 유효 기간(초)입니다.
|refresh_token|OAuth 2.0 새로 고침 토큰입니다. 현재 액세스 토큰이 만료되면 앱에서 이 토큰을 사용하여 추가 액세스 토큰을 획득할 수 있습니다. refresh_token은 수명이 길며, 리소스에 대한 액세스를 오랫동안 유지하는 데 사용할 수 있습니다.| 
|refresh_token_expires_in|새로 고침 토큰의 유효 기간(초)입니다.| 
|id_token|JWT(JSON 웹 토큰)입니다. 앱에서 이 토큰의 세그먼트를 디코딩하여 로그인한 사용자에 대한 정보를 요청할 수 있습니다. 앱에서 값을 캐시하고 표시할 수 있지만, 권한 부여 또는 보안 경계에 이러한 값을 사용하지 않아야 합니다.|

### <a name="use-the-access-token"></a>액세스 토큰 사용 
 
```
GET /v1.0/me/messages 
Host: https://webapi.com 
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q... 
 ```

### <a name="refresh-the-access-token"></a>액세스 토큰 새로 고침 
 
access_token은 수명이 짧으며, 만료된 후 새로 고쳐야 리소스에 계속 액세스할 수 있습니다. 이렇게 하려면 다른 POST 요청을 `/token` 엔드포인트에 제출합니다. 이번에는 코드 대신 refresh_token을 제공합니다. 새로 고침 토큰은 클라이언트에서 이미 액세스 토큰을 받은 모든 권한에 유효합니다. 
 
새로 고침 토큰에는 지정된 수명이 없습니다. 일반적으로 새로 고침 토큰의 수명은 비교적 깁니다. 그러나 경우에 따라 새로 고침 토큰이 만료되거나, 해지되거나, 원하는 작업에 대한 충분한 권한이 없습니다. 애플리케이션은 토큰 발급 엔드포인트에서 반환되는 오류를 올바르게 예상하고 처리해야 합니다.  
 
새 액세스 토큰을 획득하는 데 사용할 때 새로 고침 토큰이 해지되지 않지만, 이전의 새로 고침 토큰은 삭제해야 합니다. OAuth 2.0 사양은 다음과 같습니다. "권한 부여 서버는 신규 새로 고침 토큰을 발급할 수 있습니다. 이 경우 클라이언트는 이전 새로 고침 토큰을 삭제하고 신규 새로 고침 토큰으로 바꿔야 합니다. 권한 부여 서버는 신규 새로 고침 토큰을 클라이언트에 발급한 후에 이전 새로 고침 토큰을 해지할 수 있습니다." 
 
```
// Line breaks for legibility only 
 
POST /adfs/oauth2/token HTTP/1.1 
Host: https://adfs.contoso.com 
Content-Type: application/x-www-form-urlencoded 
 
client_id=6731de76-14a6-49ae-97bc-6eba6914391e 
&refresh_token=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq... 
&grant_type=refresh_token 
&client_secret=JqQX2PNo9bpM0uEihUPzyrh      // NOTE: Only required for confidential clients (web apps)  
```


|매개 변수|필수/선택|설명| 
|-----|-----|-----|
|client_id|필수|AD FS에서 앱에 할당한 애플리케이션(클라이언트) ID입니다.| 
|grant_type|필수|인증 코드 흐름의 이 레그에 대해 `refresh_token` 이어야 합니다.| 
|리소스|선택적|웹 API의 URL입니다.</br>참고 - MSAL 클라이언트 라이브러리를 사용하는 경우 리소스 매개 변수를 보내지 않습니다. 대신 리소스 URL을 범위 매개 변수(`scope = [resource url]//[scope values e.g., openid]`)의 일부로 보냅니다.</br>리소스가 여기 또는 범위에 전달되지 않으면 ADFS에서 기본 urn:microsoft:userinfo 리소스를 사용합니다. MFA, 발급 또는 권한 부여 정책과 같은 userinfo 리소스 정책은 사용자 지정할 수 없습니다.|
|scope|선택적|공백으로 구분된 범위 목록입니다.| 
|refresh_token|필수|흐름의 두 번째 레그에서 획득한 refresh_token입니다.| 
|client_secret|웹앱의 경우 필수| 앱에 대한 앱 등록 포털에서 만든 애플리케이션 비밀입니다. client_secret을 디바이스에 안정적으로 저장할 수 없으므로 네이티브 앱에서 사용하면 안 됩니다. client_secret을 서버 쪽에 안전하게 저장할 수 있는 웹앱 및 웹 API에 필요합니다. 이러한 앱은 JWT에 서명하고 이를 client_assertion 매개 변수로 추가하여 키 기반 인증을 사용할 수도 있습니다.|

### <a name="successful-response"></a>성공적인 응답 
성공적인 토큰 응답은 다음과 같습니다. 
 
```
{ 
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...", 
    "token_type": "Bearer", 
    "expires_in": 3599, 
    "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4...", 
    "refresh_token_expires_in": 28800, 
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctOD...", 
}  
```
|매개 변수|설명| 
|-----|-----|
|access_token|요청된 액세스 토큰입니다. 앱에서 이 토큰을 사용하여 보안 리소스(예: 웹 API)를 인증할 수 있습니다.| 
|token_type|토큰 형식 값을 나타냅니다. AD FS에서 지원하는 유일한 형식은 Bearer입니다.|
|expires_in|액세스 토큰의 유효 기간(초)입니다.|
|scope|access_token의 유효 범위입니다.| 
|refresh_token|OAuth 2.0 새로 고침 토큰입니다. 현재 액세스 토큰이 만료되면 앱에서 이 토큰을 사용하여 추가 액세스 토큰을 획득할 수 있습니다. refresh_token은 수명이 길며, 리소스에 대한 액세스를 오랫동안 유지하는 데 사용할 수 있습니다.| 
|refresh_token_expires_in|새로 고침 토큰의 유효 기간(초)입니다.| 
|id_token|JWT(JSON 웹 토큰)입니다. 앱에서 이 토큰의 세그먼트를 디코딩하여 로그인한 사용자에 대한 정보를 요청할 수 있습니다. 앱에서 값을 캐시하고 표시할 수 있지만, 권한 부여 또는 보안 경계에 이러한 값을 사용하지 않아야 합니다.|

## <a name="on-behalf-of-flow"></a>On-Behalf-Of 흐름 
 
OAuth 2.0 OBO(On-Behalf-Of) 흐름은 애플리케이션에서 서비스/웹 API를 호출하고, 이에 따라 다른 서비스/웹 API를 호출해야 하는 사용 사례를 처리합니다. 이 개념은 요청 체인을 통해 위임된 사용자 ID 및 권한을 전파하는 것입니다. 중간 계층 서비스에서 다운스트림 서비스에 인증된 요청을 수행하려면 사용자를 대신하여 AD FS에서 액세스 토큰을 보호해야 합니다.  
 
### <a name="protocol-diagram"></a>프로토콜 다이어그램 
위에서 설명한 OAuth 2.0 인증 코드 부여 흐름을 사용하여 애플리케이션에서 사용자를 인증했다고 가정합니다. 이 시점에서 애플리케이션에는 중간 계층 웹 API(API A)에 액세스하기 위한 사용자의 클레임과 동의가 포함된 API A(토큰 A)에 대한 액세스 토큰이 있습니다. 클라이언트에서 토큰의 user_impersonation 범위를 요청하는지 확인합니다. 이제 API A는 다운스트림 웹 API(API B)에 인증된 요청을 수행해야 합니다. 

다음 단계는 OBO 흐름을 구성하며, 다음 다이어그램의 지원을 통해 설명됩니다. 

![On-Behalf-Of 흐름](media/adfs-scenarios-for-developers/obo.png)

  1. 클라이언트 애플리케이션은 토큰 A를 사용하여 API A에 요청을 합니다.  
  참고: AD FS에서 OBO 흐름을 구성하는 동안 `user_impersonation` 범위가 선택되고 클라이언트가 요청에서 `user_impersonation` 범위를 요청합니다. 
  2. API A에서 AD FS 토큰 발급 엔드포인트를 인증하고 API B에 액세스하기 위한 토큰을 요청합니다. 참고: AD FS에서 이 흐름을 구성하는 동안 API A의 리소스 ID와 동일한 값이 있는 clientID를 사용하여 API A가 서버 애플리케이션으로 등록되었는지도 확인합니다. 자세한 내용은 [여기에 On-Behalf Of 샘플 추가] 링크를 참조하세요.  
  3. AD FS 토큰 발급 엔드포인트에서 토큰 A를 사용하여 API A의 자격 증명에 대한 유효성을 검사하고, API B(토큰 B)에 대한 액세스 토큰을 발급합니다. 
  4. 토큰 B가 API B에 대한 요청의 권한 부여 헤더에 설정됩니다. 
  5. API B에서 보안 리소스의 데이터를 반환합니다. 

### <a name="service-to-service-access-token-request"></a>서비스 간 액세스 토큰 요청 
 
액세스 토큰을 요청하려면 다음 매개 변수를 사용하여 AD FS 토큰 엔드포인트에 대한 HTTP POST를 수행합니다.  


### <a name="first-case-access-token-request-with-a-shared-secret"></a>첫 번째 사례: 공유 비밀을 사용하여 액세스 토큰 요청 
 
공유 비밀을 사용하는 경우 서비스 간 액세스 토큰 요청에 포함되는 매개 변수는 다음과 같습니다. 


|매개 변수|필수/선택|설명|
|-----|-----|-----| 
|grant_type|필수|토큰 요청의 유형입니다. JWT를 사용하는 요청의 경우 값은 urn:ietf:params:oauth:grant-type:jwt-bearer여야 합니다.|  
|client_id|필수|첫 번째 웹 API를 서버 앱(중간 계층 앱)으로 등록할 때 구성하는 클라이언트 ID입니다. 첫 번째 레그(예: 첫 번째 웹 API의 URL)에서 사용된 리소스 ID와 동일해야 합니다.| 
|client_secret|필수|AD FS에서 서버 앱을 등록하는 동안 만든 애플리케이션 비밀입니다.| 
|assertion|필수|요청에 사용된 토큰의 값입니다.|  
|requested_token_use|필수|요청을 처리하는 방법을 지정합니다. OBO 흐름에서 이 값은 on_behalf_of로 설정해야 합니다.| 
|리소스|필수|첫 번째 웹 API를 서버 앱(중간 계층 앱)으로 등록하는 동안 제공된 리소스 ID입니다. 이 리소스 ID는 클라이언트를 대신하여 앱에서 호출하는 두 번째 웹 API 중간 계층의 URL이어야 합니다.|
|scope|선택적|공백으로 구분된 토큰 요청에 대한 범위의 목록입니다.| 

#### <a name="example"></a>예제 
 
다음 `HTTP POST`에서 액세스 토큰 및 새로 고침 토큰을 요청합니다. 
 
```
//line breaks for legibility only 
 
POST /adfs/oauth2/token HTTP/1.1 
Host: adfs.contoso.com  
Content-Type: application/x-www-form-urlencoded 
 
grant_type=urn:ietf:params:oauth:grant-type:jwt-bearer 
&client_id=https://webapi.com/ 
&client_secret=BYyVnAt56JpLwUcyo47XODd 
&assertion=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIm… 
&resource=https://secondwebapi.com/
&requested_token_use=on_behalf_of
&scope=openid    
```

### <a name="second-case-access-token-request-with-a-certificate"></a>두 번째 사례: 인증서를 사용하여 액세스 토큰 요청 
 
인증서를 사용하는 서비스 간 액세스 토큰 요청에 포함되는 매개 변수는 다음과 같습니다. 


|매개 변수|필수/선택|설명|
|-----|-----|-----| 
|grant_type|필수|토큰 요청의 유형입니다. JWT를 사용하는 요청의 경우 값은 urn:ietf:params:oauth:grant-type:jwt-bearer여야 합니다. |
|client_id|필수|첫 번째 웹 API를 서버 앱(중간 계층 앱)으로 등록할 때 구성하는 클라이언트 ID입니다. 첫 번째 레그(예: 첫 번째 웹 API의 URL)에서 사용된 리소스 ID와 동일해야 합니다.|  
|client_assertion_type|필수|값은 urn:ietf:params:oauth:client-assertion-type:jwt-bearer여야 합니다.| 
|client_assertion|필수|애플리케이션에 대한 자격 증명으로 등록한 인증서를 사용하여 만들고 서명해야 하는 어설션(JSON 웹 토큰)입니다.|  
|assertion|필수|요청에 사용된 토큰의 값입니다.| 
|requested_token_use|필수|요청을 처리하는 방법을 지정합니다. OBO 흐름에서 이 값은 on_behalf_of로 설정해야 합니다.| 
|리소스|필수|첫 번째 웹 API를 서버 앱(중간 계층 앱)으로 등록하는 동안 제공된 리소스 ID입니다. 이 리소스 ID는 클라이언트를 대신하여 앱에서 호출하는 두 번째 웹 API 중간 계층의 URL이어야 합니다.|
|scope|선택적|공백으로 구분된 토큰 요청에 대한 범위의 목록입니다.|


client_secret 매개 변수가 client_assertion_type 및 client_assertion의 두 가지 매개 변수로 대체된다는 점을 제외하고는 매개 변수가 공유 비밀을 통한 요청의 경우와 거의 동일합니다. 

#### <a name="example"></a>예제 
인증서를 사용하여 웹 API에 대한 액세스 토큰을 요청하는 HTTP POST는 다음과 같습니다.

``` 
// line breaks for legibility only 
 
POST /adfs/oauth2/token HTTP/1.1 
Host: https://adfs.contoso.com 
Content-Type: application/x-www-form-urlencoded 
 
grant_type=urn%3Aietf%3Aparams%3Aoauth%3Agrant-type%3Ajwt-bearer 
&client_id= https://webapi.com/ 
&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer 
&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNS… 
&resource=https://secondwebapi.com/
&requested_token_use=on_behalf_of
&scope= openid 
```    

### <a name="service-to-service-access-token-response"></a>서비스 간 액세스 토큰 응답 
 
성공 응답은 다음 매개 변수가 JSON OAuth 2.0 응답입니다. 


|매개 변수|설명|
|-----|-----| 
|token_type|토큰 형식 값을 나타냅니다. AD FS에서 지원하는 유일한 형식은 Bearer입니다. | 
|scope|토큰에 부여된 액세스의 범위입니다.| 
|expires_in|액세스 토큰의 유효 시간(초)입니다.| 
|access_token|요청된 액세스 토큰입니다. 호출 서비스에서 이 토큰을 사용하여 수신 서비스를 인증할 수 있습니다.| 
|id_token|JWT(JSON 웹 토큰)입니다. 앱에서 이 토큰의 세그먼트를 디코딩하여 로그인한 사용자에 대한 정보를 요청할 수 있습니다. 앱에서 값을 캐시하고 표시할 수 있지만, 권한 부여 또는 보안 경계에 이러한 값을 사용하지 않아야 합니다.| 
|refresh_token|요청된 액세스 토큰에 대한 새로 고침 토큰입니다. 현재 액세스 토큰이 만료되면 호출 서비스에서 이 토큰을 사용하여 다른 액세스 토큰을 요청할 수 있습니다.|
|Refresh_token_expires_in|새로 고침 토큰의 유효 시간(초)입니다. 

### <a name="success-response-example"></a>성공 응답 예제 
 
다음 예제에서는 웹 API의 액세스 토큰 요청에 대한 성공 응답을 보여 줍니다. 

``` 
{ 
  "token_type": "Bearer", 
  "scope": openid, 
  "expires_in": 3269, 
  "access_token": "eyJ0eXAiOiJKV1QiLCJub25jZSI6IkFRQUJBQUFBQUFCbmZpRy1t" 
  "id_token": "aWRfdG9rZW49ZXlKMGVYQWlPaUpLVjFRaUxDSmhiR2NpT2lKU1V6STFOa" 
  "refresh_token": "OAQABAAAAAABnfiG…" 
  "refresh_token_expires_in": 28800, 
} 
```  
 
 
액세스 토큰을 사용하여 보안 리소스에 액세스합니다. 이제 중간 계층 서비스는 Authorization 헤더에 토큰을 설정하여 위에서 획득한 토큰을 통해 다운스트림 웹 API에 인증된 요청을 수행할 수 있습니다.  

#### <a name="example"></a>예제 
``` 
GET /v1.0/me HTTP/1.1 
Host: https://secondwebapi.com 
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJub25jZSI6IkFRQUJBQUFBQUFCbmZpRy1tQ… 
``` 

## <a name="client-credentials-grant-flow"></a>클라이언트 자격 증명 부여 흐름 
 
[RFC 6749](https://tools.ietf.org/html/rfc6749#section-4.4)에 지정된 OAuth 2.0 클라이언트 자격 증명 부여를 사용하여 애플리케이션의 ID를 통해 웹 호스팅 리소스에 액세스할 수 있습니다. 이 유형의 부여는 일반적으로 사용자와의 즉각적인 상호 작용 없이 백그라운드에서 실행되어야 하는 서버 간 상호 작용에 사용됩니다. 이러한 유형의 애플리케이션을 종종 디먼 또는 서비스 계정이라고 합니다. 

OAuth 2.0 클라이언트 자격 증명 부여 흐름을 사용하면 웹 서비스(비밀 클라이언트)에서 다른 웹 서비스를 호출할 때 사용자를 가장하는 대신 고유한 자격 증명을 사용하여 인증할 수 있습니다. 이 시나리오에서 클라이언트는 일반적으로 중간 계층 웹 서비스, 디먼 서비스 또는 웹 사이트입니다. 또한 AD FS는 더 높은 수준의 보증을 위해 호출 서비스에서 공유 비밀 대신 인증서를 자격 증명으로 사용할 수 있습니다. 

### <a name="protocol-diagram"></a>프로토콜 다이어그램 

다음 다이어그램에서는 클라이언트 자격 증명 부여 흐름을 보여 줍니다. 

![클라이언트 자격 증명](media/adfs-scenarios-for-developers/credentials.png)

### <a name="request-a-token"></a>토큰 요청 
 
클라이언트 자격 증명 부여를 사용하여 토큰을 가져오려면 `POST` 요청을 /token AD FS 엔드포인트에 보냅니다.  
 
### <a name="first-case-access-token-request-with-a-shared-secret"></a>첫 번째 사례: 공유 비밀을 사용하여 액세스 토큰 요청 
 
```
POST /adfs/oauth2/token HTTP/1.1            
//Line breaks for clarity 
 
Host: https://adfs.contoso.com 
Content-Type: application/x-www-form-urlencoded 
 
client_id=535fb089-9ff3-47b6-9bfb-4f1264799865 
&client_secret=qWgdYAmab0YSkuL1qKv5bPX 
&grant_type=client_credentials 
```

|매개 변수|필수/선택|설명|
|-----|-----|-----| 
|client_id|필수|AD FS에서 앱에 할당한 애플리케이션(클라이언트) ID입니다.| 
|scope|선택적|사용자가 동의하도록 하려는 공백으로 구분된 범위의 목록입니다.| 
|client_secret|필수|앱 등록 포털에서 앱에 대해 생성한 클라이언트 암호입니다. 클라이언트 암호는 보내기 전에 URL로 인코딩해야 합니다.| 
|grant_type|필수| `client_credentials`로 설정해야 합니다.|

### <a name="second-case-access-token-request-with-a-certificate"></a>두 번째 사례: 인증서를 사용하여 액세스 토큰 요청 

``` 
POST /adfs/oauth2/token HTTP/1.1                
 
// Line breaks for clarity 
 
Host: https://adfs.contoso.com 
Content-Type: application/x-www-form-urlencoded 
 
&client_id=97e0a5b7-d745-40b6-94fe-5f77d35c6e05 
&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer 
&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg 
&grant_type=client_credentials  
```

|매개 변수|필수/선택|설명| 
|-----|-----|-----|
|client_assertion_type|필수|값은 urn:ietf:params:oauth:client-assertion-type:jwt-bearer로 설정해야 합니다.| 
|client_assertion|필수|애플리케이션에 대한 자격 증명으로 등록한 인증서를 사용하여 만들고 서명해야 하는 어설션(JSON 웹 토큰)입니다.|  
|grant_type|필수| `client_credentials`로 설정해야 합니다.|
|client_id|선택적|AD FS에서 앱에 할당한 애플리케이션(클라이언트) ID입니다. client_assertion의 일부이므로 여기에 전달할 필요가 없습니다.| 
|scope|선택적|사용자가 동의하도록 하려는 공백으로 구분된 범위의 목록입니다.| 

### <a name="use-a-token"></a>토큰 사용 
 
이제 토큰을 획득했으므로 토큰을 사용하여 리소스에 대한 요청을 수행합니다. 토큰이 만료되면 /token 엔드포인트에 요청을 반복하여 새 액세스 토큰을 획득합니다.  
 
```
GET /v1.0/me/messages 
Host: https://webapi.com 
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...  
```

## <a name="resource-owner-password-credentials-grant-flow-not-recommended"></a>리소스 소유자 암호 자격 증명 부여 흐름(추천되지 않음) 
 
ROPC(리소스 소유자 암호 자격 증명) 부여를 사용하면 애플리케이션에서 사용자의 암호를 직접 처리하여 사용자를 로그인할 수 있습니다. ROPC 흐름에는 높은 수준의 신뢰와 사용자 공개가 필요하며, 더 안전한 다른 흐름을 사용할 수 없는 경우에만 이 흐름을 사용해야 합니다.  
 
### <a name="protocol-diagram"></a>프로토콜 다이어그램 
 
다음 다이어그램에서는 ROPC 흐름을 보여 줍니다.

![ROPC 흐름](media/adfs-scenarios-for-developers/resource.png)

### <a name="authorization-request"></a>권한 부여 요청 
ROPC 흐름은 단일 요청입니다. 즉, 클라이언트 ID 및 사용자의 자격 증명을 IDP로 보낸 다음, 응답으로 토큰을 받습니다. 이렇게 하려면 먼저 클라이언트에서 사용자의 이메일 주소(UPN) 및 암호를 요청해야 합니다. 요청이 성공하는 즉시 클라이언트는 메모리에서 사용자의 자격 증명을 안전하게 해제해야 합니다. 이를 저장하면 안 됩니다.  

```
// Line breaks and spaces are for legibility only. 
 
POST /adfs/oauth2/token HTTP/1.1 
Host: https://adfs.contoso.com  
Content-Type: application/x-www-form-urlencoded 
 
client_id=6731de76-14a6-49ae-97bc-6eba6914391e 
&scope= openid  
&username=myusername@contoso.com 
&password=SuperS3cret 
&grant_type=password 
```


|매개 변수|필수/선택|설명| 
|-----|-----|-----|
|client_id|필수|클라이언트 ID| 
|grant_type|필수|password로 설정해야 합니다.| 
|username|필수|사용자의 전자 메일 주소입니다.| 
|password|필수|사용자의 암호입니다.| 
|scope|선택적|공백으로 구분된 범위의 목록입니다.|

### <a name="successful-authentication-response"></a>성공적인 인증 응답 
다음 예제에서는 성공적인 토큰 응답을 보여 줍니다. 

```
{ 
    "token_type": "Bearer", 
    "scope": "openid", 
    "expires_in": 3599, 
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIn...", 
    "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4...", 
    "refresh_token_expires_in": 28800, 
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDR..." 
}  
```


|매개 변수|설명| 
|-----|-----|
|token_type|항상 Bearer로 설정합니다.| 
|scope|액세스 토큰이 반환된 경우 이 매개 변수는 액세스 토큰의 유효 범위를 나열합니다.| 
|expires_in|포함된 액세스 토큰의 유효 시간(초)입니다.| 
|access_token|요청된 범위에 대해 발급됩니다.| 
|id_token|JWT(JSON 웹 토큰)입니다. 앱에서 이 토큰의 세그먼트를 디코딩하여 로그인한 사용자에 대한 정보를 요청할 수 있습니다. 앱에서 값을 캐시하고 표시할 수 있지만, 권한 부여 또는 보안 경계에 이러한 값을 사용하지 않아야 합니다.| 
|refresh_token_expires_in|포함된 새로 고침 토큰의 유효 시간(초)입니다.| 
|refresh_token|원본의 범위 매개 변수에 offline_access가 포함된 경우 발급됩니다.|

위의 인증 코드 부여 흐름 섹션에서 설명한 것과 동일한 흐름을 사용하여 새로 고침 토큰을 통해 새 액세스 토큰을 획득하고 토큰을 새로 고칠 수 있습니다.   

## <a name="device-code-flow"></a>디바이스 코드 흐름 
 
디바이스 코드 부여를 사용하면 사용자가 스마트 TV, IoT 디바이스 또는 프린터와 같은 입력 제한 디바이스에 로그인할 수 있습니다. 이 흐름을 사용하도록 설정하기 위해 디바이스에서 사용자가 다른 디바이스의 브라우저에 있는 웹 페이지를 방문하여 로그인하도록 합니다. 사용자가 로그인하면 디바이스에서 액세스 토큰을 가져오고 필요에 따라 해당 토큰을 새로 고칠 수 있습니다. 
 
### <a name="protocol-diagram"></a>프로토콜 다이어그램 
 
전체 디바이스 코드 흐름은 다음 다이어그램과 비슷합니다. 이 문서의 뒷부분에서 각 단계에 대해 설명합니다. 
 
![디바이스 코드 흐름](media/adfs-scenarios-for-developers/device.png)

### <a name="device-authorization-request"></a>디바이스 권한 부여 요청 
클라이언트에서 먼저 인증을 시작하는 데 사용되는 디바이스 및 사용자 코드에 대한 인증 서버를 확인해야 합니다. 클라이언트는 /devicecode 엔드포인트에서 이 요청을 수집합니다. 이 요청에서 클라이언트는 사용자로부터 획득해야 하는 권한도 포함해야 합니다. 사용자는 이 요청을 보낸 시점부터 15분(일반적인 terms_in 값) 동안만 로그인할 수 있으므로 사용자가 로그인할 준비가 되었음을 나타내는 경우에만 이 요청을 수행합니다. 

```
// Line breaks are for legibility only. 
 
POST https://adfs.contoso.com/adfs/oauth2/devicecode 
Content-Type: application/x-www-form-urlencoded 
 
client_id=6731de76-14a6-49ae-97bc-6eba6914391e 
scope=openid 
```


|매개 변수|조건|설명|
|-----|-----|-----| 
|client_id|필수|AD FS에서 앱에 할당한 애플리케이션(클라이언트) ID입니다.| 
|scope|선택적|공백으로 구분된 범위의 목록입니다.|

### <a name="device-authorization-response"></a>디바이스 권한 부여 응답 
성공적인 응답은 사용자가 로그인할 수 있게 하는 데 필요한 정보가 포함된 JSON 개체입니다. 


|매개 변수|설명|
|-----|-----| 
|device_code|클라이언트와 권한 부여 서버 간의 세션을 확인하는 데 사용되는 긴 문자열입니다. 클라이언트에서 이 매개 변수를 사용하여 권한 부여 서버의 액세스 토큰을 요청합니다.| 
|user_code|보조 디바이스의 세션을 식별하는 데 사용되어 사용자에게 표시되는 짧은 문자열입니다.| 
|verification_uri|로그인하기 위해 사용자가 user_code를 사용하여 이동해야 하는 URI입니다.| 
|verification_uri_complete|로그인하기 위해 사용자가 user_code를 사용하여 이동해야 하는 URI입니다. user_code를 사용하여 미리 채워져 있으므로 사용자가 user_code를 입력할 필요가 없습니다.| 
|expires_in|device_code 및 user_code가 만료될 때까지의 시간(초)입니다.| 
|interval|클라이언트에서 폴링 요청 간에 가 대기해야 하는 시간(초)입니다.| 
|message|사용자를 위한 지침이 포함된 사람이 읽을 수 있는 문자열입니다. 이는 쿼리 매개 변수를 ?mkt=xx-XX 형식의 요청에 포함시키고 해당 언어 문화권 코드를 입력하여 지역화할 수 있습니다.  

### <a name="authenticating-the-user"></a>사용자 인증 
user_code 및 verification_uri를 받은 후 클라이언트에서 사용자에게 이러한 항목을 표시하여 휴대폰 또는 PC 브라우저를 통해 로그인하도록 지시합니다. 또한 클라이언트에서 QR 코드 또는 비슷한 메커니즘을 사용하여 verfication_uri_complete을 표시할 수 있습니다. 이 경우 사용자에 대한 user_code를 입력하는 단계가 수행됩니다. 사용자가 verification_uri에서 인증하는 동안 클라이언트에서 device_code를 사용하여 요청된 토큰에 대한 /token 엔드포인트를 폴링해야 합니다. 

```
POST https://adfs.contoso.com /adfs/oauth2/token 
Content-Type: application/x-www-form-urlencoded 
 
grant_type: urn:ietf:params:oauth:grant-type:device_code 
client_id: 6731de76-14a6-49ae-97bc-6eba6914391e 
device_code: GMMhmHCXhWEzkobqIHGG_EnNYYsAkukHspeYUk9E8 
```


|매개 변수|필수|설명|
|-----|-----|-----| 
|grant_type|필수|urn:ietf:params:oauth:grant-type:device_code여야 합니다.| 
|client_id|필수|초기 요청에 사용된 client_id와 일치해야 합니다.| 
|code|필수|디바이스 권한 부여 요청에서 반환된 device_code입니다.|

### <a name="successful-authentication-response"></a>성공적인 인증 응답 
성공적인 토큰 응답은 다음과 같습니다.  


|매개 변수|설명|
|-----|-----| 
|token_type|항상 Bearer입니다.| 
|scope|액세스 토큰이 반환된 경우 이 매개 변수는 액세스 토큰의 유효 범위를 나열합니다.| 
|expires_in|포함된 액세스 토큰이 유효하게 될 때까지의 시간(초)입니다.| 
|access_token|요청된 범위에 대해 발급됩니다.| 
|id_token|원본의 범위 매개 변수에 openid 범위가 포함된 경우 발급됩니다.| 
|refresh_token|원본의 범위 매개 변수에 offline_access가 포함된 경우 발급됩니다.| 
|refresh_token_expires_in|포함된 새로 고침 토큰이 유효하게 될 때까지의 시간(초)입니다.| 


## <a name="related-content"></a>관련 콘텐츠  
관련 흐름을 사용하는 방법에 대한 단계별 지침을 제공하는 전체 연습 문서 목록은 [AD FS 개발](../AD-FS-Development.md)을 참조하세요. 
