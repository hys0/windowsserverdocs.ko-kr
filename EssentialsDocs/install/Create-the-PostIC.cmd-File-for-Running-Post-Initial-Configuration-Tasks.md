---
title: "초기 구성 게시물 작업을 실행 하기 위한 PostIC.cmd 파일 만들기"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99e258bc-0695-48c9-b694-a7f3cbe2a2d0
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: f5042204cd189e3101f5e0126fd98e786a49032d
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="create-the-posticcmd-file-for-running-post-initial-configuration-tasks"></a>초기 구성 게시물 작업을 실행 하기 위한 PostIC.cmd 파일 만들기

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

코드를 작성 한 다음 PostIC.cmd 스크립트 파일에서 해당 코드를 호출 하 여 사용자 지정 마이그레이션 초기 구성 추가할 수 있습니다. PostIC.cmd 파일을 사용 하는 경우 다음 지침을 따라야 합니다.  
  
-   사용자 지정 코드 자동 실행 합니다 (사용자 인터페이스 표시할 수 없는).  
  
-   사용자 지정 코드 서버를 다시 시작을 시작할 수 없습니다. 초기 구성 마지막 작업으로 서버를 다시 시작 됩니다.  
  
-   사용자 지정 코드 3 분 이하의 실행 해야 합니다.  
  
 코드를 성공적으로 실행 하는 경우 0 돌아가려면 PostIC.cmd 파일을 정의 합니다. 파일에 대 한 운영 체제를 찾는 경우 다른 값을 반환 [SetupFailure.cmd](Create-the-PostIC.cmd-File-for-Running-Post-Initial-Configuration-Tasks.md#BKMK_SetupFailure), PostIC.cmd 파일의 코드를 성공적으로 실행 되지 않는 경우 실행 해야 하는 코드가 포함 되어 있는 합니다. PostIC.cmd 파일 및 SetupFailure.cmd 파일 해야 C:\Windows\Setup\Scripts 있습니다.  
  
#### <a name="to-define-post-initial-configuration-customizations"></a>정의 사용자 지정 마이그레이션 초기 구성 하려면  
  
1.  PostIC.cmd 스크립트에서 호출 되는 코드를 작성 합니다.  
  
2.  메모장을 사용 하 라는 PostIC.cmd 파일 만들고 1 단계에서 만든 코드에 대 한 호출을 추가 합니다. 코드가 성공을 값을 반환 있는지 확인 합니다.  
  
3.  PostIC.cmd C:\Windows\Setup\Scripts에 저장 합니다.  
  
4.  (선택 사항) 코드 PostIC.cmd 0이 아닌 다른 항목을 반환 하는 경우 자동으로 실행 하는 SetupFailure.cmd 파일을 만듭니다.  
  
###  <a name="BKMK_SetupFailure"></a>SetupFailure.cmd  
 초기 구성에서 문제에 대 한 알림을 SetupFailure.cmd를 사용 하 여 제공할 수 있습니다. SetupFailure.cmd 파일 문제가 발생 하는 경우 실행 하려는 코드가 포함 되어 있습니다. SetupFailure.cmd 파일 C:\Windows\Setup\Scripts에 저장 하 고 문제가 있거나 설치 작업과 또는 PostIC.cmd 파일 0이 아닌 값을 반환 하면 실행 됩니다.  
  
##### <a name="to-define-notifications"></a>정의할 알림  
  
1.  SetupFailure.cmd 스크립트에서 호출 되는 코드를 작성 합니다.  
  
2.  메모장을 사용 하 라는 SetupFailure.cmd 파일 만들고 1 단계에서 만든 코드에 대 한 호출을 추가 합니다. 코드가 성공을 값을 반환 있는지 확인 합니다.  
  
3.  SetupFailure.cmd C:\Windows\Setup\Scripts에 저장 합니다.  
  
## <a name="see-also"></a>참조 하십시오  
 [Windows Server Essentials ADK 시작](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](Testing-the-Customer-Experience.md)