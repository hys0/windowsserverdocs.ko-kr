---
ms.assetid: 03c82f43-ae2d-4038-b286-ae3858aed35a
title: "ADFS 암호 만료 클레임 보내려면 구성"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 386a5ac921ba609c371121b8657351667628951b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="configure-ad-fs-to-send-password-expiry-claims"></a>ADFS 암호 만료 클레임 보내려면 구성

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

AD FS(Active Directory Federation Services) 암호 만료 클레임 ADFS로 보호 되는 신뢰 파티 신뢰 (응용 프로그램)을 보내려면 구성할 수 있습니다. 이러한 클레임 사용 되는 방식을 응용 프로그램에 따라 다릅니다. 예를 들어, 사용자 당사자로 Office 365, 업데이트 곧-에--만료 암호 연합된 사용자에 게 알리려면 교환 및 Outlook을 구현 되었습니다 했습니다.

암호를 보내려면 ADFS 구성 하려면 만료 주장 신뢰 파티 신뢰 하 추가 해야 다음 청구 규칙이 신뢰 파티 신뢰를:

```
c1:[Type == "https://schemas.microsoft.com/ws/2012/01/passwordexpirationtime"]
=> issue(store = "_PasswordExpiryStore", types = ("https://schemas.microsoft.com/ws/2012/01/passwordexpirationtime", "https://schemas.microsoft.com/ws/2012/01/passwordexpirationdays", "https://schemas.microsoft.com/ws/2012/01/passwordchangeurl"), query = "{0};", param = c1.Value);
```

> [!NOTE]
> 암호 만료 클레임 작업 인증 유형 사용자 이름 및 암호 Microsoft Passport 수만 있습니다.  해당 사용자가 인증 인증과 Passport을 통합 하는 Windows 사용 하 여 구성 되어 있지 않으면 클레임 사용할 수 없습니다 및 사용자가 암호 만료 알림이 표시 되지 않습니다.

> [!NOTE]
> 보낸된 클레임 암호 14 일 이내 만료 되는 경우에 채울 수 있도록에 14 일 창입니다.

## <a name="see-also"></a>참조 하십시오
[AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md)
