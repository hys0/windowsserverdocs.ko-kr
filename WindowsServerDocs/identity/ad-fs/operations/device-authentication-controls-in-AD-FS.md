---
title: AD FS의 장치 인증 제어
description: 이 문서에서는 Windows Server 2016 및 2012 r 2에 대 한 AD FS에서 장치 인증을 사용 하도록 설정 하는 방법을 설명 합니다.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 11/09/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 87c011b18ad4a1d464072c1ea90b09a44e831378
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407369"
---
# <a name="device-authentication-controls-in-ad-fs"></a>AD FS의 장치 인증 제어
다음 문서에서는 Windows Server 2016 및 2012 r 2에서 장치 인증 제어를 사용 하도록 설정 하는 방법을 보여 줍니다.

## <a name="device-authentication-controls-in-ad-fs-2012-r2"></a>AD FS 2012 R2의 장치 인증 제어
원래 AD FS 2012 r 2에서는 장치 인증을 제어 하는 `DeviceAuthenticationEnabled` 라는 전역 인증 속성이 하나 있습니다.

설정을 구성 하기 위해 `Set-AdfsGlobalAuthenticationPolicy` cmdlet은 아래와 같이 사용 되었습니다.


``` powershell
PS:\>Set-AdfsGlobalAuthenticationPolicy –DeviceAuthenticationEnabled $true
```



장치 인증을 사용 하지 않도록 설정 하려면 동일한 cmdlet을 사용 하 여 값을 $false 설정 합니다.

## <a name="device-authentication-controls-in-ad-fs-2016"></a>AD FS 2016의 장치 인증 제어
2012 r 2에서 지원 되는 장치 인증 유형은 clientTLS 뿐입니다.  AD FS 2016에는 clientTLS 외에도 최신 장치 인증에 대 한 두 가지 새로운 유형의 장치 인증이 있습니다.  이러한 항목은 다음과 같습니다.
- PKeyAuth
- .PRT

새 동작을 제어 하기 위해 `DeviceAuthenticationEnabled` 속성은 `DeviceAuthenticationMethod`라는 새 속성과 함께 사용 됩니다.  

장치 인증 방법에 따라 수행 되는 장치 인증 유형 (PRT, PKeyAuth, clientTLS 또는 일부 조합)이 결정 됩니다.
값은 다음과 같습니다.
 - 이상 토큰: PRT만
 - PKeyAuth: PRT + PKeyAuth
 - ClientTLS: PRT + clientTLS
 - 모두: 위의 모든

여기서 볼 수 있듯이, PRT는 모든 장치 인증 방법의 일부 이므로 `DeviceAuthenticationEnabled` `$true`설정 된 경우 항상 사용 하도록 설정 되는 기본 메서드에 적용 됩니다.

예: 메서드를 구성 하려면 새 속성과 함께 다음과 같이 DeviceAuthenticationEnabled cmdlet을 사용 합니다.

``` powershell
PS:\>Set-AdfsGlobalAuthenticationPolicy –DeviceAuthenticationEnabled $true
```

>[!NOTE]
> ADFS 2019에서는 `Set-AdfsRelyingPartyTrust` 명령과 함께 `DeviceAuthenticationMethod`를 사용할 수 있습니다.

``` powershell
PS:\>Set-AdfsRelyingPartyTrust -DeviceAuthenticationMethod ClientTLS
```

>[!NOTE]
> 장치 인증을 사용 하도록 설정 하면 (`DeviceAuthenticationEnabled` `$true`) `DeviceAuthenticationMethod` 암시적으로 `SignedToken`로 설정 되 고,이는 **PRT**와 동일 함을 의미 합니다.


``` powershell
PS:\>Set-AdfsGlobalAuthenticationPolicy –DeviceAuthenticationMethod All
```
> [!NOTE]
> 기본 장치 인증 방법을 `SignedToken`합니다.  다른 값은 **PKeyAuth,** <strong>Clienttls</strong> 및 **All**입니다.

AD FS 2016가 릴리스된 이후 `DeviceAuthenticationMethod` 값의 의미가 약간 변경 되었습니다.  업데이트 수준에 따라 각 값의 의미에 대해서는 아래 표를 참조 하세요.


|AD FS 버전|DeviceAuthenticationMethod 값|그러므로|
| ----- | ----- | ----- |
|2016 RTM|서명 토큰|PRT + PkeyAuth|
||clientTLS|clientTLS|
||모두|PRT + PkeyAuth + clientTLS|
|2016 RTM 이상 Windows 업데이트 포함 된 최신 버전|공용 토큰 (변경 된 의미)|PRT (만 해당)|
||PkeyAuth (신규)|PRT + PkeyAuth|
||clientTLS|PRT + clientTLS|
||모두|PRT + PkeyAuth + clientTLS|

## <a name="see-also"></a>참고 항목
[AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md)
