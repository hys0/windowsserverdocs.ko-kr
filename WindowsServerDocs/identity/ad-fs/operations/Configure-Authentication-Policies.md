---
ms.assetid: 8e7015bc-c489-4ec7-8b6e-3ece90f72317
title: 인증 정책 구성
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 2215f172128a533e0e0d4e10b72be53ad455a262
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444966"
---
# <a name="configure-authentication-policies"></a>인증 정책 구성

Windows Server 2012 r 2에서 AD FS에 모두 액세스 제어 및 사용자, 장치, 위치 및 인증 데이터를 포함 하는 다중 요소 인증 메커니즘 개선 됩니다. 사용자 인터페이스를 통해 또는 AD FS에 대 한 액세스 권한 부여의 위험을 관리 하려면 Windows PowerShell을 통해 이러한 향상 된 기능,\-다중을 통해 응용 프로그램 보안\-액세스 제어 및 다중 팩터링\-사용자 id 또는 그룹 멤버 자격, 네트워크 위치, 작업 공간에 연결 하는 장치 데이터를 기반으로 하는 요소 인증\-조인 인증 상태 및 다중\-요소 인증 \(MFA\) 수행 되었습니다.  

MFA 및 다중 하는 방법에 대 한 자세한 내용은\-Active Directory Federation Services에서 액세스 제어를 팩터링 \(AD FS\) Windows Server 2012 r 2에서는 다음 항목을 참조 합니다.  


-   [SSO 및 원활한 두 번째 위한 모든 장치의 작업 공간 연결 단계 회사 응용 프로그램에서 인증](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)

-   [조건부 액세스 제어를 사용하여 위험 관리](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md)

-   [추가 Multi-factor Authentication for Sensitive Applications 사용 하 여 위험 관리](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)

## <a name="configure-authentication-policies-via-the-ad-fs-management-snap-in"></a>AD FS 관리 스냅인을 통해 인증 정책을 구성\-에서  
로컬 컴퓨터에서 이러한 절차를 완료하기 위해서는 최소한 **관리자** 또는 이와 동등한 자격이 있어야 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   

Windows Server 2012 r 2에서 AD FS에서 모든 응용 프로그램 및 AD FS에서 보안이 유지 되는 서비스에 적용 되는 전역 범위의 인증 정책을 지정할 수 있습니다. 또한 특정 응용 프로그램 및 당사자 트러스트에 의존 하며 AD FS를 통해 보호 되는 서비스에 대 한 인증 정책을 설정할 수 있습니다. 신뢰 당 특정 응용 프로그램에 대 한 인증 정책을 지정 당사자 트러스트 전역 인증 정책을 재정의 하지 않습니다. 전역 또는 신뢰 당 경우 당사자 트러스트 인증 정책에서 MFA를 MFA 요구는 사용자가이 신뢰 당사자 트러스트에 인증 하려고 하는 경우 트리거됩니다. 전역 인증 정책은 응용 프로그램 및 특정 구성 된 인증 정책을 포함 하지 않는 서비스에 대 한 신뢰 당사자 트러스트에 대 한 대체 (fallback)입니다. 

## <a name="to-configure-primary-authentication-globally-in-windows-server-2012-r2"></a>Windows Server 2012 r 2에서 기본 인증을 전역적으로 구성 하려면 

1.  서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  

2.  AD FS에서 스냅\-클릭 **인증 정책**합니다.  

3.  에 **기본 인증** 섹션에서 클릭 **편집** 옆에 **전역 설정**합니다. 마우스 오른쪽 단추로 수\-클릭 **인증 정책**, 선택한 **전역 기본 인증 편집**, 또는 **작업** 창에서 **전역 기본 인증 편집**합니다.  
![인증 정책](media/Configure-Authentication-Policies/authpolicy1.png)

4.  에 **전역 인증 정책 편집** 창에는 **기본** 탭을 전역 인증 정책의 일부로 다음 설정을 구성할 수 있습니다.  

    -   기본 인증에 사용할 인증 방법입니다. 아래에서 사용할 수 있는 인증 방법을 선택할 수는 **익스트라넷** 및 **인트라넷**합니다.  

    -   장치 인증을 통해는 **장치 인증 사용** 확인란입니다. 자세한 내용은 [Join to Workplace from Any Device for SSO and Seamless Second Factor Authentication Across Company Applications](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)를 참조하세요.  
![인증 정책](media/Configure-Authentication-Policies/authpolicy2.png)  

## <a name="to-configure-primary-authentication-per-relying-party-trust"></a>신뢰 당 기본 인증을 구성 하려면 신뢰 당사자  

1.  서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  

2.  AD FS에서 스냅\-에서 클릭 **인증 정책**\\**신뢰 당사자 트러스트 당**, 인증 정책을 구성 하려면 신뢰 당사자 트러스트를 클릭 하 고 있습니다.  

3.  오른쪽\-인증 정책을 구성 하 고 다음을 선택 하려면 원하는 신뢰 당사자 트러스트를 클릭 합니다. **사용자 지정 기본 인증 편집**, 또는 **작업** 창 **사용자 지정 기본 인증 편집**합니다.  
![인증 정책](media/Configure-Authentication-Policies/authpolicy5.png)   

4.  에 **에 대 한 인증 정책 편집 < 신뢰\_파티\_신뢰\_이름 >** 창 아래에서 **기본** 탭의 일부로 다음 설정을 구성할 수는 **신뢰 당사자 트러스트 당** 인증 정책:  

    -   사용자는 at 기호 때마다 자격 증명을 제공 해야 하는지 여부\-에서 통해는 **사용자는 at 기호 때마다 자격 증명을 제공 해야\-에서** 확인란입니다.  
![인증 정책](media/Configure-Authentication-Policies/authpolicy6.png) 

## <a name="to-configure-multi-factor-authentication-globally"></a>다단계 인증을 전역적으로 구성 하려면  

1.  서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  

2.  AD FS에서 스냅\-클릭 **인증 정책**합니다.  

3.  에 **다중\-단계 인증** 섹션에서 클릭 **편집** 옆에 **전역 설정**합니다. 마우스 오른쪽 단추로 수\-클릭 **인증 정책**, 선택한 **글로벌 다중 편집\-단계 인증**, 또는 **작업** 창에서 **글로벌 다중 편집\-단계 인증**.  
![인증 정책](media/Configure-Authentication-Policies/authpolicy8.png)   

4.  에 **전역 인증 정책 편집** 창 아래에서 **다중\-비율** 탭 글로벌 다중의 일부로 다음 설정을 구성할 수 있습니다\-팩터링 인증 정책:  

    -   설정 또는 MFA에 대 한 조건에서 사용할 수 있는 옵션을 통해는 **사용자\/그룹**, **장치**, 및 **위치** 섹션입니다.  

    -   이러한 설정에 대 한 MFA를 사용 하려면 하나 이상의 추가 인증 방법을 선택 해야 합니다. **인증서 인증** 사용할 수 있는 기본 옵션입니다. 또한 다른 사용자 지정 추가 인증 방법, 예를 들어 Windows Azure 활성 인증을 구성할 수 있습니다. 자세한 내용은 참조 하세요. [연습 가이드: 추가 Multi-factor Authentication for Sensitive Applications 사용 하 여 위험 관리](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)합니다.  

> [!WARNING]  
> 전역적으로 추가 인증 방법만 구성할 수 있습니다.  
![인증 정책](media/Configure-Authentication-Policies/authpolicy9.png)  

## <a name="to-configure-multi-factor-authentication-per-relying-party-trust"></a>다중 구성 하려면\-인증 당 신뢰 당사자 트러스트  

1.  서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  

2.  AD FS에서 스냅\-에서 클릭 **인증 정책**\\**신뢰 당사자 트러스트 당**, MFA를 구성 하려면 신뢰 당사자 트러스트를 클릭 하 고 있습니다.  

3.  오른쪽\-MFA를 구성 하 고 선택 후 원하는 신뢰 당사자 트러스트를 클릭 합니다. **사용자 지정 다중 편집\-단계 인증**, 또는 **작업** 창 **사용자 지정 다중 편집\-단계 인증**합니다.  

4.  에 **에 대 한 인증 정책 편집 < 신뢰\_파티\_신뢰\_이름 >** 창 아래에서 **다중\-비율** 탭의 일부로 다음 설정을 구성할 수는 당\-신뢰 당사자 트러스트 인증 정책:  

    -   설정 또는 MFA에 대 한 조건에서 사용할 수 있는 옵션을 통해는 **사용자\/그룹**, **장치**, 및 **위치** 섹션입니다.  

## <a name="configure-authentication-policies-via-windows-powershell"></a>Windows PowerShell을 통해 인증 정책 구성  
Windows PowerShell을 사용 하는 액세스 제어의 다양 한 요소를 사용 하 여 유연성 및 인증 정책 및 권한 부여를 구성 하려면 Windows Server 2012 r 2에서 AD FS에서 사용할 수 있는 인증 메커니즘 하는 AD FS에 대 한 조건부 액세스를 구현 하는 데 필요한 규칙 \-보안 리소스입니다.  

관리자 또는 로컬 컴퓨터에서 해당 그룹의 멤버 자격이 이러한 절차를 완료 하기 위해서는 최소한 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/go.microsoft.com\/fwlink\/? LinkId\=83477\)합니다.   

### <a name="to-configure-an-additional-authentication-method-via-windows-powershell"></a>Windows PowerShell을 통해 추가 인증 방법을 구성 하려면  

1.  페더레이션 서버에서 Windows PowerShell 명령 창을 열고 다음 명령을 실행 합니다.  


~~~
`Set-AdfsGlobalAuthenticationPolicy –AdditionalAuthenticationProvider CertificateAuthentication  `
~~~


> [!WARNING]  
> 이 명령이 성공적으로 실행을 실행할 수를 확인 하는 `Get-AdfsGlobalAuthenticationPolicy` 명령입니다.  

### <a name="to-configure-mfa-per-relying-party-trust-that-is-based-on-a-users-group-membership-data"></a>당 MFA를 구성 하려면\-사용자의 그룹 구성원 자격 데이터를 기반으로 하는 신뢰 당사자 트러스트  

1.  페더레이션 서버에서 Windows PowerShell 명령 창을 열고 다음 명령을 실행합니다.  


~~~
`$rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust`  
~~~


> [!WARNING]  
> 교체 해야 *< 신뢰\_파티\_신뢰 >* 신뢰 당사자 트러스트의 이름입니다.  

2. 동일한 Windows PowerShell 명령 창에서 다음 명령을 실행 합니다.  


~~~
$MfaClaimRule = “c:[Type == ‘“https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid’”, Value =~ ‘“^(?i) <group_SID>$’”] => issue(Type = ‘“https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod’”, Value ‘“https://schemas.microsoft.com/claims/multipleauthn’”);” 

Set-AdfsRelyingPartyTrust –TargetRelyingParty $rp –AdditionalAuthenticationRules $MfaClaimRule
~~~


> [!NOTE]  
> 교체 해야 < 그룹\_SID > 보안 식별자의 값을 가진 \(SID\) Active Directory의 \(AD\) 그룹입니다.  

### <a name="to-configure-mfa-globally-based-on-users-group-membership-data"></a>전체적으로 사용자의 그룹 구성원 자격 데이터를 기반으로 MFA를 구성 하려면  

1.  페더레이션 서버에서 Windows PowerShell 명령 창을 열고 다음 명령을 실행 합니다.  


~~~
$MfaClaimRule = “c:[Type == ‘" https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid’", Value == ‘"group_SID’"]  
 => issue(Type = ‘"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod’", Value = ‘"https://schemas.microsoft.com/claims/multipleauthn’");”  

Set-AdfsAdditionalAuthenticationRule $MfaClaimRule  
~~~


> [!NOTE]  
> 교체 해야 *< 그룹\_SID >* AD 그룹의 sid 값입니다.  

### <a name="to-configure-mfa-globally-based-on-users-location"></a>전체적으로 사용자의 위치에 따라 MFA를 구성 하려면  

1.  페더레이션 서버에서 Windows PowerShell 명령 창을 열고 다음 명령을 실행 합니다.  


~~~
$MfaClaimRule = “c:[Type == ‘" https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork’", Value == ‘"true_or_false’"]  
 => issue(Type = ‘"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod’", Value = ‘"https://schemas.microsoft.com/claims/multipleauthn’");”  

Set-AdfsAdditionalAuthenticationRule $MfaClaimRule  
~~~



> [!NOTE]  
> 교체 해야 *< true\_또는\_false >* 하나로 `true` 또는 `false`합니다. 값 엑스트라넷 또는 인트라넷에서 액세스 요청 하는 여부에 따라 특정 규칙 조건에 따라 다릅니다.  

### <a name="to-configure-mfa-globally-based-on-users-device-data"></a>전체적으로 사용자의 장치 데이터를 기반으로 MFA를 구성 하려면  

1.  페더레이션 서버에서 Windows PowerShell 명령 창을 열고 다음 명령을 실행 합니다.  


~~~
$MfaClaimRule = "c:[Type == ‘" https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser’", Value == ‘"true_or_false"']  
 => issue(Type = ‘"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod’", Value = ‘"https://schemas.microsoft.com/claims/multipleauthn’");"  

Set-AdfsAdditionalAuthenticationRule $MfaClaimRule  
~~~


> [!NOTE]  
> 교체 해야 *< true\_또는\_false >* 하나로 `true` 또는 `false`합니다. 값이 장치가 작업 공간 연결 인지에 따라 특정 규칙 조건에 종속\-가입 합니다.  

### <a name="to-configure-mfa-globally-if-the-access-request-comes-from-the-extranet-and-from-a-non-workplace-joined-device"></a>엑스트라넷 및 비에서 액세스를 요청한 경우 MFA를 전역적으로 구성 하려면\-작업 공간\-조인 된 장치  

1.  페더레이션 서버에서 Windows PowerShell 명령 창을 열고 다음 명령을 실행 합니다.  


~~~
`Set-AdfsAdditionalAuthenticationRule "c:[Type == '"https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser'", Value == '"true_or_false'"] && c2:[Type == '"https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork'", Value == '" true_or_false '"] => issue(Type = '"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod'", Value ='"https://schemas.microsoft.com/claims/multipleauthn'");" ` 
~~~


> [!NOTE]  
> 두 인스턴스를 대체 해야 *< true\_또는\_false >* 하나로 `true` 또는 `false`, 는 특정 규칙 조건에 따라 달라 집니다. 규칙 조건을 기반으로 작업 공간에 장치가 인지\-가입 또는 엑스트라넷에서 액세스 요청 하는 없고 여부 또는 인트라넷 합니다.  

### <a name="to-configure-mfa-globally-if-access-comes-from-an-extranet-user-that-belongs-to-a-certain-group"></a>액세스는 엑스트라넷에 속한 사용자가 특정 그룹에서 제공 되는 경우 MFA를 전역적으로 구성 하려면  

1.  페더레이션 서버에서 Windows PowerShell 명령 창을 열고 다음 명령을 실행 합니다.  


~~~
Set-AdfsAdditionalAuthenticationRule "c:[Type == `"https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid`", Value == `"group_SID`"] && c2:[Type == `"https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork`", Value== `"true_or_false`"] => issue(Type = `"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod`", Value =`"https://schemas.microsoft.com/claims/
~~~

> [!NOTE]  
> 교체 해야 *< 그룹\_SID >* 그룹 SID 값을 가진 및 *< true\_또는\_false >* 하나로 `true` 또는 `false`, 엑스트라넷에서 액세스 요청 하는 여부에 따라 특정 규칙 조건에 따라 또는 인트라넷 합니다.  

### <a name="to-grant-access-to-an-application-based-on-user-data-via-windows-powershell"></a>Windows PowerShell을 통해 사용자 데이터를 기반으로 하는 응용 프로그램에 대 한 액세스 권한을 부여 하려면  

1.  페더레이션 서버에서 Windows PowerShell 명령 창을 열고 다음 명령을 실행 합니다.  

    ```  
    $rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust  

    ```  

> [!NOTE]  
> 교체 해야 *< 신뢰\_파티\_트러스트 >* 신뢰 당사자 트러스트의 값입니다.  

2. 동일한 Windows PowerShell 명령 창에서 다음 명령을 실행 합니다.  

   ```  

     $GroupAuthzRule = "@RuleTemplate = `“Authorization`” @RuleName = `"Foo`" c:[Type == `"https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid`", Value =~ `"^(?i)<group_SID>$`"] =>issue(Type = `"https://schemas.microsoft.com/authorization/claims/deny`", Value = `"DenyUsersWithClaim`");"  
   Set-AdfsRelyingPartyTrust –TargetRelyingParty $rp –IssuanceAuthorizationRules $GroupAuthzRule  
   ```  

> [!NOTE]  
> > 교체 해야 *< 그룹\_SID >* AD 그룹의 sid 값입니다.  

### <a name="to-grant-access-to-an-application-that-is-secured-by-ad-fs-only-if-this-users-identity-was-validated-with-mfa"></a>이 사용자의이 id 경우에만 AD FS에서 보호 되는 응용 프로그램에 대 한 액세스 권한을 부여 하려면의 유효성을 검사할 mfa  

1.  페더레이션 서버에서 Windows PowerShell 명령 창을 열고 다음 명령을 실행 합니다.  


~~~
`$rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust ` 
~~~


> [!NOTE]  
> 교체 해야 *< 신뢰\_파티\_트러스트 >* 신뢰 당사자 트러스트의 값입니다.  

2. 동일한 Windows PowerShell 명령 창에서 다음 명령을 실행 합니다.  

   ```  
   $GroupAuthzRule = "@RuleTemplate = `"Authorization`"  
   @RuleName = `"PermitAccessWithMFA`"  
   c:[Type == `"https://schemas.microsoft.com/claims/authnmethodsreferences`", Value =~ `"^(?i)https://schemas\.microsoft\.com/claims/multipleauthn$`"] => issue(Type = `"https://schemas.microsoft.com/authorization/claims/permit`", Value = ‘“PermitUsersWithClaim’");"  

   ```  

### <a name="to-grant-access-to-an-application-that-is-secured-by-ad-fs-only-if-the-access-request-comes-from-a-workplace-joined-device-that-is-registered-to-the-user"></a>액세스 경우에만 AD FS에서 보호 되는 응용 프로그램에 대 한 액세스 권한을 부여 하는 작업 공간에서 요청이 오는\-사용자에 게 등록 되어 있는 연결된 장치  

1.  페더레이션 서버에서 Windows PowerShell 명령 창을 열고 다음 명령을 실행 합니다.  

    ```  
    $rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust  

    ```  

> [!NOTE]  
> 교체 해야 *< 신뢰\_파티\_트러스트 >* 신뢰 당사자 트러스트의 값입니다.  

2. 동일한 Windows PowerShell 명령 창에서 다음 명령을 실행 합니다.  


~~~
$GroupAuthzRule = "@RuleTemplate = `"Authorization`"  
@RuleName = `"PermitAccessFromRegisteredWorkplaceJoinedDevice`"  
c:[Type == `"https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser`", Value =~ `"^(?i)true$`"] => issue(Type = `"https://schemas.microsoft.com/authorization/claims/permit`", Value = `"PermitUsersWithClaim`");  
~~~



### <a name="to-grant-access-to-an-application-that-is-secured-by-ad-fs-only-if-the-access-request-comes-from-a-workplace-joined-device-that-is-registered-to-a-user-whose-identity-has-been-validated-with-mfa"></a>액세스 경우에만 AD FS에서 보호 되는 응용 프로그램에 대 한 액세스 권한을 부여 하는 작업 공간에서 요청이 오는\-mfa id 유효성을 확인 된 사용자에 게 등록 되어 있는 연결된 장치  

1.  페더레이션 서버에서 Windows PowerShell 명령 창을 열고 다음 명령을 실행 합니다.  


~~~
`$rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust ` 
~~~


> [!NOTE]  
> 교체 해야 *< 신뢰\_파티\_트러스트 >* 신뢰 당사자 트러스트의 값입니다.  

2. 동일한 Windows PowerShell 명령 창에서 다음 명령을 실행 합니다.  

   ```  
   $GroupAuthzRule = ‘@RuleTemplate = “Authorization”  
   @RuleName = “RequireMFAOnRegisteredWorkplaceJoinedDevice”  
   c1:[Type == `"https://schemas.microsoft.com/claims/authnmethodsreferences`", Value =~ `"^(?i)http://schemas\.microsoft\.com/claims/multipleauthn$`"] &&  
   c2:[Type == `"https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser`", Value =~ `"^(?i)true$”] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit`", Value = `"PermitUsersWithClaim`");"  

   ```  

### <a name="to-grant-extranet-access-to-an-application-secured-by-ad-fs-only-if-the-access-request-comes-from-a-user-whose-identity-has-been-validated-with-mfa"></a>Mfa id 유효성을 확인 된 사용자 로부터 액세스 요청 하는 경우에 AD FS에서 보호 되는 응용 프로그램에 대 한 엑스트라넷 액세스 권한을 부여 하려면  

1.  페더레이션 서버에서 Windows PowerShell 명령 창을 열고 다음 명령을 실행 합니다.  


~~~
`$rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust`  
~~~


> [!NOTE]  
> 교체 해야 *< 신뢰\_파티\_트러스트 >* 신뢰 당사자 트러스트의 값입니다.  

2. 동일한 Windows PowerShell 명령 창에서 다음 명령을 실행 합니다.  


~~~
$GroupAuthzRule = "@RuleTemplate = `"Authorization`"  
@RuleName = `"RequireMFAForExtranetAccess`"  
c1:[Type == `"https://schemas.microsoft.com/claims/authnmethodsreferences`", Value =~ `"^(?i)http://schemas\.microsoft\.com/claims/multipleauthn$`"] &&  
c2:[Type == `"https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork`", Value =~ `"^(?i)false$`"] => issue(Type = `"https://schemas.microsoft.com/authorization/claims/permit`", Value = `"PermitUsersWithClaim`");"  
~~~

## <a name="additional-references"></a>추가 참조  

[AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md)
