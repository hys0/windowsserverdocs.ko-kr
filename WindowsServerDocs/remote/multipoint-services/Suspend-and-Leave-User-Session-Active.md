---
title: 사용자 세션 일시 중단 및 활성 상태 유지
description: 이러한 연결을 끊지 않고 MultiPoint 세션에서 사용자를 일시 중단 하는 방법 알아보기
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5263bce3-fe92-4398-8393-2e3a4e05d530
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: cc4310e6f7609464cf037b750bec6e5e805e0b26
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59815224"
---
# <a name="suspend-and-leave-user-session-active"></a>사용자 세션 일시 중단 및 활성 상태 유지
연결을 끊을 수도 있고 사용자의 세션을 종료 하지 않을 때 MultiPoint 서비스 시스템에서 사용자 일시 중단 수도 있습니다. 또한 관리자가 사용자 세션의 연결을 끊는 대신 사용자가 세션의 연결을 직접 끊을 수도 있습니다. 사용자 세션이 일시 중단되는 동안 세션은 MultiPoint 서비스 시스템의 컴퓨터가 종료되거나 다시 시작될 때까지 해당 컴퓨터의 메모리에 활성 상태로 유지됩니다. 컴퓨터가 종료되거나 다시 시작되면 일시 중단된 모든 세션이 종료되고 저장되지 않은 작업은 손실됩니다.  
  
1.  스테이션 모드의 다중 포인트 관리자를 열고 클릭는 **스테이션** 탭 합니다.  
  
2.  **컴퓨터** 열에서 세션을 일시 중단하려는 컴퓨터 이름을 클릭합니다.  
  
3.  **스테이션 작업**에서 **모든 스테이션 일시 중단**을 클릭합니다.  
  
사용자 세션이 일시 중단된 후 사용자는 같은 스테이션이나 다른 스테이션에 로그온하여 원래 세션에서 작업을 계속할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
[사용자 데스크톱 관리](manage-user-desktops-using-multipoint-dashboard.md)  
[로그 오프 또는 연결 끊기 사용자 세션](Log-off-or-Disconnect-User-Sessions.md)