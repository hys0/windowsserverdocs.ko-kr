---
ms.assetid: aa892a85-f95a-4bf1-acbb-e3c36ef02b0d
title: Windows Server 2016용 AD FS(Active Directory Federation Services)의 새로운 기능
description: ''
author: billmath
ms.author: billmath
manager: daveba
ms.date: 04/23/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fbb289c16d82da79aded49e3af4134ac7f6df325
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188702"
---
# <a name="whats-new-in-active-directory-federation-services"></a>Active Directory Federation Services의 새로운 기능


## <a name="whats-new-in-active-directory-federation-services-for-windows-server-2019"></a>Active Directory 페더레이션 서비스에 대 한 Windows Server 2019의 새로운 기능

### <a name="protected-logins"></a>보호 된 로그인
다음은 AD FS 2019에서에서 사용할 수 있는 보호 된 로그인에 대 한 업데이트의 간단한 요약입니다.
- **기본 외부 인증 공급자** -고객은 이제 타사 인증 제품을 사용 하 여 첫 번째 단계로 첫 번째 단계로 암호를 노출 하지 않습니다. 외부 인증 공급자를 2 요소를 증명할 수 있는 경우에서 해당 MFA를 요구할 수 없습니다. 
- **추가 인증 방법으로 암호 인증** -고객은 추가 단계 후 암호 적은 옵션에 대 한 첫 번째 단계로 사용 되는 암호를 사용 하는 완전히 지원 되는 수신함 옵션입니다. 따라서 고객은 있는 그대로 지원 되는 github 어댑터를 다운로드 해야 하는 ADFS 2016에서 고객 만족도를 향상 됩니다. 
- **플러그형 위험 평가 모듈** -고객은 이제 사전 인증 단계 중 특정 유형의 요청을 차단 하는 모듈 자체 플러그 인을 빌드할 수 있습니다. 그러면 고객이 Id 보호와 같은 클라우드 인텔리전스를 사용 하 여 위험한 사용자 또는 위험한 트랜잭션을 실행 하는 것에 대 한 로그인을 차단 하는 데 더 쉽습니다.  자세한 내용은 참조 하세요. [ AD FS 2019 위험 평가 모델을 사용 하 여 플러그 인 빌드](../../ad-fs/development/ad-fs-risk-assessment-model.md) 
- **ESL 향상** -다음과 같은 기능을 추가 하 여 ESL QFE 2016에서 개선
    - 통해 ADFS 2012R2부터 사용할 수 있음 '클래식' 엑스트라넷 잠금 기능을 통해 보호 되는 동안 감사 모드로 설정 될 수 있습니다. 현재 2016 고객에 게 감사 모드에서 보호 되지 않음 해야 합니다. 
    - 친숙 한 위치에 대 한 독립적인 잠금 임계값을 사용 하도록 설정 합니다. 이렇게 하면 최소한의 영향을 사용 하 여 암호를 롤오버 하는 일반적인 서비스 계정으로 실행 되는 앱의 여러 인스턴스에 대 한 합니다. 

### <a name="additional-security-improvements"></a>향상 된 추가 보안 기능
다음과 같은 추가 보안 개선 AD FS 2019에에서 사용할 수 있습니다.
- **스마트 카드 로그인을 사용 하 여 원격 PSH** -고객 수 지금 사용 하 여 스마트 카드 원격 PSH 통해 ADFS에 연결 하 고 사용 하 여 함수 모든 PSH를 관리 하는 다중 노드 PSH cmdlet이 포함 되어 있습니다.
- **사용자 지정 HTTP 헤더** -고객은 이제 ADFS 응답 중 발생 하는 HTTP 헤더를 사용자 지정할 수 있습니다. 여기에 다음 헤더가 포함 됩니다.
     - HSTS: 이 ADFS 끝점 에서만 사용할 수를 준수 하는 브라우저에 대 한 HTTPS 끝점에 적용할를 전달합니다
     - x-frame-options: ADFS 대화형 로그인 페이지에 Iframe을 포함 하는 특정 신뢰 당사자 있도록 ADFS 관리자를 수 있습니다. 신중 하 게 하 고 HTTPS 호스트에만 사용 해야 합니다. 
     - 향후 헤더: 추가 헤더는 향후도 구성할 수 있습니다. 

자세한 내용은 참조 하세요. [AD FS 2019를 사용 하 여 사용자 지정 HTTP 보안 응답 헤더](../../ad-fs/operations/customize-http-security-headers-ad-fs.md) 

### <a name="authenticationpolicy-capabilities"></a>인증/정책 기능
다음 인증/정책 기능은 AD FS 2019에서:
- **RP 당 추가 인증에 대 한 인증 방법을 지정** -고객은 이제 사용 하 여 클레임 규칙 추가 인증 공급자에 대 한 호출 하는 추가 인증 공급자를 결정 합니다. 2 사용 사례에 유용
    - 고객으로 전환 하 고 하나의 추가 인증 공급자에서 다른 합니다. 최신 인증 공급자를이 방식으로 이러한 등록 사용자 그룹 추가 인증 공급자 라고 하는 컨트롤을 사용할 수 있습니다.
    - 고객은 특정 응용 프로그램에 대 한 특정 추가 인증 공급자 (예: 인증서)에 대 한 요구를 있습니다. 
- **TLS 기반 장치 인증을 필요로 하는 응용 프로그램에만 제한** -고객에 게 TLS 응용 프로그램이 장치 기반 조건부 액세스 장치 인증을 기반으로 하는 클라이언트를 이제 제한할 수 있습니다. 이 TLS 기반 장치 인증 하지 않아도 되는 응용 프로그램에 대 한 장치 인증 (또는 클라이언트 응용 프로그램에서 처리할 수 없는 경우 오류)에 대 한 불필요 한 프롬프트를 방지 합니다.
- **MFA 지 원하는 새로 고침** -AD FS는 이제 기능을 지원 하려면 두 번째 단계 자격 증명의 새로 고침을 기반으로 두 번째 단계 자격 증명 다시 수행 합니다. 이렇게 하면 2 요소 및 정기적으로 2 단계 확인만 포함 하는 초기 트랜잭션 작업을 수행 하는 고객 수 있습니다. 이것이 요청에 추가 매개 변수를 제공할 수 있으며 ADFS에서 구성 가능한 설정이 아닙니다는 응용 프로그램에 사용할 수 있습니다. 이 매개 변수는 'supportsMFA' 플래그 설정 되 고 "X 일에 대 한 내 MFA 기억" 구성 된 경우 Azure AD에서 지원 되는 Azure AD에서 페더레이션된 도메인 트러스트 설정에 true입니다. 

### <a name="sign-in-sso-improvements"></a>로그인 SSO 향상 된 기능
AD FS 2019에에서 다음 로그인 SSO 개선이 이루어졌습니다.

- [UX 가운데에 테마를 사용 하 여 페이지를 매긴](../operations/AD-FS-paginated-sign-in.md) -이제 ADFS의 유효성을 검사 하 여 보다 원활한 로그인 환경을 제공 하는 ADFS를 허용 하는 페이지 매긴된 UX 흐름으로 이동 되었습니다. 이제 ADFS (화면 오른쪽)이 아닌 가운데 UI를 사용합니다. 이 환경에 맞게 최신 로고 및 배경 이미지를 필요할 수 있습니다. 이 Azure AD에서 제공 하는 기능을 또한 미러링합니다.
- **버그 수정: Win10 장치 PRT 인증을 수행 하는 경우에 대 한 영구 SSO 상태** PRT 인증을 사용 하 여 Windows 10 장치의 경우 MFA 상태 유지 되지 않은 문제를 해결 하는이 합니다. 문제에 대 한 결과 최종 사용자에 게는 메시지가 두 번째 단계 자격 증명 (MFA)에 대 한 자주 했습니다. 문제를 해결 하기도 환경을 일관 된 장치 인증에는 TLS 클라이언트를 통해 및 PRT 메커니즘을 통해 성공적으로 수행 되는 경우. 


### <a name="suppport-for-building-modern-line-of-business-apps"></a>최신 기간 업무 앱 빌드에 대 한 지원
AD FS 2019에 최신 LOB 앱을 빌드하기 위해 다음 지원이 추가 되었습니다.

 - **Oauth 장치 흐름/프로필** -AD FS는 이제 OAuth 장치 흐름 프로필을 다양 한 로그인 환경을 지원 하기 위해 UI 노출 영역을 되지 않은 장치에서 로그인을 수행 합니다. 이렇게 하면 사용자가 다른 장치에서 로그인 환경을 완료 합니다. 이 기능은 Azure Stack에서 Azure CLI 환경에 대 한 필수 이며 다른 경우에 사용할 수 있습니다. 
 - **'Resource' 매개 변수 제거** -AD FS는 이제 현재 Oauth 사양에 따라는 리소스 매개 변수를 지정 하는 요구 사항을 제거 되었습니다. 클라이언트가 이제를 제공할 수 신뢰 당사자 트러스트 식별자 범위 매개 변수로 또한 권한을 요청 합니다. 
 - **AD FS 응답에 CORS 헤더** -고객은 이제 클라이언트 쪽 JS 라이브러리 OIDC 검색 문서에서 AD FS에서 서명 키를 쿼리하여 id_token의 서명 유효성 검사를 허용 하는 단일 페이지 응용 프로그램을 빌드할 수 있습니다. 
 - **PKCE 지원** -AD FS OAuth 내 보안 인증 코드 흐름을 위해 PKCE 지원을 추가 합니다. 이 코드를 하이재킹 하 고 다른 클라이언트에서 재생을 방지 하기 위해이 흐름에 추가 보안 계층을 추가 합니다. 
 - **버그 수정: X5t 및 kid 클레임 보내기** -는 사소한 버그 수정입니다. AD FS 이제 또한 보냅니다 'kid' 클레임에 서명 확인에 대 한 키 id 힌트를 나타냅니다. 이전에 AD FS에만 전송이 'x5t' 클레임으로.

### <a name="supportability-improvements"></a>지원 가능성 향상
다음 지원 가능성 향상 된 AD FS 2019의 일부가 아닌:
- **AD FS 관리자에 게 오류 정보를 전송** -간편한 사용에 대 한 압축을 제출 하는 대로 저장할 최종 사용자 인증 실패와 관련 된 디버그 로그를 보내기 위해 최종 사용자를 구성 하는 관리자 수 있습니다. 관리자는 automail zip 파일을 심사 전자 메일 계정 또는 자동으로 전자 메일 기반 티켓 만들기에 대 한 SMTP 연결을 구성할 수도 있습니다. 

### <a name="deployment-updates"></a>배포 업데이트
다음 배포 업데이트는 이제 AD FS 2019에에서 포함 됩니다.
- **팜 동작 수준 2019** -ad FS 2016에는 새 팜 동작 수준 버전 위에 설명 된 새 기능을 사용 하는 데 필요한입니다. 이렇게 하면 0으로 변경 합니다.
    - 2012 R2-> 2019
    - 2016 -> 2019   

### <a name="saml-updates"></a>SAML 업데이트
다음 SAML 업데이트는 AD FS 2019에에서 있습니다.
- **버그 수정: 집계 된 페더레이션에서 버그를 수정** -집계 된 페더레이션 지원 관련 다양 한 버그 수정 되었습니다 (예: InCommon). 다음 관련 수정 되었습니다. 
  - 엔터티의 집계 된 페더레이션 메타 데이터 문서에서 대규모 #에 대 한 확장성 향상. 이전에 "ADMIN0017" 오류로 실패 하 게 됩니다. 
  - Get-AdfsRelyingPartyTrustsGroup PSH cmdlet 통해 'ScopeGroupID' 매개 변수를 사용 하 여 쿼리 합니다. 
  - 중복 된 entityID 관련 오류 조건을 처리


### <a name="azure-ad-style-resource-specification-in-scope-parameter"></a>범위 매개 변수에서 azure AD 스타일 리소스 사양 
이전에 AD FS는 범위에서 모든 인증 요청에 별도 매개 변수를 확인 하 고 원하는 리소스에 필요 합니다. 예를 들어, 일반적인 oauth 요청을 다음과 같이 표시 됩니다. 7 **https:&#47;&#47;fs.contoso.com/adfs/oauth2/authorize?</br> response_type 코드 client_id = = claimsxrayclient 리소스 = urn: microsoft:</br>adfs:claimsxray & 범위 oauth 및 redirect_uri = = https:&#47;&#47;adfshelp.microsoft.com/</br> ClaimsXray / TokenResponse & prompt = login**
 
서버 2019에 AD FS를 사용 하 여 이제 범위 매개 변수에 포함 된 리소스 값을 전달할 수 있습니다. 이 일치 하는 방법 또한 Azure AD에 대해 인증을 수행할 수 있습니다. 

범위 매개 변수에 있는 각 항목은 리소스/범위 구조를 공백으로 구분 된 목록으로 이제 구성할 수 있습니다. 예를 들면 다음과 같습니다.  

**< 잘못 샘플 요청 만들기 >**
> [!NOTE]
> 인증 요청에 리소스를 하나만 지정할 수 있습니다. 둘 이상의 리소스는 요청에 포함 하는 경우 AD FS는 오류 및 인증에 실패를 반환 합니다. 

### <a name="proof-key-for-code-exchange-pkce-support-for-oauth"></a>OAuth 용 코드 Exchange (PKCE) 지원에 대 한 증명 키 
OAuth 인증 코드 부여를 사용 하는 공용 클라이언트는 권한 부여 코드 가로채기 공격에 취약 합니다.  공격은 RFC 7636에 잘 설명 됩니다. 이 공격을 완화 하려면 AD FS 서버 2019에 지원 Proof Key 코드 Exchange (PKCE)에 대 한 OAuth 인증 코드 부여 흐름에 대 한 합니다. 
 
PKCE 지원을 활용 하려면이 사양은 OAuth 2.0 권한 부여 및 액세스 토큰 요청에 추가 매개 변수를 추가 합니다.

![Proofkey](media/whats-new-in-active-directory-federation-services-for-windows-server-2016/adfs2019.png)

1. 클라이언트 "code_verifier" 라는 비밀을 기록 및 파생 "t(code_verifier)" ("code_challenge" 라고도 함), 변환 방법 "t_m"와 함께 OAuth 2.0 권한 부여 요청에서 전송 되는 변환 된 버전을 만듭니다. 

2. 권한 부여 끝점 t(code_verifier)"레코드" 및 변환 메서드를 정상적으로 응답합니다. 

3. 클라이언트는 다음 일반적인 방식으로 액세스 토큰 요청에서 권한 부여 코드를 보냅니다 하지만 (A)에서 생성 된 "code_verifier" 암호를 포함 합니다. 

4. AD FS 변환 "code_verifier" 및 "t(code_verifier)" (B)에서 비교 합니다.  동일 하지 않은 경우 액세스가 거부 되었습니다. 

#### <a name="faq"></a>FAQ 
**Q.** Azure AD에 대해 요청은 완료 하는 방법 같은 범위 값의 일부로 리소스 값을 전달할 수 있나요? 
</br>**A.** 서버 2019에 AD FS를 사용 하 여 이제 범위 매개 변수에 포함 된 리소스 값을 전달할 수 있습니다. 범위 매개 변수에 있는 각 항목은 리소스/범위 구조를 공백으로 구분 된 목록으로 이제 구성할 수 있습니다. 예를 들면 다음과 같습니다.  
**< 잘못 샘플 요청 만들기 >**

**Q.** AD FS PKCE 확장을 지원 하나요?
</br>**A.** AD FS 서버 2019에는 지원 Proof Key 코드 Exchange (PKCE)에 대 한 OAuth 인증 코드 부여 흐름에 대 한 

## <a name="whats-new-in-active-directory-federation-services-for-windows-server-2016"></a>Windows Server 2016용 AD FS(Active Directory Federation Services)의 새로운 기능   
이전 버전의 AD FS에 대 한 정보를 찾고 다음 문서를 참조 합니다.  
 [Windows Server 2012 또는 2012 r 2에서 ADFS](https://technet.microsoft.com/library/hh831502.aspx) 및 [AD FS 2.0](https://technet.microsoft.com/library/adfs2.aspx)  

 Single sign-on 간에 다양 한 Office 365, 클라우드를 비롯 한 응용 프로그램을 기반으로 SaaS 응용 프로그램을 회사 네트워크에 있는 응용 프로그램 및 active Directory Federation Services 액세스 제어를 제공 합니다.  
* IT 조직에 대 한 수 있습니다 로그온 제공 액세스 제어 및 현대적이 고 레거시 응용 프로그램을 온-프레미스와 클라우드에서 자격 증명 및 정책의 같은 집합 기반으로 합니다.    
* 사용자를 동일 하 고 친숙 한 계정 자격 증명을 사용 하 여 원활 하 게 기호를 제공 합니다.  
* 개발자를 위한 응용 프로그램, 하지 인증 또는 identity에 노력을 집중할 수 있도록 id가 조직 디렉터리에 거주 하는 사용자를 인증 하는 간편한 방법을 제공 합니다.  

이 문서에서는 Windows Server 2016 (AD FS 2016)에서 AD FS의 새로운 기능을 설명 합니다.  

## <a name="eliminate-passwords-from-the-extranet"></a>엑스트라넷에서 암호 제거  
AD FS 2016 수 있도록 세 가지 새로운 옵션을 암호를 네트워크의 위험을 방지 하려면 조직의 없이 로그온 phished, 손실 또는 도난 방지 암호에서에서 손상 됩니다. 

### <a name="sign-in-with-azure-multi-factor-authentication"></a>Azure multi-factor Authentication을 사용 하 여 로그인
AD FS 2016 기반으로 다단계 인증 (MFA) 기능 Windows Server 2012 r 2에서 AD fs는 Azure MFA 코드를 사용 하 여 사용자 이름 및 암호를 먼저 입력 하지 않으면 로그온을 허용 하 여 합니다.

* 기본 인증 방법으로 Azure MFA를 사용 하 여 사용자가 자신의 사용자 이름 및 Azure Authenticator 앱에서 OTP 코드에 대 한 입력 합니다.  
* 보조 또는 추가 인증 방법으로 Azure MFA를 사용 하 여 OTP Azure MFA 로그인을 기반으로 기본 인증 (Windows 통합 인증, 사용자 이름 및 암호, 스마트 카드 또는 사용자 또는 장치 인증서 사용) 하는 자격 증명 한 다음 텍스트를 음성에 대 한 프롬프트를 표시 하거나 사용자가 제공 합니다.  
* 새 기본 제공 Azure MFA 어댑터와 함께 설치 및 구성 AD FS와 Azure MFA에 대 한 적이 더 간단 합니다.
* 조직에서는 Azure MFA는 온-프레미스 Azure MFA 서버에 대 한 필요 없이 활용을 걸릴 수 있습니다.
* 인트라넷 또는 엑스트라넷의 일부 또는 모든 액세스 제어 정책 azure MFA는 구성할 수 있습니다.

AD FS와 Azure MFA에 대 한 자세한 내용은
*  [AD FS 2016 및 Azure MFA 구성](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configure-ad-fs-and-azure-mfa)  

### <a name="password-less-access-from-compliant-devices"></a>호환 장치에서 암호 없이 액세스
에 로그인 할 수 있도록 하려면 이전 장치 등록 기능을 기반으로 하는 AD FS 2016 및 액세스 제어 장치 준수 상태를 기반으로 합니다. 사용자가 장치 자격 증명을 사용 하 여 로그온 할 수 있습니다 하 고 규정 준수는 재평가 장치 특성이 변경 될 때 정책이 적용 되는 항상 확인할 수 있도록 합니다.  와 같은 정책을 사용 하면이

* 관리 되는 및/또는 호환 되는 장치 에서만에서 액세스를 사용 하도록 설정  
* 엑스트라넷 액세스 관리 및/또는 호환 되는 장치 에서만에서 사용 하도록 설정  
* 관리 되는 준수 또는 미준수 있지 않은 컴퓨터에 대 한 다단계 인증을 요구 합니다.  

AD FS는 하이브리드 시나리오에서 조건부 액세스 정책의 온-프레미스 구성 요소를 제공합니다. 클라우드 리소스에 대 한 조건부 액세스에 대 한 Azure AD에 장치를 등록할 때 AD FS 정책도에 대 한 장치 id는 사용할 수 있습니다.

![새로운 기능](media/whats-new-in-active-directory-federation-services-for-windows-server-2016/ADFS_ITPRO4.png)  

 장치를 사용 하는 방법에 대 한 자세한 내용은 기반 클라우드에서 조건부 액세스   
 *  [Azure Active Directory 조건부 액세스](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access/)

장치를 사용 하는 방법에 대 한 자세한 내용은 AD FS 사용 하 여 조건부 액세스 기반
*  [AD FS 사용 하 여 조건부 액세스를 기반으로 장치에 대 한 계획](../../ad-fs/deployment/Plan-Device-based-Conditional-Access-on-Premises.md)  
* [AD FS에서 액세스 제어 정책](../../ad-fs/operations/Access-Control-Policies-in-AD-FS.md)  

### <a name="sign-in-with-windows-hello-for-business"></a>비즈니스용 Windows Hello 로그인   
Windows 10 장치는 Windows Hello 및 Windows Hello for Business에는 사용자 제스처 (PIN, 지문, 또는 안 면 인식 같은 생체 인식 제스처)으로 보호 하는 강력한 장치 바인딩된 사용자 자격 증명을 사용 하 여 사용자 암호를 대체를 소개 합니다. AD FS 2016 사용자가 인트라넷 또는 암호를 제공 하지 않아도 엑스트라넷에서 AD FS 응용 프로그램 로그인 할 수 있도록 이러한 새로운 Windows 10 기능을 지원 합니다.

Microsoft Windows Hello 비즈니스에 대 한 조직에서 사용 하는 방법에 대 한 자세한 내용은
*  [Windows Hello 비즈니스에 대 한 조직에서 사용](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-passport-deployment/)

## <a name="secure-access-to-applications"></a>응용 프로그램에 대 한 보안 액세스

### <a name="modern-authentication"></a>최신 인증
AD FS 2016 Windows 10으로 최신 iOS 및 Android 장치 및 응용 프로그램에 대 한 더 나은 사용자 환경을 제공 하는 최신 최신 프로토콜을 지원 합니다.  

자세한 내용은 참조 [개발자를 위한 AD FS 시나리오](../../ad-fs/overview/AD-FS-Scenarios-for-Developers.md)  


### <a name="configure-access-control-policies-without-having-to-know-claim-rules-language"></a>몰라도 액세스 제어 정책 구성 클레임 규칙 언어  
이전에 AD FS 관리자 구성 해야 했습니다 AD FS 클레임 규칙 언어를 사용 하 여 정책을 구성 하 고 정책을 유지 하기가 어렵습니다. 액세스 제어 정책을 사용 하 여 관리자가 템플릿을 사용 하 여 기본 제공 같은 일반적인 정책 적용
* 인트라넷 액세스에만 허용 합니다.
* 모든 사용자 허용 또는 엑스트라넷에서 MFA를 요구
* 모든 사용자 허용 및 특정 그룹에서 MFA를 요구

예외 또는 추가 정책 규칙을 추가 하려면 프로세스를 구동 하는 마법사를 사용 하 여 사용자 지정 하기 템플릿과 일치 정책 적용에 대 한 하나 이상의 응용 프로그램에 적용할 수 있습니다.

자세한 내용은 참조 [AD FS에서 액세스 제어 정책입니다.](../../ad-fs/operations/Access-Control-Policies-in-AD-FS.md)  

### <a name="enable-sign-on-with-non-ad-ldap-directories"></a>비 AD LDAP 디렉터리에 대해 로그온 사용  
많은 조직에는 Active Directory 및 타사 디렉터리의 조합입니다. LDAP v3 호환 디렉터리에 저장 된 사용자를 인증 하는 것에 대 한 AD FS 지원 추가 하 여 AD FS 이제 데 사용할 수 있습니다.
* 제 3 자, LDAP v3 호환 디렉터리의 사용자
* Active Directory 포리스트에 없는 Active Directory 양방향 트러스트 구성 되지 않은 사용자
* 사용자가 Active Directory Lightweight Directory Services (AD LDS)에서

자세한 내용은 참조 [LDAP 디렉터리에 저장 된 사용자를 인증 하도록 AD FS 구성 합니다.](../../ad-fs/operations/Configure-AD-FS-to-authenticate-users-stored-in-LDAP-directories.md)  

## <a name="better-sign-in-experience"></a>로그인 한 경험 향상
### <a name="customize-sign-in-experience-for-ad-fs-applications"></a>로그인 환경 AD FS 응용 프로그램에 대 한 사용자 지정  
이 많았습니다 사용자에 게 서 각 응용 프로그램에 대 한 로그온 환경을 사용자 지정 하는 기능에 여러 개의 서로 다른 회사 또는 브랜드를 나타내는 응용 프로그램에 대 한 기호를 제공 하는 조직에 특히 유용한 유용성 개선, 것입니다.  

이전에 Windows Server 2012 r 2에서 AD FS 모든 신뢰 당사자 응용 프로그램에 대 한 경험에 공용 기호를 제공, 텍스트의 하위 집합을 사용자 지정할 수 있는 응용 프로그램별 콘텐츠를 기반으로 합니다. Windows Server 2016 뿐만 아니라 메시지를 하지만 이미지, 응용 프로그램별 로고 및 웹 테마를 지정할 수 있습니다. 또한 새로 만들고, 사용자 지정 웹 테마 하 고 적용 당 신뢰 당사자입니다.  

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
Active Directory Federation Services (AD FS) 암호 만료 클레임을 보내도록 AD FS로 보호 되는 신뢰 당사자 트러스트 (응용 프로그램)를 구성할 수 있습니다. 이러한 클레임을 사용 하는 방법을 응용 프로그램에 따라 달라 집니다. 예를 들어, 신뢰 당사자로 Office 365를 통해 업데이트 하도록 구현 Exchange 및 Outlook 곧에-수-만료 된 암호의 페더레이션된 사용자에 게 알려야 합니다.  

자세한 내용은 참조 [암호 만료 클레임을 보내도록 AD FS 구성 합니다.](../../ad-fs/operations/Configure-AD-FS-to-Send-Password-Expiry-Claims.md)  

### <a name="moving-from-ad-fs-in-windows-server-2012-r2-to-ad-fs-in-windows-server-2016-is-easier"></a>Windows Server 2012 r 2에서 AD FS에서 Windows Server 2016에서 AD FS로 이동 하는 것이 더 쉽습니다.  
기존 팜에서 구성 내보내기 및 새로운, 병렬 팜에 가져오기 이전에 필요한 새 버전의 AD FS로 마이그레이션.  

이제 Windows Server 2016에서 AD FS를 Windows Server 2012 r 2에서 AD FS에서 이동 훨씬 쉽게 되었습니다. Windows Server 2012 R2 팜에 새 Windows Server 2016 서버를 추가 하면 팜의 매기고 Windows Server 2012 R2 팜 동작 수준에서 찾아서는 Windows Server 2012 R2 팜의 같은 방식으로 작동 하므로 합니다.  

그런 다음 새 Windows Server 2016 서버를 팜에 추가, 기능을 확인 하 고 부하 분산 장치에서 이전 서버를 제거 합니다. 모든 팜 노드에서 Windows Server 2016를 실행 하는 경우 팜 동작 수준 2016를 업그레이드 하 고 새로운 기능을 사용 하 여 시작 준비가 됩니다.  

자세한 내용은 참조 [AD FS에서 Windows Server 2016으로 업그레이드 합니다.](../../ad-fs/deployment/Upgrading-to-AD-FS-in-Windows-Server-2016.md)  
