---
ms.assetid: 8e7015bc-c489-4ec7-8b6e-3ece90f72317
title: "인증 정책을 구성합니다"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 7faffb7ccbb4b0ea3c65329d18f915d7dafcd46f
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="configure-authentication-policies"></a>인증 정책을 구성합니다

>Windows Server 2012 r 2에 적용 됩니다.

Windows Server 2012 r 2에 adfs에서 모두 액세스 제어 및 사용자, 디바이스, 위치 및 인증 데이터를 포함 하는 다중 요소 인증 메커니즘 개선 됩니다. 이러한 향상 된이 기능을 사용 하 여 사용자 인터페이스를 통해 또는 위험 multi\ 팩터 액세스 제어 하 고 사용자의 신원을 또는 그룹 구성원, 네트워크 위치, 디바이스 데이터 workplace\ 참가 기반으로 하는 multi\ 단계 인증을 통해 광고 FS\ 보안 응용 프로그램에 대 한 액세스 권한을 관리를 Windows PowerShell 및 multi\ 단계 인증은 \(MFA\) 되었을 때 인증 상태를 통해 수행 됩니다.  
  
MFA 및 multi\ 팩터 액세스 제어 Active Directory Federation Services \(AD FS\) Windows Server 2012 r 2에서에 대 한 자세한 내용은 다음 항목을 참조 하십시오.  


-   [SSO 및 원활 하 게 초에 대 한 모든 디바이스에서 회사에 가입 인증 회사 응용 프로그램에서 요인](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)

-   [관련 된 위험 조건부 액세스 제어도 관리](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md)

-   [추가 다단계 인증 민감한 응용 프로그램에 대 한 위험을 관리](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)

## <a name="configure-authentication-policies-via-the-ad-fs-management-snap-in"></a>인증 정책을 snap\에서 AD FS 관리를 통해 구성  
회원 **관리자**, 로컬 컴퓨터에서 해당 하는이 절차를 수행 하는 최소 요구 사항을 또는 합니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
ADFS Windows Server 2012 r 2에에서는 모든 응용 프로그램 및 Adfs로 보호 된 서비스에 해당 하는 세계적인 범위에 인증 정책을 지정할 수 있습니다. 특정 응용 프로그램과 Adfs에서 보안 및 파티 신뢰 사용 하는 서비스에 대 한 정책을 인증 설정할 수 있습니다. 의존 당 특정 응용 프로그램에 대 한 인증 정책 지정 파티 신뢰 글로벌 인증 정책 재정의 하지 않습니다. 글로벌 또는 의존 당 경우이 신뢰 파티 보안 인증을 열려고 할 때 인증 정책에 따라 MFA MFA 파티 신뢰 트리거됩니다. 글로벌 인증 정책을 응용 프로그램 및 서비스는 특정 구성 된 인증 정책이 없는 대해 당사자 신뢰 신뢰를 대체 합니다. 

## <a name="to-configure-primary-authentication-globally-in-windows-server-2012-r2"></a>Windows Server 2012 r 2에서 주 인증 전체적으로 구성 하려면 
  
1.  서버 관리자 클릭 **도구**를 선택한 다음 **AD FS 관리**합니다.  
  
2.  Adfs의 snap\ 클릭 **인증 정책**합니다.  
  
3.  에 **주 인증** 섹션에서 클릭 **편집** 옆에 **전역 설정**합니다. Right\ 클릭 수도 **인증 정책**, 선택한 **전 세계 주요 인증 편집**, 또는 **작업** 창, **전 세계 주요 인증 편집**합니다.  
![auth 정책](media/Configure-Authentication-Policies/authpolicy1.png)
  
4.  **글로벌 인증 정책 편집** 창에 있는 **기본** 탭을 글로벌 인증 정책의 일부로 다음 설정을 구성할 수 있습니다:  
  
    -   주 인증에 사용 되는 인증 방법을 합니다. 사용할 수 있는 인증 방법을 선택할 수 있는 **익스트라넷을** 및 **인트라넷**합니다.  
  
    -   디바이스 인증을 통해는 **활성화 장치 인증** 확인란을 선택 합니다. 자세한 내용은 참조 [SSO 및 원활 하 게 두 번째 요소 인증 간에 회사 응용 프로그램에 모든 디바이스에서 회사에 가입](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)합니다.  
![auth 정책](media/Configure-Authentication-Policies/authpolicy2.png)  

## <a name="to-configure-primary-authentication-per-relying-party-trust"></a>주 인증 의존 당 구성 파티 보안  
  
1.  서버 관리자 클릭 **도구**를 선택한 다음 **AD FS 관리**합니다.  
  
2.  Adfs의 snap\ 클릭 **인증 정책**\\**의존 파티 신뢰 별로**, 클릭 한 다음 인증 정책을 구성 하려면 신뢰 파티 신뢰 하 고 합니다.  
  
3.  두 right\ 클릭 당사자 신뢰 인증 정책, 구성 선택한 다음 원하는 **사용자 지정 주 인증 편집**, 또는 **작업** 창, **사용자 지정 주 인증 편집**합니다.  
![auth 정책](media/Configure-Authentication-Policies/authpolicy5.png)   

4.  **< relying\_party\_trust\_name > 인증 정책 편집** 창에서는 **기본** 탭에서 다음 설정을의 일환으로 구성할 수 있습니다는 **당 의존 파티 신뢰** 인증 정책:  
  
    -   사용자는 시에 sign\ 때마다 자격 증명을 제공 하는 데 필요한 여부를 통해는 **사용자가 시 sign\에 때마다 자격 증명을 제공 하는 데 필요한** 확인란을 선택 합니다.  
![auth 정책](media/Configure-Authentication-Policies/authpolicy6.png) 

## <a name="to-configure-multi-factor-authentication-globally"></a>전체적으로 다단계 인증 구성 하려면  
  
1.  서버 관리자 클릭 **도구**를 선택한 다음 **AD FS 관리**합니다.  
  
2.  Adfs의 snap\ 클릭 **인증 정책**합니다.  
  
3.  에 **Multi\ 요소 인증** 섹션에서 클릭 **편집** 옆에 **전역 설정**합니다. Right\ 클릭 수도 **인증 정책**, 선택한 **글로벌 편집 Multi\ 단계 인증**, 또는 **작업** 창을 선택 하 고 **글로벌 편집 Multi\ 단계 인증**합니다.  
![auth 정책](media/Configure-Authentication-Policies/authpolicy8.png)   

4.  에 **글로벌 인증 정책 편집** 창에서는 **Multi\ 인수** 탭을 글로벌 multi\ 팩터 인증 정책의 일부로 다음 설정을 구성할 수 있습니다:  
  
    -   설정이 나에서 사용할 수 있는 옵션을 통해 MFA 조건은 **Users\/그룹**, **디바이스**, 및 **위치** 섹션.  
  
    -   이러한 설정에 대 한 MFA을 사용 하려면 하나 이상의 추가 인증 방법을 선택 해야 합니다. **인증 인증서** 기본 사용할 수 있는 옵션이 있습니다. 다른 사용자 지정 추가 인증 방법, 예를 들어 Windows Azure Active 인증 구성할 수 있습니다. 자세한 내용은 참조 [연습 가이드: 민감한 응용 프로그램에 대 한 추가 다단계 인증 관리 위험](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)합니다.  
  
> [!WARNING]  
> 전체적으로 추가 인증 방법을 구성할 수 있습니다.  
![auth 정책](media/Configure-Authentication-Policies/authpolicy9.png)  

## <a name="to-configure-multi-factor-authentication-per-relying-party-trust"></a>의존 별로 multi\ 단계 인증을 구성 하 파티 보안  
  
1.  서버 관리자 클릭 **도구**를 선택한 다음 **AD FS 관리**합니다.  
  
2.  Adfs의 snap\ 클릭 **인증 정책**\\**의존 파티 신뢰 별로**, 클릭 한 다음 MFA 구성 하려면 신뢰 파티 신뢰 하 고 합니다.  
  
3.  두 right\ 클릭 당사자 신뢰 구성 MFA를 선택한 다음 원하는 **사용자 지정 편집 Multi\ 요소 인증**, 또는 **작업** 창을 선택 하 고 **사용자 지정 편집 Multi\ 요소 인증**합니다.  
  
4.  에 **< relying\_party\_trust\_name > 인증 정책 편집** 창는 **Multi\ 인수** 탭에서 다음 설정의 일환으로 구성할 수 있습니다 per\ 신뢰 당사자 신뢰할 인증 정책:  
  
    -   설정이 나에서 사용할 수 있는 옵션을 통해 MFA 조건은 **Users\/그룹**, **디바이스**, 및 **위치** 섹션.  

## <a name="configure-authentication-policies-via-windows-powershell"></a>Windows PowerShell 통해 인증 정책을 구성합니다  
가능 보다 유연 하 게 액세스 제어 다양 한 요인을 사용 하 여 Windows PowerShell 및 인증 정책과 인증 구성 하려면 Windows Server 2012 r 2에 Adfs에서 사용할 수 있는 인증 메커니즘 하는 조건 ADFS \-secured 리소스에 대 한 액세스를 구현 하는 데 필요한 규칙 합니다.  
  
관리자 또는 로컬 컴퓨터에서 오른쪽 단추를의 회원이이 절차를 수행 하는 최소 요구 사항을입니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477) \ (http:///\/ go.microsoft.com\/fwlink\/있나요? LinkId\ 83477\ =).   
  
### <a name="to-configure-an-additional-authentication-method-via-windows-powershell"></a>추가 인증 방법을 통해 Windows PowerShell 구성 하려면  
  
1.  해당 federation 서버를 Windows PowerShell 명령 창 열고 다음 명령을 실행 합니다.  
  

    `Set-AdfsGlobalAuthenticationPolicy –AdditionalAuthenticationProvider CertificateAuthentication  `

  
> [!WARNING]  
> 이 명령을 성공적으로 실행을 실행할 수를 확인 하 고 `Get-AdfsGlobalAuthenticationPolicy` 명령을 합니다.  
  
### <a name="to-configure-mfa-per-relying-party-trust-that-is-based-on-a-users-group-membership-data"></a>MFA per\ 의존 구성 하려면 사용자의 그룹 구성원 데이터를 기반으로 하는 타사 신뢰  
  
1.  해당 federation 서버를 Windows PowerShell 명령 창 열고 다음 명령을 실행 합니다.  
  

    `$rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust`  
  
  
> [!WARNING]  
> 교체할 수 있도록 *< relying\_party\_trust >* 여러분의 신뢰 파티 신뢰의 이름으로 합니다.  
  
2.  동일한 Windows PowerShell 명령 창에서 다음 명령을 실행 합니다.  
  
 
    $MfaClaimRule = "c: \ [유형 = = '" https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid'", 값 = ~ '" < group_SID > ^(?i) $' "] = > 문제 (유형 = '" https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod'", 값 '" https://schemas.microsoft.com/claims/multipleauthn'");" 
    
    Set-adfsrelyingpartytrust – TargetRelyingParty $rp – AdditionalAuthenticationRules $MfaClaimRule
  
  
> [!NOTE]  
> 보안 식별자 값으로 < group\_SID > 바꿀 수 있도록 Active Directory \(AD\) 그룹의 \(SID\) 합니다.  
  
### <a name="to-configure-mfa-globally-based-on-users-group-membership-data"></a>전 세계 사용자 그룹 구성원 데이터에 따라 MFA 구성 하려면  
  
1.  해당 federation 서버를 Windows PowerShell 명령 창 열고 다음 명령을 실행 합니다.  
  

    $MfaClaimRule = "c: \ [유형 = = '" https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid'", 가치 = = '" group_SID'"]  
     = > 문제 (유형 = ' "https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod'", 가치 = ' "https://schemas.microsoft.com/claims/multipleauthn'"); "  
      
    설정 AdfsAdditionalAuthenticationRule $MfaClaimRule  

  
> [!NOTE]  
> 교체할 수 있도록 *< group\_SID >* 광고 그룹 SID 값으로 합니다.  
  
### <a name="to-configure-mfa-globally-based-on-users-location"></a>전 세계 사용자의 위치에 따라 MFA 구성 하려면  
  
1.  해당 federation 서버를 Windows PowerShell 명령 창 열고 다음 명령을 실행 합니다.  
  
 
    $MfaClaimRule = "c: \ [유형 = = '" https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork'", 가치 = = '" true_or_false'"]  
     = > 문제 (유형 = ' "https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod'", 가치 = ' "https://schemas.microsoft.com/claims/multipleauthn'"); "  
  
    설정 AdfsAdditionalAuthenticationRule $MfaClaimRule  
  

  
> [!NOTE]  
> 교체할 수 있도록 *< true\_or\_false >* 하나로 `true` 또는 `false`합니다. 값은 액세스 요청 엑스트라넷 또는 인트라넷에서 제공 하는지 여부에 따라 특정 규칙 조건에 따라 달라 집니다.  
  
### <a name="to-configure-mfa-globally-based-on-users-device-data"></a>전 세계 사용자의 디바이스 데이터를 기반 MFA 구성 하려면  
  
1.  해당 federation 서버를 Windows PowerShell 명령 창 열고 다음 명령을 실행 합니다.  
  

    $MfaClaimRule = "c: \ [유형 = = '" https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser'", 가치 = ="true_or_false"]  
     = > 문제 (유형 = ' "https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod'", 가치 = ' "https://schemas.microsoft.com/claims/multipleauthn'"); "  
  
    설정 AdfsAdditionalAuthenticationRule $MfaClaimRule  

  
> [!NOTE]  
> 교체할 수 있도록 *< true\_or\_false >* 하나로 `true` 또는 `false`합니다. 값은 디바이스 인지 여부 workplace\ 가입 기반으로 하 여 특정 규칙 조건에 따라 달라 집니다.  
  
### <a name="to-configure-mfa-globally-if-the-access-request-comes-from-the-extranet-and-from-a-non-workplace-joined-device"></a>액세스 요청 엑스트라넷 및 non\ workplace\ 가입 장치에서 제공 하는 경우 MFA 전체적으로 구성 하려면  
  
1.  해당 federation 서버를 Windows PowerShell 명령 창 열고 다음 명령을 실행 합니다.  
  
 
    `Set-AdfsAdditionalAuthenticationRule "c:[Type == '"https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser'", Value == '"true_or_false'"] && c2:[Type == '"https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork'", Value == '" true_or_false '"] => issue(Type = '"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod'", Value ='"https://schemas.microsoft.com/claims/multipleauthn'");" ` 
 
  
> [!NOTE]  
> 모두 확인 *< true\_or\_false >* 하나로 `true` 또는 `false`, 특정 규칙 조건에 따라 달라 지 며 합니다. 규칙 조건은 장치 인지 여부 workplace\ 가입 액세스 요청 엑스트라넷에서 제공 하는지 여부에 따라 달라 또는 인트라넷 합니다.  
  
### <a name="to-configure-mfa-globally-if-access-comes-from-an-extranet-user-that-belongs-to-a-certain-group"></a>특정 그룹에 속하는 익스트라넷 사용자의 액세스를 제공 하는 경우 MFA 전체적으로 구성 하려면  
  
1.  해당 federation 서버를 Windows PowerShell 명령 창 열고 다음 명령을 실행 합니다.  
  

    Set-AdfsAdditionalAuthenticationRule "c: \ [유형 = = `"https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid`", 값 = = `"group_SID`"] & & c 2: [유형 = = `"https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork`", 값 = = `"true_or_false`"] = > 문제 (유형 = `"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod`", 값 ='"https://schemas.microsoft.com/claims/
      
> [!NOTE]  
> 교체할 수 있도록 *< group\_SID >* SID 그룹의 및 *< true\_or\_false >* 사용 하 여 `true` 또는 `false`, 액세스 요청 엑스트라넷에서 제공 하는지 여부에 따라 사용자 규칙 특정 조건에 따라 달라 지 며 또는 인트라넷 합니다.  
  
### <a name="to-grant-access-to-an-application-based-on-user-data-via-windows-powershell"></a>사용자 데이터를 통해 Windows PowerShell 기반 응용 프로그램에 대 한 액세스 권한을 부여 하려면  
  
1.  해당 federation 서버를 Windows PowerShell 명령 창 열고 다음 명령을 실행 합니다.  
  
    ```  
    $rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust  
  
    ```  
  
> [!NOTE]  
> 교체할 수 있도록 *< relying\_party\_trust >* 여러분의 신뢰 파티 신뢰 값으로 합니다.  
  
2.  동일한 Windows PowerShell 명령 창에서 다음 명령을 실행 합니다.  
  
    ```  
  
      $GroupAuthzRule = "@RuleTemplate = `“Authorization`” @RuleName = `"Foo`" c:[Type == `"https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid`", Value =~ `"^(?i)<group_SID>$`"] =>issue(Type = `"https://schemas.microsoft.com/authorization/claims/deny`", Value = `"DenyUsersWithClaim`");"  
    Set-AdfsRelyingPartyTrust –TargetRelyingParty $rp –IssuanceAuthorizationRules $GroupAuthzRule  
    ```  
  
> [!NOTE]  
> > 교체할 수 있도록 *< group\_SID >* 광고 그룹 SID 값으로 합니다.  
  
### <a name="to-grant-access-to-an-application-that-is-secured-by-ad-fs-only-if-this-users-identity-was-validated-with-mfa"></a>이 사용자의이 id 경우에만 Adfs로 보호 된 응용 프로그램에 대 한 액세스 권한을 부여 하려면 된 검증 된 MFA  
  
1.  해당 federation 서버를 Windows PowerShell 명령 창 열고 다음 명령을 실행 합니다.  
  

    `$rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust ` 
 
  
> [!NOTE]  
> 교체할 수 있도록 *< relying\_party\_trust >* 여러분의 신뢰 파티 신뢰 값으로 합니다.  
  
2.  동일한 Windows PowerShell 명령 창에서 다음 명령을 실행 합니다.  
  
    ```  
    $GroupAuthzRule = "@RuleTemplate = `"Authorization`"  
    @RuleName = `"PermitAccessWithMFA`"  
    c:[Type == `"https://schemas.microsoft.com/claims/authnmethodsreferences`", Value =~ `"^(?i)https://schemas\.microsoft\.com/claims/multipleauthn$`"] => issue(Type = `"https://schemas.microsoft.com/authorization/claims/permit`", Value = ‘“PermitUsersWithClaim’");"  
  
    ```  
  
### <a name="to-grant-access-to-an-application-that-is-secured-by-ad-fs-only-if-the-access-request-comes-from-a-workplace-joined-device-that-is-registered-to-the-user"></a>사용자 액세스 요청 workplace\ 가입 등록 된 디바이스에서 제공 하는 경우 Adfs만으로 보호 된 응용 프로그램에 대 한 액세스 권한을 부여 하려면  
  
1.  해당 federation 서버를 Windows PowerShell 명령 창 열고 다음 명령을 실행 합니다.  
  
    ```  
    $rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust  
  
    ```  
  
> [!NOTE]  
> 교체할 수 있도록 *< relying\_party\_trust >* 여러분의 신뢰 파티 신뢰 값으로 합니다.  
  
2.  동일한 Windows PowerShell 명령 창에서 다음 명령을 실행 합니다.  
  

    $GroupAuthzRule = "@RuleTemplate = `"Authorization`"  
    @RuleName = `"PermitAccessFromRegisteredWorkplaceJoinedDevice`"  
    c: \ [유형 = = `"https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser`", 값 = ~ `"^(?i)true$`"] = > 문제 (유형 = `"https://schemas.microsoft.com/authorization/claims/permit`", 가치 = `"PermitUsersWithClaim`").  
  

  
### <a name="to-grant-access-to-an-application-that-is-secured-by-ad-fs-only-if-the-access-request-comes-from-a-workplace-joined-device-that-is-registered-to-a-user-whose-identity-has-been-validated-with-mfa"></a>액세스 요청 MFA와 id를 검증 된 사용자에 게 workplace\ 가입 등록 된 디바이스에서 제공 하는 경우 Adfs만으로 보호 된 응용 프로그램에 대 한 액세스 권한을 부여 하려면  
  
1.  해당 federation 서버를 Windows PowerShell 명령 창 열고 다음 명령을 실행 합니다.  
  
 
    `$rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust ` 
 
  
> [!NOTE]  
> 교체할 수 있도록 *< relying\_party\_trust >* 여러분의 신뢰 파티 신뢰 값으로 합니다.  
  
2.  동일한 Windows PowerShell 명령 창에서 다음 명령을 실행 합니다.  
  
    ```  
    $GroupAuthzRule = ‘@RuleTemplate = “Authorization”  
    @RuleName = “RequireMFAOnRegisteredWorkplaceJoinedDevice”  
    c1:[Type == `"https://schemas.microsoft.com/claims/authnmethodsreferences`", Value =~ `"^(?i)http://schemas\.microsoft\.com/claims/multipleauthn$`"] &&  
    c2:[Type == `"https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser`", Value =~ `"^(?i)true$”] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit`", Value = `"PermitUsersWithClaim`");"  
  
    ```  
  
### <a name="to-grant-extranet-access-to-an-application-secured-by-ad-fs-only-if-the-access-request-comes-from-a-user-whose-identity-has-been-validated-with-mfa"></a>엑스트라넷 ADFS 액세스 요청 MFA와 id를 검증 된에서는 사용자에 게 제공 하는 경우에 보안 응용 프로그램에 권한을 부여 하려면  
  
1.  해당 federation 서버를 Windows PowerShell 명령 창 열고 다음 명령을 실행 합니다.  
  
 
    `$rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust`  

  
> [!NOTE]  
> 교체할 수 있도록 *< relying\_party\_trust >* 여러분의 신뢰 파티 신뢰 값으로 합니다.  
  
2.  동일한 Windows PowerShell 명령 창에서 다음 명령을 실행 합니다.  
  

    $GroupAuthzRule = "@RuleTemplate = `"Authorization`"  
    @RuleName = `"RequireMFAForExtranetAccess`"  
    c 1: [유형 = = `"https://schemas.microsoft.com/claims/authnmethodsreferences`", 가치 = ~ `"^(?i)http://schemas\.microsoft\.com/claims/multipleauthn$`"] & &  
    c 2: [유형 = = `"https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork`", 가치 = ~ `"^(?i)false$`"] = > 문제 (유형 = `"https://schemas.microsoft.com/authorization/claims/permit`", 가치 = `"PermitUsersWithClaim`"); "  

## <a name="additional-references"></a>추가 참조  

[AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md)
