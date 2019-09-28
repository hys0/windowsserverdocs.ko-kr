---
title: 관리자 계정 만들기
description: MultiPoint 서비스에서 관리자 권한으로 계정 만들기
ms.custom: na
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8ce4c5a9-3dec-412f-910b-54a252f8f209
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 6737f7b96396a13aa18485095e0687425cf8b93e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71389705"
---
# <a name="create-an-administrative-user-account"></a>관리자 계정 만들기
MultiPoint 서비스 시스템을 관리할 개별 사용자에 대해 *관리자 계정*을 만들 수 있습니다. 다중 포인트 관리자에서 관리 액세스 권한이 있는 사용자를 보려면 클릭는 **사용자** 탭 합니다. 관리자 계정은 계정 유형 열에 **관리자**로 표시됩니다. *관리자에 게* 같은 데스크톱 및 시스템 설정을 변경 하는 모든 다중 포인트 관리자 작업에 액세스할 수 있습니다.  
  
-   계정 만들기  
  
-   프로그램 추가 및 제거  
  
-   *데스크톱* 및 하드웨어 관리  
  
-   다른 사용자의 *세션* 종료  
  
관리자는 소프트웨어를 설치하거나 보안 설정을 변경하는 등 MultiPoint 서비스 시스템의 다른 모든 사용자에게 영향을 주는 작업을 수행할 수 있습니다. 이러한 이유로 관리자는 자신만 아는 고유한 사용자 이름 및 암호를 보유해야 합니다.  
  
관리자가 사용자 계정을 만들고 관리할 때 고려해야 하는 문제에 대한 자세한 내용은 [사용자 계정 고려 사항](User-Account-Considerations.md) 항목을 참조하세요.  
  
> [!NOTE]  
> MultiPoint 서비스 시스템에서 MultiPoint 서비스 시스템 관리와 상관없는 작업을 수행할 때 사용할 *표준 사용자 계정*을 만들 수 있습니다. 표준 사용자 계정을 사용하면 시스템 관리 작업을 수행해야 하는 경우에만 관리자 계정으로 로그온하면 됩니다.  
  
#### <a name="to-create-an-administrative-user-account"></a>관리자 계정을 만들려면  
  
1.  다중 포인트 관리자에서 클릭 된 **사용자** 탭 합니다.  
  
2.  **사용자 작업**에서 **사용자 계정 추가**를 클릭합니다. **사용자 계정 추가** 마법사가 열립니다.  
  
3.  **사용자 계정** 필드에 사용자의 로그온 이름을 입력합니다. 일반적으로 로그온 사용자 이름은 이름과 성을 공백 없이 붙여 쓰거나 이름의 이니셜과 성을 붙여 씁니다.  
  
4.  **전체 이름** 필드에 이름, 전체 이름, 애칭 등 원하는 형식으로 사용자 이름을 입력합니다.  
  
5.  **암호** 필드에 사용자의 암호를 입력합니다. 암호는 관리자와 해당 사용자만 알고 있어야 하며, 관리자는 암호 정보를 안전한 곳에 보관해야 합니다. 암호는 관리자만 변경할 수 있습니다.  
  
6.  **암호 확인** 필드에 암호를 다시 입력한 후 **다음**을 클릭합니다.  
  
7.  액세스 수준 페이지에서 **관리자**를 선택한 후 **다음**을 클릭합니다.  
  
8.  MultiPoint 서비스에서 모든 정보를 확인하고 계정이 설정되면 메시지를 표시합니다. **A new user account was successfully created(새 사용자 계정이 만들어졌습니다.)** 라는 텍스트가 표시되면 **마침**을 클릭합니다.  
