---
title: "ADFS 프롬프트 = 로그인"
description: "AD FS 2016에 대 한 질문과 대답"
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/27/2017
ms.topic: article
ms.custom: it-pro
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 8b98cdc27c9bd01d9855e98965f59ebe5257ed5c
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="active-directory-federation-services-promptlogin-parameter-support"></a>Active Directory Federation Services 프롬프트 = 로그인 매개 지원
다음 문서 Adfs에서 사용할 수 있는 프롬프트 = 로그인 매개에 대 한 기본 지원을 설명 합니다.

## <a name="what-is-promptlogin"></a>프롬프트 란 로그인 =?  

일부 Office 365 응용 프로그램 (최신 인증을 사용 하도록 설정)를 Azure ad 각 인증 요청의 일환으로 프롬프트 = 로그인 매개 변수를 보냅니다.  By default, Azure AD translates this into two parameters: <code><b>wauth</b>=urn:oasis:names:tc:SAML:1.0:am:password</code>, and <code><b>wfresh</b>=0</code>.

이 회사 인트라넷과 사용자 이름 및 암호 이외의 인증 유형 필요한 다단계 인증 시나리오를 문제가 발생할 수 있습니다.  

2016 년 7 월 업데이트 롤업와 Windows Server 2012 r 2에 ADFS 프롬프트 = 로그인 매개에 대 한 기본 지원을 도입 되었습니다.  즉, 이제이 매개 변수를 보낼 수 Azure AD 구성할 수 있는-Azure AD의 일부로 ADFS 서비스에는 및 Office 365 인증 요청 합니다.

### <a name="ad-fs-versions-that-support-promptlogin"></a>메시지를 지 원하는 광고 FS 버전 = 로그인
다음은 프롬프트 = 로그인 매개 변수 지원 ADFS 버전 목록입니다.

- Adfs의 2016 년 7 월 Windows Server 2012 R2 업데이트 롤업

- Windows Server 2016 ADFS

## <a name="how-do-to-configure-your-azure-ad-tenant-to-send-promptlogin-to-ad-fs"></a>프롬프트 전송 하 여 Azure AD 테 구성 하는 방법 = Adfs에 로그인

Azure AD PowerShell 모듈을 사용 하 여 설정을 구성할 수 있습니다.

> [!NOTE]
> The prompt=login capability (enabled by the PromptLoginBehavior property) is currently available only in the [‘version 1.0’ Azure AD Powershell module](https://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185), in which the cmdlets have names that include “Msol”, such as Set-MsolDomainFederationSettings.  통해 현재 사용할 수 없는 ' 버전 2.0' Azure AD PowerShell 모듈 cmdlet 된 이름을 갖습니다 같은 "설정-AzureAD\ *" 합니다.

프롬프트 구성 로그인 문제를 아래 cmdlet 구문 =:

예제 1:
```powershell
    Set-MsolDomainFederationSettings –DomainName <your domain name> -PreferredAuthenticationProtocol <your current protocol setting> 
```

예제 2:
```powershell
    Set-MsolDomainFederationSettings –DomainName <your domain name> -SupportsMfa <$True|$False>
```

예제 3:
```powershell
    Set-MsolDomainFederationSettings –DomainName <your domain name> -PromptLoginBehavior <TranslateToFreshPasswordAuth|NativeSupport|Disabled>
```

 
 PreferredAuthenticationProtocol, SupportsMfa PromptLoginBehavior 속성 값 cmdlet 결과 확인 하 여 확인할 수 있습니다: ![Get MsolDomainFederationSettings](media/AD-FS-Prompt-Login/GetMsol.png)
```powershell
    Get-MsolDomainFederationSettings -DomainName <your_domain_name> | fl *
 ```
> [!NOTE]
> 기본적으로 Get-MsolDomainFederationSettings 실행 될 때, 일부 속성 콘솔에 표시 되지 않습니다.  사용 하는 것이 좋습니다 이러한 매개 변수를 보려면는 | fl * 모든 개체 속성의 출력 강제로 합니다.


PromptLoginBehavior 매개 변수와 및 설정에 대 한 자세한 정보는 다음과 같습니다.
   
   - <b>TranslateToFreshPasswordAuth</b> Azure AD 기본적으로 전송 의미 <b>wauth</b> 및 <b>wfresh</b> 프롬프트 대신 ADFS = 로그인
   - <b>NativeSupport</b> ADFS 하는 것 처럼 프롬프트 = 로그인 매개 전송 될 것을 의미
   - <b>사용 안 함</b> 아무 ADFS 전송 될 것을 의미

