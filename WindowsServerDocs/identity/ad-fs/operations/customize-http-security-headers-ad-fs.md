---
title: AD FS 사용 하 여 HTTP 보안 응답 헤더를 사용자 지정
description: 이 문서 descirbes 보안 취약점 으로부터 보호 하기 위해 보안 헤더를 사용자 지정 하는 방법입니다.
author: billmath
ms.author: billmath
manager: daveba
ms.reviewer: akgoel23
ms.date: 02/19/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 54b0e055d6cfde5e5c69540ac804a38cbceb1e59
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188773"
---
# <a name="customize-http-security-response-headers-with-ad-fs-2019"></a>AD FS 2019를 사용 하 여 HTTP 보안 응답 헤더를 사용자 지정 
 
일반적인 보안 취약점 으로부터 보호 하 고 관리자에 게 브라우저 기반 보호 메커니즘의 최신 향상 기능을 활용 하는 기능 제공, AD FS 2019 추가 HTTP 보안 응답 헤더를 사용자 지정 하는 기능 AD FS에서 전송 합니다. 이 두 개의 새로운 cmdlet의 도입을 통해 수행 됩니다. `Get-AdfsResponseHeaders` 고 `Set-AdfsResponseHeaders`입니다.  
 
일반적으로 설명할 것이 문서에서 AD FS 2019에서 전송 되는 헤더를 사용자 지정 하는 방법을 보여 주는 보안 응답 헤더를 사용 합니다.   
 
>[!NOTE]
>문서는 AD FS 2019 설치 되어 있는지 가정 합니다.  

 
헤더를 이야기 하기 전에 관리자가 보안 헤더를 사용자 지정을 해야 하는 몇 가지 시나리오를 살펴보겠습니다 
 
## <a name="scenarios"></a>시나리오 
1. 관리자가 설정한 [ **HTTP Strict 전송 보안 (HSTS)** ](#http-strict-transport-security-hsts) (HTTPS 암호화를 통해 모든 연결을 강제로) 공용 wifi 액세스에서 HTTP를 사용 하 여 웹 앱에 액세스할 수 있는 사용자를 보호 하기 해킹 될 수 있는 지점입니다. 하위 도메인에 대 한 HSTS를 사용 하 여 보안을 강화 하는 추가 싶어합니다.  
2. 관리자가 구성 합니다 [ **X-프레임-옵션** ](#x-frame-options) 응답 헤더 (iFrame에서 모든 웹 페이지를 렌더링 방지) clickjacked에서 웹 페이지를 보호 하기 위해. 그러나 필요한 헤더 값 (iFrame)에서 데이터를 표시할 새 비즈니스 요구 사항에 맞게 다른 원본이 (도메인)를 사용 하 여 응용 프로그램에서 합니다.
3. 관리자가 설정한 [ **X XSS 보호** ](#x-xss-protection) (간 스크립팅 공격을 방지)를 삭제 하 여 브라우저 간 스크립팅 공격을 검색 하는 경우이 페이지를 차단 합니다. 그러나 해야 헤더 페이지 로드를 허용 하도록 사용자 지정 되 면 삭제 합니다.  
4. 관리자가 사용 하도록 설정 해야 [ **교차 원본 자원 공유 (CORS)** ](#cross-origin-resource-sharing-cors-headers) 단일 페이지 응용 프로그램을 다른 도메인을 사용 하 여 web API에 액세스할 수 있도록 AD FS에서 원점 (도메인)를 설정 합니다.  
5. 관리자가 설정한 [ **콘텐츠 보안 정책 (CSP)** ](#content-security-policy-csp) 교차 사이트 스크립팅 및 데이터 주입 방지 하기 위해 헤더 공격 도메인 간 요청을 허용 하지 않습니다. 그러나 새 비즈니스 요구 사항 해야 웹 페이지에 모든 원본에서 이미지를 로드 하 고 신뢰할 수 있는 공급자에 게 미디어를 제한할 수 있도록 헤더 사용자 지정 합니다.  

 
## <a name="http-security-response-headers"></a>HTTP 보안 응답 헤더 
응답 헤더는 웹 브라우저에 AD FS에서 보내는 나가는 HTTP 응답에 포함 됩니다. 사용 하 여 헤더를 나열할 수 있습니다는 `Get-AdfsResponseHeaders` 아래와 같이 cmdlet.  

![헤더 응답](media\customize-http-security-headers-ad-fs\header1.png)

`ResponseHeaders` 위의 스크린샷에 특성은 모든 HTTP 응답에서 AD FS에서 포함 되는 보안 헤더를 식별 합니다. 경우에 응답 헤더를 보낼지 `ResponseHeadersEnabled` 로 설정 된 `True` (기본값). 값을 설정할 수 있는 `False` 보안 헤더를 포함 하 여 HTTP 응답에서 AD FS를 방지 하기 위해. 그러나이 권장 되지 않습니다.  이렇게 하려면 다음을 사용 합니다.

```PowerShell
Set-AdfsResponseHeaders -EnableResponseHeaders $false
```
 
### <a name="http-strict-transport-security-hsts"></a>HSTS (HTTP 엄격한-전송-보안) 
HSTS는 위험을 완화 시켜 프로토콜 다운 그레이드 공격 및 HTTP와 HTTPS 끝점이 있는 서비스에 대 한 쿠키 하이재킹 웹 보안 정책 메커니즘을입니다. 웹 서버를 웹 브라우저 (또는 다른 유효한 사용자 에이전트) 상호 작용 해야 하지 HTTP 프로토콜을 통해 및 HTTPS를 사용 하 여 선언할 수 있습니다.  
 
웹 인증 트래픽에 대 한 모든 AD FS 끝점은 HTTPS를 통해서만 열립니다. 결과적으로, AD FS HTTP 엄격한 전송 보안 정책 메커니즘을 제공 하는 위협을 효과적으로 완화 (기본적으로는 없는 다운 그레이드 HTTP http에서 수신기를 찾지 되므로). 다음 매개 변수를 설정 하 여 헤더를 사용자 지정할 수 있습니다. 
 
- **최대 처리 기간 =&lt;만료 타임&gt;**  – 기간 사이트에 액세스 해야 HTTPS를 사용 하 여 만료 시간 (초) 지정 합니다. 기본 및 권장된 값은 31536000 초 (1 년)입니다.  
- **includeSubDomains** – 선택적 매개 변수입니다. 를 지정 하는 경우 HSTS 규칙이 모든 하위 도메인도 적용 됩니다.  
 
#### <a name="hsts-customization"></a>HSTS 사용자 지정 
기본적으로 헤더를 사용 하도록 설정 및 `max-age` 1 년으로 설정; 관리자가 수정할 수는 있지만 합니다 `max-age` (최대 처리 기간 값을 낮추면 권장 하지 않음) 또는 하위 도메인을 통해 HSTS 설정를 `Set-AdfsResponseHeaders` cmdlet.  
 
```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "Strict-Transport-Security" -SetHeaderValue "max-age=<seconds>; includeSubDomains" 
``` 

예: 

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "Strict-Transport-Security" -SetHeaderValue "max-age=31536000; includeSubDomains" 
 ```

기본적으로 헤더에 포함 되는 `ResponseHeaders` 특성; 그러나 관리자를 통해 헤더를 제거할 수는 `Set-AdfsResponseHeaders` cmdlet.  
 
```PowerShell
Set-AdfsResponseHeaders -RemoveHeaders "Strict-Transport-Security" 
```

### <a name="x-frame-options"></a>X-프레임-옵션 
기본적으로 AD FS에서 대화형 로그인을 수행할 때 iFrames를 사용 하는 외부 응용 프로그램을 허용 하지 않습니다. 이 특정 스타일 피싱 공격을 방지 하기 위해 수행 됩니다. 설정 된 이전 세션 수준 보안으로 인해 iFrame을 통해 비 대화형 로그인을 수행할 수 있는지 참고 합니다.  
 
그러나 드문에서 iFrame 수 있는 대화형 AD FS 로그인 페이지에 필요한 특정 응용 프로그램을 신뢰할 수 있습니다. ' X-프레임-옵션 ' 헤더는이 목적을 위해 사용 됩니다.  
 
이 HTTP 보안 응답 헤더에서 페이지를 렌더링할 수 있는지 여부를 브라우저에 통신에 사용 되는 &lt;프레임&gt;/&lt;iframe&gt;합니다. 헤더는 다음 값 중 하나로 설정할 수 있습니다. 
 
- **거부** – 프레임의 페이지 표시 되지 것입니다. 기본값이 며 권장 설정입니다.  
- **sameorigin** – 페이지만 표시할 프레임의 원본 웹 페이지의 원점으로 동일 합니다. 모든 상위 항목 동일 원본에도 않는 옵션은 매우 유용 하지 않습니다.  
- **허용 <specified origin>**  -페이지는 경우에 표시 프레임의 원본 (예를 들어 https://www. "입니다. com) 헤더에 특정 원본을 일치합니다. 

#### <a name="x-frame-options-customization"></a>X-프레임-옵션 사용자 지정  
기본적으로 헤더; 거부로 설정 됩니다. 그러나 관리자를 통해 값을 수정할 수는 `Set-AdfsResponseHeaders` cmdlet.  
```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "X-Frame-Options" -SetHeaderValue "<deny/sameorigin/allow-from<specified origin>>" 
 ```

예: 

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "X-Frame-Options" -SetHeaderValue "allow-from https://www.example.com" 
 ```

기본적으로 헤더에 포함 되는 `ResponseHeaders` 특성; 그러나 관리자를 통해 헤더를 제거할 수는 `Set-AdfsResponseHeaders` cmdlet.  

```PowerShell
Set-AdfsResponseHeaders -RemoveHeaders "X-Frame-Options" 
```

### <a name="x-xss-protection"></a>X-XSS-Protection 
이 HTTP 보안 응답 헤더는 웹 페이지에서 브라우저에서 사이트 간 스크립팅 (XSS) 공격 감지 되 면 로드를 중지 하려면 사용 됩니다. 이 필터링 하는 XSS 이라고 합니다. 다음 값 중 하나에 헤더를 설정할 수 있습니다. 
 
- **0** – 필터링 XSS 사용 하지 않도록 설정 합니다. 이 옵션은 사용하지 않는 것이 좋습니다.  
- **1** – 수 있도록 XSS 필터링 합니다. XSS 공격 감지 되 면 브라우저 페이지를 삭제 합니다.   
- **1. 모드 = 블록** – 수 있도록 XSS 필터링 합니다. XSS 공격 감지 되 면 브라우저 페이지의 렌더링이 되지 것입니다. 기본값이 며 권장 설정입니다.  

#### <a name="x-xss-protection-customization"></a>X XSS 보호 사용자 지정 
기본적으로 헤더를 1로 설정 됩니다. 모드 = 블록 그러나 관리자를 통해 값을 수정할 수는 `Set-AdfsResponseHeaders` cmdlet.  

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "X-XSS-Protection" -SetHeaderValue "<0/1/1; mode=block/1; report=<reporting-uri>>" 
``` 

예: 

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "X-XSS-Protection" -SetHeaderValue "1" 
 ```

기본적으로 헤더에 포함 되는 `ResponseHeaders` 특성; 그러나 관리자를 통해 헤더를 제거할 수는 `Set-AdfsResponseHeaders` cmdlet. 

```PowerShell
Set-AdfsResponseHeaders -RemoveHeaders "X-XSS-Protection" 
```

### <a name="cross-origin-resource-sharing-cors-headers"></a>교차 원본 자원 공유 (CORS) 헤더 
웹 브라우저 보안 스크립트 내에서 시작 된 크로스-원본 요청에서 웹 페이지를 방지 합니다. 그러나 하려는 경우가 있습니다 수 다른 원본 (도메인)의 리소스에 액세스 합니다. CORS는 서버를 동일 원본 정책을 완화할 수 있는 W3C 표준입니다. CORS를 사용하면 서버가 명시적으로 특정 교차 원본 요청만 허용하고, 다른 요청은 거부할 수 있습니다.  
 
CORS 요청을 더 잘 이해 하려면 보겠습니다 연습 시나리오는 단일 페이지 응용 프로그램 (SPA) 해야 다른 도메인을 사용 하 여 web API를 호출 합니다. 또한 살펴보겠습니다 ADFS 2019 SPA 및 API 둘 다가 구성 되어을 AD FS CORS가 활성화 되어 즉, AD FS HTTP 요청에 CORS 헤더를 식별, 헤더 값의 유효성 검사를 적절 한 CORS 헤더를 응답에 포함 (사용 하도록 설정 하는 방법에 대 한 세부 정보 및 CORS 구성 ad FS 2019 CORS 사용자 지정 섹션 아래). 샘플 흐름: 

1. 사용자는 클라이언트 브라우저를 통해 SPA를 액세스 하 고 인증에 대 한 AD FS 인증 끝점으로 리디렉션됩니다. SPA 암시적 허용 흐름으로 구성 된 후 인증에 성공 하면 브라우저에 액세스 + ID를 반환 합니다. 토큰을 요청 합니다.  
2. 사용자 인증 후 프런트 엔드 JavaScript SPA에 포함 된 웹 API에 액세스 하려면 요청을 수행 합니다. 다음 헤더와 함께 AD FS에 요청을 리디렉션할
    - 옵션 – 대상 리소스에 대 한 통신 옵션에 설명 합니다. 
    - 원본-web API의 원본 포함
    - HTTP 메서드를 식별 하는 액세스-컨트롤-요청-메서드-(예를 들어 삭제) 실제 요청이 있을 때 사용할 
    - 컨트롤-요청-헤더에 액세스-HTTP 헤더를 사용 하 여 실제 요청이 있을 때 식별 
    
   >[!NOTE]
   >그러나 CORS 요청은 표준 HTTP 요청을 유사 하으로 원본 헤더의 존재는 들어오는 요청은 CORS와 관련 된를 알립니다. 
3. AD FS 웹 API 원본 헤더에 포함 된 AD FS (CORS 사용자 지정 섹션 아래에서 신뢰할 수 있는 원본을 수정 하는 방법의 세부 정보)에 구성 된 신뢰할 수 있는 원본에 나열 되어 있는지 확인 합니다. 그러면 AD FS는 다음 헤더를 사용 하 여 응답합니다.  
    - 액세스 제어-허용-원본 – 원본 헤더와 동일한 값 
    - 액세스 제어-허용-메서드-액세스 제어-요청 메서드 헤더와 동일한 값 
    - 컨트롤-허용-헤더에 액세스-액세스 제어-요청 헤더 헤더와 동일한 값 
4. 브라우저에서 다음 헤더를 포함 하는 실제 요청 전송 
    - HTTP 메서드 (예를 들어 삭제) 
    - 원본-web API의 원본 포함 
    - 액세스 제어-허용-헤더 응답 헤더에 포함 된 모든 헤더 
5. 확인 되 면 AD FS 액세스 제어-허용-원본 응답 헤더에 웹 API 도메인 (원본)를 포함 하 여 요청을 승인 합니다.  
6. 액세스 제어-허용-원본 헤더를 포함 요청 된 API를 호출 하 여 계속 해 서 브라우저를 하면 있습니다.

#### <a name="cors-customization"></a>CORS 사용자 지정 
기본적으로 CORS 기능은 사용할 수 없습니다. 그러나 관리자 집합 AdfsResponseHeaders cmdlet 통해 기능을 설정할 수 있습니다.  

```PowerShell 
Set-AdfsResponseHeaders -EnableCORS $true 
 ```

사용 하도록 설정 하나 관리자는 동일한 cmdlet를 사용 하 여 신뢰할 수 있는 원본의 목록을 열거할 수 있습니다. 예를 들어 다음 명령은 원본에서 CORS 요청 하면 **https&#58;//example1.com** 하 고 **https&#58;//example1.com**. 
 
```PowerShell
Set-AdfsResponseHeaders -CORSTrustedOrigins https://example1.com,https://example2.com 
 ```

> [!NOTE]
> 관리자는 포함 하 여 모든 원본에서 CORS 요청 수 "*" 신뢰할 수 있는 원본 목록의 보안 취약성과 경고 메시지가 하므로이 방법은 권장 되지 않습니다 하지만 제공 하도록 선택한 경우. 

### <a name="content-security-policy-csp"></a>콘텐츠 보안 정책 (CSP) 
이 HTTP 보안 응답 헤더는 브라우저 실수로 악성 콘텐츠를 실행 하지 못하도록 하 여 사이트 간 스크립팅, 클릭 재 킹 및 기타 데이터 주입 공격을 방지 하기 위해 사용 됩니다. CSP를 지원 하지 않는 브라우저는 단순히 CSP 응답 헤더를 무시 합니다.  
 
#### <a name="csp-customization"></a>CSP 사용자 지정 
사용자 지정 CSP 헤더는 웹 페이지를 로드할 수 리소스 브라우저를 정의 하는 보안 정책을 수정 해야 합니다. 기본 보안 정책은  
 
`Content-Security-Policy: default-src ‘self’ ‘unsafe-inline’ ‘’unsafe-eval’; img-src ‘self’ data:;` 
 
합니다 **기본 src** 지시문을 수정 하 되 [-src 지시문](https://developer.mozilla.org/docs/Web/HTTP/Headers/Content-Security-Policy/default-src) 각 지시문을 명시적으로 나열 하지 않고 합니다. 예를 들어 정책 아래 예제에서는 1은 정책 2와 동일 합니다.  

정책 1 
```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "Content-Security-Policy" -SetHeaderValue "default-src 'self'" 
```
 
정책 2
```PowerShell 
Set-AdfsResponseHeaders -SetHeaderName "Content-Security-Policy" -SetHeaderValue "script-src ‘self’; img-src ‘self’; font-src 'self';  
frame-src 'self'; manifest-src 'self'; media-src 'self';" 
```

지시문을 명시적으로 나열 된 경우 지정 된 값을 기본 src 지정 된 값을 재정의 합니다. 아래 예제에서 img src 걸립니다 값을 ' *' (모든 원본에서 로드 되도록 이미지 허용) 하지만 다른-src 지시문은 값으로 '자체' (웹 페이지와 같은 원본에 대 한 제한).  

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "Content-Security-Policy" -SetHeaderValue "default-src ‘self’; img-src *" 
```
원본 기본 src 정책에 대해 정의할 수 있습니다. 
 
- 웹 페이지의 원본으로 로드 된 콘텐츠의 출처 제한 지정이 'self' – 
- ' 안전 하지 않은-인라인 '-정책에서이 지정 수를 사용 하 여 인라인 JavaScript 및 CSS 
- ' 안전 하지 않은-eval' – 정책에서이 지정 하면 사용할 수 있습니다 같은 메커니즘을 JavaScript에는 텍스트 eval 
- 로드할 모든 원본에서 콘텐츠를 제한 지정이 '없음' – 
- 데이터:-데이터를 지정 합니다. Uri에는 콘텐츠 작성자가 문서에 인라인 작은 파일을 포함할 수 있습니다. 사용이 권장 되지 않습니다.  
 
>[!NOTE]
>AD FS 인증 프로세스에서 JavaScript를 사용 하 고 ' unsafe 인라인 '를 포함 하 여 JavaScript 따라서 및 ' 안전 하지 않은 eval' 원본의 기본 정책입니다.  

### <a name="custom-headers"></a>사용자 지정 헤더 
위의 항목 외에도 보안 응답 헤더를 나열 (HSTS, CSP, X-프레임-옵션, X XSS 보호 및 CORS), AD FS 2019 새 헤더를 설정 하는 기능을 제공 합니다.  
 
예: 새 헤더 "TestHeader" 값을 사용 하 여 "TestHeaderValue"으로 설정 하려면 

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "TestHeader" -SetHeaderValue "TestHeaderValue" 
 ```

설정 되 면 새 머리글 (아래 fiddler 조각) AD FS 응답에 전송 됩니다.  
 
![Fiddler](media\customize-http-security-headers-ad-fs\header2.png)

## <a name="web-browswer-compatibility"></a>웹 브라우저 호환성
다음 표 및 링크를 사용 하 여 어떤 웹 브라우저가 각 보안 응답 헤더와 호환 되는지 확인 합니다.

|HTTP 보안 응답 헤더|브라우저 호환성|
|-----|-----|
|HSTS (HTTP 엄격한-전송-보안)|[HSTS 브라우저 호환성](https://developer.mozilla.org/docs/Web/HTTP/Headers/Strict-Transport-Security#Browser_compatibility)|
|X-프레임-옵션|[X-프레임-옵션 브라우저 호환성](https://developer.mozilla.org/docs/Web/HTTP/Headers/X-Frame-Options#Browser_compatibility)| 
|X-XSS-Protection|[X XSS 보호 브라우저 호환성](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-XSS-Protection#Browser_compatibility)| 
|교차 원본 자원 공유 (CORS)|[CORS 브라우저 호환성](https://developer.mozilla.org/docs/Web/HTTP/CORS#Browser_compatibility) 
|콘텐츠 보안 정책 (CSP)|[CSP 브라우저 호환성](https://developer.mozilla.org/docs/Web/HTTP/CSP#Browser_compatibility) 

## <a name="next"></a>다음

- [AD FS 도움말 troublehshooting 가이드를 사용 합니다.](https://aka.ms/adfshelp/troubleshooting )
- [AD FS 문제 해결](../../ad-fs/troubleshooting/ad-fs-tshoot-overview.md)
