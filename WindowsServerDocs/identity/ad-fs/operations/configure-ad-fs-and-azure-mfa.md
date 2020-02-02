---
ms.assetid: 24c4b9bb-928a-4118-acf1-5eb06c6b08e5
title: AD FS 2016 및 Azure MFA 구성
description: ''
ms.author: billmath
author: billmath
manager: mtillman
ms.date: 01/28/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: a4f9d8fa71671c4ad4651008729d4cee53c8ee2f
ms.sourcegitcommit: 74107a32efe1e53b36c938166600739a79dd0f51
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "76918255"
---
# <a name="configure-azure-mfa-as-authentication-provider-with-ad-fs"></a>AD FS를 사용 하 여 Azure MFA를 인증 공급자로 구성

조직이 Azure AD와 페더레이션 되는 경우 Azure Multi-Factor Authentication를 사용 하 여 온-프레미스와 클라우드에서 AD FS 리소스를 보호할 수 있습니다. Azure MFA를 사용 하면 암호를 제거 하 고 보다 안전한 인증 방법을 제공할 수 있습니다.  이제 Windows Server 2016부터 기본 인증을 위해 Azure MFA를 구성 하거나 추가 인증 공급자로 사용할 수 있습니다. 
  
Windows Server 2012 r 2의 AD FS와 달리 AD FS 2016 Azure MFA 어댑터는 Azure AD와 직접 통합 되며 온-프레미스 Azure MFA 서버가 필요 하지 않습니다.   Azure MFA 어댑터는 Windows Server 2016에 기본 제공 되며 추가 설치는 필요 하지 않습니다.


## <a name="registering-users-for-azure-mfa-with-ad-fs"></a>AD FS를 사용 하 여 Azure MFA에 사용자 등록

AD FS는 전화 번호 또는 &#34;모바일 앱&#34;과 같은 Azure MFA 보안 확인 정보를 인라인 증명 또는 등록 하는 기능을 지원 하지 않습니다. 즉, 사용자는 Azure MFA를 사용 하 여 AD FS 응용 프로그램에 인증 하기 전에 [https://account.activedirectory.windowsazure.com/Proofup.aspx](https://account.activedirectory.windowsazure.com/Proofup.aspx) 를 방문 하 여 proofed을 받아야 합니다. Azure AD에서 아직 proofed 되지 않은 사용자가 AD FS에서 Azure MFA를 사용 하 여 인증 하려고 하면 AD FS 오류가 발생 합니다.  AD FS 관리자는이 오류 환경을 사용자 지정 하 여 사용자가 대신 검사 페이지를 안내할 수 있습니다.  이 작업은 onload 사용자 지정을 사용 하 여 AD FS 페이지 내의 오류 메시지 문자열을 검색 하 고 새 메시지를 표시 하 여 사용자가 [https://aka.ms/mfasetup](https://aka.ms/mfasetup)를 방문한 다음 인증을 다시 시도할 수 있도록 안내 합니다. 자세한 지침은이 문서 아래에 있는 "사용자에 게 MFA 확인 방법 등록을 안내 하는 AD FS 웹 페이지 사용자 지정"을 참조 하세요.

>[!NOTE]
> 이전에는 사용자가 등록을 위해 MFA를 사용 하 여 인증 해야 했습니다 (예: 바로 가기 [https://aka.ms/mfasetup](https://aka.ms/mfasetup)를 통해 [https://account.activedirectory.windowsazure.com/Proofup.aspx](https://account.activedirectory.windowsazure.com/Proofup.aspx)).  이제 아직 MFA 확인 정보를 등록 하지 않은 AD FS 사용자는 기본 인증 (예:&#34;Windows 통합 인증 또는 AD FS 웹 페이지를 통해 사용자 이름 및 암호)만 사용 하 여 바로 가기 [https://aka.ms/mfasetup](https://aka.ms/mfasetup) 를 통해 Azure AD s 검사 페이지에 액세스할 수 있습니다.  사용자에 게 확인 방법이 구성 되어 있지 않은 경우 Azure AD는 사용자가 &#34;추가 보안 확인&#34;을 위해이 계정을 설정 하는 데 필요한 메시지를 표시 하는 인라인 등록을 수행 하 고, 사용자는 지금 &#34;&#34;설정 하도록 선택할 수 있습니다.
> 이미 하나 이상의 MFA 확인 방법을 구성 하는 사용자에 게는 검사 페이지를 방문할 때 MFA를 제공 하 라는 메시지가 표시 됩니다.

## <a name="recommended-deployment-topologies"></a>권장 배포 토폴로지

### <a name="azure-mfa-as-primary-authentication"></a>기본 인증으로 Azure MFA

AD FS를 사용 하 여 기본 인증으로 Azure MFA를 사용 하는 몇 가지 좋은 이유가 있습니다.

 - Azure AD에 대 한 로그인에 대 한 암호를 방지 하려면 Office 365 및 기타 AD FS 앱
 - 암호 이전에 확인 코드와 같은 추가 요소를 요구 하 여 암호 기반 로그인을 보호 하려면

이러한 혜택을 얻기 위해 AD FS의 기본 인증 방법으로 Azure MFA를 사용 하려는 경우 AD FS에서 추가 요소를 확인 하 여 진정한 MFA &#34;&#34; 를 비롯 한 azure AD 조건부 액세스를 사용 하는 기능을 유지할 수도 있습니다.

이제 온-프레미스에서 MFA를 수행 하도록 Azure AD 도메인 설정을 구성 하 여이 작업을 &#34;수행할 수 있습니다&#34; ($True supportsmfa 설정).  이 구성에서는 Azure AD에서이를 요구 하는 조건부 액세스 시나리오에 대 &#34;한 추가&#34; 인증 또는 진정한 MFA를 수행 하 라는 메시지를 AD FS 수 있습니다.  

위에서 설명한 것 처럼, 아직 등록 하지 않은 모든 AD FS 사용자 (MFA 확인 정보 구성)를 사용 [https://aka.ms/mfasetup](https://aka.ms/mfasetup) 하 여 사용자 지정 된 AD FS 오류 페이지를 통해 확인 정보를 구성한 다음 로그인 AD FS 다시 시도 하 라는 메시지가 표시 되어야 합니다.  
Azure MFA는 단일 요소로 간주 되므로 초기 구성 후 사용자는 Azure AD에서 인증 정보를 관리 또는 업데이트 하는 추가 요소를 제공 하거나 MFA를 요구 하는 다른 리소스에 액세스 해야 합니다.

>[!NOTE]
> ADFS 2019을 사용 하면 Active Directory 클레임 공급자 트러스트에 대 한 앵커 클레임 유형을 수정 하 고 windowsaccountname에서 UPN으로 수정 해야 합니다. 아래 제공 된 PowerShell cmdlet을 실행 합니다. 이는 AD FS 팜의 내부 기능에는 영향을 주지 않습니다. 이러한 변경이 수행 되 면 몇 명의 사용자에 게 자격 증명을 다시 입력 하 라는 메시지가 표시 될 수 있습니다. 다시 로그인 한 후에는 최종 사용자에 게 차이가 없다는 것을 볼 수 있습니다. 

```powershell
Set-AdfsClaimsProviderTrust -AnchorClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn" -TargetName "Active Directory"
```

### <a name="azure-mfa-as-additional-authentication-to-office-365"></a>Office 365에 대 한 추가 인증으로 서의 Azure MFA

이전에는 Office 365 또는 기타 신뢰 당사자에 대 한 AD FS에서 Azure MFA를 추가 인증 방법으로 사용할 수 있도록 하는 것이 가장 좋습니다. 복합 MFA를 수행 하도록 Azure AD를 구성 하는 것입니다 .이는 기본 인증이 AD FS에서 온-프레미스에서 수행 되 고 MFA는 tr입니다. Azure AD의 iggered 이제 도메인 지원 Smfa 설정이 $True으로 설정 된 경우 AD FS에서 Azure MFA를 추가 인증으로 사용할 수 있습니다.  

위에서 설명한 것 처럼, 아직 등록 하지 않은 모든 AD FS 사용자 (MFA 확인 정보 구성)를 사용 [https://aka.ms/mfasetup](https://aka.ms/mfasetup) 하 여 사용자 지정 된 AD FS 오류 페이지를 통해 확인 정보를 구성한 다음 로그인 AD FS 다시 시도 하 라는 메시지가 표시 되어야 합니다.  

## <a name="pre-requisites"></a>필수 구성 요소

AD fs 인증을 위해 Azure MFA를 사용 하는 경우 다음 필수 조건이 필요 합니다.  
  
- [Azure Active Directory와 Azure 구독](https://azure.microsoft.com/pricing/free-trial/)합니다.  
- [Azure Multi-Factor Authentication](https://azure.microsoft.com/documentation/articles/multi-factor-authentication/) 


> [!NOTE]
> Azure AD와 Azure MFA는 Azure AD Premium 및 Enterprise Mobility Suite (EMS)에 포함 됩니다.  이러한 경우에 개별 구독을 설치할 필요가 없습니다.

- Windows Server 2016 AD FS 온-프레미스 환경입니다.  
   - 서버는 443 포트를 통해 다음 Url과 통신할 수 있어야 합니다.
      - https://adnotifications.windowsazure.com
      - https://login.microsoftonline.com
- 온-프레미스 환경이 [Azure AD와 페더레이션 합니다.](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-get-started-custom/#configuring-federation-with-ad-fs)  
- [Windows PowerShell 용 Windows Azure Active Directory 모듈](https://docs.microsoft.com/powershell/module/Azuread/?view=azureadps-2.0)합니다.  
- Azure AD PowerShell을 사용 하 여 구성에 Azure AD 인스턴스를 전역 관리자 권한이 있습니다.  
- Azure MFA에 대 한 AD FS 팜을 구성 하려면 엔터프라이즈 관리자 자격 증명입니다.

## <a name="configure-the-ad-fs-servers"></a>AD FS 서버를 구성 합니다.

AD FS에 대 한 Azure MFA에 대 한 구성을 완료 하기 위해 설명 된 단계를 사용 하 여 각 AD FS 서버를 구성 해야 합니다. 

>[!NOTE]
>이 단계에서 수행 되는 확인 **모든** 팜의 AD FS 서버입니다. 팜에 여러 AD FS 서버가 있는 경우 Azure AD PowerShell을 사용 하 여 필요한 구성을 원격으로 수행할 수 있습니다.  

### <a name="step-1-generate-a-certificate-for-azure-mfa-on-each-ad-fs-server-using-the-new-adfsazuremfatenantcertificate-cmdlet"></a>1 단계: `New-AdfsAzureMfaTenantCertificate` cmdlet을 사용 하 여 각 AD FS 서버에서 Azure MFA에 대 한 인증서 생성

가장 먼저 해야 할 인증서를 사용 하 여 Azure MFA에 대 한 생성 됩니다.  이렇게 하려면 PowerShell을 사용 합니다.  로컬 컴퓨터 인증서 저장소에 생성 된 인증서를 찾을 수 및 Azure AD 디렉터리의 TenantID를 포함 하는 주체 이름으로 표시 되어 있습니다.

![AD FS와 MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA3.png)  

TenantID Azure AD에서 디렉터리의 이름의 않음을 유의 하십시오.  다음 PowerShell cmdlet를 사용 하 여 새 인증서를 생성 합니다.  
    `$certbase64 = New-AdfsAzureMfaTenantCertificate -TenantID <tenantID>`  

![AD FS와 MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA1.PNG)  
  
### <a name="step-2-add-the-new-credentials-to-the-azure-multi-factor-auth-client-service-principal"></a>2 단계: Azure Multi-factor Auth 클라이언트 서비스 주체에 새 자격 증명 추가

AD FS 서버가 Azure Multi-factor Auth 클라이언트와 통신할 수 있도록 하려면 Azure Multi-factor Auth 클라이언트에 대 한 서비스 주체에 자격 증명을 추가 해야 합니다. 사용 하 여 생성 된 인증서는 `New-AdfsAzureMFaTenantCertificate` cmdlet이 자격이 증명으로 사용 합니다. PowerShell을 사용 하 여 Azure Multi-factor Auth 클라이언트 서비스 주체에 새 자격 증명을 추가 하려면 다음을 수행 합니다.  

> [!NOTE]
> 이 단계를 완료 하려면 `Connect-MsolService`을 사용 하 여 PowerShell을 사용 하 여 Azure AD의 인스턴스에 연결 해야 합니다.  이 단계에서는 PowerShell을 통해 이미 연결 되어 가정 합니다.  자세한 내용은`Connect-MsolService`를 참조 [하세요.](https://msdn.microsoft.com/library/dn194123.aspx)  

**Azure Multi-factor Auth 클라이언트에 대 한 새 자격 증명으로 인증서를 설정 합니다.**  

`New-MsolServicePrincipalCredential -AppPrincipalId 981f26a1-7f43-403b-a875-f8b09b8cd720 -Type asymmetric -Usage verify -Value $certBase64`

> [!IMPORTANT]
> 팜의 모든 AD FS 서버에서이 명령을 실행 해야 합니다.  Azure Multi-factor Auth 클라이언트에 대 한 새 자격 증명으로 설정 된 인증서가 없는 서버에서 azure AD MFA가 실패 합니다.

> [!NOTE]  
> 981f26a1-7f43-403b-a875-f8b09b8cd720는 Azure Multi-factor Auth 클라이언트에 대 한 GUID입니다.  
  
## <a name="configure-the-ad-fs-farm"></a>AD FS 팜 구성  
  
각 AD FS 서버에서 이전 섹션을 완료 한 후에는 [AdfsAzureMfaTenant](https://docs.microsoft.com/powershell/module/adfs/export-adfsauthenticationproviderconfigurationdata) cmdlet을 사용 하 여 Azure 테 넌 트 정보를 설정 합니다. 이 cmdlet은 AD FS 팜에 대해 한 번만 실행 해야 합니다.

PowerShell 프롬프트를 열고 [AdfsAzureMfaTenant](https://docs.microsoft.com/powershell/module/adfs/export-adfsauthenticationproviderconfigurationdata) cmdlet을 사용 하 여 사용자 고유의 *tenantId* 를 입력 합니다. Microsoft Azure Government 클라우드를 사용 하는 고객의 경우 `-Environment USGov` 매개 변수를 추가 합니다.

> [!NOTE]
> 이러한 변경 내용을 적용 하려면 팜의 각 서버에서 AD FS 서비스를 다시 시작 해야 합니다. 최소 영향을 위해 각 AD FS 서버를 NLB 회전에서 한 번에 하나씩 가져와 모든 연결이 드레이닝 될 때까지 기다립니다.

```powershell
Set-AdfsAzureMfaTenant -TenantId <tenant ID> -ClientId 981f26a1-7f43-403b-a875-f8b09b8cd720
```

![AD FS와 MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA5.png)

최신 Service Pack 없는 Windows Server는 [AdfsAzureMfaTenant](https://docs.microsoft.com/powershell/module/adfs/export-adfsauthenticationproviderconfigurationdata) cmdlet에 대 한 `-Environment` 매개 변수를 지원 하지 않습니다. Azure Government 클라우드를 사용 하 고 이전 단계에서 `-Environment` 매개 변수가 누락 되어 Azure 테 넌 트를 구성 하지 못한 경우 다음 단계를 완료 하 여 레지스트리 항목을 수동으로 만듭니다. 이전 cmdlet이 테 넌 트 정보를 올바르게 등록 했거나 Azure Government 클라우드에 있지 않은 경우 다음 단계를 건너뜁니다.

1. AD FS 서버에서 **레지스트리 편집기** 를 엽니다.
1. `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ADFS`으로 이동합니다. 다음 레지스트리 키 값을 만듭니다.

    | 레지스트리 키       | Value |
    |--------------------|-----------------------------------|
    | SasUrl             | https://adnotifications.windowsazure.us/StrongAuthenticationService.svc/Connector |
    | StsUrl             | https://login.microsoftonline.us |
    | ResourceUri        | https://adnotifications.windowsazure.us/StrongAuthenticationService.svc/Connector |

1. 팜의 각 서버에서 AD FS 서비스를 다시 시작 해야 변경 내용이 적용 됩니다. 최소 영향을 위해 각 AD FS 서버를 NLB 회전에서 한 번에 하나씩 가져와 모든 연결이 드레이닝 될 때까지 기다립니다.

그런 다음 Azure MFA를 인트라넷 및 엑스트라넷 사용에 대 한 기본 인증 방법으로 사용할 수 있는지 표시 됩니다.

![AD FS와 MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA6.png)  

## <a name="renew-and-manage-ad-fs-azure-mfa-certificates"></a>AD FS Azure MFA 인증서 갱신 및 관리

다음 지침에서는 AD FS 서버에서 Azure MFA 인증서를 관리 하는 방법을 안내 합니다.
기본적으로 Azure MFA를 사용 하 여 AD FS를 구성 하는 경우 `New-AdfsAzureMfaTenantCertificate` PowerShell cmdlet을 통해 생성 된 인증서는 2 년 동안 유효 합니다.  인증서가 만료 되는 정도를 확인 한 다음 새 인증서를 갱신 하 고 설치 하려면 다음 절차를 따르십시오.

### <a name="assess-ad-fs-azure-mfa-certificate-expiration-date"></a>Azure MFA 인증서 만료 날짜 AD FS 평가

각 AD FS 서버에서 로컬 컴퓨터 내 저장소에는 발급자와 주체에 OU = Microsoft AD FS Azure MFA &#34;&#34; 를 포함 하는 자체 서명 된 인증서가 있습니다.  Azure MFA 인증서입니다.  각 AD FS 서버에서이 인증서의 유효 기간을 확인 하 여 만료 날짜를 확인 합니다.  

### <a name="create-new-ad-fs-azure-mfa-certificate-on-each-ad-fs-server"></a>각 AD FS 서버에 새 AD FS Azure MFA 인증서 만들기

인증서의 유효 기간이 끝에 가까워지면 각 AD FS 서버에서 새 Azure MFA 인증서를 생성 하 여 갱신 프로세스를 시작 합니다. PowerShell 명령 창에서 다음 cmdlet을 사용 하 여 각 AD FS 서버에 새 인증서를 생성 합니다.

```
PS C:\> $newcert = New-AdfsAzureMfaTenantCertificate -TenantId <tenant id such as contoso.onmicrosoft.com> -Renew $true
```

이 cmdlet의 결과로, 향후 2 일에서 2 년까지 유효한 새 인증서가 생성 됩니다.  AD FS 및 Azure MFA 작업은이 cmdlet 또는 새 인증서의 영향을 받지 않습니다. (참고: 2 일 지연은 의도적인 것 이며, Azure MFA에 대 한 사용을 시작 AD FS 하기 전에 테 넌 트에서 새 인증서를 구성 하기 위해 다음 단계를 실행 하는 시간을 제공 합니다.)

### <a name="configure-each-new-ad-fs-azure-mfa-certificate-in-the-azure-ad-tenant"></a>Azure AD 테 넌 트에서 새로운 새 AD FS Azure MFA 인증서를 구성 합니다.

Azure AD PowerShell 모듈을 사용 하 여 각 AD FS 서버의 새 인증서에 대해 다음과 같이 Azure AD 테 넌 트 설정을 업데이트 합니다 (참고: 다음 명령을 실행 하려면 먼저 `Connect-MsolService`를 사용 하 여 테 넌 트에 연결 해야 함).

```
PS C:/> New-MsolServicePrincipalCredential -AppPrincipalId 981f26a1-7f43-403b-a875-f8b09b8cd720 -Type Asymmetric -Usage Verify -Value $newcert
```

새 인증서가 `$certbase64` 됩니다.  Base64 인코딩 인증서는 개인 키 없이 인증서를 DER로 인코딩된 파일로 내보내고 메모장에서 연 다음 PowerShell 세션에 복사/붙여넣기 하 고 변수 `$certbase64`에 할당 하 여 가져올 수 있습니다.

### <a name="verify-that-the-new-certificates-will-be-used-for-azure-mfa"></a>새 인증서가 Azure MFA에 사용 되는지 확인 합니다.

새 인증서가 유효 하면 몇 시간 이내에 Azure MFA에 대 한 각 인증서를 선택 하 고 시작 하 AD FS 합니다.  이 문제가 발생 하면 각 서버에서 다음 정보를 사용 하 여 AD FS Admin 이벤트 로그에 기록 된 이벤트를 볼 수 있습니다.

```
Log Name:      AD FS/Admin
Source:        AD FS
Date:          2/27/2018 7:33:31 PM
Event ID:      547
Task Category: None
Level:         Information
Keywords:      AD FS
User:          DOMAIN\adfssvc
Computer:      ADFS.domain.contoso.com
Description:
The tenant certificate for Azure MFA has been renewed.  

TenantId: contoso.onmicrosoft.com.
Old thumbprint: 7CC103D60967318A11D8C51C289EF85214D9FC63.
Old expiration date: 9/15/2019 9:43:17 PM.
New thumbprint: 8110D7415744C9D4D5A4A6309499F7B48B5F3CCF.
New expiration date: 2/27/2020 2:16:07 AM.
```

## <a name="customize-the-ad-fs-web-page-to-guide-users-to-register-mfa-verification-methods"></a>사용자에 게 MFA 확인 방법 등록을 안내 하는 AD FS 웹 페이지 사용자 지정

다음 예제를 사용 하 여 아직 proofed를 구성 하지 않은 사용자 (MFA 확인 정보)에 대 한 AD FS 웹 페이지를 사용자 지정할 수 있습니다.

### <a name="find-the-error"></a>오류 찾기

먼저 사용자에 게 확인 정보가 부족 한 경우 AD FS에서 반환 하는 몇 가지 오류 메시지가 있습니다.
기본 인증으로 Azure MFA를 사용 하는 경우 proofed 사용자에 게 다음 메시지를 포함 하는 AD FS 오류 페이지가 표시 됩니다.
```
    <div id="errorArea">
        <div id="openingMessage" class="groupMargin bigText">
            An error occurred
        </div>
        <div id="errorMessage" class="groupMargin">
            Authentication attempt failed. Select a different sign in option or close the web browser and sign in again. Contact your administrator for more information.
        </div>
```
추가 인증을 시도 하는 Azure AD를 사용 하는 경우 proofed 사용자에 게 다음과 같은 메시지가 포함 된 AD FS 오류 페이지가 표시 됩니다.
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

### <a name="catch-the-error-and-update-the-page-text"></a>오류를 Catch 하 고 페이지 텍스트를 업데이트 합니다.

오류를 catch 하 고 사용자 지정 지침을 표시 하려면 AD FS 웹 테마의 일부인 onload 파일의 끝에 javascript를 추가 하기만 하면 됩니다.  이렇게 하면 다음을 수행할 수 있습니다.
 - 식별 하는 오류 문자열 검색
 - 사용자 지정 웹 콘텐츠를 제공 합니다.  

> [!NOTE]
> Onload 파일을 사용자 지정 하는 방법에 대 한 일반적인 지침은 [AD FS 로그인 페이지의 고급 사용자 지정](advanced-customization-of-ad-fs-sign-in-pages.md)문서를 참조 하세요.

다음은 간단한 예제입니다 .를 확장 하는 것이 좋습니다.

1. 기본 AD FS 서버에서 Windows PowerShell을 열고 다음 명령을 실행 하 여 새 AD FS 웹 테마를 만듭니다.
    
    ``` PowerShell
        New-AdfsWebTheme –Name ProofUp –SourceName default
    ``` 
2. 다음으로 폴더를 만들고 기본 AD FS 웹 테마를 내보냅니다.

    ``` PowerShell
       New-Item -Path 'c:\Theme' -ItemType Directory;Export-AdfsWebTheme –Name default –DirectoryPath c:\Theme
    ```
3. 텍스트 편집기에서 C:\Theme\script\onload.js 파일을 엽니다.
4. Onload 파일의 끝에 다음 코드를 추가 합니다.
    
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
        if (errorMessage) {
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
    }

    //End Customize MFA Exception
    //End Custom Code
    ```
    > [!IMPORTANT]
    > "< YOUR_DOMAIN_NAME_HERE >";을 (를) 변경 해야 합니다. 도메인 이름을 사용 합니다. 예를 들면 다음과 같습니다. `var domain_hint = "contoso.com";`
    
5. Onload 파일 저장
6. 다음 Windows PowerShell 명령을 입력 하 여 사용자 지정 테마로 onload 파일을 가져옵니다.
    
    ``` PowerShell
    Set-AdfsWebTheme -TargetName ProofUp -AdditionalFileResource @{Uri='/adfs/portal/script/onload.js';path="c:\theme\script\onload.js"}
    ```
7. 마지막으로 다음 Windows PowerShell 명령을 입력 하 여 사용자 지정 AD FS 웹 테마를 적용 합니다.
    
    ``` PowerShell
    Set-AdfsWebConfig -ActiveThemeName "ProofUp"
    ```

## <a name="next-steps"></a>다음 단계

[AD FS 및 Azure MFA에서 사용 되는 TLS/SSL 프로토콜 및 암호 그룹 관리](manage-ssl-protocols-in-ad-fs.md)
