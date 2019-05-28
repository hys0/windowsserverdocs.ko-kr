---
ms.assetid: 03c82f43-ae2d-4038-b286-ae3858aed35a
title: 암호 만료 클레임을 보내도록 AD FS 구성
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3be14b824038e9424b86c40bfd657dd988fa99e9
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189873"
---
# <a name="configure-ad-fs-to-send-password-expiry-claims"></a>암호 만료 클레임을 보내도록 AD FS 구성


Active Directory Federation Services (AD FS) ADFS로 보호 되는 신뢰 당사자 트러스트 (응용 프로그램)에 암호 만료 클레임을 보내도록 구성할 수 있습니다. 이러한 클레임을 사용 하는 방법을 응용 프로그램에 따라 달라 집니다. 예를 들어, 신뢰 당사자로 Office 365를 통해 업데이트 하도록 구현 Exchange 및 Outlook 곧에-수-만료 된 암호의 페더레이션된 사용자에 게 알려야 합니다.

암호를 보내도록 AD FS를 구성 하려면 만료 클레임을 신뢰 당사자 트러스트에 추가 해야 다음 클레임 규칙은이 신뢰 당사자 트러스트에:

```
@RuleName = "Issue Password Expiry Claims"
c1:[Type == "http://schemas.microsoft.com/ws/2012/01/passwordexpirationtime"]
 => issue(store = "_PasswordExpiryStore", types = ("http://schemas.microsoft.com/ws/2012/01/passwordexpirationtime", "http://schemas.microsoft.com/ws/2012/01/passwordexpirationdays", "http://schemas.microsoft.com/ws/2012/01/passwordchangeurl"), query = "{0};", param = c1.Value);
```

> [!NOTE]
> 암호 만료 클레임만 작업 인증 형식에 대 한 사용자 이름과 암호 및 Microsoft Passport에 대 한 제공 됩니다.  사용자가 인증 하는 경우 Windows 통합된 인증 및 Passport를 사용 하 여 구성 되지 않은, 클레임을 사용할 수 없습니다 및 사용자 암호 만료 알림이 표시 되지 않습니다.

> [!NOTE]
> 보낸된 클레임을 암호가 14 일 이내에 만료 됩니다 하는 경우에 채워집니다 수 있도록에 14 일 창.

## <a name="see-also"></a>관련 항목
[AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md)
