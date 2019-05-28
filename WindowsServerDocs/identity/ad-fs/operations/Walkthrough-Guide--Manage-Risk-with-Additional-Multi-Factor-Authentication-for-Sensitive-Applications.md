---
ms.assetid: 5fd4063d-34dc-4b15-9a88-cc6c1fff455a
title: 연습 가이드-중요 한 응용 프로그램에 대해 추가 다단계 인증을 사용 하 여 위험 관리
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: bd21f2d6e8dcb167aa2c614d096807305a7728d6
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188890"
---
# <a name="walkthrough-guide-manage-risk-with-additional-multi-factor-authentication-for-sensitive-applications"></a>연습 가이드: 추가 다단계 인증을 사용하여 중요한 응용 프로그램에 대한 위험 관리




## <a name="about-this-guide"></a>이 가이드 정보
이 연습에서는 사용자의 그룹 구성원 자격 데이터를 기반으로 한 Active Directory Federation Services (AD FS) Windows Server 2012 r 2에서에서 MFA (다단계 인증)를 구성 하기 위한 지침을 제공 합니다.

Adfs에서 MFA 및 인증 메커니즘에 대 한 자세한 내용은 참조 [중요 한 응용 프로그램에 대 한 Multi-factor Authentication 사용 하 여 위험 관리](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)합니다.

이 연습은 다음 섹션으로 구성됩니다.

-   [1단계: 랩 환경 설정](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md#BKMK_1)

-   [2단계: 기본 AD FS 인증 메커니즘 확인](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_2)

-   [3단계: 페더레이션 서버에서 MFA를 구성 합니다.](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_3)

-   [4단계: MFA 메커니즘 확인](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_4)

## <a name="BKMK_1"></a>1 단계: 랩 환경 설정
이 연습을 완료하려면 다음 구성 요소로 구성된 환경이 필요합니다.

-   테스트 사용자 및 그룹 계정, Windows Server 2012 R2 또는 Windows Server 2012 r 2로 업그레이드 하는 해당 스키마와 Windows Server 2008, Windows Server 2008 R2 또는 Windows Server 2012에서 실행 되는 Active Directory 도메인에서 실행 되는 Active Directory 도메인

-   Windows Server 2012 r 2에서 실행 하는 페더레이션 서버

-   예제 응용 프로그램을 호스팅하는 웹 서버

-   예제 응용 프로그램에 액세스할 수 있는 클라이언트 컴퓨터

> [!WARNING]
> 프로덕션 환경과 테스트 환경 모두, 서로 다른 컴퓨터를 페더레이션 서버와 웹 서버로 사용하는 것이 좋습니다.

이 환경에서 페더레이션 서버는 사용자가 예제 응용 프로그램에 액세스하는 데 필요한 클레임을 발급합니다. 웹 서버는 페더레이션 서버에서 발급된 클레임을 제공하는 사용자를 신뢰할 예제 응용 프로그램을 호스팅합니다.

이 환경을 설정 하는 방법에 대 한 지침을 참조 하십시오. [Windows Server 2012 r 2에서 AD FS에 대 한 랩 환경 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)합니다.

## <a name="BKMK_2"></a>2 단계: 기본 AD FS 인증 메커니즘 확인
이 단계에서는 사용자가 AD FS 로그인 페이지로 리디렉션된 후 유효한 자격 증명을 제공하면 응용 프로그램에 대한 액세스 권한이 부여되는 기본 AD FS 액세스 제어 메커니즘(엑스트라넷의 경우**폼 인증** 및 인트라넷의 경우 **Windows 인증** )을 확인합니다. 사용할 수는 **Robert Hatley** AD 계정 및 **claimapp** 샘플 응용 프로그램에서 구성한 [Windows Server 2012 r 2에서 AD FS에 대 한 랩 환경 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)합니다.

1.  클라이언트 컴퓨터에서 브라우저 창을 열고 샘플 응용 프로그램으로 이동 합니다. **https://webserv1.contoso.com/claimapp**합니다.

    이 작업을 수행하면 요청이 자동으로 페더레이션 서버로 리디렉션되고 사용자 이름과 암호를 사용하여 로그인하라는 메시지가 표시됩니다.

2.  자격 증명을 입력에서 **Robert Hatley** AD 계정에서 만든 [Windows Server 2012 r 2에서 AD FS에 대 한 랩 환경 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)합니다.

    그러면 응용 프로그램에 대한 액세스 권한이 부여됩니다.

## <a name="BKMK_3"></a>3 단계: 페더레이션 서버에서 MFA 구성
Windows Server 2012 r 2에서 AD FS에서 MFA를 구성 하는 방법은 두 가지가 있습니다.

-   [추가 인증 방법 선택](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_5)

-   [MFA 정책 설정](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_6)

### <a name="BKMK_5"></a>추가 인증 방법 선택
MFA를 설정하려면 추가 인증 방법을 선택해야 합니다. 이 연습에서는 다음 옵션 중 하나를 추가 인증 방법으로 선택할 수 있습니다.

-   선택 [인증서 인증](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_7) 기본적으로 Windows Server 2012 r 2에서 AD FS에서 사용할 수 있는 메서드

-   [Windows Azure Multi-Factor Authentication](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_8)을 구성하고 선택합니다.

#### <a name="BKMK_7"></a>인증서 인증
추가 인증 방법으로 인증서 인증을 선택하려면 다음 절차 중 하나를 완료합니다.

###### <a name="to-configure-certificate-authentication-as-an-additional-authentication-method-via-the-ad-fs-management-console"></a>AD FS 관리 콘솔을 통해 인증서 인증을 추가 인증 방법으로 구성하려면

1.  페더레이션 서버의 AD FS 관리 콘솔에서 **Authentication Policies(인증 정책)** 노드로 이동하여 **Multi-factor Authentication(다단계 인증)** 섹션에서 **Global Settings(전역 설정)** 하위 섹션 옆에 있는 **Edit(편집)** 링크를 클릭합니다.

2.  **Edit Global Authentication Policy(전역 인증 정책 편집)** 창에서 **Certificate Authentication(인증서 인증)** 을 추가 인증 방법으로 선택하고 **OK(확인)** 를 클릭합니다.

###### <a name="to-configure-certificate-authentication-as-an-additional-authentication-method-via-windows-powershell"></a>Windows PowerShell을 통해 인증서 인증을 추가 인증 방법으로 구성하려면

1.  페더레이션 서버에서 Windows PowerShell 명령 창을 열고 다음 명령을 실행합니다.

    ```
    Set-AdfsGlobalAuthenticationPolicy -AdditionalAuthenticationProvider CertificateAuthentication

    ```

    > [!WARNING]
    > 이 명령이 성공적으로 실행을 실행할 수를 확인 하는 `Get-AdfsGlobalAuthenticationPolicy` 명령입니다.

#### <a name="BKMK_8"></a>Windows Azure Multi-factor Authentication
페더레이션 서버에서 **Windows Azure Multi-Factor Authentication** 을 다운로드하여 추가 인증으로 구성하고 선택하려면 다음 절차를 완료합니다.

1.  [Windows 통해 Multi-factor Authentication 공급자를 만들려면 Azure Portal](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_a)

2.  [Windows Azure Multi-factor Authentication 서버 다운로드](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_b)

3.  [페더레이션 서버에서 Windows Azure Multi-factor Authentication 서버를 설치 합니다.](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_c)

4.  [Windows Azure Multi-factor Authentication을 추가 인증 방법으로 구성](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_d)

##### <a name="BKMK_a"></a>Windows 통해 Multi-factor Authentication 공급자를 만들려면 Azure Portal

1.  Windows Azure 포털에 관리자로 로그온합니다.

2.  왼쪽에서 Active Directory를 선택합니다.

3.  Active Directory 페이지 상단에서 **다단계 인증 공급자**를 선택합니다.  그런 다음 아래쪽에서 **새로 만들기**를 클릭합니다.

4.  **앱 서비스->Active Directory**에서 **다단계 인증 공급자**를 선택한 다음 **빠른 생성**을 선택합니다.

5.  **앱 서비스**에서 **활성 인증 공급자**를 선택한 다음 **빠른 생성**을 선택합니다.

6.  다음 필드를 채우고 **만들기**를 선택합니다.

    1.  **이름** -다단계 인증 공급자의 이름입니다.

    2.  **사용 모델** -다단계 인증 공급자의 사용 모델입니다.

        -   **인증 당** -인증 단위로 요금이 청구 되는 구매 모델입니다. 일반적으로 소비자용 응용 프로그램에서 Windows Azure Multi-Factor Authentication을 사용하는 시나리오에 사용됩니다.

        -   **활성화 된 사용자별** -활성화 된 사용자 단위로 요금이 청구 되는 구매 모델입니다.  일반적으로 Office 365와 같은 직원용 시나리오에 사용됩니다.

        사용 모델에 대한 자세한 내용은 [Microsoft Azure 가격 정보](http://www.windowsazure.com/pricing/details/active-directory/)를 참조하세요.

    3.  **디렉터리** -다단계 인증 공급자와 연결 된 Windows Azure Active Directory 테 넌 트입니다. 온-프레미스 응용 프로그램의 보안을 유지할 때는 공급자를 Windows Azure Active Directory에 연결할 필요가 없으므로 이는 선택 사항입니다.

7.  만들기를 클릭하면 Multi-Factor Authentication 공급자가 만들어지고 다음 메시지가 표시됩니다.  Multi-Factor Authentication 공급자를 만들었습니다.  **확인**을 클릭합니다.

이제 Windows Azure Multi-Factor Authentication 서버를 다운로드해야 합니다. Windows Azure 포털을 통해 Windows Azure Multi-Factor Authentication 포털을 시작하면 됩니다.

##### <a name="BKMK_b"></a>Windows Azure Multi-factor Authentication 서버 다운로드

1.  Windows Azure 포털에 관리자로 로그온하여 위 절차에서 만든 다단계 인증 공급자를 클릭합니다. 그런 다음 **관리** 단추를 클릭합니다.

    그러면 **Windows Azure Multi-Factor Authentication** 포털이 시작됩니다.

2.  **Windows Azure Multi-Factor Authentication** 포털에서 **다운로드**를 클릭한 다음 **다운로드** 를 클릭하여 Windows Azure Multi-Factor Authentication 서버를 다운로드합니다.

Windows Azure Multi-Factor Authentication 서버 실행 파일을 다운로드한 후에는 페더레이션 서버에 설치해야 합니다.

##### <a name="BKMK_c"></a>페더레이션 서버에서 Windows Azure Multi-factor Authentication 서버를 설치 합니다.

1.  Windows Azure Multi-Factor Authentication 서버 실행 파일을 다운로드하고 두 번 클릭합니다.  그러면 설치가 시작됩니다.

2.  사용권 계약 화면에서 계약서를 읽고 **동의함** 을 선택한 후 **다음**을 클릭합니다.

3.  대상 폴더가 올바른지 확인하고 **다음**을 클릭합니다.

4.  설치가 완료되면 **마침**을 클릭합니다.

이제 페더레이션 서버에 설치한 Windows Azure Multi-Factor Authentication 서버를 시작하여 추가 인증 방법으로 구성할 준비가 완료되었습니다.

##### <a name="BKMK_d"></a>Windows Azure Multi-factor Authentication을 추가 인증 방법으로 구성

1.  페더레이션 서버의 설치 위치에서 **Windows Azure Multi-Factor Authentication** 을 시작한 후 시작 페이지에서 **인증 구성 마법사 사용 건너뛰기** 확인란을 선택하고 **다음**을 클릭합니다.

2.  Multi-Factor Authentication Server를 정품 인증하려면 Multi-Factor Authentication Server를 다운로드한 Multi-Factor Authentication 관리 포털 페이지로 돌아가 **정품 인증 자격 증명 생성** 단추를 클릭합니다. Multi-Factor Authentication Server 사용자 인터페이스에서 생성된 자격 증명을 입력하고 **정품 인증**을 클릭합니다.

3.  그러면 **Multi-Factor Authentication Server** 사용자 인터페이스에 **다중 서버 구성 마법사**를 실행할지 묻는 메시지가 표시됩니다.  **아니요**를 선택합니다.

    > [!IMPORTANT]
    > 랩 환경에 이 연습을 완료하는 데 사용되는 페더레이션 서버가 하나만 구성된 경우 **다중 서버 구성 마법사**를 건너뛸 수 있습니다. 그러나 환경에 여러 페더레이션 서버가 있는 경우에는 Multi-Factor Authentication Server를 설치하고 각 페더레이션 서버에서 **다중 서버 구성 마법사** 를 완료해야 페더레이션 서버에서 실행되는 다단계 서버 간에 복제할 수 있습니다.

4.  **Multi-Factor Authentication 서버** 사용자 인터페이스에서 **사용자** 아이콘을 선택하고 **Active Directory에서 가져오기**를 클릭한 다음 **Robert Hatley** 계정을 선택하여 Microsoft Azure Multi-Factor Authentication에서 해당 계정을 프로비전하고 **가져오기**를 클릭합니다.

5.  **사용자** 목록에서 **Robert Hatley** 계정을 선택하고 **편집**을 클릭한 다음 **사용자 편집** 창에서 이 계정의 휴대폰 번호를 제공합니다. 그런 다음 **사용** 확인란이 선택되어 있는지 확인하고 **적용**을 클릭합니다.

6.  **사용자** 목록에서 **Robert Hatley** 계정을 선택하고 **테스트**를 클릭합니다. **테스트 사용자** 창에서 **Robert Hatley** 계정에 대한 자격 증명을 제공합니다. 휴대폰 벨 키를 눌러 계정 확인을 완료 하는 ' #'.

7.  **Multi-Factor Authentication Server** 사용자 인터페이스에서 **AD FS** 아이콘을 선택하고 **사용자 등록 허용**, **사용자가 방법을 선택하도록 허용** ( **전화 통화** 및 **문자 메시지**포함), **대체에 본인 확인 질문 사용** 및 **로깅 사용** 확인란이 선택되어 있는지 확인한 다음 **AD FS 어댑터 설치**를 클릭하고 **다단계 인증 AD FS 어댑터** 설치 마법사를 완료합니다.

    > [!NOTE]
    > **다단계 인증 AD FS 어댑터** 설치 마법사는 Active Directory에 **PhoneFactor Admins**라는 보안 그룹을 만든 다음 페더레이션 서비스의 AD FS 서비스 계정을 이 그룹에 추가합니다.
    > 
    > 도메인 컨트롤러에서 **PhoneFactor Admins** 그룹이 실제로 생성되고 AD FS 서비스 계정이 이 그룹의 구성원인지 확인하는 것이 좋습니다.
    > 
    > 필요한 경우 AD FS 서비스 계정을 도메인 컨트롤러의 **PhoneFactor Admins** 그룹에 수동으로 추가합니다.

    AD FS 어댑터 설치에 대한 자세한 내용을 보려면 Multi-Factor Authentication Server 오른쪽 상단의 도움말 링크를 클릭하세요.

8.  페더레이션 서비스에 어댑터를 등록하려면 페더레이션 서버에서 Windows PowerShell 명령 창을 시작하고 `\Program Files\Multi-Factor Authentication Server\Register-MultiFactorAuthenticationAdfsAdapter.ps1`명령을 실행합니다. 이제 어댑터가 **WindowsAzureMultiFactorAuthentication**으로 등록됩니다.  등록을 적용하려면 AD FS 서비스를 다시 시작해야 합니다.

9. Windows Azure Multi-Factor Authentication을 추가 인증 방법으로 구성하려면 AD FS 관리 콘솔에서 **Authentication Policies(인증 정책)** 노드로 이동하여 **Multi-factor Authentication(다단계 인증)** 섹션에서 **Global Settings(전역 설정)** 하위 섹션 옆에 있는 **Edit(편집)** 링크를 클릭합니다. **Edit Global Authentication Policy(전역 인증 정책 편집)** 창에서 **Multi-Factor Authentication(다단계 인증)** 을 추가 인증 방법으로 선택하고 **OK(확인)** 를 클릭합니다.

    > [!NOTE]
    > Windows Azure Multi-Factor Authentication 방법뿐 아니라 구성된 모든 타사 인증 방법의 이름 및 설명을 사용자 지정할 수 있습니다. 이는 **Set-AdfsAuthenticationProviderWebContent** cmdlet을 실행하면 AD FS UI에 표시됩니다. 자세한 내용은 [https://technet.microsoft.com/library/dn479401.aspx](https://technet.microsoft.com/library/dn479401.aspx)를 참조하세요.

### <a name="BKMK_6"></a>MFA 정책 설정
MFA를 사용하도록 설정하려면 페더레이션 서버에서 MFA 정책을 설정해야 합니다. 이 연습에서는 MFA 정책에 당 **Robert Hatley** 에 속하기 때문에 MFA를 진행 하려면 계정이 필요는 **재무** 에서 설정한 그룹 [Windows Server 2012 r 2에서 AD FS에 대 한 랩 환경 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md).

AD FS 관리 콘솔 또는 Windows PowerShell을 사용하여 MFA 정책을 설정할 수 있습니다.

##### <a name="to-configure-the-mfa-policy-based-on-users-group-membership-data-for-claimapp--via-the-ad-fs-management-console"></a>AD FS 관리 콘솔을 통해 'claimapp'에 대 한 사용자의 그룹 구성원 자격 데이터에 따라 MFA 정책을 구성 하려면

1.  페더레이션 서버의 AD FS 관리 콘솔에서 **Authentication Policies(인증 정책)** \\**Per Relying Party Trust(신뢰 당사자 트러스트별)** 노드로 이동하여 예제 응용 프로그램(**AD 계정 및**)을 나타내는 신뢰 당사자 트러스트를 선택합니다.

2.  **Actions(작업)** 페이지에서 또는 **claimapp**을 마우스 오른쪽 단추로 클릭하여 **Edit Custom Multi-factor Authentication(사용자 지정 다단계 인증 편집)** 을 선택합니다.

3.  **Edit Relying Party Trust for claimapp(claimapp에 대한 신뢰 당사자 트러스트 편집)** 창에서 **Users/Groups(사용자/그룹)** 목록 옆에 있는 **Add(추가)** 단추를 클릭합니다. 에 입력 **재무** 에서 만든 AD 그룹의 이름에 대 한 [Windows Server 2012 r 2에서 AD FS에 대 한 랩 환경 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md), 를 클릭 하 고 **이름 확인**, 는 이름이 확인 되 면 클릭 하 고 **확인**.

4.  **Edit Relying Party Trust for claimapp(claimapp에 대한 신뢰 당사자 트러스트 편집)** 창에서 **OK(확인)** 를 클릭합니다.

##### <a name="to-configure-the-mfa-policy-based-on-users-group-membership-data-for-claimapp--via-windows-powershell"></a>Windows PowerShell을 통해 'claimapp'에 대 한 사용자의 그룹 구성원 자격 데이터에 따라 MFA 정책을 구성 하려면

1.  페더레이션 서버에서 Windows PowerShell 명령 창을 열고 다음 명령을 실행합니다.

    ```
    $rp = Get-AdfsRelyingPartyTrust -Name claimapp
    ```

2.  동일한 Windows PowerShell 명령 창에서 다음 명령을 실행합니다.

    ```
    $GroupMfaClaimTriggerRule = 'c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "^(?i) <group_SID>$"] => issue(Type = "https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", Value = "https://schemas.microsoft.com/claims/multipleauthn");'
    Set-AdfsRelyingPartyTrust -TargetRelyingParty $rp -AdditionalAuthenticationRules $GroupMfaClaimTriggerRule

    ```

    > [!NOTE]
    > <group_SID>를 AD 그룹 **금융**의 SID 값으로 바꿔야 합니다.

## <a name="BKMK_4"></a>4 단계: MFA 메커니즘 확인
이 단계에서는 이전 단계에서 설정한 MFA 기능을 확인합니다. 다음 절차를 사용하여 **Robert Hatley** AD 사용자가 응용 프로그램 예제에 액세스할 수 있는지 확인할 수 있습니다. 이번에는 이 사용자가 **금융** 그룹에 속해 있으므로 MFA를 진행해야 합니다.

1.  클라이언트 컴퓨터에서 브라우저 창을 열고 샘플 응용 프로그램으로 이동 합니다. **https://webserv1.contoso.com/claimapp**합니다.

    이 작업을 수행하면 요청이 자동으로 페더레이션 서버로 리디렉션되고 사용자 이름과 암호를 사용하여 로그인하라는 메시지가 표시됩니다.

2.  **Robert Hatley** AD 계정의 자격 증명을 입력합니다.

    구성한 MFA 정책 때문에 추가 인증을 진행하라는 메시지가 표시됩니다. 기본 메시지 텍스트는 **보안상 계정을 확인하기 위해 추가 정보가 필요합니다.** 입니다. (보안상 계정을 확인하기 위해 추가 정보가 필요합니다.)이지만 이 텍스트를 원하는 대로 사용자 지정할 수 있습니다. 로그인 환경을 사용자 지정하는 방법에 대한 자세한 내용은 [Customizing the AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx)을 참조하세요.

    추가 인증 방법으로 인증서 인증을 구성한 경우에 기본 메시지 텍스트는 **인증에 사용 하려는 인증서를 선택 합니다. 작업을 취소 하면 브라우저를 닫고 다시 시도 하십시오.**

    Microsoft Azure Multi-Factor Authentication을 추가 인증 방법으로 구성한 경우 기본 메시지 텍스트는 **A call will be placed to your phone to complete your authentication.** Windows Azure Multi-factor Authentication을 사용 하 여 로그인 하 고 확인 하는 기본 방법에 대 한 다양 한 옵션을 사용 하는 방법에 대 한 자세한 내용은 참조 [Windows Azure Multi-factor Authentication 개요](https://technet.microsoft.com/library/dn249479.aspx)합니다.

## <a name="see-also"></a>관련 항목
[중요 한 응용 프로그램에 대 한 추가 다단계 인증을 사용 하 여 위험 관리](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)
[Windows Server 2012 r 2에서 AD FS에 대 한 랩 환경 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)



