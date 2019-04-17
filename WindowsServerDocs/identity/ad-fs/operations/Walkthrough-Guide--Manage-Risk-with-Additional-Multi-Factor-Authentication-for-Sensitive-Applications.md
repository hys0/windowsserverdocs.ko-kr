---
ms.assetid: 5fd4063d-34dc-4b15-9a88-cc6c1fff455a
title: "연습 가이드-추가 다단계 인증 민감한 응용 프로그램에 대 한 위험을 관리"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 414f37e86f0072863e5fa2f107c39e5518e560ec
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="walkthrough-guide-manage-risk-with-additional-multi-factor-authentication-for-sensitive-applications"></a>연습 가이드: 추가 다단계 인증 민감한 응용 프로그램에 대 한 위험을 관리

>Windows Server 2012 r 2에 적용 됩니다.


## <a name="about-this-guide"></a>이 가이드 정보
이 연습 그룹 구성원 사용자의 데이터를 기반으로 한 Active Directory Federation Services (ADFS) Windows Server 2012 r 2에서에 다단계 인증 (MFA) 구성에 대 한 지침을 제공 합니다.

Adfs의 MFA와 인증 장치에 대 한 자세한 내용은 참조 [민감한 응용 프로그램에 대 한 추가 다단계 인증 관리 위험](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)합니다.

이 연습 다음 섹션으로 구성 됩니다.

-   [1 단계: 랩 환경 설정](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md#BKMK_1)

-   [2 단계: 기본 ADFS 인증 장치 확인](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_2)

-   [3 단계: MFA 해당 federation 서버에서 구성](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_3)

-   [4 단계: MFA 장치 확인](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_4)

## <a name="BKMK_1"></a>1 단계: 랩 환경 설정
이 연습을 완료 하기 위해 다음과 같은 구성 요소도 구성 된 환경을 할 수 있습니다.

-   테스트 사용자 및 Windows Server 2012 R2 또는 Windows Server 2012 r 2로 업그레이드 스키마와 Windows Server 2008, Windows Server 2008 R2 또는 Windows Server 2012에서 실행 중인 Active Directory 도메인 실행 하는 그룹 계정, Active Directory 도메인

-   Windows Server 2012 r 2에 실행 하는 federation 서버

-   샘플 신청서 호스트 하는 웹 서버

-   클라이언트 컴퓨터 샘플 응용 프로그램 액세스할 수 있습니다

> [!WARNING]
> 권장 (생산 및 테스트 환경에서 둘 다)를 해당 federation 서버 하 고 웹 서버 동일한 컴퓨터를 사용 하지 마십시오.

이 환경에서 federation 서버는 사용자에 게 샘플 응용 프로그램에 액세스할 수 있도록 클레임 발행 합니다. 클레임은를 제공 하는 사용자가 신뢰 하는 샘플 응용 프로그램 federation 서버 문제 호스트 하는 웹 서버 합니다.

이 환경을 설정 하는 방법에 관한 참조 [랩 환경 ADFS Windows Server 2012 r 2에서에 대 한 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)합니다.

## <a name="BKMK_2"></a>2 단계: 기본 ADFS 인증 장치 확인
이 단계에서 기본 ADFS 액세스 제어 메커니즘을 확인 합니다 (**폼 인증** 에 대 한 익스트라넷 및 **Windows 인증** 인트라넷), 여기서 사용자가 ADFS 로그인 페이지로 리디렉션됩니다, 제공 유효한 자격 증명을 하 고 응용 프로그램에 대 한 액세스 권한이 부여 됩니다. 사용할 수 있는 **로버트 Hatley** AD 계정이 및 **claimapp** 샘플으로 구성 된 응용 프로그램 [랩 환경 ADFS Windows Server 2012 r 2에서에 대 한 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)합니다.

1.  클라이언트 컴퓨터에 브라우저 창을 열고 샘플 응용 프로그램으로 이동: **https://webserv1.contoso.com/claimapp**합니다.

    이 작업은 federation 서버에 요청을 자동으로 리디렉션합니다 및 사용자 이름 및 암호를 사용 하 여 로그인 하 라는 메시지가 표시 됩니다.

2.  자격 증명 입력은 **로버트 Hatley** 광고 계정에서 만든 [랩 환경 ADFS Windows Server 2012 r 2에서에 대 한 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)합니다.

    응용 프로그램에 대 한 액세스를 부여 하 고 됩니다.

## <a name="BKMK_3"></a>3 단계: MFA 해당 federation 서버에서 구성
Windows Server 2012 r 2에서 adfs에서 MFA 구성에 두 가지 부분이 있습니다.

-   [추가 인증 방법을 선택합니다](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_5)

-   [MFA 정책 설정](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_6)

### <a name="BKMK_5"></a>추가 인증 방법을 선택합니다
MFA 설정 하기 위해 추가 인증 방법을 선택 해야 합니다. 추가 인증 방법에 대 한이 연습 다음 옵션 중에서 선택할 수 있습니다.

-   선택 [인증서 인증](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_7) 기본적으로 Windows Server 2012 r 2에서 Adfs에서 사용할 수 있는 방법

-   구성 하 고 선택 [Windows Azure 다단계 인증](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_8)

#### <a name="BKMK_7"></a>인증서를 인증
추가 인증 방법으로 인증 인증서를 선택 하는 다음 절차 중 하나를 완료 합니다.

###### <a name="to-configure-certificate-authentication-as-an-additional-authentication-method-via-the-ad-fs-management-console"></a>인증서 인증 AD FS Management Console을 통해 추가 인증 방법으로 구성 하려면

1.  AD FS Management Console에 해당 federation 서버가에서 탐색 하는 **인증 정책** 노드를 고 **다단계 인증** 섹션을 클릭는 **편집** 옆에 연결는 **전역 설정** 하위 섹션.

2.  에 **글로벌 인증 정책 편집** 창을 선택 하 고 **인증서 인증** 추가 인증 방법, 다음으로 **확인**합니다.

###### <a name="to-configure-certificate-authentication-as-an-additional-authentication-method-via-windows-powershell"></a>추가 인증 방법을 통해 Windows PowerShell로 인증서 인증 구성 하려면

1.  해당 federation 서버를 Windows PowerShell 명령 창 열고 다음 명령을 실행 합니다.

    ```
    Set-AdfsGlobalAuthenticationPolicy -AdditionalAuthenticationProvider CertificateAuthentication

    ```

    > [!WARNING]
    > 이 명령을 성공적으로 실행을 실행할 수를 확인 하 고 `Get-AdfsGlobalAuthenticationPolicy` 명령을 합니다.

#### <a name="BKMK_8"></a>Windows Azure 다단계 인증
다음 절차를 다운로드 하 고 구성 하 고 선택 하기 위해 수행 **Windows Azure 다중 요소 인증** 해당 federation 서버에 추가 인증 합니다.

1.  [Windows 통해 다단계 인증 공급자 만들기 Azure 포털](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_a)

2.  [Windows Azure 다단계 인증 서버를 다운로드](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_b)

3.  [해당 Federation 서버에 Windows Azure 다단계 인증 서버를 설치](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_c)

4.  [추가 인증 방법으로 Windows Azure 다단계 인증 구성](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_d)

##### <a name="BKMK_a"></a>Windows 통해 다단계 인증 공급자 만들기 Azure 포털

1.  Windows Azure 로그온 관리자 권한으로 포털 합니다.

2.  왼쪽, Active Directory를 선택 합니다.

3.  Active Directory 페이지 맨 위에 있는 **다단계 인증 공급자**합니다.  아래에서 클릭 한 다음 **새로**합니다.

4.  아래에서 **앱 서비스 Active Directory->**선택 **다단계 인증 공급자**를 선택 하 고 **빨리 만들기**합니다.

5.  아래에서 **앱 서비스**선택 **활성 Auth 공급자**를 선택 하 고 **빨리 만들기**합니다.

6.  다음 선택한 필드를 입력 **만들기**합니다.

    1.  **이름** -다단계 인증 공급자의 이름입니다.

    2.  **사용 모델** -다단계 인증 공급자의 사용 모델 합니다.

        -   **인증 당** -인증 따라 요금을 부과 하는 모델을 구매 합니다. 소비자 전면 응용 프로그램의 Windows Azure 다단계 인증을 사용 하는 시나리오에 대해 일반적으로 사용 됩니다.

        -   **사용할 수 있는 사용자에 따라** -활성화 사용자별 요금을 부과 하는 모델을 구매 합니다.  Office 365 같은 직원 전면 시나리오에 대해 일반적으로 사용 됩니다.

        사용 모델에 대 한 자세한 내용은 참조 [세부 정보 가격 Windows Azure](http://www.windowsazure.com/pricing/details/active-directory/)합니다.

    3.  **디렉터리** -다단계 인증 공급자 관련 된 Windows Azure Active Directory 테 합니다. 공급자 보안 온-프레미스 응용 프로그램 때 Windows Azure Active Directory에 연결 하지 않아도 선택 합니다.

7.  클릭 하면 다단계 인증 공급자를 만들 수는 만들고 없다는 메시지가 표시 되어야: 다단계 인증 공급자를 만들었습니다.  클릭 **확인**합니다.

그런 다음 Windows Azure 다단계 인증 서버를 다운로드 해야 합니다. 이렇게 하려면 Windows Azure 포털을 통해 Windows Azure 다단계 인증 포털을 시작 합니다.

##### <a name="BKMK_b"></a>Windows Azure 다단계 인증 서버를 다운로드

1.  관리자로 서의 Windows Azure 포털에에 로그인 하 고 위의 절차 만든 다단계 인증 공급자를 클릭 합니다. 클릭 한 다음는 **관리** 단추.

    이 시작의 **Windows Azure 다단계 인증** 포털 합니다.

2.  에 **Windows Azure 다중 요소 인증** 포털을 클릭 **다운로드**을 차례로 클릭 하 고 **다운로드** Windows Azure 다단계 인증 서버의 복사본을 다운로드 하 합니다.

Windows Azure 다단계 인증 서버에 대 한 실행 파일을 다운로드 하 고 나면 해당 federation 서버에 설치 해야 합니다.

##### <a name="BKMK_c"></a>해당 Federation 서버에 Windows Azure 다단계 인증 서버를 설치

1.  다운로드 한 Windows Azure 다단계 인증 서버에 대 한 파일을 실행을 두 번 클릭 합니다.  이 설치가 시작 됩니다.

2.  사용권 계약 화면의 계약을 읽어 선택 **동의** 클릭 **다음**합니다.

3.  클릭 하 고 대상 폴더 올바른지 확인 **다음**합니다.

4.  클릭 하면 설치가 완료 되 면 **완료**합니다.

이제 해당 federation 서버에 설치 하는 Windows Azure 다단계 인증 서버를 실행 하 고 추가 인증 방법으로 구성 되어 준비가 되었습니다.

##### <a name="BKMK_d"></a>추가 인증 방법으로 Windows Azure 다단계 인증 구성

1.  시작 **Windows Azure 다단계 인증** 설치 했던 시작 페이지에서 해당 federation 서버를 켜고에서 확인는 **인증 구성 마법사를 사용 하 여 건너뛰고** 확인란을 클릭 하 고 **다음**합니다.

2.  다중 요소 인증 서버를 정품 인증 하려면 다시 페이지로 이동 하 여 다단계 인증 관리 포털에서 다단계 인증 서버를 다운로드 하 고 클릭는 **활성화 자격 증명을 생성** 단추. 다중 요소 인증 서버 사용자 인터페이스에서 생성 된 자격 증명을 입력 하 고 클릭 **정품 인증**합니다.

3.  다음은 **다중 요소 인증 서버** 사용자 인터페이스를 실행 하 라는 메시지가 표시는 **다중 서버 구성 마법사**합니다.  선택 **아니요**합니다.

    > [!IMPORTANT]
    > 완료 건너뛸 수는 **다중 서버 구성 마법사** 이 연습 완료 하는 데 사용 되는 하나의 federation 서버 랩 환경을 제공 합니다. 그러나 귀하의 환경 여러 federation 서버 들어 있는 경우 설치 다단계 인증 서버 하 고 해야 완료는 **다중 서버 구성 마법사** 간의 federation 서버에서 실행 되는 다중 요소 서버 복제가 활성화 하기 위해 각 federation 서버의 합니다.

4.  에 **다중 요소 인증 서버** 사용자 인터페이스는 **사용자** 아이콘을 클릭 **Active Directory에서 가져오기**는 **로버트 Hatley** 계정에서 Windows Azure 다단계 인증을 제공 하 고 클릭 한 다음 **가져오기**합니다.

5.  **사용자** 목록에서 선택는 **로버트 Hatley** 계정, 클릭 **편집**의 **사용자 편집** 창이이 계정에 휴대폰 번호를 입력 해야 합니다.는 **사용** 확인란을 선택 하 고 클릭 한 다음 **적용**합니다.

6.  **사용자** 목록에서 선택 하 고 있는 **로버트 Hatley** 계정, 클릭 한 **테스트**합니다. 에 **테스트 사용자** 창에 대 한 자격 증명을 제공는 **로버트 Hatley** 계정 합니다. 휴대폰 벨 키를 누릅니다 '#' 계정 인증을 완료 합니다.

7.  **다중 요소 인증 서버** 사용자 인터페이스는 **ADFS** 아이콘을 하 않도록 **허용 사용자 등록**, **방법을 선택할 수 있도록** (포함 하 여 **전화 통화** 및 **문자 메시지**), **대체에 대 한 보안 관련 질문을 사용 하 여** 및 **로깅 사용** 확인란 검사를 클릭 **설치 광고 FS 어댑터**, 완료 하 고는 **다단계 인증 광고 FS 어댑터** 설치 마법사 합니다.

    > [!NOTE]
    > **다단계 인증 광고 FS 어댑터** 설치 마법사 라는 보안 그룹을 만들고 **PhoneFactor 관리자** Active Directory에 다음 federation 서비스의 ADFS 서비스 계정이이 그룹에 추가 합니다.
    > 
    > 도메인 컨트롤러에서 확인 하는 것이 좋습니다 하 고 **PhoneFactor 관리자** 그룹은 정말 만들고이 그룹의 회원은는 ADFS 서비스 계정을 합니다.
    > 
    > 필요에 따라 추가 ADFS 서비스 계정을 **PhoneFactor 관리자** 도메인 컨트롤러에서 수동으로 그룹화 합니다.

    설치 AD FS 어댑터에 대 한 자세한 내용은 다단계 인증 서버의 오른쪽 위 모서리에서 도움말 링크를 클릭 합니다.

8.  어댑터 federation 서비스를 해당 federation 서버에 등록할 Windows PowerShell 명령 창을 실행 하 고 다음 명령을 실행: `\Program Files\Multi-Factor Authentication Server\Register-MultiFactorAuthenticationAdfsAdapter.ps1`합니다. 어댑터는 이제로 등록 **WindowsAzureMultiFactorAuthentication**합니다.  ADFS 사항이 적용 등록에 대 한 서비스를 다시 시작 해야 합니다.

9. 으로 이동 하려면 Windows 다단계 인증 Azure AD FS Management Console에서 추가 인증 방법으로 구성는 **인증 정책** 노드를 고 **다단계 인증** 섹션에서 클릭는 **편집** 옆에 연결는 **전역 설정** 하위 섹션 합니다. 에 **글로벌 인증 정책 편집** 창을 선택 하 고 **다단계 인증** 추가 인증 방법, 다음으로 **확인**합니다.

    > [!NOTE]
    > 이름을 지정할 수 있습니다 및 실행 하 여 광고 FS UI에 표시 된 대로 Windows Azure 다단계 인증 방법을 뿐만 아니라 모든 설명은 구성 제 3 자 인증 방법는 **설정 AdfsAuthenticationProviderWebContent** cmdlet 합니다. 자세한 내용은 참조 [https://technet.microsoft.com/library/dn479401.aspx](https://technet.microsoft.com/library/dn479401.aspx)

### <a name="BKMK_6"></a>MFA 정책 설정
MFA를 활성화 하기 위해 해당 federation 서버에 MFA 정책을 설정 해야 합니다. 우리의 MFA 정책에 따라이 연습 **로버트 Hatley** 때문에 속해 그 MFA 거쳐 계정이 필요는 **금융** 에서 설정 하는 그룹 [랩 환경 ADFS Windows Server 2012 r 2에서에 대 한 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)합니다.

AD FS Management Console 또는 사용 하 여 Windows PowerShell 통해 MFA 정책을 설정할 수 있습니다.

##### <a name="to-configure-the-mfa-policy-based-on-users-group-membership-data-for-claimapp--via-the-ad-fs-management-console"></a>사용자의 광고 FS Management Console을 통해 'claimapp'에 대 한 그룹 구성원 데이터에 따라 MFA 정책을 구성 하려면

1.  AD FS Management Console에 해당 federation 서버가에 이동 **인증 정책**\\**의존 파티 신뢰 별로** 노드와 선택 샘플 응용 프로그램을 나타내는 신뢰 파티 신뢰 (**claimapp**).

2.  에 **작업** 페이지 또는 마우스 오른쪽 단추로 클릭 하거나 **claimapp**선택 **사용자 지정 다단계 인증 편집**합니다.

3.  에 **의존 파티 신뢰 편집 claimapp에 대 한** 창을 클릭는 **추가** 단추 옆에 **사용자/그룹** 목록 합니다. 에 입력 **금융** 에서 만든 광고 그룹의 이름에 대 한 [랩 환경 ADFS Windows Server 2012 r 2에서에 대 한 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)를 클릭 하 고 **이름 확인**, 이름이 해결 때 클릭 **확인**합니다.

4.  클릭 **확인** 에 **의존 파티 신뢰 편집 claimapp에 대 한** 창 합니다.

##### <a name="to-configure-the-mfa-policy-based-on-users-group-membership-data-for-claimapp--via-windows-powershell"></a>Windows PowerShell 통해 'claimapp'에 대 한 사용자의 그룹 구성원 데이터에 따라 MFA 정책을 구성 하려면

1.  해당 federation 서버를 Windows PowerShell 명령 창 열고 다음 명령을 실행 합니다.

    ```
    $rp = Get-AdfsRelyingPartyTrust -Name claimapp
    ```

2.  동일한 Windows PowerShell 명령 창에서 다음 명령을 실행 합니다.

    ```
    $GroupMfaClaimTriggerRule = 'c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "^(?i) <group_SID>$"] => issue(Type = "https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", Value = "https://schemas.microsoft.com/claims/multipleauthn");'
    Set-AdfsRelyingPartyTrust -TargetRelyingParty $rp -AdditionalAuthenticationRules $GroupMfaClaimTriggerRule

    ```

    > [!NOTE]
    > < Group_SID > 광고 그룹 sid 값으로 대체 하 않도록 **금융**합니다.

## <a name="BKMK_4"></a>4 단계: MFA 장치 확인
이 단계에서 이전 단계에서 설정한 MFA 기능을 확인 합니다. 다음 절차 여부를 확인할 수 있습니다 **로버트 Hatley** 광고 사용자 샘플 응용 프로그램에 액세스할 수 있으며이 시간을 때문에 속해 그 MFA 거치지 필요는 **금융** 그룹입니다.

1.  클라이언트 컴퓨터에 브라우저 창을 열고 샘플 응용 프로그램으로 이동: **https://webserv1.contoso.com/claimapp**합니다.

    이 작업은 federation 서버에 요청을 자동으로 리디렉션합니다 및 사용자 이름 및 암호를 사용 하 여 로그인 하 라는 메시지가 표시 됩니다.

2.  자격 증명 입력은 **로버트 Hatley** AD 계정이 합니다.

    이 시점에서 구성 된 MFA 정책으로 인해 사용자가 될 하 라는 메시지가 표시 추가 인증을 받을 합니다. 가 기본 메시지 텍스트 **보안상의 이유로 계정을 확인 하려면 추가 정보가 필요 했습니다.** 그러나이 텍스트는 완전히 사용자 지정할 수 있습니다. 로그인 환경을 사용자 지정 하는 방법에 대 한 자세한 내용은 참조 [FS 로그인 페이지 광고를 사용자 지정](https://technet.microsoft.com/library/dn280950.aspx)합니다.

    추가 인증 방법으로 인증 인증서를 구성 하는 경우 기본 메시지 텍스트는 **인증서를 인증에 사용 하 여 선택 합니다. 작업을 취소 하면 하세요 브라우저를 닫은 후 다시 시도 합니다.**

    추가 인증 방법으로 Windows Azure 다단계 인증 구성한 경우 기본 메시지 텍스트는 **전화 인증을 완료 하려면 휴대폰에 표시 됩니다.** Windows Azure 다단계 인증을 사용 하 여 로그인 및 선호 하는 인증 방법에 대 한 여러 가지 옵션을 사용 하 여에 대 한 자세한 내용은 참조 [Windows Azure 다단계 인증 개요](https://technet.microsoft.com/library/dn249479.aspx)합니다.

## <a name="see-also"></a>참조 하십시오
[중요 한 응용 프로그램에 대 한 추가 다단계 인증 위험 관리](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)
[랩 환경 ADFS Windows Server 2012 r 2에서에 대 한 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)



