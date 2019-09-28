---
title: AD FS 2019의 추가 인증 방법
description: 이 문서에서는 AD FS 2019의 새로운 인증 방법을 설명 합니다.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 09/19/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 8a53a4cfca4f34459102b8edc8e6af82f36be70d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358373"
---
# <a name="configure-3rd-party-authentication-providers-as-primary-authentication-in-ad-fs-2019"></a>AD FS 2019에서 타사 인증 공급자를 기본 인증으로 구성


조직에는 암호 기반 인증 요청을 전송 하 여 무차별 암호 대입, 손상 또는 다른 사용자 계정을 잠그는 공격이 발생 합니다.  조직 손상 으로부터 보호 하기 위해 AD FS에는 엑스트라넷 "스마트" 잠금 및 IP 주소 기반 차단과 같은 기능이 도입 되었습니다.  

그러나 이러한 완화는 대응식 방법입니다.  자동 관리 방식을 제공 하기 위해 이러한 공격의 심각도를 줄이려면 암호를 수집 하기 전에 암호 이외의 요소를 확인 하는 기능을 AD FS 합니다.  

예를 들어 AD FS 2016에서는 인증 앱의 OTP 코드를 첫 번째 요소로 사용할 수 있도록 Azure MFA를 기본 인증으로 도입 했습니다.
AD FS 2019를 사용 하 여이를 빌드하면 외부 인증 공급자를 기본 인증 요소로 구성할 수 있습니다.

이를 사용 하는 두 가지 주요 시나리오는 다음과 같습니다.

## <a name="scenario-1-protect-the-password"></a>시나리오 1: 암호 보호
추가 외부 요소를 먼저 확인 하 여 무차별 암호 대입 공격 및 잠금 으로부터 암호 기반 로그인을 보호 합니다.  외부 인증이 성공적으로 완료 된 경우에만 사용자에 게 암호 프롬프트가 표시 됩니다.  이렇게 하면 공격자가 계정을 손상 시키거나 사용 하지 않도록 설정 하는 편리한 방법이 제거 됩니다.

이 시나리오는 다음 두 가지 구성 요소로 구성 됩니다.
- Azure MFA 또는 외부 인증 요소를 기본 인증으로 묻기
- AD FS의 추가 인증으로 서의 사용자 이름 및 암호

## <a name="scenario-2-password-free"></a>시나리오 2: 암호-무료
AD FS에서 전체 암호 기반 방법을 사용 하 여 강력한 multi-factor authentication을 완료 하지만 암호를 완전히 제거 합니다.
- Authenticator 앱을 사용 하는 Azure MFA
- 비즈니스용 Windows 10 Hello
- 인증서 인증
- 외부 인증 공급자

## <a name="concepts"></a>개념
**기본 인증** 을 사용 하는 것은 추가 요인이 되기 전에 사용자에 게 먼저 메시지를 표시 하는 방법 임을 의미 합니다.  이전에는 AD FS에서 사용할 수 있는 유일한 기본 방법은 Active Directory 또는 Azure MFA 또는 기타 LDAP 인증 저장소에 대 한 메서드를 기반으로 합니다.  외부 메서드는 기본 인증이 성공적으로 완료 된 후에 발생 하는 "추가" 인증으로 구성 될 수 있습니다.

AD FS 2019에서 외부 인증은 기본 기능으로 서 AD FS 팜에 등록 된 모든 외부 인증 공급자 (Register-adfsauthenticationprovider 사용)를 기본 인증 뿐만 아니라 "추가"에 사용할 수 있습니다. 인증은. 인트라넷 및/또는 엑스트라넷 사용을 위해 양식 인증 및 인증서 인증과 같은 기본 제공 공급자와 동일한 방식으로 사용 하도록 설정할 수 있습니다.

![인증](media/Additional-Authentication-Methods-AD-FS/auth1.png)

엑스트라넷, 인트라넷 또는 둘 다에 대해 외부 공급자를 사용 하도록 설정 하면 사용자가 사용할 수 있게 됩니다.  둘 이상의 메서드를 사용 하는 경우 사용자는 추가 인증을 위해 수행 하는 것 처럼 선택 페이지를 표시 하 고 기본 방법을 선택할 수 있습니다.

## <a name="pre-requisites"></a>필수 구성 요소
외부 인증 공급자를 기본으로 구성 하기 전에 다음 필수 구성 요소를 준비 해야 합니다.
- AD FS 팜 동작 수준 (FBL)이 ' 4 ' (으)로 .이 값은 AD FS 2019로 변환 됩니다.
    - 새 AD FS 2019 팜에 대 한 기본 FBL 값입니다.
    - Windows Server 2012 R2 또는 2016을 기반으로 하는 AD FS 팜의 경우 PowerShell AdfsFarmBehaviorLevelRaise를 사용 하 여 FBL를 발생 시킬 수 있습니다.  AD FS 팜을 업그레이드 하는 방법에 대 한 자세한 내용은 SQL 팜 또는 WID 팜에 대 한 팜 업그레이드 문서를 참조 하세요. 
    - AdfsFarmInformation cmdlet을 사용 하 여 FBL 값을 확인할 수 있습니다.
- AD FS 2019 팜이 새로운 2019 ' 페이지가 매겨진 ' 사용자가 페이지를 사용 하도록 구성 되어 있습니다.
    - 새 AD FS 2019 팜에 대 한 기본 동작입니다.
    - Windows Server 2012 R2 또는 2016에서 업그레이드 된 AD FS 팜의 경우, 아래에 설명 된 대로 외부 인증 (이 문서에 설명 된 기능)을 사용할 수 있게 되 면 페이지가 매겨진 흐름이 자동으로 설정 됩니다.

## <a name="enable-external-authentication-methods-as-primary"></a>기본으로 외부 인증 방법 사용
필수 구성 요소를 확인 한 후에는 다음과 같은 두 가지 방법으로 추가 인증 공급자를 기본으로 AD FS 구성할 수 있습니다.

### <a name="using-powershell"></a>PowerShell 사용


```powershell
PS C:\> Set-AdfsGlobalAuthenticationPolicy -AllowAdditionalAuthenticationAsPrimary $true
``` 


추가 인증을 기본으로 사용 하거나 사용 하지 않도록 설정 하 고 나면 AD FS 서비스를 다시 시작 해야 합니다.

### <a name="using-the-ad-fs-management-console"></a>AD FS 관리 콘솔 사용
AD FS 관리 콘솔의 **서비스** -> **인증 방법**아래에서 **기본 인증 방법**아래에 있는 편집을 클릭 합니다.

**추가 인증 공급자를 기본으로 허용**확인란을 클릭 합니다.

추가 인증을 기본으로 사용 하거나 사용 하지 않도록 설정 하 고 나면 AD FS 서비스를 다시 시작 해야 합니다.

## <a name="enable-username-and-password-as-additional-authentication"></a>추가 인증으로 사용자 이름 및 암호 사용
"암호 보호" 시나리오를 완료 하려면 PowerShell 또는 AD FS 관리 콘솔을 사용 하 여 추가 인증으로 사용자 이름 및 암호를 사용 하도록 설정 합니다.
### <a name="using-powershell"></a>PowerShell 사용



```powershell
PS C:\> $providers = (Get-AdfsGlobalAuthenticationPolicy).AdditionalAuthenticationProvider

PS C:\>$providers = $providers + "FormsAuthentication"

PS C:\>Set-AdfsGlobalAuthenticationPolicy -AdditionalAuthenticationProvider $providers
``` 

### <a name="using-the-ad-fs-management-console"></a>AD FS 관리 콘솔 사용
AD FS 관리 콘솔의 **서비스** -> **인증 방법**에서 **추가 인증 방법**아래에 있는 **편집** 을 클릭 합니다.

**폼 인증** 확인란을 클릭 하 여 추가 인증으로 사용자 이름 및 암호를 사용 하도록 설정 합니다.
