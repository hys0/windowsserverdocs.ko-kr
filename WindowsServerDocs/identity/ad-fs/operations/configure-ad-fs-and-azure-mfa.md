---
ms.assetid: 24c4b9bb-928a-4118-acf1-5eb06c6b08e5
title: "ADFS 2016 및 Azure MFA 구성"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 11/01/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: be8e88ae36f344f1265fb76e66c19e0ac8aeb533
ms.sourcegitcommit: ffdfbb76c7f775e20d089d3f662d4f9a7d642f1e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2018
---
# <a name="configure-ad-fs-2016-and-azure-mfa"></a>ADFS 2016 및 Azure MFA 구성

>Windows Server 2016 적용 됩니다.

조직에는 Azure AD와 연결 된, 하는 경우 Azure 다단계 인증와 클라우드의 모두 온-프레미스 보안 ADFS 리소스를 사용할 수 있습니다. Azure MFA 암호를 제거 하 고 더 안전 하 게 인증을 제공할 수 있습니다.  Windows Server 2016 부터는 주 인증을 위한 Azure MFA을 이제 구성할 수 있습니다. 
  
달리 Windows Server 2012 r 2에 ADFS ADFS 2016 Azure MFA 어댑터 Azure AD에 직접 통합 및에 프레미스 Azure MFA 서버 필요 하지 않습니다.   Azure MFA 어댑터는 Windows Server 2016에 기본 제공 하 고 추가로 설치할 필요가 없습니다.

## <a name="registering-users-for-azure-mfa-with-ad-fs-2016"></a>Registering users for Azure MFA with AD FS 2016
Adfs는 인라인 "증명을"를 또는 전화 번호 또는 모바일 앱 등 Azure MFA 보안 확인 정보를 등록 지원 하지 않습니다. 즉,에 Azure MFA 인증 ADFS 응용 프로그램을 사용 하 여 이전 https://account.activedirectory.windowsazure.com/Proofup.aspx 방문 하 여을 사용자에 게를도 성능이 보장 다운로드 해야 합니다. 사용자가 하지 아직도 성능이 보장를 Azure AD에 ADFS Azure MFA 인증 하려고에서가, ADFS 오류를 받게 됩니다.  ADFS 관리자로 서 proofup 페이지에는 사용자를 대신 안내이 오류 환경을 사용자 지정할 수 있습니다.  ADFS 페이지 내에서 오류 메시지 문자열을 감지 하 여 방문 https://aka.ms/mfasetup, 사용자가 안내 새 메시지를 표시 onload.js 사용자 지정을 사용 하 여 이렇게 다음 인증 다시 시도할 수 있습니다. 자세한 지침 "사용자 지정은 ADFS 웹 페이지의 지침에 따라 사용자에 게 MFA 인증 방법을 등록 하려면" 아래 설명 참조이 문서의 합니다.

>[!NOTE]
> 이전에 사용자에 게 MFA (예를 들어 aka.ms/mfasetup 바로 가기를 통해 https://account.activedirectory.windowsazure.com/Proofup.aspx 방문) 등록에 대 한 인증 해야 했습니다.  이제는 ADFS 사용자에 게 MFA 인증 정보 아직 등록 되지 않은 Azure AD에 액세스할 수 있습니다의 aka.ms/mfasetup 바로 가기를 통해 proofup 페이지를 사용 하 여 기본만 인증 (와 같은 Windows 통합 된 인증 또는 사용자 이름 및 암호는 ADFS 통해 웹 페이지) .  경우 사용자에 게 구성 없는 인증 방법, Azure AD 수행 하는 사용자가 메시지를 보고 인라인 등록 "프로그램 관리자에 필요한 추가 보안 인증을 위해이 계정을 설정 하 는" 사용자 선택할 수 있습니다 "설정 이제" 합니다.
> 이미 구성 하나 이상의 MFA 인증 방법을 사용자 proofup 페이지를 방문 하는 경우 MFA 제공 하 라는 메시지가 계속 표시 됩니다.

### <a name="recommended-deployment-topologies"></a>추천된 배포가 토폴로지

#### <a name="azure-mfa-as-primary-authentication"></a>Azure MFA 주 인증 방법으로
좋은 혜택 Azure MFA Adfs로 주 인증 방법으로 사용 하는 몇 가지가 있습니다.
 - Office 365 및 기타 ADFS 앱 Azure AD에 로그인에 대 한 암호를 방지 하려면
 - 암호를 보호 하기 위해 기반 로그인 인증 코드 이전 암호와 같은 추가 될 요구 하 여

이러한 혜택 달성 하기 위해 Azure MFA adfs에서 주 인증 방법으로 사용 하려면 사용자 것도 되돌리려는 조건부 Azure AD 사용 하는 기능을 유지 하려면 "true MFA" 라는 메시지를 통해 추가 요소 들에 대 한 Adfs의 등 대 한 액세스 합니다.

온-프레미스 ($True 설정이 "SupportsMfa") MFA 작업을 수행 하 여 Azure AD 도메인 설정을 구성 하 여 이제 수행할 수 있습니다.  이 구성 ADFS 수 있는 Azure AD 하 라는 해야 하는 조건 액세스 시나리오가 대 한 추가 인증 또는 "진정한 MFA"를 수행 합니다.  

위에서 설명한 대로 ADFS 있는 사용자가 등록된 (구성 된 MFA 인증 정보) 묻는 메시지를 사용자 지정 된 ADFS 오류 페이지를 통해 인증 정보를 구성할 aka.ms/mfasetup를 방문 하지 후 다시 시도 ADFS 로그인 합니다.  
기본 언어로 Azure MFA 초기 구성 사용자가 관리를 Azure AD에 해당 인증 정보를 업데이트 하거나 MFA 해야 하는 기타 리소스에 액세스 하는 추가 단계를 제공 해야 후 한 요소 것으로 간주 됩니다.


#### <a name="azure-mfa-as-additional-authentication-to-office-365"></a>추가 인증을에 Office 365로 azure MFA
이전에 Azure MFA Office 365 또는 기타 신뢰 당사자, 최상의 옵션에 대 한 추가 인증 방법을 Adfs의 온-프레미스 ADFS 및 MFA 주 인증을 수행 하는 MFA 복합 수행를 Azure AD 구성 하는 것 이었습니다이 tr Azure ad iggered 합니다. 이제 $True로 설정 되어 있는 도메인 SupportsMfa 설정을 Azure MFA adfs에서 추가 인증으로 사용할 수 있습니다.  

위에서 설명한 대로 ADFS 있는 사용자가 등록된 (구성 된 MFA 인증 정보) 묻는 메시지를 사용자 지정 된 ADFS 오류 페이지를 통해 인증 정보를 구성할 aka.ms/mfasetup를 방문 하지 후 다시 시도 ADFS 로그인 합니다.  


## <a name="pre-requisites"></a>필수  
Azure MFA ADFS 인증에 사용 하는 경우 필수 다음과 같은 사항이 필요 합니다.  
  
- [Azure Active Directory를 사용 하 여 Azure 구독](https://azure.microsoft.com/pricing/free-trial/)합니다.  
- [Azure 다단계 인증](https://azure.microsoft.com/documentation/articles/multi-factor-authentication/)  

>[!NOTE]   
> Azure AD Azure MFA Azure AD Premium 및 (EMS (엔터프라이즈 이동성 Suite)에 포함 됩니다.  다음 중 하나를 설정한 경우에 개별 구독을 설치할 필요가 없습니다.   
- Windows Server 2016 광고 FS 온-프레미스 환경 합니다.  
- 온-프레미스 환경이 [Azure AD로 연결 합니다.](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-get-started-custom/#configuring-federation-with-ad-fs)  
- [Windows Azure Active Directory Module for Windows PowerShell](https://go.microsoft.com/fwlink/p/?linkid=236297).  
- 전역 관리자에 대 한 권한을 Azure AD 인스턴스를 사용 하 여 Azure AD PowerShell 구성 합니다.  
- 관리자 자격 증명을 ADFS 농장 MFA Azure에 대 한 구성 엔터프라이즈 합니다.  
  
  
## <a name="configure-the-ad-fs-servers"></a>AD FS 서버 구성  
Adfs MFA Azure에 대 한 구성을 완료 하기 위해 설명 하는 단계를 사용 하 여 각 ADFS 서버 구성 해야 합니다. 

>[!NOTE]
>다음이 단계를 수행 확인 **모든** 그룹에 ADFS 서버 합니다. 사용자 농장 ADFS 서버 여러 개 있는 경우 원격으로 Azure AD Powershell 사용 하는 데 필요한 구성을 수행할 수 있습니다.  
  
  
  
### <a name="step-1-generate-a-certificate-for-azure-mfa-on-each-ad-fs-server-using-the-new-adfsazuremfatenantcertificate-cmdlet"></a>1 단계: MFA Azure에 대 한 사용 하 여 각 ADFS 서버에 인증서를 생성는 `New-AdfsAzureMfaTenantCertificate`cmdlet 합니다.   
해야 할 것을 사용 하 여 Azure MFA에 대 한 인증서를 생성 합니다.  이 작업은 PowerShell 사용 합니다.  로컬 컴퓨터 인증서 스토어에서 생성 된 인증서를 찾을 수 있습니다 하 고 포함 하 여 Azure AD 디렉터리에 대 한 TenantID 제목 이름으로 표시 됩니다.    
  
![ADFS 및 MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA3.png)  
  
참고 TenantID 디렉터리의 이름을 Azure AD에 있습니다.  다음 PowerShell cmdlet를 사용 하 여 새 인증서를 생성 합니다.  
    `$certbase64 = New-AdfsAzureMfaTenantCertificate -TenantID <tenantID>`  
      
![ADFS 및 MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA1.PNG)  
  
### <a name="step-2-add-the-new-credentials-to-azure-multi-factor-auth-client-spn"></a>2 단계: 다단계 인증 클라이언트 SPN Azure에 새 자격 증명 추가   
Azure 다단계 인증 클라이언트 통신할 수 있는 ADFS 서버를 활성화 하기 위해 Azure 다단계 인증 클라이언트에 대 한 자격 증명 SPN에 추가 해야 합니다. 사용 하 여 생성 인증서는 `New-AdfsAzureMFaTenantCertificate`cmdlet 이러한 자격 증명으로 제공 됩니다. 다음을 수행 PowerShell를 사용 하 여 Azure 다단계 인증 클라이언트 SPN에 새 자격 증명을 추가 합니다.  

>[!NOTE]   
>이 단계를 완료 하기 위해 사용자와 PowerShell Connect-MsolService를 사용 하 여 Azure AD 인스턴스를 연결 해야 합니다.  이러한 단계 가정 PowerShell를 통해 이미 연결 되어 있습니다.  자세한 내용은 참조 [MsolService 연결 합니다.](https://msdn.microsoft.com/library/dn194123.aspx)  
     
  
2. **Azure 다단계 인증 클라이언트에 대 한 새로운 자격 증명으로 인증서 설정**  
    
    `New-MsolServicePrincipalCredential -AppPrincipalId 981f26a1-7f43-403b-a875-f8b09b8cd720 -Type asymmetric -Usage verify -Value $certBase64 `

>[!IMPORTANT]
>  This command needs to be run on all of the AD FS servers in your farm.  Azure AD MFA will fail on servers that have not have the certificate set as the new credential against the Azure Multi-Factor Auth Client. 

>[!NOTE]  
> 981f26a1-7f43-403b-a875-f8b09b8cd720는 Azure 다단계 인증 클라이언트 guid.  
  
## <a name="configure-the-ad-fs-farm"></a>AD FS 농장 구성  
  
실행 해야 각 ADFS 서버의 이전 섹션을 완료 했으면는 `Set-AdfsAzureMfaTenant`cmdlet 합니다.  
  
이 cmdlet ADFS 팜에 대 한 번만 실행 해야 합니다.  PowerShell을 사용 하 여이 단계를 완료 합니다.    
  
>[!NOTE]  
>이러한 변경 사항이 적용 되기 전에 팜에서 각 서버의 ADFS 서비스를 다시 시작 해야 합니다.  
  
    Set-AdfsAzureMfaTenant -TenantId <tenant ID> -ClientId 981f26a1-7f43-403b-a875-f8b09b8cd720  
      
![ADFS 및 MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA5.png)  
  
그런 다음, Azure MFA를 인트라넷과 엑스트라넷용에 대 한 기본 인증 방법으로 사용할 수 있는지 표시 됩니다.    
  
![ADFS 및 MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA6.png)  

## <a name="renew-and-manage-ad-fs-azure-mfa-certificates"></a>갱신 하 고 관리 FS Azure AD MFA 인증서
다음 지침 ADFS 서버에 Azure MFA 인증서를 관리 하는 방법을 안내 합니다.
기본적으로 ADFS Azure MFA를 구성할 때 New-AdfsAzureMfaTenantCertificate PowerShell cmdlet 통해 생성 인증서 올바른지 2 년 동안 합니다.  에 가까이 방법을 확인 하려면 만료 인증서를 되며 갱신 하 고 설치 새로운 인증서를 사용 하 여 다음 절차 됩니다.

### <a name="assess-ad-fs-azure-mfa-certificate-expiration-date"></a>평가 광고 FS Azure MFA 인증서 만료 날짜
로컬 컴퓨터에서 각 ADFS 서버의 내 스토어 자체 서명된 인증서를 제공 될 예정 "OU Microsoft MFA FS Azure AD =" 발행인이 및 제목 합니다.  Azure MFA 인증서입니다.  만료 날짜를 확인 하려면 각 ADFS 서버의이 인증서 유효 기간의 확인 합니다.  

### <a name="create-new-ad-fs-azure-mfa-certificate-on-each-ad-fs-server"></a>각 ADFS 서버에 새 광고 FS Azure MFA 인증서 만들기
인증서 유효 기간의의 끝에 가까워지고, 각 ADFS 서버에 새 Azure MFA 인증서를 생성 하 여 갱신 프로세스를 시작 합니다. Powershell 명령 창에서 다음 cmdlet 사용 하 여 각 ADFS 서버에 새 인증서를 생성 합니다.

```
PS C:\> $newcert = New-AdfsAzureMfaTenantCertificate -TenantId <tenant id such as contoso.onmicrosoft.com> -Renew $true
```

이 cmdlet 결과 유효 2 일 나중에에서 2 일 + 2 년에 새 인증서를 생성 됩니다.  ADFS 및 Azure MFA 작업이이 cmdlet 또는 새 인증서 적용 되지 않습니다. (참고: 2 일 지연 의도적 하 고 새 인증서의 테 구성할 ADFS MFA Azure에 대 한 사용을 시작 하기 전에 다음 단계를 실행 하는 시간을 제공 합니다.)


### <a name="configure-each-new-ad-fs-azure-mfa-certificate-in-the-azure-ad-tenant"></a>Azure AD 테에서 각 새로운 광고 FS Azure MFA 인증서를 구성 합니다.
다음과 같이 Azure AD 테 설정을 Azure AD PowerShell 모듈에 대 한 각 새 (서버의 인증서 각 ADFS), 사용 하 여 업데이트 (참고: 먼저 Connect-MsolService)입니다.

```
PS C:/> New-MsolServicePrincipalCredential -AppPrincipalId 981f26a1-7f43-403b-a875-f8b09b8cd720 -Type Asymmetric -Usage Verify -Value $certbase64
```
    Where $certbase64 is the new certificate.  The base64 encoded certificate can be obtained by exporting the certificate (without the private key) as a DER encoded file and opening in Notepad.exe, then copy/pasting to the PSH session and assigning to the variable $certbase64

### <a name="verify-that-the-new-certificates-will-be-used-for-azure-mfa"></a>새로운 인증서 Azure MFA에 사용할 수 있는지 확인
한 번 새 인증서 유효 하 게, ADFS 다시 시작 되며 하루를 몇 시간 안에 MFA Azure에 대 한 각 해당 인증서를 사용 하 여 시작 합니다.  이 문제가 발생 각 서버에 표시 됩니다 이벤트는 다음과 같은 정보를 광고 FS 관리자 이벤트 로그에 기록: 로그 이름: 광고 FS/관리자 소스: 광고 FS 날짜: 2018 년 2 월 27 일 7: 오후 33:31 이벤트 ID: 547 작업 범주: None 수준: 정보 키워드 : 광고 FS 사용자: DOMAIN\adfssvc 컴퓨터: 설명 ADFS.domain.contoso.com: Azure MFA에 대 한 테 인증서 갱신 되었습니다.  

TenantId: contoso.onmicrosoft.com 합니다. 이전 지문: 7CC103D60967318A11D8C51C289EF85214D9FC63 합니다. 오래 된 만료 날짜: 2019 년 9 월 15 일 오후 9시 43분: 17 합니다. 새 지문: 8110D7415744C9D4D5A4A6309499F7B48B5F3CCF 합니다. 새로운 만료 날짜: 2020 년 2 월 27 일 오전 2시 16분: 07 합니다.

## <a name="customize-the-ad-fs-web-page-to-guide-users-to-register-mfa-verification-methods"></a>ADFS 웹 페이지의 지침에 따라 등록 MFA 인증 방법을 사용자 지정

다음은 사용자에 게는 하지 아직도 성능이 보장 위로 ADFS 웹 페이지에 지정 (구성 MFA 인증 정보) 사용 합니다.

### <a name="find-the-error"></a>오류 찾기
먼저, 다른 오류 메시지가 Adfs는 반환 사용자는 확인 정보가 없는 경우에는 몇 가지가 있습니다.
Azure MFA 주 인증을 사용 중인 경우 없다고 proofed 사용자 다음 메시지를 포함 하는 ADFS 오류 페이지를 표시 됩니다.
```
    <div id="errorArea"> 
        <div id="openingMessage" class="groupMargin bigText">
            An error occurred 
        </div> 
        <div id="errorMessage" class="groupMargin">
            Authentication attempt failed. Select a different sign in option or close the web browser and sign in again. Contact your administrator for more information. 
        </div>
```
추가 인증으로 Azure AD를 시도 없다고 proofed 사용자 다음 메시지를 포함 하는 ADFS 오류 페이지를 표시 됩니다.
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

### <a name="catch-the-error-and-update-the-page-text"></a>오류 접 하 든 및 페이지 텍스트 업데이트
오류를 파악 하 고가 보여 주는 사용자 지정 지침 문제는 Adfs의 일부인 onload.js 파일의 끝에 javascript 추가 웹 (1) 신원 파악이 가능한 오류 문자열을 검색 하 고 (2) 사용자 지정 제공 테마 웹 콘텐츠 합니다.  (일반적으로 onload.js 파일을 사용자 지정 하는 방법에 대 한 지침을 위해 문서를 참조 [여기](https://docs.microsoft.com/en-us/windows-server/identity/ad-fs/operations/advanced-customization-of-ad-fs-sign-in-pages).)

