---
title: 사용자 세션 일시 중단 및 활성 상태 유지
description: 연결을 끊지 않고 MultiPoint 세션에서 사용자를 일시 중단 하는 방법을 알아봅니다.
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 5263bce3-fe92-4398-8393-2e3a4e05d530
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 2d2771fd60f4d8c11c602a4c5d55f3b5ae2d8b11
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861626"
---
# <a name="suspend-and-leave-user-session-active"></a>사용자 세션 일시 중단 및 활성 상태 유지
사용자의 세션을 종료 하지 않으려는 경우 MultiPoint 서비스 시스템에서 사용자의 연결을 끊거나 일시 중단할 수 있습니다. 또한 관리자가 사용자 세션의 연결을 끊는 대신 사용자가 세션의 연결을 직접 끊을 수도 있습니다. 사용자 세션이 일시 중단 된 동안에는 컴퓨터가 종료 되거나 다시 시작 될 때까지 MultiPoint 서비스 시스템의 컴퓨터 메모리에서 세션이 활성 상태로 유지 됩니다. 컴퓨터가 종료되거나 다시 시작되면 일시 중단된 모든 세션이 종료되고 저장되지 않은 작업은 손실됩니다.  
  
1.  스테이션 모드의 다중 포인트 관리자를 열고 클릭는 **스테이션** 탭 합니다.  
  
2.  **컴퓨터** 열에서 세션을 일시 중단하려는 컴퓨터 이름을 클릭합니다.  
  
3.  **스테이션 작업**에서 **모든 스테이션 일시 중단**을 클릭합니다.  
  
사용자 세션이 일시 중단된 후 사용자는 같은 스테이션이나 다른 스테이션에 로그온하여 원래 세션에서 작업을 계속할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[사용자 데스크톱 관리](manage-user-desktops-using-multipoint-dashboard.md)  
[사용자 세션 로그오프 또는 연결 끊기](Log-off-or-Disconnect-User-Sessions.md)