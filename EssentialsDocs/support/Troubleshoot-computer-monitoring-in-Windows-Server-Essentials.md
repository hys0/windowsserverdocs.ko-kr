---
title: "Windows Server Essentials의 컴퓨터를 모니터링 하는 문제 해결"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f1e6b377-4a24-4d28-9b25-05910914826b
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 72fe309e0e7ce6d7227cce8b7f2c5dbf018eb4a1
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="troubleshoot-computer-monitoring-in-windows-server-essentials"></a>Windows Server Essentials의 컴퓨터를 모니터링 하는 문제 해결

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

이 항목에서는 Alert 뷰어 및 Windows Server Essentials에 알림에 메일을 통해 컴퓨터의 상태를 모니터링 하는 동안 발생 하는 문제를 해결 합니다.  
  
> [!NOTE]
>  Windows Server Essentials 커뮤니티에서 가장 최근 문제 해결 정보에 대 한 것이 좋습니다 방문 하 여 [Windows Server Essentials 포럼](https://social.technet.microsoft.com/Forums/winserveressentials/threads)합니다. Windows Server Essentials 포럼에 대 한 도움말을 검색 하거나 질문 하기에 좋은 장소입니다.  
  
##  <a name="BKMK_TS"></a>알림에 대 한 메일 알림을 문제 해결  
 이 섹션에 알림에 대 한 메일 알림을 사용 하는 경우 발생할 수 있는 다양 한 문제 나열 됩니다.  
  
### <a name="cannot-send-the-test-email-for-the-alert"></a>알림에 대 한 테스트 메일을 받을 수 없습니다  
 **문제** 오류가 발생 하 라는 메시지가 표시 알림에 대 한 테스트 메일을 받을 수 없습니다.  
  
 **원인** 알림 기능에 대 한 설정에는 다음과 같은 문제 때문에이 오류가 발생할 수 있습니다.  
  
-   잘못 된 SMTP 서버 이름 또는 포트 번호입니다.  
  
-   것은 잘못 지정 SMTP 서버 단일 소켓 층 (SSL) 연결을 해야 한다는.  
  
-   잘못 된 자격 증명 입력 된 및 SMTP 서버 인증을 요구 합니다.  
  
 **솔루션** 메일 알림 설정에서 오류를 수정 합니다.  
  
##### <a name="to-identify-issues-in-your-email-notification-settings"></a>메일 알림 설정의 문제를 식별  
  
-   인터넷 서비스 공급자 (ISP) 정확한 SMTP 서버 이름, 포트 번호 및 SSL 사용 요청 합니다.  
  
-   서버에서이 위치에 알림에 대 한 메일 알림에 대 한 로그 파일을 검토 합니다.  
  
     %ProgramData%\Microsoft\Windows Server\Logs\SharedServiceHost-AlertServiceConfig.log  
  
    > [!TIP]
    >  ProgramData 폴더를 보려면 표시 되는 항목 숨겨진 해야 합니다. 함 t s 리본 ProgramData 폴더를 표시 하는 경우 **보기** 탭에 있는 **표시/숨기기** 그룹에서 **숨겨진 항목이** 텍스트 상자 합니다.  
  
##### <a name="to-update-your-email-notification-setup-for-alerts"></a>에 알림에 대 한 메일 알림을 설정을 업데이트합니다  
  
1.  대시보드에서 경고 뷰어를 열려면 오른쪽 위 모서리에서 알림 아이콘을 클릭 합니다.  
  
2.  알림 뷰어 아래쪽 클릭 **알림에 대 한 메일 알림을 설정**합니다.  
  
3.  에 **알림에 대 한 메일 알림을 설정** 대화 상자를 클릭 **사용**합니다.  
  
4.  에 **SMTP 설정** 대화 상자 SMTP 설정을 업데이트와 클릭 한 다음 **확인**합니다.  
  
5.  업데이트 설정을 테스트를 하려면 클릭 **적용 하 여 보내기 메일**합니다.  
  
6.  테스트 메일에 성공 했음을 확인 하 고 나면 클릭 **확인** 업데이트 설정을 저장 합니다.  
  
### <a name="test-email-notification-does-not-list-any-alerts"></a>테스트 메일 알림 경고 나열 되지 않는  
 **문제** 알림이 알림 뷰어에 나열 된 경우에 알림에 대 한 테스트 메일 알림 경고를 표시 하지 않습니다.  
  
 **해결 방법** 경고 뷰어에서 보고 되는 모든 알림을 전자 메일 알림을 생성 합니다. 자신의 의료 정의 파일 내에서 메일 알림으로 에스컬레이션 하도록 구성 된 알림은 메일으로 지정된 메일 받는 사람에 게 전송 됩니다.  
  
 클릭 하면 **적용 하 여 보내기 메일**, 일반적으로 나열 된 상태 알림 없음 있는 샘플 메일 알림을 받게 됩니다. 그러나이 테스트 과정 메일 알림을 보냅니다 하도록 구성 된 상태 경고를 발견 되 면 해당 알림은 테스트 메일에 포함 됩니다.  
  
### <a name="active-alerts-are-displayed-for-an-uninstalled-application"></a>설치 되지 않은 응용 프로그램에 대 한 활성 알림이  
 **문제** 응용 프로그램에 대 한 활성 알림을 응용 프로그램 하 고 해당 의료 정의 파일 제거 된 경우에 표시 됩니다.  
  
 **해결 방법** 수동으로 제거 응용 프로그램의 활성 경고를 삭제 해야 합니다. 알림을 삭제 하려면 다음을 수행 합니다.  
  
##### <a name="to-delete-an-alert-from-the-server-by-using-the-dashboard"></a>서버에서 알림을 대시보드를 사용 하 여 삭제 하려면  
  
1.  서버에서 대시보드를 엽니다.  
  
2.  탐색 창에서 알림 표시 된 아이콘 (중요, 경고 또는 알림)를 클릭 합니다. 알림 뷰어를 시작합니다.  
  
3.  클릭 한 다음 고 삭제 하려는 경고를 마우스 오른쪽 단추로 클릭 경고 뷰어에서 **이 알림을**합니다.
