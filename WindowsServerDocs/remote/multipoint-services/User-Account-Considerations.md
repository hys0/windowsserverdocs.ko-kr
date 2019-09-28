---
title: 사용자 계정 고려 사항
description: MultiPoint 서비스에 대 한 사용자 계정, 사용자 이름 및 암호 고려 사항을 제공 합니다.
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: c81d14d46e96d39676e1fb6fa31892e0d5e1b683
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71389262"
---
# <a name="user-account-considerations"></a>사용자 계정 고려 사항
이 항목에서는, 관리자는 사용자를 고려해 야 할 사용자 계정 관리를 만들 때 문제를 설명 합니다. 다중 포인트 관리자의 사용자 탭에서 사용자 계정을 관리할 수 있습니다. 자세한 내용은 [사용자 계정 관리](Manage-User-Accounts.md) 항목을 참조하세요.  
  
## <a name="user-account-types"></a>사용자 계정 유형  
사용자 계정은 MultiPoint 서비스에 사용자가 액세스할 수 있는 파일 및 폴더, MultiPoint 서비스 시스템에 대해 수행할 수 있는 변경 내용 및 바탕 화면 배경과 같은 각 사용자의 기본 설정에 대 한 정보 모음입니다. 각 사용자는 고유한 사용자 이름 및 암호를 사용하여 자신의 사용자 계정에 액세스합니다. MultiPoint 서비스에는 세 가지 유형의 사용자 계정 지원합니다.  
  
-   **관리자 계정은** 다중 포인트 관리자를 사용 하 여 사용 하 고 MultiPoint 서비스 시스템 관리를 위한 됩니다. 자세한 내용은 [관리자 계정 만들기](Create-an-Administrative-User-Account.md) 항목을 참조하세요.  
  
-   **표준 사용자 계정**은 스테이션에 정기적으로 액세스하지만 시스템을 관리하지는 않을 개인용 계정입니다. 일반적으로 MultiPoint 서비스 시스템의 대다수 사용자에 대해 표준 사용자 계정을 만들어야 합니다. 자세한 내용은 [표준 사용자 계정 만들기](Create-a-Standard-User-Account.md) 항목을 참조하세요.  
  
-   **MultiPoint 대시보드 사용자 계정**은 MultiPoint 대시보드를 사용하여 표준 사용자 세션을 관리하며 모든 스테이션에서 로그온할 수 있는 개인용 계정입니다. 자세한 내용은 [MultiPoint 대시보드 사용자 계정 만들기](Create-a-MultiPoint-Dashboard-User-Account.md) 항목을 참조하세요.  
  
## <a name="user-name-and-password-considerations"></a>사용자 이름 및 암호 고려 사항  
관리자는 소프트웨어를 설치하거나 보안 설정을 변경하는 등 MultiPoint 서비스 시스템의 다른 모든 사용자에게 영향을 주는 작업을 수행할 수 있습니다. 이러한 이유로 관리자는 자신만 아는 고유한 사용자 이름 및 암호를 보유해야 합니다.  
  
사용자 계정에 대한 한 가지 중요한 고려 사항은 Windows 탐색기에서 **내 문서** 폴더를 포함하는 고유한 **문서** 라이브러리를 각 사용자 계정에 할당하는 것입니다. MultiPoint 서비스 시스템의 표준 사용자가 Windows 탐색기에서 자신의 **문서** 라이브러리에 프라이빗 문서를 저장할 경우 자신만 아는 고유한 사용자 이름 및 암호를 사용하여 MultiPoint 서비스 시스템에 로그온해야 합니다. Windows 탐색기에서 문서를 저장하는 방법에 대한 자세한 내용은 [사용자 파일 관리](Manage-User-Files.md) 항목을 참조하세요.  
  
> [!TIP]  
> 더 강력한 시스템 보안을 위해 모든 사용자의 암호는 강력한 암호 여야 합니다. 강력 하 게 추측 하거나 해독할 수 없는 암호는 8 자 이상, 사용자 계정 이름 전체 또는 일부를 포함 하지 않고 대문자, 소문자 등의 네 가지 문자 범주 중 세 가지 이상을 포함 하는 암호입니다. 키보드에서 문자, 숫자 및 기호 (예:!, @, #)를 찾을 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
[관리자 계정 만들기](Create-an-Administrative-User-Account.md)  
[표준 사용자 계정 만들기](Create-a-Standard-User-Account.md)  
[사용자 파일을 관리](Manage-User-Files.md)
[사용자 계정 관리](Manage-User-Accounts.md)