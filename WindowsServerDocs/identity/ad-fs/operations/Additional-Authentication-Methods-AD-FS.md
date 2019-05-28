---
title: AD FS 2019에에서 추가 인증 방법
description: 이 문서에서는 AD FS 2019에에서 새 인증 방법을 설명 합니다.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 09/19/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b0d5754a4622df9ca26a80bd4e32c355dda0f684
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190057"
---
# <a name="configure-3rd-party-authentication-providers-as-primary-authentication-in-ad-fs-2019"></a>AD FS 2019에에서 기본 인증으로 타사 인증 공급자 구성


조직 공격 (brute force)을 시도 하는 발생 하는, 손상 또는 그렇지 않은 경우 암호 기반 인증 요청을 전송 하 여 사용자를 잠글  AD FS는 조직 손상 으로부터 보호 하기 위해, IP 주소 기반 차단 "스마트" 엑스트라넷 잠금 등의 기능을 도입 되었습니다.  

그러나 이러한 완화는 반응 형입니다.  심각도입니다. 이러한 공격을 줄이기 위해 자동 관리 방식으로 제공 AD FS는 암호를 수집 하기 전에 암호 이외의 요인에 대 한 프롬프트를 수가 있습니다.  

예를 들어 AD FS 2016 Authenticator 앱에서 OTP 코드를 첫 번째 단계로 사용할 수 있습니다 기본 인증으로 Azure MFA를 도입 합니다.
AD FS 2019를 사용 하 여이 토대로 기본 인증 요소로 외부 인증 공급자를 구성할 수 있습니다.

이렇게 하면 두 가지 주요 시나리오는

## <a name="scenario-1-protect-the-password"></a>시나리오 1: 암호를 보호 합니다.
처음에 추가, 외부 요소에 게 잠금을 무차별 대입 공격 으로부터 암호 기반 로그인을 보호 합니다.  외부 인증이 성공적으로 완료 된 경우에 않습니다 사용자 다음 암호 라는 메시지가 표시 됩니다.  이렇게 하면 공격자가 하려고 손상을 유발 하거나 계정을 사용 하지 않도록 하는 편리한 방법이 없습니다.

이 시나리오는 두 가지 구성 요소로 구성 됩니다.
- 기본 인증으로 Azure MFA 또는 외부 인증 요소를 확인합니다.
- 사용자 이름 및 암호를 AD FS에서 추가 인증

## <a name="scenario-2-password-free"></a>시나리오 2: 암호가 없는!
암호를 완전히 제거 하지만 강력한 완료를 완전히 되지 않은 암호를 사용 하 여 multi-factor authentication AD FS에서 메서드를 기반
- Authenticator 앱을 사용 하 여 azure MFA
- Windows 10 Hello for Business
- 인증서 인증
- 외부 인증 공급자

## <a name="concepts"></a>개념
어떤 **기본 인증** 실제로 의미 있다는 것 메서드 첫 번째 요소를 추가 하기 전에 대 한 메시지가 표시 됩니다.  이전에 AD FS에서 사용 가능한 주 메서드 빌드된 메서드에서 Active Directory 또는 Azure MFA 또는 다른 LDAP 인증을 위한 저장소입니다.  외부 메서드는 기본 인증을 완료 된 후에 수행 되는 "추가" 인증으로 구성할 수 있습니다.

AD FS 2019에 기본 기능으로 외부 인증 의미는 AD FS 팜에 (등록 AdfsAuthenticationProvider 사용)에 등록 된 모든 외부 인증 공급자 뿐만 대 한 기본 인증 "추가" 사용 가능 인증 합니다. 마찬가지로 인트라넷 및/또는 엑스트라넷 사용에 대 한 폼 인증 및 인증서 인증과 같은 기본 제공된 공급자를 사용할 수 있습니다 이러한.

![인증](media/Additional-Authentication-Methods-AD-FS/auth1.png)

엑스트라넷, 인트라넷에 대 한 외부 공급자가 활성화 되 면 또는 둘 다를 사용 하 여 사용자가 사용할 수 있습니다.  둘 이상의 메서드를 사용 하는 경우 사용자가 선택 페이지를 참조 하 고 추가 인증에 대 한 것 처럼 기본 메서드를 선택 하는 일을 할 수 있습니다.

## <a name="pre-requisites"></a>필수 구성 요소
기본 외부 인증 공급자를 구성 하기 전에 다음 사전 요구 사항이 준비를 확인합니다
- '4' (이 값이 AD FS 2019로 변환)에 AD FS 팜 동작 수준 (FBL) 발생 했습니다.
    - 새 AD FS 2019 팜에 대 한 기본값 FBL입니다.
    - Windows Server 2012 R2 또는 2016 기반으로 AD FS 팜에서 FBL Invoke AdfsFarmBehaviorLevelRaise PowerShell commandlet을 사용 하 여 발생할 수 있습니다.  AD FS 팜을 업그레이드에 대 한 자세한 내용은 팜에 WID 팜 또는 SQL 팜에 대 한 문서를 업그레이드를 참조 하세요. 
    - Get-AdfsFarmInformation cmdlet을 사용 하 여 FBL 값을 확인할 수 있습니다.
- AD FS 2019 팜에 새 2019 '페이지 매긴된' 사용자 마주보는 페이지를 사용 하도록 구성 된
    - 이 새 AD FS 2019 팜에 대 한 기본 동작
    - AD FS 팜을 Windows Server 2012 R2 또는 2016에서 업그레이드에 대 한 페이지 매긴된 흐름으로 기본 외부 인증 (이 문서에 설명 된 기능) 사용 하는 경우 아래 설명 된 대로 자동으로 활성화 됩니다.

## <a name="enable-external-authentication-methods-as-primary"></a>기본 외부 인증 방법을 사용 하도록 설정
필수 구성 요소를 확인 한 후 두 가지 기본으로 AD FS 추가 인증 공급자를 구성 하려면:

### <a name="using-powershell"></a>PowerShell 사용


```powershell
PS C:\> Set-AdfsGlobalAuthenticationPolicy -AllowAdditionalAuthenticationAsPrimary $true
``` 


AD FS 서비스를 활성화 또는 비활성화를 주 추가 인증 한 후 다시 시작 해야 합니다.

### <a name="using-the-ad-fs-management-console"></a>AD FS 관리 콘솔을 사용 하 여
AD FS 관리 콘솔에서 아래 **서비스** -> **인증 방법**아래에 있는 **기본 인증 방법**, 편집 클릭

에 대 한 확인란을 클릭 **기본 추가 인증 공급자를 허용**합니다.

AD FS 서비스를 활성화 또는 비활성화를 주 추가 인증 한 후 다시 시작 해야 합니다.

## <a name="enable-username-and-password-as-additional-authentication"></a>추가 인증으로 사용자 이름 및 암호를 사용 하도록 설정
"암호를 보호" 시나리오를 완료 하려면 사용 사용자 이름 및 암호 PowerShell 또는 AD FS 관리 콘솔을 사용 하 여 추가 인증으로
### <a name="using-powershell"></a>PowerShell 사용



```powershell
PS C:\> $providers = (Get-AdfsGlobalAuthenticationPolicy).AdditionalAuthenticationProvider

PS C:\>$providers = $providers + "FormsAuthentication"

PS C:\>Set-AdfsGlobalAuthenticationPolicy -AdditionalAuthenticationProvider $providers
``` 

### <a name="using-the-ad-fs-management-console"></a>AD FS 관리 콘솔을 사용 하 여
AD FS 관리 콘솔에서 아래 **서비스** -> **인증 방법**아래에 있는 **추가 인증 방법**, 클릭  **편집**

에 대 한 확인란을 클릭 **폼 인증** 사용자 이름 및 암호 추가 인증으로 사용할 수 있도록 합니다.
