---
ms.assetid: 24c4b9bb-928a-4118-acf1-5eb06c6b08e5
title: AD FS 2016 및 Azure MFA 구성
description: ''
ms.author: billmath
author: billmath
manager: mtillman
ms.date: 01/28/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: ae7809089a69ac0ff48168db0aa2e9d61c35257a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814094"
---
# <a name="configure-azure-mfa-as-authentication-provider-with-ad-fs"></a>AD FS와 함께 인증 공급자로 Azure MFA를 구성 합니다.

>적용 대상: Windows Server 2016, Windows Server 2019

Azure AD와 페더레이션 한 조직의 하는 경우 AD FS 리소스 보안에 온-프레미스 및 클라우드에서 Azure Multi-factor Authentication을 사용할 수 있습니다. Azure MFA를 사용 하면 암호를 제거 하 고 인증을 더욱 안전 하 게 제공할 수 있습니다.  Windows Server 2016부터 이제 기본 인증을 위해 Azure MFA를 구성 하거나 추가 인증 공급자로 사용 합니다. 
  
Windows Server 2012 R2에서 AD FS를 사용 하 여 AD FS 2016 Azure MFA 어댑터를 Azure AD와 직접 통합과 달리 온-프레미스 Azure MFA 서버를 사용할 필요가 없습니다.   Azure MFA 어댑터는 Windows Server 2016에 기본 제공 하 고 추가 설치 하지 않아도 됩니다.


## <a name="registering-users-for-azure-mfa-with-ad-fs"></a>AD FS와 Azure MFA에 대 한 사용자 등록

AD FS 인라인을 지원 하지 않습니다 &#34;등록 개념&#34;, 또는 모바일 앱 또는 전화 번호와 같은 Azure MFA 보안 확인 정보를 등록 합니다. 즉, 사용자가 해야 가져올 검증 했습니다를 방문 하 여 [ https://account.activedirectory.windowsazure.com/Proofup.aspx ](https://account.activedirectory.windowsazure.com/Proofup.aspx) 전에 Azure MFA를 사용 하 여 AD FS 응용 프로그램에 인증할 수 있습니다. 경우에 하지 아직 검증 했습니다를 AD FS에서 Azure MFA를 사용 하 여 인증 하려고 하는 Azure AD에서 사용자를 AD FS 오류가 받게 됩니다.  AD FS 관리자 대신 검사 페이지에 사용자를 안내 하도록 이러한 오류 환경을 사용자 지정할 수 있습니다.  AD FS 페이지 내에서 오류 메시지 문자열을 검색 하 고 사용자가 방문 하도록 안내 하는 새 메시지를 표시 하려면 onload.js 사용자 지정을 사용 하 여 수행할 수 있습니다 [ https://aka.ms/mfasetup ](https://aka.ms/mfasetup), 인증을 다시 시도 합니다. 자세한 지침은 아래의 "사용자 지정 AD FS 웹 페이지를 MFA 인증 방법을 등록 하는 사용자 가이드" 참조이 문서의.

>[!NOTE]
> 이전에 사용자가 된 등록에 대 한 MFA를 사용 하 여 인증 해야 (방문 [ https://account.activedirectory.windowsazure.com/Proofup.aspx ](https://account.activedirectory.windowsazure.com/Proofup.aspx)에서 바로 가기를 통해 예를 들어 [ https://aka.ms/mfasetup ](https://aka.ms/mfasetup)).  이제 MFA 인증 정보가 아직 등록 하지는 AD FS 사용자는 Azure AD를 액세스할 수&#34;바로 가기를 통해 검사 페이지 [ https://aka.ms/mfasetup ](https://aka.ms/mfasetup) 기본 인증만 사용 하 여 (예: Windows 통합 인증 또는 사용자 이름 및 암호를 AD FS 통해 웹 페이지).  사용자가 구성한 검증 방법 없습니다 하는 경우 Azure AD는 사용자가 메시지를 보고 하는 인라인 등록을 수행 합니다 &#34;관리자에 게이 계정에서 추가 보안 확인 설정 하는 데 필요한&#34;, 그런 다음 사용자 및 선택 하 여 &#34;지금 설정&#34;합니다.
> 검사 페이지를 방문할 때 MFA 수 있도록 구성 된 MFA 인증 방법을 하나 이상에 이미 있는 사용자를 묻는 여전히 나타납니다.

## <a name="recommended-deployment-topologies"></a>권장된 배포 토폴로지

### <a name="azure-mfa-as-primary-authentication"></a>기본 인증으로 azure MFA

AD FS 사용 하 여 기본 인증으로 Azure MFA를 사용 하는 좋은 이유 중 몇 가지가 있습니다.

 - Office 365 및 기타 AD FS 앱 로그인에 Azure AD에 암호를 방지 하려면
 - 암호를 보호 하기 위해 기반 로그인 암호를 이전 인증 코드와 같은 추가 요소를 요구 하 여

이러한 혜택을 달성 하기 위해 AD FS에서 기본 인증 방법으로 Azure MFA를 사용 하려는 경우 있습니다 수도 포함 하 여 Azure AD 조건부 액세스를 사용 하는 기능을 유지 하려면 &#34;MFA true&#34; AD FS에서 추가 요소에 대 한 메시지를 표시 하 여 합니다.

온-프레미스에서 MFA를 수행 하는 Azure AD 도메인 설정을 구성 하 여이 이제 수행할 수 있습니다 (설정 &#34;SupportsMfa&#34; $True에).  이 구성에서는 AD FS 수 하 라는 메시지가 Azure AD에서 추가 인증을 수행 하거나 &#34;MFA true&#34; 해야 하는 조건부 액세스 시나리오에 대 한 합니다.  

위에서 설명한 대로 (구성 된 MFA 인증 정보) 아직 등록 되지 않은 모든 AD FS 사용자 묻는 메시지를 통해 사용자 지정된 ADFS 오류 페이지를 방문 [ https://aka.ms/mfasetup ](https://aka.ms/mfasetup) 확인 정보를 구성 하려면 AD FS 로그인을 다시 시도 합니다.  
초기 구성을 사용자가 MFA를 요구 하는 다른 리소스에 액세스 하거나 관리 하거나 Azure AD에서 인증 정보를 업데이트 하는 추가 단계를 제공 해야 하는 후 기본으로 Azure MFA는 단일 요소를 간주 됩니다 때문에.

>[!NOTE]
> ADFS 2019를 사용 하 여 앵커 클레임 유형이 Active Directory 클레임 공급자 트러스트에 대 한 수정 및과 UPN의 windowsaccountname에서 값을 수정할 필요가 됩니다. 실행은 아래에 제공 된 powershell commandlet 아래. 이 AD FS 팜에의 내부 작동에 영향 없음. 이 변경 되 면 자격 증명에 대 한 소수의 사용자를 reprompted 수를 확인할 수 있습니다. 다시 로그인 한 후 최종 사용자에 게는 아무런 차이가 표시 됩니다. 

```powershell
Set-AdfsClaimsProviderTrust -AnchorClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn" -TargetName "Active Directory"
```

### <a name="azure-mfa-as-additional-authentication-to-office-365"></a>Office 365에 추가 인증으로 azure MFA

이전에 하도록 하려는 경우 Azure MFA AD FS에서 추가 인증 방법: Office 365 또는 다른 신뢰 당사자, 가장 적합 한 옵션에 대 한 MFA를 온-프레미스 AD FS와 MFA를 수행 되는 기본 인증을 복합 수행 하려면 Azure AD를 구성 하는 것 이었습니다는 tr Azure AD에서 iggered 합니다. 이제 도메인 SupportsMfa 설정을 $True로 설정 된 경우 AD FS에서 추가 인증으로 Azure MFA를 사용할 수 있습니다.  

위에서 설명한 대로 (구성 된 MFA 인증 정보) 아직 등록 되지 않은 모든 AD FS 사용자 묻는 메시지를 통해 사용자 지정된 ADFS 오류 페이지를 방문 [ https://aka.ms/mfasetup ](https://aka.ms/mfasetup) 확인 정보를 구성 하려면 AD FS 로그인을 다시 시도 합니다.  

## <a name="pre-requisites"></a>필수 구성 요소

AD fs 인증을 위해 Azure MFA를 사용 하는 경우 다음 필수 조건이 필요 합니다.  
  
- [Azure Active Directory와 Azure 구독](https://azure.microsoft.com/pricing/free-trial/)합니다.  
- [Azure Multi-factor Authentication](https://azure.microsoft.com/documentation/articles/multi-factor-authentication/)  
- 웹 앱 프록시는 포트 80 및 443을 통해 다음을 사용 하 여 communticate 수

    - https://adnotifications.windowsazure.com
    - https://login.microsoftonline.com


> [!NOTE]
> Azure AD와 Azure MFA는 Azure AD Premium 및 Enterprise Mobility Suite (EMS)에 포함 됩니다.  이러한 경우에 개별 구독을 설치할 필요가 없습니다.
- Windows Server 2016 AD FS 온-프레미스 환경입니다.  
   - 서버 포트 80 및 443을 통해 다음 Url과 통신할 수 있어야 합니다.
      - https://adnotifications.windowsazure.com
      - https://login.microsoftonline.com
- 온-프레미스 환경이 [Azure AD와 페더레이션 합니다.](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-get-started-custom/#configuring-federation-with-ad-fs)  
- [Windows PowerShell 용 Windows Azure Active Directory 모듈](https://docs.microsoft.com/powershell/module/Azuread/?view=azureadps-2.0)합니다.  
- Azure AD PowerShell을 사용 하 여 구성에 Azure AD 인스턴스를 전역 관리자 권한이 있습니다.  
- Azure MFA에 대 한 AD FS 팜을 구성 하려면 엔터프라이즈 관리자 자격 증명입니다.  
  
## <a name="configure-the-ad-fs-servers"></a>AD FS 서버를 구성 합니다.

AD FS에 대 한 Azure MFA에 대 한 구성을 완료 하기 위해 설명 된 단계를 사용 하 여 각 AD FS 서버를 구성 해야 합니다. 

>[!NOTE]
>이 단계에서 수행 되는 확인 **모든** 팜의 AD FS 서버입니다. 팜에 여러 AD FS 서버를 설정한 경우에 Azure AD Powershell을 사용 하 여 원격 필요한 구성을 수행할 수 있습니다.  

### <a name="step-1-generate-a-certificate-for-azure-mfa-on-each-ad-fs-server-using-the-new-adfsazuremfatenantcertificate-cmdlet"></a>1단계: Azure MFA에 대 한 인증서를 사용 하 여 각 AD FS 서버에서 생성 된 `New-AdfsAzureMfaTenantCertificate` cmdlet

가장 먼저 해야 할 인증서를 사용 하 여 Azure MFA에 대 한 생성 됩니다.  이렇게 하려면 PowerShell을 사용 합니다.  로컬 컴퓨터 인증서 저장소에 생성 된 인증서를 찾을 수 및 Azure AD 디렉터리의 TenantID를 포함 하는 주체 이름으로 표시 되어 있습니다.

![AD FS와 MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA3.png)  

TenantID Azure AD에서 디렉터리의 이름의 않음을 유의 하십시오.  다음 PowerShell cmdlet를 사용 하 여 새 인증서를 생성 합니다.  
    `$certbase64 = New-AdfsAzureMfaTenantCertificate -TenantID <tenantID>`  

![AD FS와 MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA1.PNG)  
  
### <a name="step-2-add-the-new-credentials-to-the-azure-multi-factor-auth-client-service-principal"></a>2단계: 새 자격 증명을 Azure Multi-factor Auth 클라이언트의 서비스 주체 추가

Azure Multi-factor Auth 클라이언트와 통신 하는 AD FS 서버를 사용 하도록 설정 하기 위해 Azure Multi-factor Auth 클라이언트에 대 한 서비스 주체에 자격 증명을 추가 해야 합니다. 사용 하 여 생성 된 인증서는 `New-AdfsAzureMFaTenantCertificate` cmdlet이 자격이 증명으로 사용 합니다. 다음을 수행 PowerShell를 사용 하 여 새 자격 증명을 Azure Multi-factor Auth 클라이언트의 서비스 주체를 추가 합니다.  

> [!NOTE]
> 이 단계를 완료 하기 위해 powershell Connect-msolservice를 사용 하 여 Azure AD의 인스턴스에 연결 해야 합니다.  이 단계에서는 PowerShell을 통해 이미 연결 되어 가정 합니다.  정보를 참조 하십시오. [Connect-msolservice 합니다.](https://msdn.microsoft.com/library/dn194123.aspx)  

**Azure Multi-factor Auth 클라이언트에 대 한 새 자격 증명으로 인증서를 설정**  

`New-MsolServicePrincipalCredential -AppPrincipalId 981f26a1-7f43-403b-a875-f8b09b8cd720 -Type asymmetric -Usage verify -Value $certBase64`

> [!IMPORTANT]
> 이 명령은 모든 팜의 AD FS 서버에서 실행 해야 합니다.  Azure AD MFA는 Azure Multi-factor Auth 클라이언트에 대 한 새 자격 증명으로 설정 된 인증서가 있는 서버에서 실패 합니다.

> [!NOTE]  
> 981f26a1-7f43-403b-a875-f8b09b8cd720에 Azure Multi-factor Auth 클라이언트에 대 한 GUID입니다.  
  
## <a name="configure-the-ad-fs-farm"></a>AD FS 팜 구성  
  
각 AD FS 서버에서 이전 섹션을 완료 한 후 실행 해야 합니다는 `Set-AdfsAzureMfaTenant` cmdlet입니다.  
  
이 cmdlet은 AD FS 팜에 대해 한 번만 실행 해야 합니다.  PowerShell을 사용 하 여이 단계를 완료 합니다.
  
> [!NOTE]  
> 이러한 변경 내용이 적용 되기 전에 팜의 각 서버에서 AD FS 서비스를 다시 시작 해야 합니다.  
  
    Set-AdfsAzureMfaTenant -TenantId <tenant ID> -ClientId 981f26a1-7f43-403b-a875-f8b09b8cd720  

![AD FS와 MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA5.png)  
  
그런 다음 Azure MFA를 인트라넷 및 엑스트라넷 사용에 대 한 기본 인증 방법으로 사용할 수 있는지 표시 됩니다.    
  
![AD FS와 MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA6.png)  

## <a name="renew-and-manage-ad-fs-azure-mfa-certificates"></a>갱신 하 고 관리할 AD FS Azure MFA 인증서

다음 지침에서는 AD FS 서버에서 Azure MFA 인증서를 관리 하는 방법을 안내 합니다.
기본적으로 Azure MFA를 사용 하 여 AD FS를 구성한 경우 AdfsAzureMfaTenantCertificate 새로 만들기 PowerShell cmdlet을 통해 생성 된 인증서는 올바른 2 년 동안.  닫기에 어떻게 결정할 만료 인증서, 되며 다음 갱신을 새 인증서를 설치 하려면 다음 절차를 따르십시오.

### <a name="assess-ad-fs-azure-mfa-certificate-expiration-date"></a>AD FS Azure MFA 인증서 만료 날짜를 평가 합니다.

각 AD FS 서버의 로컬 컴퓨터에서 내 저장소를 사용 하 여 자체 서명 된 인증서를 됩니다 &#34;OU = Microsoft AD FS Azure MFA&#34; 발급자 및 주체.  Azure MFA 인증서입니다.  만료 날짜를 확인 하려면 각 AD FS 서버에서이 인증서의 유효 기간을 확인 합니다.  

### <a name="create-new-ad-fs-azure-mfa-certificate-on-each-ad-fs-server"></a>각 AD FS 서버에서 새 AD FS Azure MFA 인증서 만들기

인증서의 유효 기간, 곧 해당 종료 하는 경우 각 AD FS 서버에서 새 Azure MFA 인증서를 생성 하 여 갱신 프로세스를 시작 합니다. Powershell 명령 창에서 다음 cmdlet을 사용 하 여 각 AD FS 서버에서 새 인증서를 생성 합니다.

```
PS C:\> $newcert = New-AdfsAzureMfaTenantCertificate -TenantId <tenant id such as contoso.onmicrosoft.com> -Renew $true
```

이 cmdlet의 결과로 2 일 + 2 년으로 앞으로 2 일 동안에서 유효한 새 인증서를 생성 됩니다.  이 cmdlet 또는 새 인증서를 Azure MFA 및 AD FS 작업을 받지 않습니다. (참고: 2 일 지연 하기 위해 의도 된 및 AD FS를 사용 하 여 Azure MFA에 대 한 시작 하기 전에 테 넌 트에 새 인증서를 구성 하려면 다음 단계를 실행 하는 시간을 제공 합니다.)

### <a name="configure-each-new-ad-fs-azure-mfa-certificate-in-the-azure-ad-tenant"></a>Azure AD 테 넌 트에서 각 새 AD FS Azure MFA 인증서를 구성 합니다.

다음과 같이 Azure AD 테 넌 트 설정을 업데이트 (각 AD FS 서버에서), 각 새 인증서에 대 한 Azure AD PowerShell 모듈을 사용 하 여 (참고: Connect-msolservice를 사용 하 여 다음 명령을 실행 하는 테 넌 트에 먼저 연결 해야 합니다).

```
PS C:/> New-MsolServicePrincipalCredential -AppPrincipalId 981f26a1-7f43-403b-a875-f8b09b8cd720 -Type Asymmetric -Usage Verify -Value $newcert
```

$certbase64 새 인증서입니다.  Base64로 인코딩된 인증서를 DER 인코딩 파일 notepad.exe를 열고 다음 PSH 세션에 복사/붙여넣기 및 $certbase64 변수에 할당 (개인 키)가 없는 인증서를 내보내고 가져올 수 있습니다.

### <a name="verify-that-the-new-certificates-will-be-used-for-azure-mfa"></a>Azure MFA에 대 한 새 인증서를 사용할지를 확인 합니다.

새 인증서를 유효 하 게 되 면 AD FS를 집어 몇 시간 내에서 Azure MFA에 대 한 각 해당 인증서를 사용 하 여 시작 합니다.  이 문제가 발생 한 후 각 서버에서 다음 정보를 사용 하 여 AD FS 관리자 이벤트 로그에 기록 된 이벤트를 표시 됩니다. 로그 이름:      AD F s/관리자 원본:        AD FS 날짜:          2018 년 2 월 27 오후 7시 33분: 31 이벤트 ID:      547 작업 범주: None 수준:         정보 키워드:      AD FS 사용자:          DOMAIN\adfssvc 컴퓨터:      ADFS.domain.contoso.com Description: Azure MFA에 대 한 테 넌 트 인증서 갱신 되었습니다.  

TenantId: contoso.onmicrosoft.com.
이전 지문: 7CC103D60967318A11D8C51C289EF85214D9FC63.
이전 만료 날짜: 9/15/2019 9:43:17 PM.
새 지문: 8110D7415744C9D4D5A4A6309499F7B48B5F3CCF.
새 만료 날짜: 2020 27/2/2시 16분: 07 AM입니다.

## <a name="customize-the-ad-fs-web-page-to-guide-users-to-register-mfa-verification-methods"></a>MFA 인증 메서드를 등록할 사용자를 AD FS 웹 페이지 사용자 지정

다음 예에서는 등록 아직 검증 했습니다 없습니다가 사용자에 대 한 AD FS 웹 페이지에 맞게 (정보를 구성 MFA 확인)를 사용 합니다.

### <a name="find-the-error"></a>오류를 찾으려면

먼저, AD FS는 사용자는 인증 정보에 게 없는 경우에 반환 하는 다른 오류 메시지의 두 가지가 있습니다.
Azure MFA를 기본 인증을 사용 하는 경우 proofed 되지 않은 사용자는 다음 메시지가 포함 된 AD FS 오류 페이지가 나타납니다.
```
    <div id="errorArea">
        <div id="openingMessage" class="groupMargin bigText">
            An error occurred
        </div>
        <div id="errorMessage" class="groupMargin">
            Authentication attempt failed. Select a different sign in option or close the web browser and sign in again. Contact your administrator for more information.
        </div>
```
추가 인증으로 Azure AD를 시도 중인 proofed 되지 않은 사용자는 다음 메시지를 포함 하는 ADFS 오류 페이지를 나타납니다.
```
<div id='mfaGreetingDescription' class='groupMargin'>For security reasons, we require additional information to verify your account (mahesh@jenfield.net)</div>
    <div id="errorArea">
        <div id="openingMessage" class="groupMargin bigText">
            An error occurred
        </div>
        <div id="errorMessage" class="groupMargin">
            The selected authentication method is not available for &#39;username@contoso.com&#39;. Choose another authentication method or contact your system administrator for details.
        </div>
```

### <a name="catch-the-error-and-update-the-page-text"></a>오류를 catch 하 고 페이지 텍스트를 업데이트 합니다.

오류를 catch 하 고 사용자에 게 표시 하려면 사용자 지정 지침의 AD FS 웹 테마를 일부인 onload.js 파일의 끝에 javascript 단순히 추가 합니다.  이 옵션을 사용 하면 다음을 수행할 수 있습니다.
 - 식별 오류 문자열 검색
 - 사용자 지정 웹 콘텐츠를 제공 합니다.  

(Onload.js 파일을 사용자 지정 하는 방법에 대 한 일반 지침은, 문서를 참조 [Advanced Customization of AD FS 로그인 페이지](advanced-customization-of-ad-fs-sign-in-pages.md).)

다음은 간단한 예제, 확장 하는 것이 좋습니다.

1. 기본 AD FS 서버에서 Windows PowerShell을 열고 다음 명령을 실행 하 여 새 AD FS 웹 테마를 만듭니다.
    
    ``` PowerShell
        New-AdfsWebTheme –Name ProofUp –SourceName default
    ``` 
2. 그런 다음 기본 AD FS 웹 테마를 내보냅니다.

    ``` PowerShell
       Export-AdfsWebTheme –Name default –DirectoryPath c:\Theme
    ```
3. 텍스트 편집기에서 C:\Theme\script\onload.js 파일을 엽니다.
4. Onload.js 파일의 끝에 다음 코드를 추가 합니다.
    
    ``` JavaScript
    //Custom Code
    //Customize MFA exception
    //Begin

    var domain_hint = "<YOUR_DOMAIN_NAME_HERE>";
    var mfaSecondFactorErr = "The selected authentication method is not available for";
    var mfaProofupMessage = "You will be automatically redirected in 5 seconds to set up your account for additional security verification. Once you have completed the setup, please return to the application you are attempting to access.<br><br>If you are not redirected automatically, please click <a href='{0}'>here</a>."
    var authArea = document.getElementById("authArea");
    if (authArea) {
        var errorMessage = document.getElementById("errorMessage");
        if (errorMessage.innerHTML.indexOf(mfaSecondFactorErr) >= 0) {

        //Hide the error message
            var openingMessage = document.getElementById("openingMessage");
            if (openingMessage) {
                openingMessage.style.display = 'none'
            }
            var errorDetailsLink = document.getElementById("errorDetailsLink");
            if (errorDetailsLink) {
                errorDetailsLink.style.display = 'none'
            }

            //Provide a message and redirect to Azure AD MFA Registration Url
            var mfaRegisterUrl = "https://account.activedirectory.windowsazure.com/proofup.aspx?proofup=1&whr=" + domain_hint;
            errorMessage.innerHTML = "<br>" + mfaProofupMessage.replace("{0}", mfaRegisterUrl);
            window.setTimeout(function () { window.location.href = mfaRegisterUrl; }, 5000);
        }
    }

    //End Customize MFA Exception
    //End Custom Code
    ```
    > [!IMPORTANT]
    > "< YOUR_DOMAIN_NAME_HERE >"; 변경 해야 합니다. 에 도메인 이름을 사용 합니다. 예: `var domain_hint = "contoso.com";`
    
5. Onload.js 파일 저장
6. 다음 Windows PowerShell 명령을 입력 하 여 사용자 지정 테마를 onload.js 파일을 가져옵니다.
    
    ``` PowerShell
    Set-AdfsWebTheme -TargetName ProofUp -AdditionalFileResource @{Uri=’/adfs/portal/script/onload.js’;path="c:\theme\script\onload.js"}
    ```
7. 마지막으로 다음 Windows PowerShell 명령을 입력 하 여 사용자 지정 AD FS 웹 테마를 적용 합니다.
    
    ``` PowerShell
    Set-AdfsWebConfig -ActiveThemeName
    ```

## <a name="next-steps"></a>다음 단계

[TLS/SSL 프로토콜 및 AD FS 및 Azure MFA 사용 되는 암호 그룹 관리](manage-ssl-protocols-in-ad-fs.md)
