---
title: AD FS를 사용 하 여 HTTP 보안 응답 헤더 사용자 지정
description: 이 문서에서는 보안 취약성을 방지 하기 위해 보안 헤더를 사용자 지정 하는 방법을 descirbes.
author: billmath
ms.author: billmath
manager: daveba
ms.reviewer: akgoel23
ms.date: 02/19/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: e1042ad4dae0b023c9816dff798c25b05b60eccf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407446"
---
# <a name="customize-http-security-response-headers-with-ad-fs-2019"></a>AD FS 2019를 사용 하 여 HTTP 보안 응답 헤더 사용자 지정 
 
일반적인 보안 취약점을 방지 하 고 관리자에 게 최신 버전의 브라우저 기반 보호 메커니즘을 활용할 수 있는 기능을 제공 하는 기능을 제공 하 AD FS 2019에는 HTTP 보안 응답 헤더를 사용자 지정 하는 기능이 추가 되었습니다. AD FS에서 보냅니다. 이 작업은 두 개의 새로운 cmdlet 인 및 `Get-AdfsResponseHeaders` `Set-AdfsResponseHeaders`를 도입 하 여 수행 됩니다.  

>[!NOTE]
>Cmdlet `Get-AdfsResponseHeaders` 을 사용 하 여 HTTP 보안 응답 헤더 (CORS 헤더 제외)를 사용자 지정 하 `Set-AdfsResponseHeaders` 는 기능 및 AD FS 2016으로 포팅 되었습니다. [KB4493473](https://support.microsoft.com/en-us/help/4493473/windows-10-update-kb4493473) 및 [KB4507459](https://support.microsoft.com/en-us/help/4507459/windows-10-update-kb4507459)를 설치 하 여 AD FS 2016에 기능을 추가할 수 있습니다. 

이 문서에서는 AD FS 2019에서 보낸 헤더를 사용자 지정 하는 방법을 보여 주기 위해 일반적으로 사용 되는 보안 응답 헤더에 대해 설명 합니다.   
 
>[!NOTE]
>이 문서에서는 AD FS 2019가 설치 되어 있다고 가정 합니다.  

 
헤더에 대해 설명 하기 전에 관리자가 보안 헤더를 사용자 지정 하기 위해 필요한 몇 가지 시나리오를 살펴보겠습니다. 
 
## <a name="scenarios"></a>시나리오 
1. 관리자는 [**Http Strict (Transport-Transport) (HSTS)** ](#http-strict-transport-security-hsts) 를 사용 하도록 설정 (HTTPS 암호화를 통해 모든 연결 강제 적용) 하 여 해킹을 받을 수 있는 공용 wifi 액세스 지점에서 http를 사용 하 여 웹 앱에 액세스할 수 있는 사용자를 보호 합니다. 하위 도메인에 대 한 HSTS를 사용 하도록 설정 하 여 보안을 강화 하고자 합니다.  
2. 관리자가 [**X 프레임 옵션**](#x-frame-options) 응답 헤더를 구성 하 여 (iFrame의 웹 페이지 렌더링 방지) 웹 페이지가 clickjacked 않도록 보호 합니다. 그러나 다른 원본 (도메인)을 사용 하는 응용 프로그램에서 데이터 (iFrame)를 표시 하려면 새 비즈니스 요구 사항으로 인해 헤더 값을 사용자 지정 해야 합니다.
3. 관리자가 크로스 스크립팅 공격을 감지 하는 경우 페이지를 삭제 하 고 차단 하기 [**위해 (크로스 스크립팅 공격 방지)** ](#x-xss-protection) 를 사용 하도록 설정 했습니다. 그러나 페이지를 삭제 한 후에 로드할 수 있도록 헤더를 사용자 지정 해야 합니다.  
4. 관리자는 CORS ( [**원본 간 리소스 공유)** ](#cross-origin-resource-sharing-cors-headers) 를 사용 하도록 설정 하 고 AD FS의 원본 (도메인)을 설정 하 여 단일 페이지 응용 프로그램이 다른 도메인을 사용 하 여 web API에 액세스할 수 있도록 해야 합니다.  
5. 관리자는 도메인 간 요청을 허용 하지 않기 때문에 사이트 간 스크립팅 및 데이터 삽입 공격을 방지 하기 위해 [**CSP (콘텐츠 보안 정책)** ](#content-security-policy-csp) 헤더를 사용 하도록 설정 했습니다. 그러나 새로운 비즈니스 요구 사항으로 인해 웹 페이지에서 원본의 이미지를 로드 하 고 미디어를 신뢰할 수 있는 공급자로 제한할 수 있도록 헤더를 사용자 지정 해야 합니다.  

 
## <a name="http-security-response-headers"></a>HTTP 보안 응답 헤더 
응답 헤더는 AD FS에서 보내는 HTTP 응답에 웹 브라우저에 포함 됩니다. 아래와 같이 cmdlet을 `Get-AdfsResponseHeaders` 사용 하 여 헤더를 나열할 수 있습니다.  

![헤더 응답](media/customize-http-security-headers-ad-fs/header1.png)

위의 `ResponseHeaders` 스크린 샷에서 특성은 모든 HTTP 응답에서 AD FS에 포함 될 보안 헤더를 식별 합니다. 응답 헤더는가 (기본값)로 `ResponseHeadersEnabled` 설정 된 경우 `True` 에만 전송 됩니다. HTTP 응답의 보안 헤더를 `False` 포함 하 AD FS을 방지 하기 위해 값을로 설정할 수 있습니다. 그러나이 방법은 권장 되지 않습니다.  이렇게 하려면 다음을 사용 합니다.

```PowerShell
Set-AdfsResponseHeaders -EnableResponseHeaders $false
```
 
### <a name="http-strict-transport-security-hsts"></a>HTTP Strict-Transport-보안 (HSTS) 
HSTS는 HTTP 및 HTTPS 끝점을 모두 포함 하는 서비스에 대해 프로토콜 다운 그레이드 공격 및 쿠키 가로채기를 완화 하는 데 도움이 되는 웹 보안 정책 메커니즘입니다. 웹 서버에서 웹 브라우저 (또는 기타 준수 사용자 에이전트)가 HTTPS를 사용 하 여 HTTP 프로토콜을 통해 상호 작용 하는 경우에만 해당 웹 브라우저 또는 다른 사용자 에이전트를 선언할 수 있습니다.  
 
웹 인증 트래픽에 대 한 모든 AD FS 끝점은 HTTPS를 통해서만 열 수 있습니다. 결과적으로 http 엄격한 전송 보안 정책 메커니즘이 제공 하는 위협을 효과적으로 완화 하는 AD FS (HTTP에 수신기가 없기 때문에 기본적으로 HTTP에 다운 그레이드는 없습니다). 다음 매개 변수를 설정 하 여 헤더를 사용자 지정할 수 있습니다. 
 
- **max-age =&lt;만료 시간&gt;**  – 만료 시간 (초)은 HTTPS를 사용 하 여 사이트에 액세스 해야 하는 기간을 지정 합니다. 기본값 및 권장 값은 31536000 초 (1 년)입니다.  
- **Includesubdomains 도메인** – 선택적 매개 변수입니다. 지정 된 경우 HSTS 규칙은 모든 하위 도메인에도 적용 됩니다.  
 
#### <a name="hsts-customization"></a>HSTS 사용자 지정 
기본적으로 헤더는 사용 하도록 설정 되 `max-age` 고 1 년으로 설정 됩니다. 그러나 관리자는 `max-age` 를 수정할 수 있습니다 (최대 보존 기간 값 낮추기 권장 되지 않음) 또는 `Set-AdfsResponseHeaders` cmdlet을 통해 하위 도메인에 hsts를 사용 하도록 설정 합니다.  
 
```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "Strict-Transport-Security" -SetHeaderValue "max-age=<seconds>; includeSubDomains" 
``` 

예: 

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "Strict-Transport-Security" -SetHeaderValue "max-age=31536000; includeSubDomains" 
 ```

기본적으로 헤더는 `ResponseHeaders` 특성에 포함 되지만 관리자는 `Set-AdfsResponseHeaders` cmdlet을 통해 헤더를 제거할 수 있습니다.  
 
```PowerShell
Set-AdfsResponseHeaders -RemoveHeaders "Strict-Transport-Security" 
```

### <a name="x-frame-options"></a>X 프레임-옵션 
기본적으로 AD FS는 대화형 로그인을 수행할 때 외부 응용 프로그램에서 Iframe을 사용 하는 것을 허용 하지 않습니다. 이는 특정 유형의 피싱 공격을 방지 하기 위해 수행 됩니다. 비 대화형 로그인은 설정 된 이전 세션 수준 보안으로 인해 iFrame을 통해 수행할 수 있습니다.  
 
그러나 드문 경우 지만 iFrame 가능 대화형 AD FS 로그인 페이지가 필요한 특정 응용 프로그램을 신뢰할 수 있습니다. 이 용도로는 ' X-프레임-옵션 ' 헤더가 사용 됩니다.  
 
이 HTTP 보안 응답 헤더는 &lt;프레임&gt;/&lt;iframe&gt;에서 페이지를 렌더링할 수 있는지 여부를 브라우저에 전달 하는 데 사용 됩니다. 헤더는 다음 값 중 하나로 설정할 수 있습니다. 
 
- **deny** – 프레임의 페이지는 표시 되지 않습니다. 기본 설정 및 권장 설정입니다.  
- **sameorigin** – 원본이 웹 페이지의 원본과 동일한 경우에만 페이지를 프레임에 표시 합니다. 이 옵션은 모든 상위 항목이 동일한 원점에도 있는 경우에만 유용 합니다.  
- 허용-원본 (예: .")인경우에만페이지가프레임에표시됩니다. https://www **<specified origin>** com)는 헤더의 특정 원본과 일치 합니다. 

#### <a name="x-frame-options-customization"></a>X 프레임-옵션 사용자 지정  
기본적으로 헤더는 거부로 설정 됩니다. 그러나 관리자는 `Set-AdfsResponseHeaders` cmdlet을 통해 값을 수정할 수 있습니다.  
```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "X-Frame-Options" -SetHeaderValue "<deny/sameorigin/allow-from<specified origin>>" 
 ```

예: 

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "X-Frame-Options" -SetHeaderValue "allow-from https://www.example.com" 
 ```

기본적으로 헤더는 `ResponseHeaders` 특성에 포함 되지만 관리자는 `Set-AdfsResponseHeaders` cmdlet을 통해 헤더를 제거할 수 있습니다.  

```PowerShell
Set-AdfsResponseHeaders -RemoveHeaders "X-Frame-Options" 
```

### <a name="x-xss-protection"></a>X-XSS-보호 
이 HTTP 보안 응답 헤더는 브라우저에서 XSS (교차 사이트 스크립팅) 공격을 감지 하는 경우 웹 페이지 로드를 중지 하는 데 사용 됩니다. 이를 XSS 필터링 이라고 합니다. 헤더는 다음 값 중 하나로 설정할 수 있습니다. 
 
- **0** – XSS 필터링을 사용 하지 않도록 설정 합니다. 이 옵션은 사용하지 않는 것이 좋습니다.  
- **1** – XSS 필터링을 사용 합니다. XSS 공격이 감지 되 면 브라우저는 페이지를 삭제 합니다.   
- **1; mode = block** – XSS 필터링을 사용 합니다. XSS 공격이 감지 되 면 브라우저에서 페이지 렌더링을 방지 합니다. 기본 설정 및 권장 설정입니다.  

#### <a name="x-xss-protection-customization"></a>X-XSS-보호 사용자 지정 
기본적으로 헤더는 1로 설정 됩니다. mode = block; 그러나 관리자는 `Set-AdfsResponseHeaders` cmdlet을 통해 값을 수정할 수 있습니다.  

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "X-XSS-Protection" -SetHeaderValue "<0/1/1; mode=block/1; report=<reporting-uri>>" 
``` 

예: 

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "X-XSS-Protection" -SetHeaderValue "1" 
 ```

기본적으로 헤더는 `ResponseHeaders` 특성에 포함 되지만 관리자는 `Set-AdfsResponseHeaders` cmdlet을 통해 헤더를 제거할 수 있습니다. 

```PowerShell
Set-AdfsResponseHeaders -RemoveHeaders "X-XSS-Protection" 
```

### <a name="cross-origin-resource-sharing-cors-headers"></a>CORS (원본 간 리소스 공유) 헤더 
웹 브라우저 보안은 웹 페이지에서 스크립트 내에서 원본 간 요청을 시작할 수 없도록 합니다. 그러나 다른 원본 (도메인)에 있는 리소스에 액세스 하려는 경우가 있습니다. CORS는 서버에서 동일한 원본 정책을 완화할 수 있게 해 주는 W3C 표준입니다. CORS를 사용하면 서버가 명시적으로 특정 교차 원본 요청만 허용하고, 다른 요청은 거부할 수 있습니다.  
 
CORS 요청을 보다 잘 이해 하려면 SPA (단일 페이지 응용 프로그램)가 다른 도메인을 사용 하 여 web API를 호출 해야 하는 시나리오를 연습 하겠습니다. 또한 SPA 및 API가 모두 ADFS 2019에 구성 되어 AD FS CORS를 사용 하도록 설정 되어 있습니다 AD FS. 즉, HTTP 요청에서 CORS 헤더를 식별 하 고, 헤더 값의 유효성을 검사 하 고, 적절 한 CORS 헤더를 응답에 포함할 수 있습니다 (및을 사용 하도록 설정 하는 방법에 대 한 자세한 내용 아래 CORS 사용자 지정 섹션의 AD FS 2019에서 CORS를 구성 합니다. 샘플 흐름: 

1. 사용자는 클라이언트 브라우저를 통해 SPA에 액세스 하 고 인증을 위해 AD FS 인증 끝점으로 리디렉션됩니다. SPA가 암시적 권한 부여 흐름에 대해 구성 되어 있으므로 요청은 인증에 성공한 후 브라우저에 액세스 + ID 토큰을 반환 합니다.  
2. 사용자 인증 후 SPA에 포함 된 프런트 엔드 JavaScript는 web API에 액세스 하는 요청을 수행 합니다. 요청은 다음 헤더와 함께 AD FS 리디렉션됩니다.
    - 옵션-대상 리소스에 대 한 통신 옵션을 설명 합니다. 
    - 원본-web API의 출처를 포함 합니다.
    - 액세스 제어-요청-메서드 – 실제 요청을 수행할 때 사용할 HTTP 메서드 (예: 삭제)를 식별 합니다. 
    - 액세스-요청-헤더-실제 요청을 수행할 때 사용할 HTTP 헤더를 식별 합니다. 
    
   >[!NOTE]
   >CORS 요청은 표준 HTTP 요청과 유사 하지만, 원본 헤더가 있으면 들어오는 요청이 CORS와 관련 된 것으로 신호를 보냅니다. 
3. AD FS 헤더에 포함 된 웹 API 원본이 AD FS에 구성 된 신뢰할 수 있는 원본에 나열 되어 있는지 확인 합니다 (아래 CORS 사용자 지정에서 신뢰할 수 있는 원본을 수정 하는 방법에 대 한 세부 정보 섹션 참조). 그런 다음 AD FS 다음 헤더를 사용 하 여 응답 합니다.  
    - 액세스 제어-허용-원본-원본 헤더의 값과 동일 합니다. 
    - 액세스 제어-요청-메서드 헤더의 값과 동일 합니다. 
    - 액세스 제어-헤더 값은 액세스 제어-요청 헤더의 헤더와 동일 합니다. 
4. 브라우저는 다음 헤더를 포함 하 여 실제 요청을 보냅니다. 
    - HTTP 메서드 (예: 삭제) 
    - 원본-web API의 출처를 포함 합니다. 
    - 액세스 제어-헤더 응답 헤더에 포함 된 모든 헤더 
5. 확인 되 면 액세스 제어-원본 응답 헤더에 웹 API 도메인 (원본)을 포함 하 여 요청을 승인 AD FS 합니다.  
6. 액세스 제어-원본 헤더를 포함 하는 경우 브라우저에서 요청 된 API를 호출 하 여 계속 진행할 수 있습니다.

#### <a name="cors-customization"></a>CORS 사용자 지정 
기본적으로 CORS 기능은 사용 하도록 설정 되지 않습니다. 그러나 관리자는 AdfsResponseHeaders cmdlet을 통해 기능을 사용 하도록 설정할 수 있습니다.  

```PowerShell 
Set-AdfsResponseHeaders -EnableCORS $true 
 ```

하나를 사용 하도록 설정 하면 관리자는 동일한 cmdlet을 사용 하 여 신뢰할 수 있는 원본 목록을 열거할 수 있습니다. 예를 들어 다음 명령은 원본 **https&#58;//example1.com** 및 **&#58;https//example1.com**에서 CORS 요청을 허용 합니다. 
 
```PowerShell
Set-AdfsResponseHeaders -CORSTrustedOrigins https://example1.com,https://example2.com 
 ```

> [!NOTE]
> 관리자는 신뢰할 수 있는 원본 목록에 "*"를 포함 하 여 모든 원본의 CORS 요청을 허용할 수 있습니다. 단, 보안 취약성으로 인해이 방법이 권장 되지 않으며, 선택 하는 경우 경고 메시지가 제공 됩니다. 

### <a name="content-security-policy-csp"></a>CSP (콘텐츠 보안 정책) 
이 HTTP 보안 응답 헤더는 브라우저에서 악의적인 콘텐츠를 실수로 실행 하지 못하도록 하 여 사이트 간 스크립팅, 클릭 재 킹 및 기타 데이터 삽입 공격을 방지 하는 데 사용 됩니다. CSP를 지원 하지 않는 브라우저는 단순히 CSP 응답 헤더를 무시 합니다.  
 
#### <a name="csp-customization"></a>CSP 사용자 지정 
CSP 헤더의 사용자 지정에는 웹 페이지에 대 한 리소스 브라우저 로드를 정의 하는 보안 정책을 수정 하는 작업이 포함 됩니다. 기본 보안 정책은입니다.  
 
`Content-Security-Policy: default-src ‘self' ‘unsafe-inline' ‘'unsafe-eval'; img-src ‘self' data:;` 
 
**기본-src** 지시문은 각 지시문을 명시적으로 나열 하지 않고 [-src 지시문](https://developer.mozilla.org/docs/Web/HTTP/Headers/Content-Security-Policy/default-src) 을 수정 하는 데 사용 됩니다. 예를 들어 아래 예제에서 정책 1은 정책 2와 같습니다.  

정책 1 
```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "Content-Security-Policy" -SetHeaderValue "default-src 'self'" 
```
 
정책 2
```PowerShell 
Set-AdfsResponseHeaders -SetHeaderName "Content-Security-Policy" -SetHeaderValue "script-src ‘self'; img-src ‘self'; font-src 'self';  
frame-src 'self'; manifest-src 'self'; media-src 'self';" 
```

지시문이 명시적으로 나열 되는 경우 지정 된 값은 기본-src에 지정 된 값을 재정의 합니다. 아래 예제에서 img-src는 값을 ' * '로 사용 하 고 (모든 원본에서 이미지를 로드 하도록 허용) 다른-src 지시문은 값을 ' self ' (웹 페이지와 같은 원본으로 제한)로 사용 합니다.  

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "Content-Security-Policy" -SetHeaderValue "default-src ‘self'; img-src *" 
```
다음 소스는 기본-src 정책에 대해 정의할 수 있습니다. 
 
- ' self ' –이를 지정 하면 콘텐츠 원점이 웹 페이지의 원본에 로드 되도록 제한 됩니다. 
- ' unsafe-inline ' – 정책에이를 지정 하면 인라인 JavaScript 및 CSS를 사용할 수 있습니다. 
- ' unsafe-eval ' – 정책에이를 지정 하면 eval 같은 JavaScript 메커니즘에 텍스트를 사용할 수 있습니다. 
- ' 없음 ' –이를 지정 하면 모든 원본의 콘텐츠가 로드 됩니다. 
- 데이터:-데이터를 지정 합니다. Uri를 사용 하면 콘텐츠 작성자가 문서에 작은 파일을 인라인으로 포함할 수 있습니다. 사용 하지 않는 것이 좋습니다.  
 
>[!NOTE]
>AD FS는 인증 프로세스에서 JavaScript를 사용 하므로 기본 정책에 ' unsafe-inline ' 및 ' unsafe-eval ' 원본을 포함 하 여 JavaScript를 사용 하도록 설정 합니다.  

### <a name="custom-headers"></a>사용자 지정 헤더 
위에 나열 된 보안 응답 헤더 (HSTS, CSP, X 프레임-옵션, X-XSS-보호 및 CORS) 외에도 AD FS 2019는 새 헤더를 설정 하는 기능을 제공 합니다.  
 
예: 값이 "TestHeaderValue" 인 새 헤더 "TestHeader"를 설정 하려면 

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "TestHeader" -SetHeaderValue "TestHeaderValue" 
 ```

설정 되 면 새 헤더가 AD FS 응답으로 전송 됩니다 (아래 fiddler 코드 조각).  
 
![Fiddler](media/customize-http-security-headers-ad-fs/header2.png)

## <a name="web-browswer-compatibility"></a>웹 브라우저 호환성
다음 표와 링크를 사용 하 여 각 보안 응답 헤더와 호환 되는 웹 브라우저를 확인 합니다.

|HTTP 보안 응답 헤더|브라우저 호환성|
|-----|-----|
|HTTP Strict-Transport-보안 (HSTS)|[HSTS 브라우저 호환성](https://developer.mozilla.org/docs/Web/HTTP/Headers/Strict-Transport-Security#Browser_compatibility)|
|X 프레임-옵션|[X 프레임-옵션 브라우저 호환성](https://developer.mozilla.org/docs/Web/HTTP/Headers/X-Frame-Options#Browser_compatibility)| 
|X-XSS-보호|[X-XSS-보호 브라우저 호환성](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-XSS-Protection#Browser_compatibility)| 
|CORS (원본 간 리소스 공유)|[CORS 브라우저 호환성](https://developer.mozilla.org/docs/Web/HTTP/CORS#Browser_compatibility) 
|CSP (콘텐츠 보안 정책)|[CSP 브라우저 호환성](https://developer.mozilla.org/docs/Web/HTTP/CSP#Browser_compatibility) 

## <a name="next"></a>다음

- [AD FS 도움말 troublehshooting 가이드 사용](https://aka.ms/adfshelp/troubleshooting )
- [AD FS 문제 해결](../../ad-fs/troubleshooting/ad-fs-tshoot-overview.md)
