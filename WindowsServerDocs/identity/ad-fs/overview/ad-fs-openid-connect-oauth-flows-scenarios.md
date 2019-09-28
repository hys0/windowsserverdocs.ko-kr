---
ms.assetid: 8a64545b-16bd-4c13-a664-cdf4c6ff6ea0
title: AD FS Openid connect Connect/OAuth 흐름 및 응용 프로그램 시나리오
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
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385597"
---
# <a name="ad-fs-openid-connectoauth-flows-and-application-scenarios"></a>AD FS Openid connect Connect/OAuth 흐름 및 응용 프로그램 시나리오
AD FS 2016 이상에 적용 됩니다.


|시나리오|샘플을 사용 하는 시나리오 연습|OAuth 2.0 Flow/Grant|클라이언트 유형|
|-----|-----|-----|-----|
|단일 페이지 앱</br> | &bull;[ADAL을 사용 하는 샘플](../development/Single-Page-Application-with-AD-FS.md)|[명시적](#implicit-grant-flow)|Public| 
|사용자가 로그인 하는 웹 앱</br> | &bull;[OWIN를 사용 하는 샘플](../development/enabling-openid-connect-with-ad-fs.md)|[인증 코드](#authorization-code-grant-flow)|공개, 기밀|  
|네이티브 앱이 Web API를 호출 합니다.</br>|&bull;[MSAL을 사용 하는 샘플](../development/msal/adfs-msal-native-app-web-api.md)</br>&bull;[ADAL을 사용 하는 샘플](../development/native-client-with-ad-fs.md)|[인증 코드](#authorization-code-grant-flow)|Public|   
|웹 앱이 Web API를 호출 합니다.</br>|&bull;[MSAL을 사용 하는 샘플](../development/msal/adfs-msal-web-app-web-api.md)</br>&bull;[ADAL을 사용 하는 샘플](../development/enabling-oauth-confidential-clients-with-ad-fs.md)|[인증 코드](#authorization-code-grant-flow)|Confidential| 
|Web API는 (OBO) 사용자를 대신 하 여 다른 웹 API를 호출 합니다.</br>|&bull;[MSAL을 사용 하는 샘플](../development/msal/adfs-msal-web-api-web-api.md)</br>&bull;[ADAL을 사용 하는 샘플](../development/ad-fs-on-behalf-of-authentication-in-windows-server.md)|[대리](#on-behalf-of-flow)|웹 앱은 기밀 역할을 합니다.| 
|디먼 앱이 Web API를 호출 합니다.||[클라이언트 자격 증명](#client-credentials-grant-flow)|Confidential| 
|웹 앱은 사용자 자격 증명을 사용 하 여 Web API를 호출 합니다.||[리소스 소유자 암호 자격 증명](#resource-owner-password-credentials-grant-flow-not-recommended)|공개, 기밀| 
|Browserless 앱 호출 Web API||[장치 코드](#device-code-flow)|공개, 기밀| 

## <a name="implicit-grant-flow"></a>암시적 허용 흐름 
 
단일 페이지 응용 프로그램 (AngularJS, Ember.js, node.js 등)의 경우 AD FS OAuth 2.0 암시적 권한 부여 흐름을 지원 합니다. 암시적 흐름은 [OAuth 2.0 사양](https://tools.ietf.org/html/rfc6749#section-4.2)에 설명 되어 있습니다. 주요 장점은 앱이 백 엔드 서버 자격 증명 교환을 수행 하지 않고 AD FS에서 토큰을 가져올 수 있다는 것입니다. 이렇게 하면 앱에서 사용자에 게 로그인 하 고, 세션을 유지 관리 하 고, 클라이언트 JavaScript 코드 내에서 다른 web Api에 대 한 토큰을 가져올 수 있습니다.  [클라이언트](https://tools.ietf.org/html/rfc6749#section-10.3)와 관련 된 암시적 흐름을 사용 하는 경우 고려해 야 할 몇 가지 중요 한 보안 고려 사항이 있습니다.  
 
암시적 흐름 및 AD FS를 사용 하 여 JavaScript 앱에 인증을 추가 하려면 아래 일반적인 단계를 수행 합니다.  
  
### <a name="protocol-diagram"></a>프로토콜 다이어그램

다음 다이어그램에서는 전체 암시적 로그인 흐름이 어떻게 표시 되는지 보여 줍니다. 다음 섹션에서는 각 단계에 대해 자세히 설명 합니다.  

![암시적 로그인](media/adfs-scenarios-for-developers/implicit.png)

### <a name="request-id-token-and-access-token"></a>요청 ID 토큰 및 액세스 토큰 
 
처음에 사용자를 앱에 로그인 하기 위해 Openid connect Connect 인증 요청을 보내고 AD FS 끝점에서 id_token 및 액세스 토큰을 가져올 수 있습니다.  
 
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
|client_id|필수|앱에 할당 AD FS는 응용 프로그램 (클라이언트) ID입니다.| 
|response_type|필수|Openid connect Connect `id_token`로그인을 포함 해야 합니다. Response_type @ no__t-0도 포함 될 수 있습니다. 여기에서 토큰을 사용 하면 앱이 토큰 끝점에 대 한 두 번째 요청을 수행 하지 않고도 권한 부여 끝점에서 즉시 액세스 토큰을 받을 수 있습니다.| 
|redirect_uri|필수|앱에서 인증 응답을 보내고 받을 수 있는 앱의 redirect_uri입니다. AD FS에서 구성한 redirect_uris 중 하 나와 정확 하 게 일치 해야 합니다.| 
|임시|필수|앱에서 생성 한 요청에 포함 된 값으로, 결과로 생성 된 id_token에 클레임으로 포함 됩니다. 그러면 앱에서 토큰 재생 공격을 완화 하기 위해이 값을 확인할 수 있습니다. 값은 일반적으로 요청의 출처를 식별 하는 데 사용할 수 있는 임의의 고유 문자열입니다. Id_token가 요청 된 경우에만 필요 합니다.|
|범위|선택적|공백으로 구분 된 범위 목록입니다. Openid connect Connect의 경우 범위 `openid`를 포함 해야 합니다.|
|resource|선택적|웹 API의 url입니다.</br>참고 – MSAL 클라이언트 라이브러리를 사용 하는 경우 리소스 매개 변수가 전송 되지 않습니다. 대신 리소스 url은 범위 매개 변수의 일부로 전송 됩니다.`scope = [resource url]//[scope values e.g., openid]`</br>리소스가 여기에 전달 되지 않거나 범위에서 ADFS는 기본 리소스 urn: microsoft: userinfo를 사용 합니다. MFA, 발급 또는 권한 부여 정책과 같은 사용자 정보 리소스 정책은 사용자 지정할 수 없습니다.| 
|response_mode|선택적| 결과 토큰을 앱에 다시 보내는 데 사용 해야 하는 메서드를 지정 합니다. 기본값은 `fragment`입니다.| 
|state|선택적|토큰 응답에도 반환 되는 요청에 포함 된 값입니다. 원하는 모든 콘텐츠의 문자열일 수 있습니다. 임의로 생성 된 고유 값은 일반적으로 교차 사이트 요청 위조 공격을 방지 하는 데 사용 됩니다. 상태는 인증 요청이 발생 하기 전에 앱에서 사용자 상태에 대 한 정보 (예: 설정 된 페이지 또는 보기)를 인코딩하는 데도 사용 됩니다.| 
|prompt|선택적|필요한 사용자 상호 작용의 유형을 나타냅니다. 현재 유일 하 게 유효한 값은 로그인 이며 없음입니다.</br>- `prompt=login` 는 사용자가 해당 요청에 대 한 자격 증명을 입력 하도록 하 여 single sign-on을 부정 합니다. </br>- `prompt=none` 그 반대의 경우에는 사용자에 게 대화형 프롬프트가 표시 되지 않습니다. Single sign-on을 통해 요청을 자동으로 완료할 수 없는 경우 AD FS는 interaction_required 오류를 반환 합니다.| 
|login_hint|선택적|사용자의 사용자 이름을 미리 알고 있는 경우 사용자에 대 한 로그인 페이지의 사용자 이름/이메일 주소 필드를 미리 채우는 데 사용할 수 있습니다. 앱에서 `upn`클레임을 사용 하 여 이전 로그인에서 사용자 이름을 이미 추출 하 여 다시 인증 하는 동안이 매개 변수를 사용 하는 경우가 많습니다. `id_token`| 
|domain_hint|선택적|포함 되는 경우 사용자가 로그인 페이지에서 이동 하는 도메인 기반 검색 프로세스를 건너뛰고 약간 더 간소화 된 사용자 환경을 제공 합니다.| 

이 시점에서 사용자에 게 자격 증명을 입력 하 고 인증을 완료 하 라는 메시지가 표시 됩니다. 사용자가 AD FS 인증 되 면 response_mode 매개 변수에 지정 된 메서드를 사용 하 여 지정 된 redirect_uri에서 앱에 대 한 응답을 반환 합니다.  
 
### <a name="successful-response"></a>성공적인 응답 
 
을 사용 하 `response_mode=fragment and response_type=id_token+token` 는 성공적인 응답은 다음과 같습니다.  
 
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
|access_token|Response_type에 @ no__t-0이 포함 된 경우 포함 됩니다.|
|token_type|Response_type에 @ no__t-0이 포함 된 경우 포함 됩니다. 는 항상 전달자입니다.| 
|expires_in| Response_type에 @ no__t-0이 포함 된 경우 포함 됩니다. 캐싱을 위해 토큰이 유효한 시간 (초)을 나타냅니다.| 
|범위| Access_token이 유효한 범위를 나타냅니다.|  
|id_token|Response_type에 @ no__t-0이 포함 된 경우 포함 됩니다. JWT (서명 된 JSON Web Token)입니다. 앱은이 토큰의 세그먼트를 디코드 하 여 로그인 한 사용자에 대 한 정보를 요청할 수 있습니다. 앱은 값을 캐시 하 고 표시할 수 있지만 권한 부여 또는 보안 경계에는이 값을 사용 하지 않아야 합니다.| 
|state|요청에 state 매개 변수가 포함 되어 있으면 동일한 값이 응답에 표시 되어야 합니다. 앱은 요청 및 응답의 상태 값이 동일한 지 확인 해야 합니다.|

### <a name="refresh-tokens"></a>토큰 새로 고침 
암시적 권한 부여는 새로 고침 토큰을 제공 하지 않습니다.  `id_tokens` 및 `access_tokens` 는 짧은 기간 후에 만료 되므로 앱이 정기적으로 이러한 토큰을 새로 고칠 수 있도록 준비 해야 합니다. 두 가지 유형의 토큰을 새로 고치려면 `prompt=none` 매개 변수를 사용 하 여 위와 동일한 숨겨진 iframe 요청을 수행 하 여 id 플랫폼의 동작을 제어할 수 있습니다. 를 수신 `new id_token`하려면를 사용 `response_type=id_token`해야 합니다. 

## <a name="authorization-code-grant-flow"></a>인증 코드 부여 흐름 
 
OAuth 2.0 인증 코드 부여는 웹 Api와 같은 보호 된 리소스에 대 한 액세스 권한을 얻기 위해 웹 앱에서 사용할 수 있습니다. OAuth 2.0 인증 코드 흐름은 [oauth 2.0 사양의 섹션 4.1](https://tools.ietf.org/html/rfc6749)에 설명 되어 있습니다. 웹 앱 및 기본적으로 설치 된 앱을 비롯 하 여 대부분의 앱 형식에서 인증 및 권한 부여를 수행 하는 데 사용 됩니다. 흐름을 통해 앱은 AD FS를 신뢰 하는 리소스에 액세스 하는 데 사용할 수 있는 access_tokens를 안전 하 게 획득할 수 있습니다.  
 
### <a name="protocol-diagram"></a>프로토콜 다이어그램 
 
상위 수준에서 네이티브 응용 프로그램에 대 한 인증 흐름은 다음과 같습니다.

![인증 코드 부여 흐름](media/adfs-scenarios-for-developers/authorization.png)

### <a name="request-an-authorization-code"></a>인증 코드 요청 
 
권한 부여 코드 흐름은 클라이언트에서 시작 하 여 사용자에 게/crl 끝점을 지시 합니다. 이 요청에서 클라이언트는 사용자 로부터 획득 해야 하는 권한을 나타냅니다. 
 
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
|client_id|필수|앱에 할당 AD FS는 응용 프로그램 (클라이언트) ID입니다.|  
|response_type|필수| 인증 코드 흐름에 대 한 코드를 포함 해야 합니다.| 
|redirect_uri|필수|앱에서 인증 응답을 보내고 받을 수 있는 앱 의입니다.`redirect_uri` 클라이언트의 AD FS에 등록 한 redirect_uris 중 하 나와 정확 하 게 일치 해야 합니다.|  
|resource|선택적|웹 API의 url입니다.</br>참고 – MSAL 클라이언트 라이브러리를 사용 하는 경우 리소스 매개 변수가 전송 되지 않습니다. 대신 리소스 url은 범위 매개 변수의 일부로 전송 됩니다.`scope = [resource url]//[scope values e.g., openid]`</br>리소스가 여기에 전달 되지 않거나 범위에서 ADFS는 기본 리소스 urn: microsoft: userinfo를 사용 합니다. MFA, 발급 또는 권한 부여 정책과 같은 사용자 정보 리소스 정책은 사용자 지정할 수 없습니다.| 
|범위|선택적|공백으로 구분 된 범위 목록입니다.|
|response_mode|선택적|결과 토큰을 앱에 다시 보내는 데 사용 해야 하는 메서드를 지정 합니다. 다음 중 하나일 수 있습니다. </br>-쿼리 </br>-조각 </br>- form_post</br>`query` 코드를 리디렉션 URI에 대 한 쿼리 문자열 매개 변수로 제공 합니다. 코드를 요청 하는 경우 쿼리, 조각 또는 form_post를 사용할 수 있습니다.  `form_post` @ no__t-1은 코드를 포함 하는 POST를 리디렉션 URI에 실행 합니다.|
|state|선택적|토큰 응답에도 반환 되는 요청에 포함 된 값입니다. 원하는 모든 콘텐츠의 문자열일 수 있습니다. 임의로 생성 된 고유 값은 일반적으로 교차 사이트 요청 위조 공격을 방지 하는 데 사용 됩니다. 또한이 값은 인증 요청이 발생 하기 전에 앱에서 사용자 상태에 대 한 정보 (예: 설정 된 페이지 또는 보기)를 인코딩할 수 있습니다.|
|prompt|선택적|필요한 사용자 상호 작용의 유형을 나타냅니다. 현재 유일 하 게 유효한 값은 로그인 이며 없음입니다.</br>- `prompt=login` 는 사용자가 해당 요청에 대 한 자격 증명을 입력 하도록 하 여 single sign-on을 부정 합니다. </br>- `prompt=none` 그 반대의 경우에는 사용자에 게 대화형 프롬프트가 표시 되지 않습니다. Single sign-on을 통해 요청을 자동으로 완료할 수 없는 경우 AD FS는 interaction_required 오류를 반환 합니다.|
|login_hint|선택적|사용자의 사용자 이름을 미리 알고 있는 경우 사용자에 대 한 로그인 페이지의 사용자 이름/이메일 주소 필드를 미리 채우는 데 사용할 수 있습니다. 앱에서 `upn` `id_token`클레임을 사용 하 여 이전 로그인에서 사용자 이름을 이미 추출 하 여 다시 인증 하는 동안이 매개 변수를 사용 하는 경우가 많습니다.|
|domain_hint|선택적|포함 되는 경우 사용자가 로그인 페이지에서 이동 하는 도메인 기반 검색 프로세스를 건너뛰고 약간 더 간소화 된 사용자 환경을 제공 합니다.|
|code_challenge_method|선택적|Code_challenge 매개 변수에 대 한 code_verifier를 인코딩하는 데 사용 되는 메서드입니다. 다음 값 중 하나입니다. </br>-일반 </br>- S256 </br>제외 하는 경우 @ no__t-0 @ no__t-1is가 포함 된 경우 code_challenge는 일반 텍스트로 간주 됩니다. AD FS는 일반 및 S256을 모두 지원 합니다. 자세한 내용은 [Pkce RFC](https://tools.ietf.org/html/rfc7636)를 참조 하세요.|
|code_challenge|선택적| 인증 코드의 보안을 유지 하는 데 사용 됩니다. 가 포함 `code_challenge_method`된 경우 필수입니다. 자세한 내용은 [Pkce RFC](https://tools.ietf.org/html/rfc7636) 를 참조 하세요.|

이 시점에서 사용자에 게 자격 증명을 입력 하 고 인증을 완료 하 라는 메시지가 표시 됩니다. 사용자가 AD FS 인증 되 면 `redirect_uri` 매개 변수에 지정 `response_mode`된 메서드를 사용 하 여 지정 된에서 앱에 대 한 응답을 반환 합니다.  
 
### <a name="successful-response"></a>성공적인 응답 
 
Response_mode = query를 사용 하는 성공적인 응답은 다음과 같습니다. 
 
```
GET https://adfs.contoso.com/common/oauth2/nativeclient? 
code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq... 
&state=12345  
```


|매개 변수|설명|
|-----|-----|
|code|앱 `authorization_code` 이 요청한입니다. 앱은 권한 부여 코드를 사용 하 여 대상 리소스에 대 한 액세스 토큰을 요청할 수 있습니다. Authorization_codes은 수명이 짧습니다. 일반적으로 약 10 분 후에 만료 됩니다.|
|state|요청에 `state` 매개 변수가 포함 되어 있으면 동일한 값이 응답에 표시 되어야 합니다. 앱은 요청 및 응답의 상태 값이 동일한 지 확인 해야 합니다.|

### <a name="request-an-access-token"></a>액세스 토큰 요청 
 
를 획득 `authorization_code` 하 고 사용자가 사용 권한을 부여 했으므로 이제 `access_token` 에 대 한 코드를 원하는 리소스로 전환할 수 있습니다. 이 작업을 수행 하려면/stoken 끝점에 POST 요청을 보냅니다.  
 
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

|매개 변수|필수/옵션|설명|
|-----|-----|-----| 
|client_id|필수|앱에 할당 AD FS는 응용 프로그램 (클라이언트) ID입니다.| 
|grant_type|필수|인증 코드 흐름의 경우 이어야 합니다.  `authorization_code`| 
|code|필수|흐름의 첫 번째 레그에서 가져온 입니다.`authorization_code`| 
|redirect_uri|필수|`redirect_uri` 을`authorization_code`획득 하는 데 사용 된 것과 동일한 값입니다.| 
|client_secret|웹 앱에 필요|AD FS에서 앱을 등록 하는 동안 만든 응용 프로그램 암호입니다. Client_secrets를 장치에 안정적으로 저장할 수 없기 때문에 네이티브 앱에서 응용 프로그램 암호를 사용 하면 안 됩니다. Client_secret을 서버 쪽에 안전 하 게 저장할 수 있는 웹 앱과 web Api에 필요 합니다. 클라이언트 암호를 보내기 전에 URL로 인코딩해야 합니다. 이러한 앱은 JWT에 서명 하 고 client_assertion 매개 변수로 추가 하 여 키 기반 인증을 사용할 수도 있습니다.| 
|code_verifier|선택적|Authorization_code를 가져오는 데 사용 된 것과 동일한 `code_verifier`입니다. 권한 부여 코드 부여 요청에서 PKCE를 사용한 경우에 필요 합니다. 자세한 내용은 [Pkce RFC](https://tools.ietf.org/html/rfc7636)를 참조 하세요.</br>참고 – AD FS 2019 이상에 적용 됩니다.| 

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
|access_token|요청 된 액세스 토큰입니다. 앱은이 토큰을 사용 하 여 보안 리소스 (Web API)에 인증할 수 있습니다.| 
|token_type|토큰 유형 값을 나타냅니다. AD FS 지원 되는 유일한 형식은 전달자입니다.
|expires_in|액세스 토큰이 유효한 기간 (초)입니다.
|refresh_token|OAuth 2.0 새로 고침 토큰입니다. 앱은 현재 액세스 토큰이 만료 된 후이 토큰을 사용 하 여 추가 액세스 토큰을 획득할 수 있습니다. Refresh_tokens은 수명이 길며, 오랜 시간 동안 리소스에 대 한 액세스를 유지 하는 데 사용할 수 있습니다.| 
|refresh_token_expires_in|새로 고침 토큰이 유효한 기간 (초)입니다.| 
|id_token|JWT (JSON Web Token)입니다. 앱은이 토큰의 세그먼트를 디코드 하 여 로그인 한 사용자에 대 한 정보를 요청할 수 있습니다. 앱은 값을 캐시 하 고 표시할 수 있지만 권한 부여 또는 보안 경계에 의존 하지 않아야 합니다.|

### <a name="use-the-access-token"></a>액세스 토큰 사용 
 
```
GET /v1.0/me/messages 
Host: https://webapi.com 
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q... 
 ```

### <a name="refresh-the-access-token"></a>액세스 토큰 새로 고침 
 
Access_tokens은 수명이 짧고 리소스에 계속 액세스할 수 있도록 만료 된 후 새로 고쳐야 합니다. @ No__t-0 @ no__t 끝점에 다른 POST 요청을 제출 하 여이 작업을 수행할 수 있습니다. 이번에는 코드 대신 refresh_token를 제공 합니다. 새로 고침 토큰은 클라이언트에서 이미 액세스 토큰을 받은 모든 사용 권한에 대해 유효 합니다. 
 
새로 고침 토큰에 지정 된 수명이 없습니다. 일반적으로 새로 고침 토큰의 수명은 비교적 깁니다. 그러나 경우에 따라 새로 고침 토큰이 만료 되거나 해지 되거나 원하는 작업을 수행할 수 있는 권한이 부족 합니다. 응용 프로그램은 토큰 발급 끝점에서 반환 하는 오류를 정확 하 게 예측 하 고 처리 해야 합니다.  
 
새로 고침 토큰은 새 액세스 토큰을 획득 하는 데 사용 될 때 해지 되지 않지만 이전 새로 고침 토큰을 삭제 해야 합니다. OAuth 2.0 spec은 다음을 의미 합니다. "권한 부여 서버에서 새 새로 고침 토큰을 발급할 수 있습니다 .이 경우 클라이언트는 이전 새로 고침 토큰을 삭제 하 고 새 새로 고침 토큰으로 바꾸어야 합니다. 권한 부여 서버에서 새 새로 고침 토큰을 클라이언트에 발급 한 후 이전 새로 고침 토큰을 해지할 수 있습니다. " 
 
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
|client_id|필수|앱에 할당 AD FS는 응용 프로그램 (클라이언트) ID입니다.| 
|grant_type|필수|이 인증 코드 흐름의 레그에대해이어야합니다.  `refresh_token`| 
|resource|선택적|웹 API의 url입니다.</br>참고 – MSAL 클라이언트 라이브러리를 사용 하는 경우 리소스 매개 변수가 전송 되지 않습니다. 대신 리소스 url은 범위 매개 변수의 일부로 전송 됩니다.`scope = [resource url]//[scope values e.g., openid]`</br>리소스가 여기에 전달 되지 않거나 범위에서 ADFS는 기본 리소스 urn: microsoft: userinfo를 사용 합니다. MFA, 발급 또는 권한 부여 정책과 같은 사용자 정보 리소스 정책은 사용자 지정할 수 없습니다.|
|범위|선택적|공백으로 구분 된 범위 목록입니다.| 
|refresh_token|필수|흐름의 두 번째 레그에서 얻은 refresh_token입니다.| 
|client_secret|웹 앱에 필요| 앱에 대 한 앱 등록 포털에서 만든 응용 프로그램 암호입니다. Client_secrets를 장치에 안정적으로 저장할 수 없기 때문에 네이티브 앱에서 사용 하면 안 됩니다. Client_secret을 서버 쪽에 안전 하 게 저장할 수 있는 웹 앱과 web Api에 필요 합니다. 이러한 앱은 JWT에 서명 하 고 client_assertion 매개 변수로 추가 하 여 키 기반 인증을 사용할 수도 있습니다.|

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
|access_token|요청 된 액세스 토큰입니다. 앱은이 토큰을 사용 하 여 web API와 같은 보안 리소스를 인증할 수 있습니다.| 
|token_type|토큰 유형 값을 나타냅니다. AD FS 지원 되는 유일한 형식은 전달자입니다.|
|expires_in|액세스 토큰이 유효한 기간 (초)입니다.|
|범위|Access_token이 유효한 범위입니다.| 
|refresh_token|OAuth 2.0 새로 고침 토큰입니다. 앱은 현재 액세스 토큰이 만료 된 후이 토큰을 사용 하 여 추가 액세스 토큰을 획득할 수 있습니다. Refresh_tokens은 수명이 길며, 오랜 시간 동안 리소스에 대 한 액세스를 유지 하는 데 사용할 수 있습니다.| 
|refresh_token_expires_in|새로 고침 토큰이 유효한 기간 (초)입니다.| 
|id_token|JWT (JSON Web Token)입니다. 앱은이 토큰의 세그먼트를 디코드 하 여 로그인 한 사용자에 대 한 정보를 요청할 수 있습니다. 앱은 값을 캐시 하 고 표시할 수 있지만 권한 부여 또는 보안 경계에 의존 하지 않아야 합니다.|

## <a name="on-behalf-of-flow"></a>흐름에 대 한 
 
OAuth 2.0 OBO (주문형 흐름)는 응용 프로그램이 서비스/웹 API를 호출 하는 사용 사례를 제공 하며,이를 통해 다른 서비스/웹 API를 호출 해야 합니다. 이 개념은 요청 체인을 통해 위임 된 사용자 id 및 사용 권한을 전파 하는 것입니다. 중간 계층 서비스에서 다운스트림 서비스로 인증 된 요청을 수행 하려면 사용자를 대신 하 여 AD FS에서 액세스 토큰을 보호 해야 합니다.  
 
### <a name="protocol-diagram"></a>프로토콜 다이어그램 
위에서 설명한 OAuth 2.0 인증 코드 부여 흐름을 사용 하 여 사용자가 응용 프로그램에서 인증 된 것으로 가정 합니다. 이 시점에서 응용 프로그램은 사용자의 클레임을 포함 하는 API A (토큰 A)에 대 한 액세스 토큰을 포함 하 고 중간 계층 web API (API A)에 액세스 하는 데 동의 합니다. 클라이언트에서 토큰의 user_impersonation 범위를 요청 하는지 확인 합니다. 이제 API A는 다운스트림 web API (API B)에 인증 된 요청을 해야 합니다. 

다음 단계는 OBO flow를 구성 하 고 다음 다이어그램의 도움으로 설명 됩니다. 

![흐름에 대 한](media/adfs-scenarios-for-developers/obo.png)

  1. 클라이언트 응용 프로그램은 토큰 A를 사용 하 여 API A를 요청 합니다.  
  참고: AD FS에서 obo flow를 구성 하는 동안 `user_impersonation` 범위가 선택 되어 있는지 확인 `user_impersonation` 하 고 요청에서 클라이언트에서 요청 범위를 요청 합니다. 
  2. API A는 AD FS 토큰 발급 끝점을 인증 하 고 API B에 액세스 하기 위한 토큰을 요청 합니다. 참고: AD FS에서이 흐름을 구성 하는 동안 api A가 API A의 리소스 ID와 동일한 값을 갖는 서버 응용 프로그램으로 등록 되어 있는지 확인 합니다. 자세한 내용은 여기에 있는 샘플 추가 링크를 참조 하세요.  
  3. 토큰 발급 끝점 AD FS 토큰 A를 사용 하 여 API A의 자격 증명의 유효성을 검사 하 고 API B (토큰 B)에 대 한 액세스 토큰을 발급 합니다. 
  4. 토큰 B는 API B에 대 한 요청의 권한 부여 헤더에 설정 됩니다. 
  5. 보안 리소스의 데이터는 API B에서 반환 됩니다. 

### <a name="service-to-service-access-token-request"></a>서비스 간 액세스 토큰 요청 
 
액세스 토큰을 요청 하려면 다음 매개 변수를 사용 하 여 AD FS 토큰 끝점에 HTTP POST를 수행 합니다.  


### <a name="first-case-access-token-request-with-a-shared-secret"></a>첫 번째 사례: 공유 암호를 사용 하 여 액세스 토큰 요청 
 
공유 암호를 사용 하는 경우 서비스 간 액세스 토큰 요청에는 다음 매개 변수가 포함 됩니다. 


|매개 변수|필수/선택|설명|
|-----|-----|-----| 
|grant_type|필수|토큰 요청의 유형입니다. JWT를 사용 하는 요청의 경우 값은 urn: ietf: params: oauth: grant-type: jwt-전달자 여야 합니다.|  
|client_id|필수|첫 번째 Web API를 서버 앱 (중간 계층 앱)으로 등록할 때 구성 하는 클라이언트 ID입니다. 첫 번째 웹 API의 첫 번째 레그 url에 사용 된 리소스 ID와 동일 해야 합니다.| 
|client_secret|필수|AD FS에서 서버 앱을 등록 하는 동안 만든 응용 프로그램 암호입니다.| 
|assertion|필수|요청에 사용 되는 토큰의 값입니다.|  
|requested_token_use|필수|요청을 처리 하는 방법을 지정 합니다. OBO 흐름에서 값을 on_behalf_of로 설정 해야 합니다.| 
|resource|필수|첫 번째 Web API를 서버 앱 (중간 계층 앱)으로 등록 하는 동안 제공 된 리소스 ID입니다. 리소스 ID는 클라이언트를 대신 하 여 호출 하는 두 번째 Web API 중간 계층 앱의 url 이어야 합니다.|
|범위|선택적|토큰 요청에 대 한 공백으로 구분 된 범위 목록입니다.| 

#### <a name="example"></a>예제 
 
다음 `HTTP POST` 은 액세스 토큰과 새로 고침 토큰을 요청 합니다. 
 
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

### <a name="second-case-access-token-request-with-a-certificate"></a>두 번째 사례: 인증서를 사용 하 여 액세스 토큰 요청 
 
인증서를 사용 하는 서비스 간 액세스 토큰 요청에는 다음 매개 변수가 포함 됩니다. 


|매개 변수|필수/선택|설명|
|-----|-----|-----| 
|grant_type|필수|토큰 요청의 유형입니다. JWT를 사용 하는 요청의 경우 값은 urn: ietf: params: oauth: grant-type: jwt-전달자 여야 합니다. |
|client_id|필수|첫 번째 Web API를 서버 앱 (중간 계층 앱)으로 등록할 때 구성 하는 클라이언트 ID입니다. 첫 번째 웹 API의 첫 번째 레그 url에 사용 된 리소스 ID와 동일 해야 합니다.|  
|client_assertion_type|필수|값은 urn: ietf: params: oauth: client-assertion: jwt-전달자 여야 합니다.| 
|client_assertion|필수|응용 프로그램에 대 한 자격 증명으로 등록 한 인증서를 사용 하 여 만들고 서명 해야 하는 어설션 (JSON 웹 토큰)입니다.|  
|assertion|필수|요청에 사용 되는 토큰의 값입니다.| 
|requested_token_use|필수|요청을 처리 하는 방법을 지정 합니다. OBO 흐름에서 값을 on_behalf_of로 설정 해야 합니다.| 
|resource|필수|첫 번째 Web API를 서버 앱 (중간 계층 앱)으로 등록 하는 동안 제공 된 리소스 ID입니다. 리소스 ID는 클라이언트를 대신 하 여 호출 하는 두 번째 Web API 중간 계층 앱의 url 이어야 합니다.|
|범위|선택적|토큰 요청에 대 한 공백으로 구분 된 범위 목록입니다.|


Client_secret 매개 변수가 두 개의 매개 변수 (client_assertion_type 및 client_assertion)로 대체 된다는 점을 제외 하 고 매개 변수는 공유 암호에의 한 요청의 경우와 거의 동일 합니다. 

#### <a name="example"></a>예제 
다음 HTTP POST는 인증서를 사용 하 여 Web API에 대 한 액세스 토큰을 요청 합니다.

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
 
성공 응답은 다음 매개 변수를 포함 하는 JSON OAuth 2.0 응답입니다. 


|매개 변수|설명|
|-----|-----| 
|token_type|토큰 유형 값을 나타냅니다. AD FS 지원 되는 유일한 형식은 전달자입니다. | 
|범위|토큰에 부여 된 액세스의 범위입니다.| 
|expires_in|액세스 토큰이 유효한 시간 (초)입니다.| 
|access_token|요청 된 액세스 토큰입니다. 호출 서비스는이 토큰을 사용 하 여 수신 서비스에 인증할 수 있습니다.| 
|id_token|JWT (JSON Web Token)입니다. 앱은이 토큰의 세그먼트를 디코드 하 여 로그인 한 사용자에 대 한 정보를 요청할 수 있습니다. 앱은 값을 캐시 하 고 표시할 수 있지만 권한 부여 또는 보안 경계에 의존 하지 않아야 합니다.| 
|refresh_token|요청 된 액세스 토큰에 대 한 새로 고침 토큰입니다. 호출 서비스는이 토큰을 사용 하 여 현재 액세스 토큰이 만료 된 후에 다른 액세스 토큰을 요청할 수 있습니다.|
|Refresh_token_expires_in|새로 고침 토큰이 유효한 시간 (초)입니다. 

### <a name="success-response-example"></a>성공 응답 예제 
 
다음 예제에서는 web API에 대 한 액세스 토큰 요청에 대 한 성공 응답을 보여 줍니다. 

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
 
 
이제 액세스 토큰을 사용 하 여 보안 리소스에 액세스 합니다. 중간 계층 서비스는 인증 헤더에서 토큰을 설정 하 여 위에서 획득 한 토큰을 사용 하 여 다운스트림 웹 API에 대 한 인증 된 요청을 수행할 수 있습니다.  

#### <a name="example"></a>예제 
``` 
GET /v1.0/me HTTP/1.1 
Host: https://secondwebapi.com 
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJub25jZSI6IkFRQUJBQUFBQUFCbmZpRy1tQ… 
``` 

## <a name="client-credentials-grant-flow"></a>클라이언트 자격 증명 부여 흐름 
 
[RFC 6749](https://tools.ietf.org/html/rfc6749#section-4.4)에 지정 된 OAuth 2.0 클라이언트 자격 증명 부여를 사용 하 여 응용 프로그램의 id를 사용 하 여 웹 호스팅 리소스에 액세스할 수 있습니다. 이 권한 부여는 일반적으로 사용자와 즉각적인 상호 작용 없이 백그라운드에서 실행 해야 하는 서버 간 상호 작용에 사용 됩니다. 이러한 유형의 응용 프로그램은 종종 디먼 또는 서비스 계정 이라고 합니다. 

OAuth 2.0 클라이언트 자격 증명 부여 흐름은 사용자를 가장 하는 대신 다른 웹 서비스를 호출할 때 웹 서비스 (기밀 클라이언트)가 자체 자격 증명을 사용 하 여 인증 하도록 허용 합니다. 이 시나리오에서 클라이언트는 일반적으로 중간 계층 웹 서비스, 데몬 서비스 또는 웹 사이트입니다. 높은 보증 수준을 위해 AD FS를 사용 하 여 호출 하는 서비스에서 공유 암호 대신 인증서를 자격 증명으로 사용할 수도 있습니다. 

### <a name="protocol-diagram"></a>프로토콜 다이어그램 

다음 다이어그램에서는 클라이언트 자격 증명 부여 흐름을 보여 줍니다. 

![클라이언트 자격 증명](media/adfs-scenarios-for-developers/credentials.png)

### <a name="request-a-token"></a>토큰 요청 
 
클라이언트 자격 증명 부여를 사용 하 여 토큰을 가져오려면/토큰 `POST` AD FS 끝점에 요청을 보냅니다.  
 
### <a name="first-case-access-token-request-with-a-shared-secret"></a>첫 번째 사례: 공유 암호를 사용 하 여 액세스 토큰 요청 
 
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
|client_id|필수|앱에 할당 AD FS는 응용 프로그램 (클라이언트) ID입니다.| 
|범위|선택적|사용자가 동의할 수 있도록 할 공백으로 구분 된 범위 목록입니다.| 
|client_secret|필수|앱 등록 포털에서 앱에 대해 생성 한 클라이언트 암호입니다. 클라이언트 암호를 보내기 전에 URL로 인코딩해야 합니다.| 
|grant_type|필수|로 `client_credentials`설정 해야 합니다.|

### <a name="second-case-access-token-request-with-a-certificate"></a>두 번째 사례: 인증서를 사용 하 여 액세스 토큰 요청 

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
|client_assertion_type|필수|값은 urn: ietf: params: oauth: client-assertion: jwt-전달자로 설정 되어야 합니다.| 
|client_assertion|필수|응용 프로그램에 대 한 자격 증명으로 등록 한 인증서를 사용 하 여 만들고 서명 해야 하는 어설션 (JSON 웹 토큰)입니다.|  
|grant_type|필수|로 `client_credentials`설정 해야 합니다.|
|client_id|선택적|앱에 할당 AD FS는 응용 프로그램 (클라이언트) ID입니다. 이는 client_assertion의 일부 이므로 여기에 전달할 필요가 없습니다.| 
|범위|선택적|사용자가 동의할 수 있도록 할 공백으로 구분 된 범위 목록입니다.| 

### <a name="use-a-token"></a>토큰 사용 
 
토큰을 획득 했으므로 토큰을 사용 하 여 리소스에 요청을 만듭니다. 토큰이 만료 되 면/ctoken 끝점에 대 한 요청을 반복 하 여 새 액세스 토큰을 획득 합니다.  
 
```
GET /v1.0/me/messages 
Host: https://webapi.com 
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...  
```

## <a name="resource-owner-password-credentials-grant-flow-not-recommended"></a>리소스 소유자 암호 자격 증명 부여 흐름 (권장 하지 않음) 
 
ROPC (리소스 소유자 암호 자격 증명) 부여를 통해 응용 프로그램은 자신의 암호를 직접 처리 하 여 사용자에 게 로그인 할 수 있습니다. ROPC flow에는 높은 수준의 신뢰 및 사용자 노출이 필요 하며, 다른 보안 흐름을 사용할 수 없는 경우에만이 흐름을 사용 해야 합니다.  
 
### <a name="protocol-diagram"></a>프로토콜 다이어그램 
 
다음 다이어그램은 ROPC 흐름을 보여 줍니다.

![ROPC 흐름](media/adfs-scenarios-for-developers/resource.png)

### <a name="authorization-request"></a>권한 부여 요청 
ROPC 흐름은 단일 요청으로, 클라이언트 id와 사용자의 자격 증명을 IDP에 보낸 다음 반환 되는 토큰을 받습니다. 클라이언트는이 작업을 수행 하기 전에 사용자의 메일 주소 (UPN)와 암호를 요청 해야 합니다. 클라이언트는 성공적인 요청 직후에 메모리에서 사용자의 자격 증명을 안전 하 게 해제 해야 합니다. 저장 해서는 안 됩니다.  

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
|grant_type|필수|암호로 설정 해야 합니다.| 
|username|필수|사용자의 전자 메일 주소입니다.| 
|password|필수|사용자의 암호입니다.| 
|범위|선택적|공백으로 구분 된 범위 목록입니다.|

### <a name="successful-authentication-response"></a>성공적인 인증 응답 
다음 예에서는 성공적인 토큰 응답을 보여 줍니다. 

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
|token_type|항상 전달자로 설정 합니다.| 
|범위|액세스 토큰이 반환 된 경우이 매개 변수는 액세스 토큰이 유효한 범위를 나열 합니다.| 
|expires_in|포함 된 액세스 토큰이 유효한 시간 (초)입니다.| 
|access_token|요청 된 범위에 대해 발급 됩니다.| 
|id_token|JWT (JSON Web Token)입니다. 앱은이 토큰의 세그먼트를 디코드 하 여 로그인 한 사용자에 대 한 정보를 요청할 수 있습니다. 앱은 값을 캐시 하 고 표시할 수 있지만 권한 부여 또는 보안 경계에 의존 하지 않아야 합니다.| 
|refresh_token_expires_in|포함 된 새로 고침 토큰이 유효한 시간 (초)입니다.| 
|refresh_token|원래 범위 매개 변수에 offline_access이 포함 된 경우 발급 됩니다.|

위의 인증 코드 부여 흐름 섹션에 설명 된 것과 같은 흐름을 사용 하 여 새 액세스 토큰을 획득 하 고 새로 고침 토큰을 사용 하 여 토큰을 새로 고칠 수 있습니다.   

## <a name="device-code-flow"></a>장치 코드 흐름 
 
장치 코드 부여를 사용 하면 사용자가 스마트 TV, IoT 장치 또는 프린터와 같은 입력 제한 장치에 로그인 할 수 있습니다. 이 흐름을 사용 하도록 설정 하기 위해 장치는 사용자가 다른 장치에서 브라우저의 웹 페이지를 방문 하 여 로그인 하도록 합니다. 사용자가 로그인 하면 장치에서 필요에 따라 액세스 토큰 및 새로 고침 토큰을 가져올 수 있습니다. 
 
### <a name="protocol-diagram"></a>프로토콜 다이어그램 
 
전체 장치 코드 흐름은 다음 다이어그램과 유사 하 게 표시 됩니다. 이 문서의 뒷부분에서 각 단계에 대해 설명 합니다. 
 
![장치 코드 흐름](media/adfs-scenarios-for-developers/device.png)

### <a name="device-authorization-request"></a>장치 권한 부여 요청 
클라이언트는 인증을 시작 하는 데 사용 되는 장치 및 사용자 코드에 대 한 인증 서버를 먼저 확인 해야 합니다. 클라이언트는/devicecode 끝점에서이 요청을 수집 합니다. 이 요청에서 클라이언트는 사용자 로부터 획득 해야 하는 사용 권한을 포함 해야 합니다. 이 요청이 전송 되는 순간 (expires_in에 대 한 일반적인 값)은 15 분 동안만 로그인 할 수 있으므로 사용자가 로그인 할 준비가 되었음을 나타내는 경우에만이 요청을 수행 합니다. 

```
// Line breaks are for legibility only. 
 
POST https://adfs.contoso.com/adfs/oauth2/devicecode 
Content-Type: application/x-www-form-urlencoded 
 
client_id=6731de76-14a6-49ae-97bc-6eba6914391e 
scope=openid 
```


|매개 변수|조건|설명|
|-----|-----|-----| 
|client_id|필수|앱에 할당 AD FS는 응용 프로그램 (클라이언트) ID입니다.| 
|범위|선택적|공백으로 구분 된 범위 목록입니다.|

### <a name="device-authorization-response"></a>장치 권한 부여 응답 
성공적인 응답은 사용자가 로그인 할 수 있도록 하는 데 필요한 정보를 포함 하는 JSON 개체입니다. 


|매개 변수|설명|
|-----|-----| 
|device_code|클라이언트와 권한 부여 서버 간의 세션을 확인 하는 데 사용 되는 긴 문자열입니다. 클라이언트는이 매개 변수를 사용 하 여 권한 부여 서버에서 액세스 토큰을 요청 합니다.| 
|user_code|보조 장치에서 세션을 식별 하는 데 사용 되는 사용자에 게 표시 되는 간단한 문자열입니다.| 
|verification_uri|사용자가 로그인 하기 위해 user_code로 이동 해야 하는 URI입니다.| 
|verification_uri_complete|사용자가 로그인 하기 위해 user_code로 이동 해야 하는 URI입니다. 사용자가 user_code를 입력할 필요가 없도록 미리 user_code으로 채워집니다.| 
|expires_in|Device_code 및 user_code가 만료 되기까지의 시간 (초)입니다.| 
|간격|클라이언트에서 폴링 요청 사이에 대기 해야 하는 시간 (초)입니다.| 
|message|사용자에 대 한 지침이 포함 된 사람이 인식할 수 있는 문자열입니다. 이를 지역화 하려면? mkt = xx-XX 형식의 요청에 쿼리 매개 변수를 포함 하 여 해당 언어 문화권 코드를 입력 합니다.  

### <a name="authenticating-the-user"></a>사용자 인증 
User_code 및 verification_uri를 받은 후 클라이언트는 이러한 항목을 사용자에 게 표시 하 여 휴대폰 또는 PC 브라우저를 사용 하 여 로그인 하도록 지시 합니다. 또한 클라이언트는 QR 코드 또는 유사한 메커니즘을 사용 하 여 verfication_uri_complete를 표시할 수 있습니다 .이 경우 사용자에 대 한 user_code를 입력 하는 단계가 소요 됩니다. 사용자가 verification_uri에서 인증 하는 동안 클라이언트는 device_code를 사용 하 여 요청 된 토큰에 대 한/stoken 끝점을 폴링합니다. 

```
POST https://adfs.contoso.com /adfs/oauth2/token 
Content-Type: application/x-www-form-urlencoded 
 
grant_type: urn:ietf:params:oauth:grant-type:device_code 
client_id: 6731de76-14a6-49ae-97bc-6eba6914391e 
device_code: GMMhmHCXhWEzkobqIHGG_EnNYYsAkukHspeYUk9E8 
```


|매개 변수|필수|설명|
|-----|-----|-----| 
|grant_type|필수|Urn: ietf: params: oauth: grant-type: device_code 여야 합니다.| 
|client_id|필수|초기 요청에 사용 된 client_id 일치 해야 합니다.| 
|code|필수|장치 권한 부여 요청에서 반환 된 device_code입니다.|

### <a name="successful-authentication-response"></a>성공적인 인증 응답 
성공적인 토큰 응답은 다음과 같습니다.  


|매개 변수|설명|
|-----|-----| 
|token_type|항상 "전달자입니다.| 
|범위|액세스 토큰이 반환 된 경우 액세스 토큰이 유효한 범위를 나열 합니다.| 
|expires_in|에 대해 포함 된 액세스 토큰이 유효한 시간 (초)입니다.| 
|access_token|요청 된 범위에 대해 발급 됩니다.| 
|id_token|원래 범위 매개 변수가 openid connect 범위를 포함 하는 경우 발급 됩니다.| 
|refresh_token|원래 범위 매개 변수에 offline_access이 포함 된 경우 발급 됩니다.| 
|refresh_token_expires_in|포함 된 새로 고침 토큰이에 유효 하기 전의 시간 (초)입니다.| 


## <a name="related-content"></a>관련 내용  
관련 흐름 사용에 대 한 단계별 지침을 제공 하는 전체 연습 문서 목록은 [AD FS 개발](../AD-FS-Development.md) 을 참조 하세요. 
