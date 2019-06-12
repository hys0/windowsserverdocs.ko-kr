---
title: AD FS에서 장치 인증 제어
description: 이 문서에서는 Windows Server 2016 및 2012 R2 용 AD FS에서 장치 인증을 사용 하는 방법 설명
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 11/09/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f52d3d237573e4ed0028e228ff80273862a0aaf2
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444647"
---
# <a name="device-authentication-controls-in-ad-fs"></a>AD FS에서 장치 인증 제어
다음 문서에는 Windows Server 2016 및 2012 R2에서 장치 인증 제어를 사용 하도록 설정 하는 방법을 보여 줍니다.

## <a name="device-authentication-controls-in-ad-fs-2012-r2"></a>AD FS 2012 r 2에서에서 장치 인증 제어
AD FS 2012 r 2 쓰였던 라는 전역 인증 속성에 원래 `DeviceAuthenticationEnabled` 제어 장치 인증 합니다.

설정을 구성 하는 `Set-AdfsGlobalAuthenticationPolicy` 아래와 같이 cmdlet을 사용 했습니다.


``` powershell
PS:\>Set-AdfsGlobalAuthenticationPolicy –DeviceAuthenticationEnabled $true
```



장치 인증을 사용 하지 않으려면 $false에 값을 설정 하는 동일한 cmdlet 사용 되었습니다.

## <a name="device-authentication-controls-in-ad-fs-2016"></a>AD FS 2016에서에서 장치 인증 제어
2012 R2에서에서 지원 되는 장치 인증 유형만 clientTLS 했습니다.  Ad FS 2016에서 clientTLS 외에도 두 가지가 새 최신 장치 인증에 대 한 장치 인증 합니다.  이러한 항목은 다음과 같습니다.
- PKeyAuth
- PRT

새 동작을 제어 하는 `DeviceAuthenticationEnabled` 라는 새 속성을 조합 하 여 속성은 사용 `DeviceAuthenticationMethod`합니다.  

장치 인증 방법을 수행 되는 장치 인증 유형을 결정 합니다. PRT, PKeyAuth, clientTLS, 또는 이들의 조합 합니다.
다음 값을 포함 합니다.
 - SignedToken: PRT만
 - PKeyAuth: PRT + PKeyAuth
 - ClientTLS: PRT + clientTLS
 - All: 위의 모든 항목

알 수 있듯이 PRT 일부인 모든 장치 인증 방법의 기본 메서드는 항상를 적용에서 하기 사용할 `DeviceAuthenticationEnabled` 로 설정 된 `$true`합니다.

예: 메서드를 구성 하려면 DeviceAuthenticationEnabled cmdlet으로 위의 새 속성과 함께 사용 합니다.

``` powershell
PS:\>Set-AdfsGlobalAuthenticationPolicy –DeviceAuthenticationEnabled $true
```

>[!NOTE]
> ADFS 2019에 `DeviceAuthenticationMethod` 와 함께 사용할 수는 `Set-AdfsRelyingPartyTrust` 명령입니다.

``` powershell
PS:\>Set-AdfsRelyingPartyTrust -DeviceAuthenticationMethod ClientTLS
```

>[!NOTE]
> 장치 인증을 사용 하도록 설정 (설정 `DeviceAuthenticationEnabled` 를 `$true`) 의미 합니다 `DeviceAuthenticationMethod` 로 암시적으로 설정 되어 `SignedToken`, 동등 **PRT**합니다.


``` powershell
PS:\>Set-AdfsGlobalAuthenticationPolicy –DeviceAuthenticationMethod All
```
> [!NOTE]
> 기본 장치 인증 방법이 `SignedToken`합니다.  다른 값은 **PKeyAuth 합니다**<strong>ClientTLS,</strong> 하 고 **모든**합니다.

의미는 `DeviceAuthenticationMethod` AD FS 2016이 릴리스된 이후 값이 약간 변경 합니다.  업데이트 수준에 따라 각 값의 의미에 대 한 아래 표를 참조 하세요.


|AD FS 버전|DeviceAuthenticationMethod 값|의미|
| ----- | ----- | ----- |
|2016 RTM|SignedToken|PRT + PkeyAuth|
||clientTLS|clientTLS|
||All|PRT + PkeyAuth + clientTLS|
|2016 RTM + Windows 업데이트를 사용 하 여 날짜를 설정 합니다.|SignedToken (변경 된 의미 함)|PRT (전용)|
||PkeyAuth (신규)|PRT + PkeyAuth|
||clientTLS|PRT + clientTLS|
||All|PRT + PkeyAuth + clientTLS|

## <a name="see-also"></a>관련 항목
[AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md)
