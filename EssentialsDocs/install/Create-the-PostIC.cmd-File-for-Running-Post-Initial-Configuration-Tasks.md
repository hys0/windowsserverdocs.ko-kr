---
title: 초기 구성 후 작업 실행을 위해 PostIC.cmd 파일 만들기
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
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
ms.openlocfilehash: e15cb8591fc701094dde884d0a55e08d2cf422bb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433603"
---
# <a name="create-the-posticcmd-file-for-running-post-initial-configuration-tasks"></a>초기 구성 후 작업 실행을 위해 PostIC.cmd 파일 만들기

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

직접 코드를 작성하여 초기 구성 후 사용자 지정을 추가하고 이 코드를 PostIC.cmd라는 스크립트 파일에서 호출할 수 있습니다. PostIC.cmd 파일을 사용하려면 다음 지침을 따라야 합니다.  
  
- 사용자 지정 코드는 자동으로 실행해야 합니다(사용자 인터페이스를 표시할 수 없음).  
  
- 사용자 지정 코드는 서버 다시 시작을 시작할 수 없습니다. 초기 구성은 마지막 작업으로 서버를 다시 시작합니다.  
  
- 사용자 지정 코드는 3분 이내에 실행해야 합니다.  
  
  코드가 성공적으로 실행되면 PostIC.cmd 파일을 정의하여 0을 반환합니다. 다른 값이 반환되면 운영 체제는 이름이 [SetupFailure.cmd](Create-the-PostIC.cmd-File-for-Running-Post-Initial-Configuration-Tasks.md#BKMK_SetupFailure)인 파일을 검색합니다. 이 파일에는 PostIC.cmd 파일에 있는 코드가 성공적으로 실행되지 않는 경우 실행해야 할 코드가 포함되어 있습니다. PostIC.cmd 파일과 SetupFailure.cmd 파일은 모두 C:\Windows\Setup\Scripts에 있어야 합니다.  
  
#### <a name="to-define-post-initial-configuration-customizations"></a>초기 구성 후 사용자 지정을 정의하려면  
  
1.  PostIC.cmd 스크립트에서 호출되는 코드를 작성합니다.  
  
2.  메모장을 사용하여 이름이 PostIC.cmd인 파일을 만들고 1단계에서 만든 코드에 호출을 추가합니다. 코드가 올바른 값을 반환했는지 확인합니다.  
  
3.  PostIC.cmd를 C:\Windows\Setup\Scripts에 저장합니다.  
  
4.  (선택 사항) PostIC.cmd가 0이 아닌 값을 반환하면 코드를 실행하는 SetupFailure.cmd 파일을 만듭니다.  
  
###  <a name="BKMK_SetupFailure"></a> SetupFailure.cmd  
 SetupFailure.cmd를 사용하여 초기 구성에서의 문제에 대한 알림을 제공할 수 있습니다. SetupFailure.cmd 파일은 문제 발생 시 실행을 원하는 코드를 포함합니다. SetupFailure.cmd 파일은 C:\Windows\Setup\Scripts에 있으며 설치 작업에 문제가 발생하거나 PostIC.cmd 파일이 0이 아닌 값을 반환할 경우 실행됩니다.  
  
##### <a name="to-define-notifications"></a>알림을 정의하려면  
  
1.  SetupFailure.cmd 스크립트에서 호출되는 코드를 작성합니다.  
  
2.  메모장을 사용하여 이름이 SetupFailure.cmd인 파일을 만들고 1단계에서 만든 코드에 호출을 추가합니다. 코드가 올바른 값을 반환했는지 확인합니다.  
  
3.  SetupFailure.cmd를 C:\Windows\Setup\Scripts에 저장합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Windows Server Essentials ADK 시작 하기](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가 사용자 지정](Additional-Customizations.md)   
 [배포용 이미지 준비](Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](Testing-the-Customer-Experience.md)