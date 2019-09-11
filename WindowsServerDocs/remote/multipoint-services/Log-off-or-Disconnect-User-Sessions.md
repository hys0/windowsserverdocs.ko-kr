---
title: 사용자 세션 로그오프 또는 연결 끊기
description: 사용자를 수동으로 로그 오프 하는 방법 알아보기
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3e9bbcdc-e33b-481e-8b46-787a4f6d58bc
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 0e516a617341ffebadbdeb571a39f50369446f11
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70871651"
---
# <a name="log-off-or-disconnect-user-sessions"></a>사용자 세션 로그오프 또는 연결 끊기
MultiPoint 서비스 사용자가 로그온 하 고 더라도 모든 Windows 세션의 데스크톱 세션에서 로그 수 있습니다. 또한 사용자는 MultiPoint 서비스 스테이션을 사용 하지 않도록 세션의 연결을 끊거나 일시 중단 하거나, 해당 세션이 MultiPoint 서비스 시스템의 컴퓨터 메모리에 활성 상태로 남아 있습니다.  
  
또한 관리자는 사용자가 MultiPoint 서비스 세션에서 다른 일을 하거나 시스템에서 로그 오프 하는 것을 잊은 경우 사용자의 세션을 종료할 수 있습니다.  
  
## <a name="logging-off-or-disconnecting-a-session"></a>세션 로그오프 또는 연결 끊기  
다음 표에서는 관리자나 다른 사용자가 세션을 로그오프하거나 일시 중단하거나 종료하는 데 사용할 수 있는 다양한 옵션에 대해 설명합니다.  
  
|||  
|-|-|  
|**작업**|**효과**|  
|클릭 **시작**, 설정, 사용자 이름 (오른쪽 위 모퉁이)을 클릭 한 다음 **로그 아웃**합니다.|세션이 종료되고 모든 사용자가 스테이션에 로그온할 수 있습니다.|  
|**시작**, **설정**, 전원, **연결 끊기**를 차례로 클릭합니다.|세션의 연결이 끊기고 세션은 컴퓨터 메모리에 유지됩니다. 동일한 사용자나 다른 사용자가 스테이션에 로그온할 수 있게 됩니다.|  
|클릭 **시작**, 설정, 사용자 이름 (오른쪽 위 모퉁이)을 클릭 한 다음 **잠금**|스테이션이 잠기고 세션은 컴퓨터 메모리에 유지됩니다.|  
  
## <a name="suspending-or-ending-a-users-session"></a>사용자 세션 일시 중단 또는 종료  
다음 표에서는 관리자가 사용자 세션의 연결을 끊거나 사용자 세션을 종료 하는 데 사용할 수 있는 다양 한 옵션에 대해 설명 합니다.  
  
|||  
|-|-|  
|**작업**|**효과**|  
|**일시 중단** 다중 포인트 관리자에서 **스테이션** 탭을 사용 하 여 사용자 세션을 일시 중단 합니다. 자세한 내용은 [사용자 세션 일시 중단 및 활성 상태 유지](Suspend-and-Leave-User-Session-Active.md) 항목을 참조하세요.|사용자의 세션이 종료 되 고 컴퓨터 메모리에 유지 됩니다. 동일한 사용자나 다른 사용자가 스테이션에 로그온할 수 있게 됩니다. 사용자는 동일한 스테이션이나 다른 스테이션에 로그온하여 해당 작업을 계속할 수 있습니다.|  
|**종단** 다중 포인트 관리자에서 **스테이션** 탭을 사용 하 여 사용자의 세션을 종료 합니다. **스테이션** 탭에서 모든 사용자 세션을 종료할 수도 있습니다. 자세한 내용은 [사용자 세션 종료](End-a-User-Session.md) 항목을 참조하세요.|사용자의 세션이 종료 되 고 모든 사용자가 스테이션에 로그온 하는 데 사용할 수 있습니다. 사용자의 세션이 더 이상 **스테이션** 탭에 표시 되지 않고 컴퓨터 메모리에 표시 되지 않습니다.|  
  
## <a name="see-also"></a>관련 항목  
[사용자 세션 일시 중단 및 활성 상태로 유지](Suspend-and-Leave-User-Session-Active.md)  
[사용자 세션 종료](End-a-User-Session.md)  
[사용자 데스크톱 관리](manage-user-desktops-using-multipoint-dashboard.md)  
[사용자 세션 로그오프](Log-Off-User-Sessions.md)    