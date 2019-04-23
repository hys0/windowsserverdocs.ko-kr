---
title: 사용자 계정 고려 사항
description: 사용자 계정, 사용자 이름 및 암호 고려 사항 MultiPoint 서비스를 제공합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e225900b-cee9-48c9-b21c-394dc5e72b78
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 00fb5e83921ba0b8ad86a6f75bdfd7bf16419b73
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850794"
---
# <a name="user-account-considerations"></a>사용자 계정 고려 사항
이 항목에서는, 관리자는 사용자를 고려해 야 할 사용자 계정 관리를 만들 때 문제를 설명 합니다. 다중 포인트 관리자의 사용자 탭에서 사용자 계정을 관리할 수 있습니다. 자세한 내용은 [사용자 계정 관리](Manage-User-Accounts.md) 항목을 참조하세요.  
  
## <a name="user-account-types"></a>사용자 계정 유형  
사용자 계정은 사용자가 액세스할 수 있는 파일 및 폴더, MultiPoint 서비스 시스템에 대해 변경할 수 있는 사항 및 각 사용자의 기본 설정(예: 바탕 화면 배경)에 관해 MultiPoint 서비스에 알려 주는 정보 컬렉션입니다. 각 사용자는 고유한 사용자 이름 및 암호를 사용하여 자신의 사용자 계정에 액세스합니다. MultiPoint 서비스에는 세 가지 유형의 사용자 계정 지원합니다.  
  
-   **관리자 계정은** 다중 포인트 관리자를 사용 하 여 사용 하 고 MultiPoint 서비스 시스템 관리를 위한 됩니다. 자세한 내용은 [관리자 계정 만들기](Create-an-Administrative-User-Account.md) 항목을 참조하세요.  
  
-   **표준 사용자 계정**은 스테이션에 정기적으로 액세스하지만 시스템을 관리하지는 않을 개인용 계정입니다. 일반적으로 MultiPoint 서비스 시스템의 대다수 사용자에 대해 표준 사용자 계정을 만들어야 합니다. 자세한 내용은 [표준 사용자 계정 만들기](Create-a-Standard-User-Account.md) 항목을 참조하세요.  
  
-   **MultiPoint 대시보드 사용자 계정**은 MultiPoint 대시보드를 사용하여 표준 사용자 세션을 관리하며 모든 스테이션에서 로그온할 수 있는 개인용 계정입니다. 자세한 내용은 [MultiPoint 대시보드 사용자 계정 만들기](Create-a-MultiPoint-Dashboard-User-Account.md) 항목을 참조하세요.  
  
## <a name="user-name-and-password-considerations"></a>사용자 이름 및 암호 고려 사항  
관리자는 소프트웨어를 설치하거나 보안 설정을 변경하는 등 MultiPoint 서비스 시스템의 다른 모든 사용자에게 영향을 주는 작업을 수행할 수 있습니다. 이러한 이유로 관리자는 자신만 아는 고유한 사용자 이름 및 암호를 보유해야 합니다.  
  
사용자 계정에 대한 한 가지 중요한 고려 사항은 Windows 탐색기에서 **내 문서** 폴더를 포함하는 고유한 **문서** 라이브러리를 각 사용자 계정에 할당하는 것입니다. MultiPoint 서비스 시스템의 표준 사용자가 Windows 탐색기에서 자신의 **문서** 라이브러리에 개인 문서를 저장할 경우 자신만 아는 고유한 사용자 이름 및 암호를 사용하여 MultiPoint 서비스 시스템에 로그온해야 합니다. Windows 탐색기에서 문서를 저장하는 방법에 대한 자세한 내용은 [사용자 파일 관리](Manage-User-Files.md) 항목을 참조하세요.  
  
> [!TIP]  
> 시스템 보안을 더욱 강력하게 구현하기 위해 모든 사용자의 암호는 강력한 암호여야 합니다. 강력한 암호는 쉽게 추측할 수 없는 하나 또는 금이 인데 적어도 8 자, 전체 또는 사용자의 계정 이름의 일부를 포함 하지 않는 문자 다음 네 가지 범주 중 세 가지 이상을: 대문자, 소문자, 숫자 및 키보드에 있는 기호 (예:!, @, #).  
  
## <a name="see-also"></a>관련 항목  
[관리 사용자 계정 만들기](Create-an-Administrative-User-Account.md)  
[표준 사용자 계정 만들기](Create-a-Standard-User-Account.md)  
[사용자 파일을 관리](Manage-User-Files.md)
[사용자 계정 관리](Manage-User-Accounts.md)