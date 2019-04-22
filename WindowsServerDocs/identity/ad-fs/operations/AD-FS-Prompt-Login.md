---
title: AD FS 프롬프트 = 로그인
description: AD FS 2016에 대 한 질문과 대답
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/27/2017
ms.topic: article
ms.custom: it-pro
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 6a4b6cfe98064181824e210be9031a0f67cb4b75
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824634"
---
# <a name="active-directory-federation-services-promptlogin-parameter-support"></a>Active Directory Federation Services 프롬프트 = 로그인 매개 변수 지원
다음 문서에는 AD FS에서 사용할 수 있는 prompt = login 매개 변수에 대 한 네이티브 지원을 설명 합니다.

## <a name="what-is-promptlogin"></a>이란 prompt = login?  

일부 Office 365 응용 프로그램 (최신 인증 사용) 각 인증 요청의 일부로 Azure AD에 prompt = login 매개 변수를 보냅니다.  기본적으로 Azure AD로 변환 두 개의 매개 변수: <code> <b> wauth </b> =urn:oasis:names:tc:SAML:1.0:am:password </code>, 및 <code> <b> wfresh </b> =0 </code> .

이 인해 회사 인트라넷 및 사용자 이름 및 암호 이외의 인증 유형이 필요한 multi-factor authentication 시나리오를 사용 하 여 문제가 발생할 수 있습니다.  

2016 년 7 월 업데이트 롤업 사용 하 여 Windows Server 2012 R2에서 AD FS에는 prompt = login 매개 변수에 대 한 네이티브 지원이 추가 되었습니다.  즉, 이제 Azure AD를 구성 하는 옵션으로이 매개 변수를 보낼-AD FS 서비스에는 Azure AD의 일부로 및 Office 365 인증 요청 합니다.

### <a name="ad-fs-versions-that-support-promptlogin"></a>프롬프트를 지 원하는 AD FS 버전 = 로그인
다음은 prompt = login 매개 변수를 지 원하는 AD FS 버전의 목록입니다.

- 2016 년 7 월을 사용 하 여 Windows Server 2012 R2에서 AD FS 업데이트 롤업

- Windows Server 2016에서에서 AD FS

## <a name="how-do-to-configure-your-azure-ad-tenant-to-send-promptlogin-to-ad-fs"></a>프롬프트를 보내도록 Azure AD 테 넌를 구성 하는 방법 = AD FS에 로그인

설정을 구성 하려면 Azure AD PowerShell 모듈을 사용 합니다.

> [!NOTE]
> (PromptLoginBehavior 속성으로 사용) prompt = login 기능은 현재에 사용할 수는 [' 버전 1.0' Azure AD Powershell 모듈](https://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185)를 cmdlet에 같은 "Msol"를 포함 하는 이름 Set-msoldomainfederationsettings 합니다.  통해 현재 사용할 수 없는 ' 버전 2.0' Azure AD PowerShell 모듈, 해당 cmdlet의 이름이 같은 "집합 AzureAD\*"입니다.

프롬프트 구성 = 로그인 동작을 아래 cmdlet 구문:

예 1:
```powershell
    Set-MsolDomainFederationSettings –DomainName <your domain name> -PreferredAuthenticationProtocol <your current protocol setting> 
```

예 2:
```powershell
    Set-MsolDomainFederationSettings –DomainName <your domain name> -SupportsMfa <$True|$False>
```

예제 3:
```powershell
    Set-MsolDomainFederationSettings –DomainName <your domain name> -PromptLoginBehavior <TranslateToFreshPasswordAuth|NativeSupport|Disabled>
```

 
 Cmdlet의 출력을 확인 하 여 PreferredAuthenticationProtocol, SupportsMfa, 및 PromptLoginBehavior 속성 값을 찾을 수 있습니다. ![Get-MsolDomainFederationSettings](media/AD-FS-Prompt-Login/GetMsol.png)
```powershell
    Get-MsolDomainFederationSettings -DomainName <your_domain_name> | fl *
 ```
> [!NOTE]
> 기본적으로 Get-msoldomainfederationsettings를 실행 하는 경우, 특정 속성이 콘솔에 표시 되지 않습니다.  사용 하는 것이 좋습니다. 이러한 매개 변수를 보려면를 | fl *의 모든 개체의 속성이 출력 하도록 합니다.


다음은 PromptLoginBehavior 매개 변수 및 해당 설정에 대 한 자세한 정보입니다.
   
   - <b>TranslateToFreshPasswordAuth</b> 전송의 기본 Azure AD 동작을 의미 <b>wauth</b> 하 고 <b>wfresh</b> 프롬프트 대신 AD FS 로그인 =
   - <b>NativeSupport</b> prompt = login 매개 변수는 AD FS에 전송 되는 방법
   - <b>사용 안 함</b> AD FS에 전송할 수는 아무 것도 의미 합니다.

