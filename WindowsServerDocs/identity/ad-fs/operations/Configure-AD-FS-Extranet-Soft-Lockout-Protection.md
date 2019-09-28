---
ms.assetid: 777aab65-c9c7-4dc9-a807-9ab73fac87b8
title: AD FS 엑스트라넷 잠금 보호 구성
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 02/01/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: bb5958f8205271fe3ab2258ed9812ae03f2a0be0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358213"
---
# <a name="configure-ad-fs-extranet-lockout-protection"></a>AD FS 엑스트라넷 잠금 보호 구성

Windows Server 2012 r 2의 AD FS에는 엑스트라넷 잠금 이라는 보안 기능이 도입 되었습니다.  이 기능을 사용 하면 "악의적인" 사용자 계정에 대 한 인증을 일정 기간 동안 "중지" 할 AD FS.  이렇게 하면 사용자 계정이 Active Directory에서 잠기는 것을 방지할 수 있습니다.  AD 계정 잠금에서 사용자를 보호 하는 것 외에도 AD FS 엑스트라넷 잠금은 무작위 암호 추측 공격 으로부터 보호 합니다.

> [!NOTE]
> 이 기능은 인증 요청이 웹 응용 프로그램 프록시를 통해 제공 되 고 **사용자 이름 및 암호 인증**에만 적용 되는 **엑스트라넷 시나리오** 에서만 작동 합니다.

## <a name="advantages-of-extranet-lockout"></a>엑스트라넷 잠금의 이점
엑스트라넷 잠금은 다음과 같은 주요 이점을 제공 합니다.
- 공격자가 인증 요청을 지속적으로 전송 하 여 사용자의 암호를 추측 하려고 하는 **무차별 암호 대입 공격** 으로부터 사용자 계정을 보호 합니다. 이 경우 AD FS는 엑스트라넷 액세스를 위해 악의적인 사용자 계정을 잠급니다.
- 공격자가 잘못 된 암호로 인증 요청을 전송 하 여 사용자 계정을 잠그려는 **악의적인 계정 잠금의** 사용자 계정을 보호 합니다. 이 경우 엑스트라넷 액세스에 대 한 AD FS 사용자 계정이 잠기기는 하지만 AD의 실제 사용자 계정은 잠기지 않으며 사용자는 조직 내의 회사 리소스에 계속 액세스할 수 있습니다. 이를 **소프트 잠금**이라고 합니다.

## <a name="how-it-works"></a>작동 방법
이 기능을 사용 하도록 구성 해야 하는 AD FS에는 다음과 같은 3 가지 설정이 있습니다. 
- **EnableExtranetLockout &lt; 부울 @ no__t-2** 엑스트라넷 잠금을 사용 하도록 설정 하려는 경우이 부울 값을 True로 설정 합니다.
- **ExtranetLockoutThreshold &lt; 정수 @ no__t-2** 이는 잘못 된 암호 시도의 최대 수를 정의 합니다. 임계값에 AD FS 도달 하면 인증을 위해 도메인 컨트롤러에 연결 하지 않고도 엑스트라넷의 요청을 즉시 거부 합니다 .이 경우에는 엑스트라넷 관찰 창이 전달 될 때까지 암호의 양호한 지 여부에 관계 없이 인증을 위해 도메인 컨트롤러에 연결을 시도 하지 않습니다. 즉, 계정이 소프트 잠겨 있는 동안에는 AD 계정의 **badPwdCount** 특성 값이 증가 하지 않습니다.
- **ExtranetObservationWindow &lt;TimeSpan @ no__t-2** 는 사용자 계정이 소프트 잠기는 기간을 결정 합니다. AD FS은 창이 전달 될 때 사용자 이름 및 암호 인증을 다시 수행 하기 시작 합니다. AD FS는 AD 특성 badPasswordTime을 엑스트라넷 관찰 창이 통과 했는지 여부를 확인 하기 위한 참조로 사용 합니다. 현재 시간 > badPasswordTime + ExtranetObservationWindow 인 경우 창이 전달 됩니다. 

> [!NOTE]
> AD 잠금 정책과 별개로 엑스트라넷 잠금 기능을 AD FS 합니다. 그러나 **ExtranetLockoutThreshold** 매개 변수 값을 AD 계정 잠금 임계값 보다 작은 값으로 설정 하는 것이 좋습니다. 이렇게 하지 않으면 AD FS Active Directory에서 계정이 잠기는 것을 보호할 수 없습니다. 

최대 15 개의 잘못 된 암호 시도 횟수와 30 분 소프트 잠금 기간을 사용 하는 엑스트라넷 잠금 기능을 사용 하는 예는 다음과 같습니다.

```powershell
Set-AdfsProperties -EnableExtranetLockout $true -ExtranetLockoutThreshold 15 -ExtranetObservationWindow (new-timespan -Minutes 30)
```

이러한 설정은 AD FS 서비스가 인증할 수 있는 모든 도메인에 적용 됩니다. AD FS 인증 요청을 수신 하는 경우에는 LDAP 호출을 통해 PDC (주 도메인 컨트롤러)에 액세스 하 고 PDC의 사용자에 대 한 **badPwdCount** 특성 조회를 수행 하는 방식으로 작동 합니다. AD FS **badPwdCount** > = ExtranetLockoutThreshold 설정 값을 찾을 때 엑스트라넷 관찰 창에 정의 된 시간이 아직 전달 되지 않은 경우에는 AD FS에서 즉시 요청을 거부 하 게 됩니다. 즉, 사용자가 양호 하거나 잘못 입력 했는지 여부에 관계 없이 엑스트라넷의 암호는 AD FS에서 AD로 자격 증명을 보내지 않으므로 로그온이 실패 합니다. AD FS **badPwdCount** 또는 잠긴 사용자 계정과 관련 하 여 상태를 유지 하지 않습니다. AD FS은 모든 상태 추적에 AD를 사용 합니다. 

> [!warning]
> 서버 2012 r 2에서 AD FS 엑스트라넷 잠금을 사용 하도록 설정 된 경우 WAP를 통한 모든 인증 요청은 PDC에서 AD FS 유효성을 검사 합니다. PDC를 사용할 수 없는 경우 사용자는 엑스트라넷에서 인증할 수 없습니다.

서버 2016에서는 PDC를 사용할 수 없을 때 다른 도메인 컨트롤러에 대 한 대체 AD FS 허용 하는 추가 매개 변수를 제공 합니다.

- **ExtranetLockoutRequirePDC &lt; 부울 @ no__t-2** -사용 하도록 설정 하면 엑스트라넷 잠금에 주 도메인 컨트롤러 (PDC)가 필요 합니다. 사용 하지 않도록 설정 된 경우: PDC를 사용할 수 없는 경우 엑스트라넷 잠금이 다른 도메인 컨트롤러에 대체 됩니다.

다음 Windows PowerShell 명령을 사용 하 여 서버 2016에서 AD FS 엑스트라넷 잠금을 구성할 수 있습니다.

```powershell
Set-AdfsProperties -EnableExtranetLockout $true -ExtranetLockoutThreshold 15 -ExtranetObservationWindow (new-timespan -Minutes 30) -ExtranetLockoutRequirePDC $false
```

## <a name="working-with-the-active-directory-lockout-policy"></a>Active Directory 잠금 정책 사용
AD FS의 엑스트라넷 잠금 기능은 AD 잠금 정책과 독립적으로 작동 합니다. 그러나 엑스트라넷 잠금에 대 한 설정이 AD 잠금 정책에서 보안 용도를 제공할 수 있도록 적절 하 게 구성 되어 있는지 확인 해야 합니다.
먼저 AD 잠금 정책을 살펴보겠습니다. AD의 잠금 정책과 관련 하 여 다음과 같은 세 가지 설정이 있습니다.
- **계정 잠금 임계값**:이 설정은 AD FS의 ExtranetLockoutThreshold 설정과 유사 합니다. 사용자 계정이 잠기는 실패 한 로그온 시도 횟수를 결정 합니다. 악의적인 계정 잠금 공격 으로부터 사용자 계정을 보호 하려면 AD FS에서 ExtranetLockoutThreshold의 값을 설정 하려고 합니다 &lt; AD의 계정 잠금 임계값 값
- **계정 잠금 기간**:이 설정은 사용자 계정이 잠겨 있는 기간을 결정 합니다. 이 대화에서는이 대화에 거의 영향을 주지 않습니다. 익스트라넷 잠금은 정상적으로 구성 된 경우 AD 잠금이 발생 하기 전에 항상 발생 해야 합니다.
- **다음 시간 이후에 계정 잠금 카운터 다시 설정**:이 설정은 **badPwdCount** 가 0으로 다시 설정 되기 전에 사용자의 마지막 로그온 오류에서 경과 되어야 하는 시간을 결정 합니다. AD FS의 엑스트라넷 잠금 기능이 AD 잠금 정책에서 잘 작동 하려면 AD FS의 ExtranetObservationWindow 값을 확인 해야 합니다 .이 값은 AD의 [계정 잠금] 카운터 다시 설정 값을 @no__t 합니다. 다음 예에서는 이러한 이유를 설명 합니다.  

두 가지 예를 살펴보고 다양 한 설정 및 상태에 따라 시간이 지남에 따라 **badPwdCount** 어떻게 변화 하는지 살펴보겠습니다. 두 예제 **계정 잠금 임계값** = 4 및 **ExtranetLockoutThreshold** = 2를 가정해 보겠습니다. **빨간색** 화살표는 잘못 된 암호 시도를 나타내고 **녹색** 화살표는 좋은 암호 시도를 나타냅니다. 예 #1에서 **ExtranetObservationWindow** 는 1 @no__t **계정 잠금 카운터를 다시 설정**합니다. 예 #2에서 **ExtranetObservationWindow** 는 1 @no__t **계정 잠금 카운터를 다시 설정**합니다. 

### <a name="example-1"></a>예제 1
![Example1](media/Configure-AD-FS-Extranet-Lockout-Protection/one.png)

### <a name="example-2"></a>예제 2
![Example1](media/Configure-AD-FS-Extranet-Lockout-Protection/two.png)

위에서 볼 수 있듯이 **badPwdCount** 가 0으로 다시 설정 되는 경우 두 가지 조건이 있습니다. 하나는 성공적인 로그온이 있는 경우입니다. 다른 것은 설정 **후 계정 잠금 카운터 다시 설정** 에 정의 된 대로이 카운터를 다시 설정 해야 하는 경우입니다. @No__t-1 **ExtranetObservationWindow** **후 계정 잠금 카운터를 다시 설정** 하는 경우 계정은 AD에 의해 잠기는 위험이 없습니다. 그러나 &gt; **ExtranetObservationWindow** **후 계정 잠금 해제 카운터를 다시 설정** 하는 경우 계정이 AD에 의해 잠겨 있지만 "지연 된 방식"으로 잠겨 있을 가능성이 있습니다. 구성에 따라 AD에서 잠긴 계정을 가져오는 데 시간이 걸릴 수 있습니다 AD FS는 **BadPwdCount** **계정 잠금 임계값**에 도달할 때까지 관찰 기간 동안 잘못 된 암호 시도를 허용 합니다.

자세한 내용은 [계정 잠금 구성](https://blogs.technet.microsoft.com/secguide/2014/08/13/configuring-account-lockout/)을 참조 하세요. 

## <a name="known-issues"></a>알려진 문제
**BadPwdCount** 특성이 adfs에서 쿼리 하는 도메인 컨트롤러에 복제 되지 않기 때문에 AD 사용자 계정이 AD FS를 사용 하 여 인증할 수 없는 알려진 문제가 있습니다. 자세한 내용은 [2971171](https://support.microsoft.com/help/2971171/adfs-authentication-issue-for-active-directory-users-when-extranet-loc) 을 참조 하세요. 지금까지 출시 된 모든 AD FS Qfe를 찾을 수 [있습니다.](../deployment/updates-for-active-directory-federation-services-ad-fs.md)

## <a name="key-points-to-remember"></a>기억할 주요 사항
- 엑스트라넷 잠금 기능은 인증 요청이 웹 응용 프로그램 프록시를 통해 제공 되는 **엑스트라넷 시나리오** 에만 적용 됩니다.
- 엑스트라넷 잠금 기능은 **사용자 이름 & 암호 인증** 에만 적용 됩니다.
- AD FS은 일시적으로 잠긴 **badPwdCount** 또는 사용자의 추적을 유지 하지 않습니다. 모든 상태 추적에 AD를 사용 AD FS
- AD FS는 모든 인증 시도에 대해 PDC에서 사용자에 대 한 LDAP 호출을 통해 **badPwdCount** 특성에 대 한 조회를 수행 합니다.  
- 2016 보다 오래 된 AD FS PDC에 액세스할 수 없는 경우 실패 합니다. AD FS 2016에는 PDC를 사용할 수 없는 경우 AD FS 다른 도메인 컨트롤러로 대체 될 수 있는 향상 된 기능이 도입 되었습니다. 
- BadPwdCount < ExtranetLockoutThreshold 인 경우 AD FS는 엑스트라넷의 인증 요청을 허용 합니다. 
- **BadPwdCount** >= **ExtranetLockoutThreshold** 및 **badpasswordtime** + **ExtranetObservationWindow** < 현재 시간 AD FS 엑스트라넷의 인증 요청을 거부 합니다.
- 악의적인 계정 잠금을 방지 하려면 **ExtranetLockoutThreshold** < **계정 잠금 임계값** 및 **ExtranetObservationWindow**@no__t**계정 잠금 다시 설정 계정 잠금 카운터가** 있는지 확인 해야 합니다.


## <a name="additional-references"></a>추가 참조  
- [Active Directory Federation Services 보안에 대 한 모범 사례](../../ad-fs/deployment/best-practices-securing-ad-fs.md)
- [관리자가 아닌 사용자에게 AD FS Powershell Commandlet 액세스 위임](delegate-ad-fs-pshell-access.md)
- [Set-adfsproperties](https://technet.microsoft.com/itpro/powershell/windows/adfs/set-adfsproperties)

[AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md)

    
