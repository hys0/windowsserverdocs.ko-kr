---
ms.assetid: aa892a85-f95a-4bf1-acbb-e3c36ef02b0d
title: Active Directory 페더레이션 서비스에 대 한 Windows Server 2016의 새로운 기능
author: billmath
ms.author: billmath
manager: daveba
ms.date: 01/22/2020
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: e88297bdbd55d2f834f1bff72b6d05bdf356bb85
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "80860256"
---
# <a name="whats-new-in-active-directory-federation-services"></a>Active Directory Federation Services의 새로운 기능


## <a name="whats-new-in-active-directory-federation-services-for-windows-server-2019"></a>Active Directory 페더레이션 서비스에 대 한 Windows Server 2019의 새로운 기능

### <a name="protected-logins"></a>보호된 로그인
다음은 AD FS 2019에서 사용할 수 있는 보호된 로그인 업데이트에 대한 간략한 요약 정보입니다.
- **외부 인증 공급자를 기본 공급자로 사용** - 이제 고객은 타사 인증 제품을 첫 번째 요소로 사용하고 암호를 첫 번째 요소로 노출하지 않을 수 있습니다. 외부 인증 공급자는 2개 요소를 증명할 수 있으면 MFA를 요청할 수 있습니다. 
- **추가 인증으로 암호 인증 사용** - 고객이 암호 없는 옵션을 첫 번째 요소로 사용한 후 추가 요소에만 암호를 사용할 수 있는 완전히 지원되는 수신함 옵션이 제공됩니다. 이렇게 하면 고객이 github 어댑터를 지원되는 그대로 다운로드해야 했던 ADFS 2016보다 고객 환경이 개선됩니다. 
- **플러그형 위험 평가 모듈** - 이제 고객은 사전 인증 단계에서 특정 유형의 요청을 차단하는 고유의 플러그 인 모듈을 빌드할 수 있습니다. 이렇게 하면 고객은 ID 보호와 같은 클라우드 인텔리전스를 사용하여 위험한 사용자 또는 위험한 트랜잭션에 대한 로그인을 쉽게 차단할 수 있습니다.  자세한 내용은 [AD FS 2019 위험 평가 모델을 사용하여 플러그 인 빌드](../../ad-fs/development/ad-fs-risk-assessment-model.md)를 참조하세요. 
- **ESL 개선** - 다음 기능을 추가하여 2016의 ESL QFE를 개선했습니다.
    - 고객이 ADFS 2012R2부터 사용 가능한 '클래식' 엑스트라넷 잠금 기능의 보호를 받는 동안 감사 모드를 사용할 수 있습니다. 현재 2016 고객은 감사 모드에서 보호를 받을 수 없습니다. 
    - 익숙한 위치에 독립적인 잠금 임계값을 사용할 수 있습니다. 이를 통해 공통 서비스 계정으로 실행되는 여러 앱 인스턴스가 최소한의 영향으로 암호를 롤오버할 수 있습니다. 

### <a name="additional-security-improvements"></a>향상된 추가 보안 기능
AD FS 2019에서는 다음과 같은 향상된 추가 보안 기능을 사용할 수 있습니다.
- **스마트 카드 로그인을 사용하는 원격 PSH** - 이제 고객은 스마트 카드를 사용하여 PSH를 통해 ADFS에 원격으로 연결하고, 해당 기능을 사용하여 다중 노드 PSH cmdlet을 포함한 모든 원격 PSH 기능을 관리할 수 있습니다.
- **HTTP 헤더 사용자 지정** - 이제 고객은 ADFS 응답 중에 내보낸 HTTP 헤더를 사용자 지정할 수 있습니다. 여기에는 다음 헤더가 포함됩니다.
     - HSTS: 호환 브라우저에서 적용할 HTTPS 엔드포인트에서만 ADFS 엔드포인트를 사용할 수 있습니다.
     - x-frame-options: ADFS 관리자는 특정 신뢰 당사자가 ADFS 대화형 로그인 페이지에 대한 iFrame을 포함하도록 허용할 수 있습니다. 이 옵션은 HTTPS 호스트에서만 신중하게 사용해야 합니다. 
     - 이후 헤더: 이후 헤더를 추가로 구성할 수도 있습니다. 

자세한 내용은 [AD FS 2019를 사용하여 HTTP 보안 응답 헤더 사용자 지정](../../ad-fs/operations/customize-http-security-headers-ad-fs.md)을 참조하세요. 

### <a name="authenticationpolicy-capabilities"></a>인증/정책 기능
다음은 AD FS 2019에의 인증/정책 기능입니다.
- **RP별로 추가 인증을 위한 인증 방법 지정** - 이제 고객은 클레임 규칙을 사용하여 추가 인증 공급자에 대해 호출할 추가 인증 공급자를 결정할 수 있습니다. 이것은 다음과 같은 2가지 사용 사례에 유용합니다.
    - 고객이 한 추가 인증 공급자에서 다른 인증 공급자로 전환하려 합니다. 고객은 사용자를 최신 인증 공급자에게 온보딩하는 이 방법을 통해, 그룹을 사용하여 호출되는 추가 인증 공급자를 제어할 수 있습니다.
    - 고객은 특정 애플리케이션에 사용할 특정 추가 인증 공급자(예: 인증서)가 필요합니다. 
- **TLS 기반 디바이스 인증이 필요한 애플리케이션으로 제한**  - 이제 고객은 클라이언트 TLS 기반 디바이스 인증을 디바이스 기반 조건부 액세스를 수행하는 애플리케이션으로 제한할 수 있습니다. 이렇게 하면 TLS 기반 디바이스 인증이 필요 없는 애플리케이션에서 원치 않는 디바이스 인증(또는 클라이언트 애플리케이션에서 처리할 수 없는 경우에는 오류)을 요구하는 프롬프트를 방지할 수 있습니다.
- **MFA 새로 고침 지원**    - 이제 AD FS는 2번째 요소 자격 증명의 새로 고침을 기반으로 2번째 요소 자격 증명을 다시 수행할 수 있는 기능을 지원합니다. 따라서 고객은 2개 요소를 사용하여 초기 트랜잭션을 수행하고 2번째 요소를 정기적으로 요청할 수 있습니다. 이 방법은 요청에 추가 매개 변수를 제공할 수 있는 애플리케이션에만 사용할 수 있고 ADFS에서는 구성할 수 없는 설정입니다. 이 매개 변수는 Azure AD에서 "Remember my MFA for X days(X일 동안 MFA 저장)"를 구성하고 페더레이션된 도메인 트러스트 설정에서 'supportsMFA' 플래그를 true로 설정한 경우에 Azure AD에서 지원됩니다. 

### <a name="sign-in-sso-improvements"></a>로그인 SSO 개선
AD FS 2019에서는 로그인 SSO가 다음과 같이 개선되었습니다.

- [중앙 테마를 사용하는 페이지가 매겨진 UX](../operations/AD-FS-paginated-sign-in.md) - 이제 ADFS는 유효성을 검사하고 보다 원활한 로그인 환경을 제공할 수 있는 페이지가 매겨진 UX 흐름으로 이동되었습니다. 이제 ADFS는 화면 오른쪽 대신 가운데 맞춤 UI를 사용합니다. 이 환경에 맞는 새 로고와 배경 이미지가 필요할 수도 있습니다. 또한 Azure AD에서 제공되는 기능도 미러링합니다.
- **버그 수정: PRT 인증을 수행할 때 Win10 디바이스의 영구적 SSO 상태**    Windows 10 디바이스에 PRT 인증을 사용할 때 MFA 상태가 유지되지 않는 문제를 해결합니다. 이 문제가 발생하면 최종 사용자에게 MFA(2번째 단계 자격 증명)를 요청하는 메시지가 자주 표시되었습니다. 또한 이 수정 버전은 클라이언트 TLS 및 PRT 메커니즘을 통해 수행한 디바이스 인증이 성공하면 일관적인 환경을 제공합니다. 


### <a name="suppport-for-building-modern-line-of-business-apps"></a>최신 기간 업무 앱 빌드 지원
최신 LOB 앱 빌드에 대한 다음 지원이 AD FS 2019에 추가되었습니다.

 - **Oauth 디바이스 흐름/프로필** - 이제 AD FS는 풍부한 로그인 환경을 지원하기 위해 UI 노출 영역이 없는 디바이스에서 로그인을 수행할 수 있도록 OAuth 디바이스 흐름 프로필을 지원합니다. 따라서 사용자가 다른 디바이스에서 로그인 경험을 완료할 수 있습니다. 이 기능은 Azure Stack에서 Azure CLI 환경에 필요하며 다른 사용 사례에도 사용할 수 있습니다. 
 - **'Resource' 매개 변수 제거** - 이제 AD FS를 사용하기 위해 현재 Oauth 사양과 일치하는 리소스 매개 변수를 지정할 필요가 없습니다. 이제 클라이언트는 요청된 권한 외에도 신뢰 당사자 트러스트 식별자를 범위 매개 변수로 제공할 수 있습니다. 
 - **AD FS 응답의 CORS 헤더** - 이제 고객은 AD FS의 OIDC 검색 문서에서 서명 키를 쿼리하여 클라이언트 쪽 JS 라이브러리에서 id_token 서명의 유효성을 검사할 수 있는 단일 페이지 애플리케이션을 빌드할 수 있습니다. 
 - **PKCE 지원**    - AD FS는 OAuth 내에서 보안 인증 코드 흐름을 제공하는 PKCE 지원을 추가합니다. 그러면 코드를 하이재킹하여 다른 클라이언트에서 재생하지 못하게 방지하는 추가 보안 레이어가 이 흐름이 추가됩니다. 
 - **버그 수정: x5t 및 어린이 클레임 보내기** - 사소한 버그 수정입니다. 이제 AD FS는 '어린이' 클레임을 추가로 전송하여 서명을 확인하는 키 id 힌트를 표시합니다. 이전에는 AD FS가 이것을 'x5t' 클레임으로만 전송했습니다.

### <a name="supportability-improvements"></a>향상된 지원 가능성
다음 향상된 지원 가능성은 AD FS 2019에 포함되지 않습니다.
- **AD FS 관리자에게 오류 세부 정보 전송** - 관리자는 쉽게 사용할 수 있도록 최종 사용자 인증 실패와 관련된 디버그 로그를 보내 압축 파일로 저장하도록 최종 사용자를 구성할 수 있습니다. 또한 관리자는 압축 파일을 심사 이메일 계정으로 자동 전송하도록 또는 이메일을 기반으로 티켓을 자동 생성하도록 SMTP 연결을 구성할 수도 있습니다. 

### <a name="deployment-updates"></a>배포 업데이트
AD FS 2019에는 다음 배포 업데이트가 포함되어 있습니다.
- **팜 동작 수준 2019** - AD FS 2016과 마찬가지로, 위에 설명된 새 기능을 사용하려면 필요한 새 팜 동작 수준 버전이 있습니다. 이 버전을 통해 다음과 같이 전환할 수 있습니다.
    - 2012 R2 -> 2019
    - 2016 -> 2019     

### <a name="saml-updates"></a>SAML 업데이트
다음은 AD FS 2019의 SAML 업데이트입니다.
- **버그 수정: 집계된 페더레이션의 버그 수정** - 집계된 페더레이션 지원(예: InCommon)과 관련된 여러 버그가 수정되었습니다. 수정 사항은 다음과 같습니다. 
  - 집계된 페더레이션 메타데이터 문서에 있는 수많은 엔터티의 스케일링이 향상되었습니다. 이전에는 이 작업이 "ADMIN0017" 오류로 인해 실패했습니다. 
  - Get-AdfsRelyingPartyTrustsGroup PSH cmdlet을 통해 'ScopeGroupID' 매개 변수를 사용하여 쿼리합니다. 
  - 중복 entityID와 관련된 오류 조건 처리


### <a name="azure-ad-style-resource-specification-in-scope-parameter"></a>범위 매개 변수의 Azure AD 스타일 리소스 사양 
이전에는 AD FS를 사용하려면 원하는 리소스 및 범위가 인증 요청에서 별도의 매개 변수에 있어야 했습니다. 예를 들어 일반적인 oauth 요청은 다음과 같습니다. 7 **https:&#47;&#47;fs.contoso.com/adfs/oauth2/authorize?</br>response_type=code&client_id=claimsxrayclient&resource=urn:microsoft:</br>adfs:claimsxray&scope=oauth&redirect_uri=https:&#47;&#47;adfshelp.microsoft.com/</br> ClaimsXray/TokenResponse&prompt=login**
 
Server 2019에서 AD FS를 사용하면 이제 범위 매개 변수에 포함된 리소스 값을 전달할 수 있습니다. 이는 사용자가 Azure AD에 인증하는 방법과도 일치합니다. 

이제 범위 매개 변수를 공백으로 구분된 목록으로 구성할 수 있습니다. 여기서 각 항목은 리소스/범위로 구조화됩니다. 

> [!NOTE]
> 인증 요청에서 리소스를 하나만 지정할 수 있습니다. 요청에 둘 이상의 리소스가 포함된 경우 AD FS에서 오류를 반환하고 인증이 실패합니다. 

### <a name="proof-key-for-code-exchange-pkce-support-for-oauth"></a>oAuth에 PKCE(코드 교환용 증명 키) 지원 
인증 코드 부여를 사용하는 OAuth 퍼블릭 클라이언트는 인증 코드 가로채기 공격에 취약합니다.  이 공격은 RFC 7636에 잘 설명되어 있습니다. 이 공격을 완화하기 위해, Server 2019의 AD FS는 OAuth 인증 코드 부여 흐름을 위한 PKCE(코드 교환용 증명 키)를 지원합니다. 
 
PKCE 지원을 활용하기 위해 이 사양에서는 OAuth 2.0 권한 부여 및 액세스 토큰 요청에 추가 매개 변수를 추가합니다.

![Proofkey](media/whats-new-in-active-directory-federation-services-for-windows-server-2016/adfs2019.png)

A. 클라이언트는 "code_verifier"라는 비밀을 만들고 기록하고, 변환된 버전 "t(code_verifier)"("code_challenge"라고도 함)을 파생합니다. 변환된 버전은 "t_m"과 함께 OAuth 2.0 권한 부여 요청에 전송됩니다. 

B. 권한 부여 엔드포인트는 평소처럼 응답하지만, "t(code_verifier)" 및 변환 메서드를 기록합니다. 

C. 그러면 클라이언트는 평소처럼 액세스 토큰 요청에 권한 부여 코드를 전송하지만, (A)에서 생성된 "code_verifier" 비밀을 포함합니다. 

D. AD FS는 "code_verifier"를 변환하고 (B)의 "t(code_verifier)"와 비교합니다.  둘이 같지 않으면 액세스가 거부됩니다. 

#### <a name="faq"></a>FAQ 
> [!NOTE] 
> ADFS 관리자 이벤트 로그에서 다음 오류가 발생할 수 있습니다. 잘못된 OAuth 요청을 받았습니다. 'NAME' 클라이언트는 범위가 'ugs'인 리소스에 액세스할 수 없습니다. 이 오류를 해결하려면 다음을 수행합니다. 
> 1. AD FS 관리 콘솔을 시작합니다. "서비스 > 범위 설명"으로 이동합니다.
> 2. "범위 설명"을 마우스 오른쪽 단추로 클릭하고 "범위 설명 추가"를 선택합니다.
> 3. 이름 아래에 "ugs"를 입력하고 적용 > 확인을 클릭합니다.
> 4. 관리자 권한으로 PowerShell을 시작합니다.
> 5. "Get-AdfsApplicationPermission" 명령을 실행합니다. ClientRoleIdentifier가 있는 ScopeNames :{openid, aza}를 찾습니다. ObjectIdentifier를 적어둡니다.
> 6. "Set-AdfsApplicationPermission -TargetIdentifier <5단계의 ObjectIdentifier> -AddScope 'ugs' 명령을 실행합니다.
> 7. ADFS 서비스를 다시 시작합니다.
> 8. 클라이언트에서: 클라이언트를 다시 시작합니다. WHFB를 프로비저닝하라는 메시지가 표시되어야 합니다.
> 9. 프로비저닝 창이 나타나지 않으면 NGC 추적 로그를 수집하여 추가 문제 해결이 필요합니다.

**Q.** Azure AD에 대한 요청 수행 방식과 같이 리소스 값을 범위 값의 일부로 전달할 수 있나요? 
</br>**A.** Server 2019에서 AD FS를 사용하면 이제 범위 매개 변수에 포함된 리소스 값을 전달할 수 있습니다. 이제 범위 매개 변수를 공백으로 구분된 목록으로 구성할 수 있습니다. 여기서 각 항목은 리소스/범위로 구조화됩니다. 예를 들면 다음과 같습니다.  
**<올바른 샘플 요청 만들기>**

**Q.** AD FS에서 PKCE 확장을 지원하나요?
</br>**A.** 서버 2019의 AD FS는 OAuth 인증 코드 부여 흐름에 대한 PKCE(코드 교환용 증명 키)를 지원합니다. 

## <a name="whats-new-in-active-directory-federation-services-for-windows-server-2016"></a>Active Directory 페더레이션 서비스에 대 한 Windows Server 2016의 새로운 기능   
이전 버전의 AD FS에 대 한 정보를 찾고 다음 문서를 참조 합니다.  
 [Windows Server 2012 또는 2012 r 2에서 ADFS](https://technet.microsoft.com/library/hh831502.aspx) 및 [AD FS 2.0](https://technet.microsoft.com/library/adfs2.aspx)  

 Single sign-on 간에 다양 한 Office 365, 클라우드를 비롯 한 애플리케이션을 기반으로 SaaS 애플리케이션을 회사 네트워크에 있는 애플리케이션 및 active Directory Federation Services 액세스 제어를 제공 합니다.  
* IT 조직에 대 한 수 있습니다 로그온 제공 액세스 제어 및 현대적이 고 레거시 애플리케이션을 온-프레미스와 클라우드에서 자격 증명 및 정책의 같은 집합 기반으로 합니다.    
* 사용자를 동일 하 고 친숙 한 계정 자격 증명을 사용 하 여 원활 하 게 기호를 제공 합니다.  
* 개발자를 위한 애플리케이션, 하지 인증 또는 identity에 노력을 집중할 수 있도록 id가 조직 디렉터리에 거주 하는 사용자를 인증 하는 간편한 방법을 제공 합니다.  

이 문서에서는 Windows Server 2016 (AD FS 2016)에서 AD FS의 새로운 기능을 설명 합니다.  

## <a name="eliminate-passwords-from-the-extranet"></a>엑스트라넷에서 암호 제거  
AD FS 2016 수 있도록 세 가지 새로운 옵션을 암호를 네트워크의 위험을 방지 하려면 조직의 없이 로그온 phished, 손실 또는 도난 방지 암호에서에서 손상 됩니다. 

### <a name="sign-in-with-azure-multi-factor-authentication"></a>Azure multi-factor Authentication을 사용 하 여 로그인
AD FS 2016 기반으로 다단계 인증 (MFA) 기능 Windows Server 2012 r 2에서 AD fs는 Azure MFA 코드를 사용 하 여 사용자 이름 및 암호를 먼저 입력 하지 않으면 로그온을 허용 하 여 합니다.

* 기본 인증 방법으로 Azure MFA를 사용 하 여 사용자가 자신의 사용자 이름 및 Azure Authenticator 앱에서 OTP 코드에 대 한 입력 합니다.  
* 보조 또는 추가 인증 방법으로 Azure MFA를 사용 하 여 OTP Azure MFA 로그인을 기반으로 기본 인증 (Windows 통합 인증, 사용자 이름 및 암호, 스마트 카드 또는 사용자 또는 디바이스 인증서 사용) 하는 자격 증명 한 다음 텍스트를 음성에 대 한 프롬프트를 표시 하거나 사용자가 제공 합니다.  
* 새 기본 제공 Azure MFA 어댑터와 함께 설치 및 구성 AD FS와 Azure MFA에 대 한 적이 더 간단 합니다.
* 조직에서는 Azure MFA는 온-프레미스 Azure MFA 서버에 대 한 필요 없이 활용을 걸릴 수 있습니다.
* 인트라넷 또는 엑스트라넷의 일부 또는 모든 액세스 제어 정책 azure MFA는 구성할 수 있습니다.

AD FS와 Azure MFA에 대 한 자세한 내용은
*  [AD FS 2016 및 Azure MFA 구성](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configure-ad-fs-and-azure-mfa)  

### <a name="password-less-access-from-compliant-devices"></a>호환 디바이스에서 암호 없이 액세스
에 로그인 할 수 있도록 하려면 이전 디바이스 등록 기능을 기반으로 하는 AD FS 2016 및 액세스 제어 디바이스 준수 상태를 기반으로 합니다. 사용자가 디바이스 자격 증명을 사용 하 여 로그온 할 수 있습니다 하 고 규정 준수는 재평가 디바이스 특성이 변경 될 때 정책이 적용 되는 항상 확인할 수 있도록 합니다.  와 같은 정책을 사용 하면이

* 관리 되는 및/또는 호환 되는 디바이스 에서만에서 액세스를 사용 하도록 설정  
* 엑스트라넷 액세스 관리 및/또는 호환 되는 디바이스 에서만에서 사용 하도록 설정  
* 관리 되는 준수 또는 미준수 있지 않은 컴퓨터에 대 한 다단계 인증을 요구 합니다.  

AD FS는 하이브리드 시나리오에서 조건부 액세스 정책의 온-프레미스 구성 요소를 제공합니다. 클라우드 리소스에 대 한 조건부 액세스에 대 한 Azure AD에 디바이스를 등록할 때 AD FS 정책도에 대 한 디바이스 id는 사용할 수 있습니다.

![새로운 기능](media/whats-new-in-active-directory-federation-services-for-windows-server-2016/ADFS_ITPRO4.png)  

 디바이스를 사용 하는 방법에 대 한 자세한 내용은 기반 클라우드에서 조건부 액세스   
 *  [Azure Active Directory 조건부 액세스](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access/)

디바이스를 사용 하는 방법에 대 한 자세한 내용은 AD FS 사용 하 여 조건부 액세스 기반
*  [AD FS를 사용하여 디바이스 기반 조건부 액세스 계획 수립](../../ad-fs/deployment/Plan-Device-based-Conditional-Access-on-Premises.md)  
* [AD FS의 액세스 제어 정책](../../ad-fs/operations/Access-Control-Policies-in-AD-FS.md)  

### <a name="sign-in-with-windows-hello-for-business"></a>비즈니스용 Windows Hello로 로그인  

> [!NOTE]
> 현재 Google Chrome 및 [Chromium 기반의 최신 Microsoft Edge](https://www.microsoft.com/edge?form=MB110A&OCID=MB110A) 오픈 소스 프로젝트 브라우저는 비즈니스용 Windows Hello를 사용하는 브라우저 기반 SSO(Single Sign-On)를 지원하지 않습니다. Internet Explorer 또는 이전 버전의 Microsoft Edge를 사용하세요.  

Windows 10 디바이스는 Windows Hello 및 비즈니스용 Windows Hello를 도입하여 사용자 암호를 사용자 제스처(PIN, 지문 또는 안 면 인식 같은 생체 인식 제스처)로 보호된 강력한 디바이스 바인딩 사용자 자격 증명으로 바꿉니다. AD FS 2016은 이러한 새 Windows 10 기능을 지원하므로, 사용자가 암호를 입력하지 않고도 인트라넷 또는 엑스트라넷에서 AD FS 애플리케이션에 로그인할 수 있습니다.

Microsoft Windows Hello 비즈니스에 대 한 조직에서 사용 하는 방법에 대 한 자세한 내용은
*  [조직에서 비즈니스용 Windows Hello 사용](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-passport-deployment/)

## <a name="secure-access-to-applications"></a>애플리케이션에 대 한 보안 액세스

### <a name="modern-authentication"></a>최신 인증
AD FS 2016 Windows 10으로 최신 iOS 및 Android 디바이스 및 응용 프로그램에 대 한 더 나은 사용자 환경을 제공 하는 최신 최신 프로토콜을 지원 합니다.  

자세한 내용은 참조 [개발자를 위한 AD FS 시나리오](../../ad-fs/overview/ad-fs-openid-connect-oauth-flows-scenarios.md)  


### <a name="configure-access-control-policies-without-having-to-know-claim-rules-language"></a>몰라도 액세스 제어 정책 구성 클레임 규칙 언어  
이전에 AD FS 관리자 구성 해야 했습니다 AD FS 클레임 규칙 언어를 사용 하 여 정책을 구성 하 고 정책을 유지 하기가 어렵습니다. 액세스 제어 정책을 사용 하 여 관리자가 템플릿을 사용 하 여 기본 제공 같은 일반적인 정책 적용
* 인트라넷 액세스에만 허용 합니다.
* 모든 사용자 허용 또는 엑스트라넷에서 MFA를 요구
* 모든 사용자 허용 및 특정 그룹에서 MFA를 요구

예외 또는 추가 정책 규칙을 추가 하려면 프로세스를 구동 하는 마법사를 사용 하 여 사용자 지정 하기 템플릿과 일치 정책 적용에 대 한 하나 이상의 애플리케이션에 적용할 수 있습니다.

자세한 내용은 참조 [AD FS에서 액세스 제어 정책입니다.](../../ad-fs/operations/Access-Control-Policies-in-AD-FS.md)  

### <a name="enable-sign-on-with-non-ad-ldap-directories"></a>비 AD LDAP 디렉터리에 대해 로그온 사용  
많은 조직에는 Active Directory 및 타사 디렉터리의 조합입니다. LDAP v3 호환 디렉터리에 저장 된 사용자를 인증 하는 것에 대 한 AD FS 지원 추가 하 여 AD FS 이제 데 사용할 수 있습니다.
* 제 3 자, LDAP v3 호환 디렉터리의 사용자
* Active Directory 포리스트에 없는 Active Directory 양방향 트러스트 구성 되지 않은 사용자
* 사용자가 Active Directory Lightweight Directory Services (AD LDS)에서

자세한 내용은 참조 [LDAP 디렉터리에 저장 된 사용자를 인증 하도록 AD FS 구성 합니다.](../../ad-fs/operations/Configure-AD-FS-to-authenticate-users-stored-in-LDAP-directories.md)  

## <a name="better-sign-in-experience"></a>더 나은 로그인 환경
### <a name="customize-sign-in-experience-for-ad-fs-applications"></a>로그인 환경 AD FS 애플리케이션에 대 한 사용자 지정  
이 많았습니다 사용자에 게 서 각 애플리케이션에 대 한 로그온 환경을 사용자 지정 하는 기능에 여러 개의 서로 다른 회사 또는 브랜드를 나타내는 애플리케이션에 대 한 기호를 제공 하는 조직에 특히 유용한 유용성 개선, 것입니다.  

이전에 Windows Server 2012 r 2에서 AD FS 모든 신뢰 당사자 애플리케이션에 대 한 경험에 공용 기호를 제공, 텍스트의 하위 집합을 사용자 지정할 수 있는 애플리케이션별 콘텐츠를 기반으로 합니다. Windows Server 2016 뿐만 아니라 메시지를 하지만 이미지, 애플리케이션별 로고 및 웹 테마를 지정할 수 있습니다. 또한 새로 만들고, 사용자 지정 웹 테마 하 고 적용 당 신뢰 당사자입니다.  

자세한 내용은 참조 [AD FS 사용자 지정 로그인 합니다.](../../ad-fs/operations/AD-FS-user-sign-in-customization.md)  



## <a name="manageability-and-operational-enhancements"></a>관리 효율성 및 운영 기능 향상  
다음 섹션에서 Windows Server 2016 Active Directory Federation Services에 도입 된 향상 된 운영 시나리오를 설명 합니다.  

### <a name="streamlined-auditing-for-easier-administrative-management"></a>더 쉽게 관리 관리에 대 한 감사 간소화  
Ad에서 FS Windows Server 2012 R2에 대 한 단일 요청 및 로그인에 대 한 관련 정보에 대해 생성 된 다양 한 감사 이벤트 되었거나 토큰 발급 활동은 없는 (AD FS의 일부 버전)에서 또는 여러 감사 이벤트에 걸쳐 있습니다. AD FS 기본적으로 감사 이벤트의 자세한 특성으로 인해 해제 됩니다.  
AD FS 2016 릴리스마다 감사 되었습니다 더 효율적이 고 상대적으로 간단 합니다.  

자세한 내용은 참조 [Windows Server 2016에서 AD FS에 대 한 향상을 감사 합니다.](../../ad-fs/technical-reference/auditing-enhancements-to-ad-fs-in-windows-server.md)  

### <a name="improved-interoperability-with-saml-20-for-participation-in-confederations"></a>Confederations에 참가 하기 위해 SAML 2.0와의 상호 운용성 향상  
AD FS 2016 여러 엔터티를 포함 하는 메타 데이터에 따라 트러스트 가져오기에 대 한 지원을 포함 하는 SAML 프로토콜 지원 추가 포함 합니다. 그러면 confederations InCommon 페더레이션 등 eGov 2.0 표준에 맞는 다른 구현에에서 참여 하도록 AD FS를 구성할 수 있습니다.  

자세한 내용은 참조 [SAML 2.0와의 상호 운용성을 개선 합니다.](../../ad-fs/operations/Improved-interoperability-with-SAML-2.0.md)  

### <a name="simplified-password-management-for-federated-o365-users"></a>간소화 된 암호 관리에 대 한 페더레이션 O365 사용자  
Active Directory Federation Services (AD FS) 암호 만료 클레임을 보내도록 AD FS로 보호 되는 신뢰 당사자 트러스트 (애플리케이션)를 구성할 수 있습니다. 이러한 클레임을 사용 하는 방법을 애플리케이션에 따라 달라 집니다. 예를 들어, 신뢰 당사자로 Office 365를 통해 업데이트 하도록 구현 Exchange 및 Outlook 곧에-수-만료 된 암호의 페더레이션된 사용자에 게 알려야 합니다.  

자세한 내용은 참조 [암호 만료 클레임을 보내도록 AD FS 구성 합니다.](../../ad-fs/operations/Configure-AD-FS-to-Send-Password-Expiry-Claims.md)  

### <a name="moving-from-ad-fs-in-windows-server-2012-r2-to-ad-fs-in-windows-server-2016-is-easier"></a>Windows Server 2012 r 2에서 AD FS에서 Windows Server 2016에서 AD FS로 이동 하는 것이 더 쉽습니다.  
기존 팜에서 구성 내보내기 및 새로운, 병렬 팜에 가져오기 이전에 필요한 새 버전의 AD FS로 마이그레이션.  

이제 Windows Server 2016에서 AD FS를 Windows Server 2012 r 2에서 AD FS에서 이동 훨씬 쉽게 되었습니다. Windows Server 2012 R2 팜에 새 Windows Server 2016 서버를 추가 하면 팜의 매기고 Windows Server 2012 R2 팜 동작 수준에서 찾아서는 Windows Server 2012 R2 팜의 같은 방식으로 작동 하므로 합니다.  

그런 다음 새 Windows Server 2016 서버를 팜에 추가, 기능을 확인 하 고 부하 분산 장치에서 이전 서버를 제거 합니다. 모든 팜 노드에서 Windows Server 2016를 실행 하는 경우 팜 동작 수준 2016를 업그레이드 하 고 새로운 기능을 사용 하 여 시작 준비가 됩니다.  

자세한 내용은 참조 [AD FS에서 Windows Server 2016으로 업그레이드 합니다.](../../ad-fs/deployment/Upgrading-to-AD-FS-in-Windows-Server-2016.md)  
