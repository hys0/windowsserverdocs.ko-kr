---
title: 사용자 스테이션 관리
description: MultiPoint 서비스에서 사용자 스테이션을 관리 하는 방법 알아보기
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: b418578d-3a4c-49b0-90db-8389b320b2f6
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 7b434002b5f542e3a9242290217fa66d418ee2f1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853496"
---
# <a name="manage-user-stations"></a>사용자 스테이션 관리
이 섹션에서는 MultiPoint 서비스 시스템을 구성하는 *스테이션*의 관리에 대해 논의합니다. MultiPoint 서비스 시스템 관리에는 다중 포인트 관리자의 하드웨어 및 소프트웨어 구성 요소 관리가 모두 포함 됩니다. MultiPoint 서비스 시스템에서 데스크톱은 각 사용자 스테이션의 모니터에 표시 된 소프트웨어 사용자 인터페이스입니다.  
  
## <a name="station-status"></a>스테이션 상태  
**스테이션** 탭에서 각 데스크톱에 대해 다음과 같은 유형의 상태를 확인할 수 있습니다. 상태는 다음과 같습니다.  
  
-   로그온된 사용자  
  
-   일시 중단되었지만, 컴퓨터에서 계속 활성화된 사용자 세션  
  
-   사용 중인 스테이션 및 해당 사용자  
  
데스크톱 상태를 보는 방법에 대한 자세한 내용은 [사용자 연결 상태 보기](View-User-Connection-Status.md) 항목을 참조하세요.  

>[!TIP] 
> 각 스테이션에 이름을 할당하면 스테이션을 보다 쉽게 식별할 수 있습니다. 할당된 화면에 스테이션 이름을 표시하는 **Identify station**(스테이션 식별)을 사용합니다.
  
## <a name="different-ways-to-log-standard-users-off-of-the-multipoint-services-system"></a>표준 사용자를 MultiPoint 서비스 시스템에서 로그오프하는 다양한 방법  
*관리자*는 언제든지 Windows에서 로그오프할 수 있으며, 이는 MultiPoint 서비스 시스템의 활성 사용자에게 어떤 영향도 주지 않습니다. *표준 사용자*도 세션의 *연결을 끊거나* MultiPoint 서비스 시스템에서 *로그오프*할 수 있습니다. 관리자가 디스크 보호를 사용하도록 설정한 경우 사용자는 업무를 마치면 작업을 컴퓨터 또는 외부 저장 장치에 저장해야 합니다. 그렇게 하면 MultiPoint 서비스 시스템이 종료되더라도, 다음 날 저장했던 작업을 계속 검색할 수 있습니다.  
  
관리자는 사용자가 로그 오프 하는 대신 표준 사용자의 *세션*을 종료 해야 할 수 있습니다. 다음 두 가지 방법 중 하나로 표준 사용자의 세션을 종료할 수 있습니다.  
  
-   세션을 종료하고 사용자를 로그오프합니다. 사용자의 세션을 종료 하는 방법에 대 한 자세한 내용은 [사용자 세션 종료](End-a-User-Session.md) 항목을 참조 하세요.  
  
-   사용자를 일시 중단 하 여 사용자의 세션을 일시적으로 종료 하지만 MultiPoint 서비스 시스템의 컴퓨터 메모리에서 세션을 활성 상태로 유지 합니다. 이렇게 하면 연결이 일시 중단된 사용자는 동일한 스테이션이나 다른 스테이션에서 해당 세션에 다시 연결하여 작업을 계속할 수 있습니다. 사용자의 세션을 일시 중단 하는 방법에 대 한 자세한 내용은 [사용자 세션 일시 중단 및 활성 상태 유지](Suspend-and-Leave-User-Session-Active.md) 항목을 참조 하세요.  
  
## <a name="set-a-station-to-automatically-log-on"></a>스테이션이 자동으로 로그온되도록 설정  
관리자는 MultiPoint 서비스를 실행 중인 컴퓨터가 시작되면 하나 이상의 스테이션이 자동으로 로그온되도록 설정할 수 있습니다. 자동으로 로그온하는 방법에 대한 자세한 내용은 [스테이션에서 자동 로그온 설정](Set-up-a-Station-for-Automatic-Logon.md) 항목을 참조하세요.  
  
## <a name="split-a-station"></a>스테이션 분할  
해상도가 1024x768 이상인 모든 스테이션 모니터는 두 스테이션으로 분할할 수 있습니다. 스테이션을 분할하는 방법에 대한 자세한 내용은 [사용자 스테이션 분할](Split-a-User-Station.md) 항목을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
[사용자 연결 상태 보기](View-User-Connection-Status.md)  
[사용자 세션 로그오프 또는 연결 끊기](Log-off-or-Disconnect-User-Sessions.md)  
[사용자 세션 일시 중단 및 활성 상태로 유지](Suspend-and-Leave-User-Session-Active.md)  
[자동 로그온을 위한 스테이션 설정](Set-up-a-Station-for-Automatic-Logon.md)  
[사용자 세션 종료](End-a-User-Session.md)  
[사용자 스테이션 분할](Split-a-User-Station.md)