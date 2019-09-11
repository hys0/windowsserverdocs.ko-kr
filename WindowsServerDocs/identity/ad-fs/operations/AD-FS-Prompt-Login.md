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
ms.openlocfilehash: cc116701f9d03e6ca2e6d086ac7a93b0df595366
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70866181"
---
# <a name="active-directory-federation-services-promptlogin-parameter-support"></a>Active Directory Federation Services 프롬프트 = 로그인 매개 변수 지원

다음 문서에서는 AD FS에서 사용할 수 있는 prompt = login 매개 변수에 대 한 기본 지원을 설명 합니다.

## <a name="what-is-promptlogin"></a>프롬프트 = 로그인 이란?

응용 프로그램이 azure ad에서 새로운 인증을 요청 해야 하는 경우 사용자가 이미 인증 된 경우라도 사용자를 다시 인증 하는 데 azure ad가 필요한 경우 인증의 일부로 azure `prompt=login` ad에 매개 변수를 보낼 수 있습니다. 요구.

페더레이션된 사용자에 대 한 요청인 경우 Azure AD는 IdP (예: AD FS)에 게 새 인증에 대 한 요청을 알려 주어 야 합니다.

기본적으로 Azure AD는이 `prompt=login` 유형의 인증 `wauth=http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password` 요청을 페더레이션된 IdP로 전송 하는 경우 및로 `wfresh=0` 변환 합니다.

이러한 매개 변수는 다음과 같습니다.

- `wfresh=0`: 새 인증을 수행 합니다.
- `wauth=http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`: 새 인증 요청에 대 한 사용자 이름/암호를 사용 합니다.

이 경우 `wauth` 매개 변수에 의해 요청 된 대로 사용자 이름 및 암호 이외의 인증 유형이 필요한 회사 인트라넷 및 multi-factor authentication 시나리오에서 문제가 발생할 수 있습니다.  

2012 년 7 월 2016 업데이트 롤업으로 Windows Server 2012 r 2의 AD FS에는 `prompt=login` 매개 변수에 대 한 기본 지원이 도입 되었습니다. 즉, 이제 azure AD는 Azure AD 및 Office 365 인증 요청의 일부로 서비스를 AD FS 하는 그대로이 매개 변수를 보낼 수 있습니다.

## <a name="ad-fs-versions-that-support-promptlogin"></a>프롬프트를 지 원하는 AD FS 버전 = 로그인

다음은 매개 변수를 `prompt=login` 지 원하는 AD FS 버전의 목록입니다.

- 2012 년 7 월 2016 업데이트 롤업이 포함 된 Windows Server R2의 AD FS
- Windows Server 2016의 AD FS

## <a name="how-to-configure-a-federated-domain-to-send-promptlogin-to-ad-fs"></a>프롬프트를 보내도록 페더레이션된 도메인을 구성 하는 방법 AD FS에 로그인 합니다.

Azure AD PowerShell 모듈을 사용 하 여 설정을 구성 합니다.

> [!NOTE]
> `PromptLoginBehavior` 속성에서 사용 하는 기능은 현재 AzureADPowershell 모듈의 [버전1.0에서만 `prompt=login`사용할수있습니다. ](https://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185)이모듈의cmdlet에는get-msoldomainfederationsettings와같이"msol"이포함된 이름이 있습니다.  현재 cmdlet에 이름이 "AzureAD\*" 인 Azure AD PowerShell 모듈의 ' 버전 2.0 '을 통해 사용할 수 없습니다.

1. 먼저 다음 PowerShell 명령을 실행 하 `PreferredAuthenticationProtocol`여 `SupportsMfa`페더레이션된 도메인 `PromptLoginBehavior` 에 대해, 및의 현재 값을 가져옵니다.

```powershell
    Get-MsolDomainFederationSettings -DomainName <your_domain_name> | Format-List *
```

> [!NOTE]
> 기본적 `Get-MsolDomainFederationSettings` 으로 출력은 콘솔에 특정 속성을 표시 하지 않습니다. 모든 속성을 보려면 출력을로`|` `Format-List *` 파이프 () 하 여 개체의 모든 속성을 강제로 출력 해야 합니다.

![Get-MsolDomainFederationSettings](media/AD-FS-Prompt-Login/GetMsol.png)

> [!NOTE]
> 속성이 비어 있으면 (`$null`)이 고의 `TranslateToFreshPasswordAuth`기본 동작을 의미 합니다. `PreferredAuthenticationMethod`

2. 다음 명령을 실행 하 여 `PromptLoginBehavior` 의 원하는 값을 구성 합니다.

```powershell
    Set-MsolDomainFederationSettings –DomainName <your_domain_name> -PreferredAuthenticationProtocol <current_value_from_step1> -SupportsMfa <current_value_from_step1> -PromptLoginBehavior <TranslateToFreshPasswordAuth|NativeSupport|Disabled>
```

`PromptLoginBehavior` 매개 변수의 가능한 값과 해당 의미는 다음과 같습니다.

- **TranslateToFreshPasswordAuth**: 및 `prompt=login` 로`wfresh=0`변환 하는 기본 Azure AD 동작을 의미 합니다. `wauth=http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`
- **NativeSupport**: `prompt=login` 매개 변수가 AD FS 하는 것으로 전송 됨을 의미 합니다. 이 값은 AD FS Windows Server 2012 r 2에서 7 월 2016 업데이트 롤업 이상이 있는 경우 권장 되는 값입니다.
- **Disabled**:만 `wfresh=0` AD FS로 전송 됨을 의미 합니다.
