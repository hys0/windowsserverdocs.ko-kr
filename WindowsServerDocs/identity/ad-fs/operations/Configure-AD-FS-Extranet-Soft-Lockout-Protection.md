---
ms.assetid: 777aab65-c9c7-4dc9-a807-9ab73fac87b8
title: AD FS 엑스트라넷 잠금 보호를 구성 합니다.
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 02/01/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 6612c05e664b50c5a50b10b712b91715cc85d230
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189876"
---
# <a name="configure-ad-fs-extranet-lockout-protection"></a>AD FS 엑스트라넷 잠금 보호를 구성 합니다.

Windows Server 2012 R2에서 AD FS 엑스트라넷 잠금 라는 보안 기능을 소개 했습니다.  이 기능을 사용 하 여 AD FS는 "stop" 기간에 대 한 외부에서 "악의적인" 사용자 계정을 인증 합니다.  이렇게 하면 사용자 계정을 Active Directory에서 잠기지 않습니다.  사용자가 AD 계정 잠금에서를 보호 하는 것 외에도 AD FS 엑스트라넷 잠금도 막을 무차별 암호 추측 공격

> [!NOTE]
> 이 기능에만 작동 합니다 **엑스트라넷 시나리오** 인증 요청에 적용 됩니다 및 웹 응용 프로그램 프록시를 통해 제공 하는 경우 **사용자 이름 및 암호 인증**합니다.

## <a name="advantages-of-extranet-lockout"></a>엑스트라넷 잠금의 장점
엑스트라넷 잠금 다음과 같은 이점이 키:
- 사용자 계정을 보호 **무차별 암호 대입 공격** 공격자가 지속적으로 인증 요청을 전송 하 여 사용자의 암호를 추측 하려고 하는 위치입니다. AD FS 엑스트라넷 액세스에 대 한 악의적인 사용자 계정을 잠그게 될이 예제의 경우
- 사용자 계정을 보호 **악성 계정 잠금** 공격자가 잘못 된 암호를 사용 하 여 인증 요청을 전송 하 여 사용자 계정을 잠글 하려고 하는 위치입니다. 이 경우에 대 한 엑스트라넷 액세스에 대 한 AD FS에서 사용자 계정이 잠기게 됩니다, 있지만 AD에서 실제 사용자 계정이 잠겨 있지 및 사용자 조직 내에서 회사 리소스에 계속 액세스할 수 있습니다. 이것을 **소프트 잠금**합니다.

## <a name="how-it-works"></a>작동 방법
이 기능을 사용 하도록 구성 해야 하는 AD FS에는 다음과 같은 3 개의 설정이 있습니다. 
- **EnableExtranetLockout &lt;부울&gt;**  이 부울 값으로 설정 엑스트라넷 잠금을 사용 하도록 설정 하려는 경우 True입니다.
- **ExtranetLockoutThreshold &lt;정수&gt;**  이 잘못 된 암호 시도의 최대 수를 정의 합니다. 임계값에 도달 하면, ADFS 암호 정상 인지, 엑스트라넷 관찰 창 전달 될 때까지 여부에 관계 없이 인증에 대 한 도메인 컨트롤러에 연결을 시도 하지 않고 엑스트라넷의 요청을 즉시 거부 합니다. 즉, 변수의 **badPwdCount** 계정이 소프트 잠긴 초과 하는 동안 AD 계정의 특성 늘어납니다.
- **ExtranetObservationWindow &lt;TimeSpan&gt;**  기간 사용자 계정이 더 소프트-잠겨 결정 합니다. AD FS는 창에 전달 되 면 사용자 이름 및 암호 인증을 다시 수행 하기 시작 합니다. AD FS 엑스트라넷 관찰 창에 통과 하는지 여부를 결정 하는 것에 대 한 참조로 AD 특성 badPasswordTime를 사용 합니다. 현재 창이 경과 시간 > badPasswordTime + ExtranetObservationWindow 합니다. 

> [!NOTE]
> AD FS 엑스트라넷 잠금 AD 잠금 정책에서 독립적으로 작동 합니다. 그러나이 좋습니다 설정 하는 **ExtranetLockoutThreshold** AD 계정 잠금 임계값 보다 작은 값으로 매개 변수 값입니다. 이렇게 하려면 실패 한 AD FS에서 Active Directory에서 잠긴 계정을 보호 하는 것으로 반환 됩니다. 

최대 15 잘못 된 암호 시도 횟수와 30 분 소프트 잠금 기간을 사용 하 여 엑스트라넷 잠금 기능 사용의 예는 다음과 같습니다.

```powershell
Set-AdfsProperties -EnableExtranetLockout $true -ExtranetLockoutThreshold 15 -ExtranetObservationWindow (new-timespan -Minutes 30)
```

이러한 설정은 AD FS 서비스를 인증할 수 있는 모든 도메인에 적용 됩니다. 작동 하는 방식은 AD FS 인증 요청을 받으면 LDAP 호출을 통해 주 도메인 컨트롤러 (PDC)에 액세스 하 고에 대 한 조회를 수행 합니다 **badPwdCount** PDC에서 사용자에 대 한 특성입니다. AD FS의 값을 찾으면 **badPwdCount** > = ExtranetLockoutThreshold 설정 및 엑스트라넷 관찰 창에 정의 된 시간이 경과 하지 않은 아직 AD FS는 여부에 관계 없이 즉는 요청을 즉시 거부 합니다 엑스트라넷에서 좋은 또는 잘못 된 암호를 입력 하는 사용자, 로그온 실패로 인해 AD FS ad 자격 증명을 보내지 않습니다. AD FS 관련해 서 모든 상태를 유지 하지 않습니다 **badPwdCount** 또는 사용자 계정이 잠겨 있습니다. AD FS 추적 하는 모든 상태에 대 한 AD를 사용 합니다. 

> [!warning]
> Server 2012 R2에서 AD FS 엑스트라넷 잠금 사용 하는 경우 WAP 통해 모든 인증 요청은 PDC에서 AD FS에서 유효성이 검사 됩니다. PDC를 사용할 수 없는 사용자가 엑스트라넷에서 인증할 수 없습니다.

Server 2016 PDC를 사용할 수 없는 경우 다른 도메인 컨트롤러에 게 대체 하도록 AD FS를 허용 하는 추가 매개 변수를 제공 합니다.

- **ExtranetLockoutRequirePDC &lt;부울&gt;**  -사용 하도록 설정 하는 경우: 엑스트라넷 잠금 주 도메인 컨트롤러 (PDC) 필요 합니다. 사용 하지 않도록 설정 하는 경우: 엑스트라넷 잠금 PDC를 사용할 수 없는 경우 다른 도메인 컨트롤러에 대체 됩니다.

Server 2016에서 AD FS 엑스트라넷 잠금 구성 하려면 다음 Windows PowerShell 명령을 사용할 수 있습니다.

```powershell
Set-AdfsProperties -EnableExtranetLockout $true -ExtranetLockoutThreshold 15 -ExtranetObservationWindow (new-timespan -Minutes 30) -ExtranetLockoutRequirePDC $false
```

## <a name="working-with-the-active-directory-lockout-policy"></a>Active Directory 잠금 정책을 사용 하 여 작업
AD fs에서 엑스트라넷 잠금 기능은 작동 하지 AD 잠금 정책에서 독립적으로 합니다. 그러나 for 있는지 확인 하려면 설정을 엑스트라넷 잠금이 AD 잠금 정책을 사용 하 여 해당 보안 목적을 서비스할 수 있도록 올바르게 구성 되어 수행 해야 합니다.
첫 번째 AD 잠금 정책에 대해를 살펴보겠습니다. AD에서 가지 잠금 정책에 대 한 세 가지 설정이 있습니다.
- **계정 잠금 임계값**:이 설정은 AD FS에서 ExtranetLockoutThreshold 설정을 비슷합니다. 사용자 계정을 잠글 수에 실패 한 로그온 시도 횟수를 결정 합니다. AD FS에서 ExtranetLockoutThreshold의 값을 설정 하려는 사용자 계정을 악의적인 계정 잠금 공격 으로부터 보호 하기 위해 &lt; AD의 계정 잠금 임계값
- **계정 잠금 기간**: 계정이 잠겼습니다 기간 사용자에 대 한이 설정에 따라 결정 됩니다. 이 설정에 상관 없이 훨씬이 대화에서 엑스트라넷 잠금 해야 올바르게 구성 하는 경우 AD 잠금 발생 하기 전에 항상 발생 됩니다.
- **시간 이후 계정 잠금 재설정**:이 설정은 결정 하기 전에 사용자의 마지막 로그온 실패에서 시간 경과 해야 **badPwdCount** 0으로 다시 설정 됩니다. 되도록 ExtranetObservationWindow은 AD FS에서 원하는 순서로 AD fs에서 엑스트라넷 잠금 기능에 대 한 AD 잠금 정책을 잘 작동 하도록 &gt; AD에서 재설정 시간 이후 계정 잠금 값입니다. 아래 예제에서는 그 이유를 설명 합니다.  

참조와 두 가지 예를 살펴보면 보겠습니다 어떻게 **badPwdCount** 다른 설정 및 상태에 따라 시간이 지남에 따라 변경 합니다. 두 예에서 가정해 보겠습니다 **계정 잠금 임계값** = 4 및 **ExtranetLockoutThreshold** = 2입니다. 합니다 **빨간색** 화살표 나타내는 잘못 된 암호 시도가 합니다 **녹색** 화살표 적절 한 암호 시도 나타냅니다. 예제 #1 **ExtranetObservationWindow** &gt; **재설정 시간 이후 계정 잠금**합니다. 예제 #2 **ExtranetObservationWindow** &lt; **재설정 시간 이후 계정 잠금**합니다. 

### <a name="example-1"></a>예제 1
![Example1](media/Configure-AD-FS-Extranet-Lockout-Protection/one.png)

### <a name="example-2"></a>예제 2
![Example1](media/Configure-AD-FS-Extranet-Lockout-Protection/two.png)

위에서 볼 수 있습니다, 두 가지 조건 **badPwdCount** 0으로 다시 설정 됩니다. 하나는 성공적으로 로그온 한 경우입니다. 때에 정의 된 대로이 카운터를 다시 설정 하는 다른 **다시 설정 시간 이후 계정 잠금** 설정 합니다. 때 **다시 설정 시간 이후 계정 잠금** &lt; **ExtranetObservationWindow**, 계정에 ad 잠그기의 위험 없는 합니다. 그러나 경우 **다시 설정 시간 이후 계정 잠금** &gt; **ExtranetObservationWindow**, 가능성이 계정을 "지연 방식 으로" 하지만 AD에 의해 잠겨 있을 수 있습니다. 잠겨 AD에서 구성에 따라 AD FS만 허용 하는 한 잘못 된 암호 시도 될 때까지 해당 관찰 기간 동안 계정을 생성 하려면 잠시 걸릴 수 있습니다 **badPwdCount** 도달 하면 **계정 잠금 임계값** .

자세한 내용은 [계정 잠금 구성](https://blogs.technet.microsoft.com/secguide/2014/08/13/configuring-account-lockout/)합니다. 

## <a name="known-issues"></a>알려진 문제
알려진된 문제 때문에 AD FS를 사용 하 여 AD 사용자 계정을 인증할 수 없습니다는 **badPwdCount** 특성 ADFS를 쿼리 하는 도메인 컨트롤러에 복제 되지 않습니다. 참조 [2971171](https://support.microsoft.com/help/2971171/adfs-authentication-issue-for-active-directory-users-when-extranet-loc) 대 한 자세한 내용은 합니다. 지금까지 출시 된 모든 AD FS Qfe를 찾을 수 있습니다 [여기](../deployment/updates-for-active-directory-federation-services-ad-fs.md)합니다.

## <a name="key-points-to-remember"></a>기억해 야 할 주요 사항
- 엑스트라넷 잠금 기능에만 작동 합니다 **엑스트라넷 시나리오** 웹 응용 프로그램 프록시를 통한 인증 요청이 발생 한 위치
- 엑스트라넷 잠금 기능에만 적용 됩니다 **사용자 이름 및 암호 인증**
- AD FS의 모든 추적을 유지 하지 않습니다 **badPwdCount** 또는 소프트-차단 된 사용자입니다. AD FS 추적 하는 모든 상태에 대 한 AD 사용
- AD FS에 대 한 조회를 수행 합니다 **badPwdCount** 모든 인증 시도 대 한 PDC에서 사용자에 대 한 LDAP 호출을 통해 특성  
- AD FS 2016 보다 오래 된 PDC에 액세스할 수 없으면 실패 합니다. AD FS 2016 AD FS PDC 경우 다른 도메인 컨트롤러에 대체를 사용할 수 없는 수 있도록 향상 된 기능을 도입 합니다. 
- AD FS 엑스트라넷 경우의 인증 요청을 사용 하면 badPwdCount < ExtranetLockoutThreshold 
- 하는 경우 **badPwdCount** >= **ExtranetLockoutThreshold** AND **badPasswordTime** + **ExtranetObservationWindow** < 현재 AD FS 엑스트라넷에서 인증 요청을 거부 됩니다
- 악의적인 계정 잠금을 방지 하려면 해야 **ExtranetLockoutThreshold** < **계정 잠금 임계값** AND **ExtranetObservationWindow**  >  **계정 잠금 해제 카운터 다시 설정**


## <a name="additional-references"></a>추가 참조  
- [Active Directory Federation Services 보안에 대 한 모범 사례](../../ad-fs/deployment/best-practices-securing-ad-fs.md)
- [관리자가 아닌 사용자에게 AD FS Powershell Commandlet 액세스 위임](delegate-ad-fs-pshell-access.md)
- [Set-AdfsProperties](https://technet.microsoft.com/itpro/powershell/windows/adfs/set-adfsproperties)

[AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md)

    
