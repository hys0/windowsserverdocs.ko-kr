---
title: AD FS 프롬프트 = 로그인
description: AD FS 2016에 대 한 질문과 대답
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/27/2017
ms.topic: article
ms.custom: it-pro
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: a80678f5d2773e3fcd7a95032853249dc36d5616
ms.sourcegitcommit: 2a15de216edde8b8e240a4aa679dc6d470e4159e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77465527"
---
# <a name="active-directory-federation-services-promptlogin-parameter-support"></a>Active Directory Federation Services 프롬프트 = 로그인 매개 변수 지원

다음 문서에서는 AD FS에서 사용할 수 있는 prompt = login 매개 변수에 대 한 기본 지원을 설명 합니다.

## <a name="what-is-promptlogin"></a>프롬프트 = 로그인 이란?

응용 프로그램이 Azure AD에서 새로운 인증을 요청 해야 하는 경우 사용자가 이미 인증 된 경우에도 사용자를 다시 인증 하는 데 Azure AD가 필요한 경우 인증 요청의 일부로 Azure AD에 `prompt=login` 매개 변수를 보낼 수 있습니다.

페더레이션된 사용자에 대 한 요청인 경우 Azure AD는 IdP (예: AD FS)에 게 새 인증에 대 한 요청을 알려 주어 야 합니다.

기본적으로 Azure AD는이 유형의 인증 요청을 페더레이션된 IdP로 전송할 때 `prompt=login`를 `wfresh=0` 및 `wauth=https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`로 변환 합니다.

이러한 매개 변수는 다음과 같습니다.

- `wfresh=0`: 새 인증 수행
- `wauth=https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`: 새 인증 요청에 대 한 사용자 이름/암호를 사용 합니다.

이로 인해 `wauth` 매개 변수에 의해 요청 된 대로 사용자 이름 및 암호 이외의 인증 유형이 필요한 회사 인트라넷 및 multi-factor authentication 시나리오에서 문제가 발생할 수 있습니다.  

2012 년 7 월 2016 업데이트 롤업으로 Windows Server 2012 r 2의 AD FS에는 `prompt=login` 매개 변수에 대 한 기본 지원이 도입 되었습니다. 즉, 이제 azure AD는 Azure AD 및 Office 365 인증 요청의 일부로 서비스를 AD FS 하는 그대로이 매개 변수를 보낼 수 있습니다.

## <a name="ad-fs-versions-that-support-promptlogin"></a>프롬프트를 지 원하는 AD FS 버전 = 로그인

다음은 `prompt=login` 매개 변수를 지 원하는 AD FS 버전의 목록입니다.

- 2012 년 7 월 2016 업데이트 롤업이 포함 된 Windows Server R2의 AD FS
- Windows Server 2016의 AD FS

## <a name="how-to-configure-a-federated-domain-to-send-promptlogin-to-ad-fs"></a>프롬프트를 보내도록 페더레이션된 도메인을 구성 하는 방법 AD FS에 로그인 합니다.

Azure AD PowerShell 모듈을 사용 하 여 설정을 구성 합니다.

> [!NOTE]
> `PromptLoginBehavior` 속성에서 사용 하는 `prompt=login` 기능은 현재 [AZURE AD Powershell 모듈의 버전 1.0](https://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185)에서만 사용할 수 있습니다 .이 모듈에는 cmdlet에 "msol" (예: get-msoldomainfederationsettings)이 포함 된 이름이 있습니다.  현재 cmdlet의 이름이 "AzureAD\*"와 같은 Azure AD PowerShell 모듈의 ' 버전 2.0 '를 통해 사용할 수 없습니다.

1. 먼저 다음 PowerShell 명령을 실행 하 여 페더레이션된 도메인에 대 한 `PreferredAuthenticationProtocol`, `SupportsMfa`및 `PromptLoginBehavior`의 현재 값을 가져옵니다.

```powershell
    Get-MsolDomainFederationSettings -DomainName <your_domain_name> | Format-List *
```

> [!NOTE]
> 기본적으로 `Get-MsolDomainFederationSettings` 출력은 콘솔에 특정 속성을 표시 하지 않습니다. 모든 속성을 보려면 개체의 모든 속성의 출력을 강제 적용 하기 위해 출력 `Format-List *`을 파이프 (`|`) 해야 합니다.

![Get-MsolDomainFederationSettings](media/AD-FS-Prompt-Login/GetMsol.png)

> [!NOTE]
> 속성 `PromptLoginBehavior`의 값이 비어 있으면 (`$null`) `TranslateToFreshPasswordAuth` 동작이 사용 됩니다.

2. 다음 명령을 실행 하 여 원하는 `PromptLoginBehavior` 값을 구성 합니다.

```powershell
    Set-MsolDomainFederationSettings –DomainName <your_domain_name> -PreferredAuthenticationProtocol <current_value_from_step1> -SupportsMfa <current_value_from_step1> -PromptLoginBehavior <TranslateToFreshPasswordAuth|NativeSupport|Disabled>
```

`PromptLoginBehavior` 매개 변수의 가능한 값과 해당 의미는 다음과 같습니다.

- **TranslateToFreshPasswordAuth**: `wauth=https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password` 및 `wfresh=0``prompt=login`를 변환 하는 기본 Azure AD 동작을 의미 합니다.
- **NativeSupport**: AD FS 하기 위해 `prompt=login` 매개 변수가 그대로 전송 됨을 의미 합니다. 이 값은 AD FS Windows Server 2012 r 2에서 7 월 2016 업데이트 롤업 이상이 있는 경우 권장 되는 값입니다.
- **Disabled**: `wfresh=0`만 AD FS으로 전송 됨을 의미 합니다.
