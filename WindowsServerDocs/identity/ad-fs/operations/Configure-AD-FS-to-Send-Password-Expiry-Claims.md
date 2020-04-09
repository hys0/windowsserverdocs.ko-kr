---
ms.assetid: 03c82f43-ae2d-4038-b286-ae3858aed35a
title: 암호 만료 클레임을 보내도록 AD FS 구성
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: a0c04f42cbe29b1ea36d09f1f148fb28280d7fec
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859896"
---
# <a name="configure-ad-fs-to-send-password-expiry-claims"></a>암호 만료 클레임을 보내도록 AD FS 구성


ADFS로 보호 되는 신뢰 당사자 트러스트 (응용 프로그램)에 암호 만료 클레임을 보내도록 Active Directory Federation Services (AD FS)을 구성할 수 있습니다. 이러한 클레임을 사용 하는 방법을 애플리케이션에 따라 달라 집니다. 예를 들어, 신뢰 당사자로 Office 365를 통해 업데이트 하도록 구현 Exchange 및 Outlook 곧에-수-만료 된 암호의 페더레이션된 사용자에 게 알려야 합니다.

신뢰 당사자 트러스트에 암호 만료 클레임을 보내도록 AD FS를 구성 하려면이 신뢰 당사자 트러스트에 다음 클레임 규칙을 추가 해야 합니다.

```
@RuleName = "Issue Password Expiry Claims"
c1:[Type == "https://schemas.microsoft.com/ws/2012/01/passwordexpirationtime"]
 => issue(store = "_PasswordExpiryStore", types = ("https://schemas.microsoft.com/ws/2012/01/passwordexpirationtime", "https://schemas.microsoft.com/ws/2012/01/passwordexpirationdays", "https://schemas.microsoft.com/ws/2012/01/passwordchangeurl"), query = "{0};", param = c1.Value);
```

> [!NOTE]
> 암호 만료 클레임은 사용자 이름 및 암호와 Microsoft Passport for Work 인증 유형에만 사용할 수 있습니다.  사용자가 Windows 통합 인증을 사용 하 여 인증 하 고 Passport가 구성 되지 않은 경우에는 클레임을 사용할 수 없게 되며 사용자에 게 암호 만료 알림이 표시 되지 않습니다.

> [!NOTE]
> 14 일 기간이 있으므로 암호가 14 일 이내에 만료 되는 경우에만 전송 된 클레임이 채워집니다.

## <a name="see-also"></a>참고 항목
[AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md)
