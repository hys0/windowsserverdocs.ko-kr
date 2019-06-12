---
title: Windows Server Essentials의 컴퓨터 모니터링 문제 해결
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
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
ms.openlocfilehash: 1adf8ae2dd8763d0bc5a514609bb2470de6acde4
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436074"
---
# <a name="troubleshoot-computer-monitoring-in-windows-server-essentials"></a>Windows Server Essentials의 컴퓨터 모니터링 문제 해결

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

이 항목에서는 경고 뷰어 및 Windows Server Essentials에서 전자 메일 알림을 통해 컴퓨터의 상태를 모니터링 하는 동안 발생 하는 문제 해결 방법을 제공 합니다.  
  
> [!NOTE]
>  Windows Server Essentials 커뮤니티에서 최신 문제 해결 정보에 대 한 것이 좋습니다를 방문 하 여 [Windows Server Essentials 포럼](https://social.technet.microsoft.com/Forums/winserveressentials/threads)합니다. Windows Server Essentials 포럼은 도움말을 검색하거나 질문하기 좋은 곳입니다.  
  
##  <a name="BKMK_TS"></a> 경고에 대 한 전자 메일 알림 문제 해결  
 이 섹션에서는 경고에 대한 메일 알림을 사용하는 경우 발생할 수 있는 다양한 문제를 설명합니다.  
  
### <a name="cannot-send-the-test-email-for-the-alert"></a>경고에 대한 테스트 메일을 보낼 수 없음  
 **문제** 오류가 발생 하는 메시지 경고에 대 한 테스트 메일을 보낼 수 없습니다.  
  
 **원인** 이 오류는 경고 알림에 대한 설정에 다음과 같은 문제가 있어 발생할 수 있습니다.  
  
- SMTP 서버 이름 또는 포트 번호가 잘못되었습니다.  
  
- SMTP 서버에 SSL(Single Sockets Layer) 연결이 필요하다고 잘못 지정되어 있습니다.  
  
- SMTP 서버에 인증이 필요하고, 잘못된 자격 증명이 입력되었습니다.  
  
  **해결 방법** 메일 알림 설정의 모든 오류를 수정합니다.  
  
##### <a name="to-identify-issues-in-your-email-notification-settings"></a>전자 메일 알림 설정에서 문제를 식별하려면  
  
-   ISP(인터넷 서비스 공급자)에 올바른 SMTP 서버 이름, 포트 번호 및 SSL 사용을 문의합니다.  
  
-   다음 위치에서 서버의 경고에 대한 메일 알림의 로그 파일을 검토합니다.  
  
     %ProgramData%\Microsoft\Windows Server\Logs\SharedServiceHost-AlertServiceConfig.log  
  
    > [!TIP]
    >  ProgramData 폴더를 보려면 표시되는 항목을 숨겼음에 틀림없습니다. 리본의 ProgramData 폴더가 표시 되지 않으면 **보기** 탭의 **표시/숨기기** 그룹을 선택 합니다 **숨겨진 항목** 텍스트 상자.  
  
##### <a name="to-update-your-email-notification-setup-for-alerts"></a>경고에 대한 메일 알림 설정을 업데이트하려면  
  
1.  대시보드에서 오른쪽 위에 있는 경고 아이콘을 클릭하여 경고 뷰어를 엽니다.  
  
2.  경고 뷰어 아래쪽에서 **경고에 대한 메일 알림 설정**을 클릭합니다.  
  
3.  **경고에 대한 메일 알림 설정** 대화 상자에서 **사용**을 클릭합니다.  
  
4.  **SMTP 설정** 대화 상자에서 SMTP 설정을 업데이트한 후 **확인**을 클릭합니다.  
  
5.  업데이트된 설정을 테스트하려면 **적용 후 메일 보내기**를 클릭합니다.  
  
6.  테스트 전자 메일이 성공적인지 확인한 후 **확인**을 클릭하여 업데이트된 설정을 저장합니다.  
  
### <a name="test-email-notification-does-not-list-any-alerts"></a>테스트 메일 알림에 경고가 나열되지 않음  
 **문제** 경고 뷰어에 경고가 나열된 경우에도 경고에 대한 테스트 메일 알림에 경고가 표시되지 않습니다.  
  
 **해결 방법** 경고 뷰어에 보고된 모든 경고가 메일 알림을 생성하지는 않습니다. 해당 상태 정의 파일 내에 메일 알림으로 에스컬레이션되도록 구성된 경고만 지정된 메일 받는 사람에게 메일로 전송됩니다.  
  
 **적용 후 메일 보내기**를 클릭하면 일반적으로 상태 경고가 나열되지 않은 샘플 메일 알림을 받게 됩니다. 그러나 메일 알림을 보내도록 구성된 상태 경고가 이 테스트 프로세스 중에 식별되면 해당 경고가 테스트 메일에 포함됩니다.  
  
### <a name="active-alerts-are-displayed-for-an-uninstalled-application"></a>제거된 응용 프로그램에 대한 활성 경고가 표시됨  
 **문제** 응용 프로그램 및 해당 상태 정의 파일이 제거된 경우에도 해당 응용 프로그램에 대한 활성 경고가 표시됩니다.  
  
 **해결 방법** 제거된 응용 프로그램의 활성 경고를 수동으로 삭제해야 합니다. 경고를 삭제하려면 다음을 수행하세요.  
  
##### <a name="to-delete-an-alert-from-the-server-by-using-the-dashboard"></a>대시보드를 사용하여 서버에서 경고를 삭제하려면  
  
1.  서버에서 대시보드를 엽니다.  
  
2.  탐색 창에서 표시된 경고 아이콘(중요, 경고 또는 정보)을 클릭합니다. 그러면 경고 뷰어가 시작됩니다.  
  
3.  경고 뷰어에서 삭제하려는 경고를 마우스 오른쪽 단추로 클릭한 후 **이 경고 삭제**를 클릭합니다.
