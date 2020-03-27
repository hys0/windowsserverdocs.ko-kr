---
title: Windows Server Essentials ADK 사용에 관한 중요 정보
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 26cb2992-1250-4672-98ee-8b870baa45d5
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 9a06f3b6431ae6079869e1d7fe9bc3f0ef5e597b
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80311740"
---
# <a name="important-information-for-using-the-windows-server-essentials-adk"></a>Windows Server Essentials ADK 사용에 관한 중요 정보

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Windows Server Essentials의 이미지를 만들고 사용자 지정 하기 위해 windows [8 adk](https://go.microsoft.com/fwlink/?LinkId=248647)의 다양 한 도구를 사용 하지만 WINDOWS 8 Adk와 Windows SERVER Essentials adk 사이에는 몇 가지 중요 한 차이점이 있습니다.  
  
 다음 중요한 차이점에 대해 알고 있어야 합니다.  
  
-   **%windir%\setup\script\SetupComplete.cmd**에서 일부 설정이 변경되었습니다. 이 명령을 사용하기 위해 명령줄을 추가할 수 있지만 기존 명령줄을 제거하지는 마세요.  
  
## <a name="working-with-passwords"></a>암호를 사용하여 작업  
  
-   관리자의 암호는 Admin@123로 설정 되 고 자동 로그온은 wim\unattend.xml에서 사용 하도록 설정 됩니다. 따라서 서버 초기 구성 중 암호를 여러 번 다시 입력할 필요가 없습니다. 이동식 미디어의 루트에 사용자 지정된 unattend.xml이 있는 경우에는 이 설정을 덮어쓰므로 시작하는 동안 암호를 설정하고 로그온해야 합니다.  
  
-   초기 구성 중에 최종 사용자에게 새 계정과 암호를 만들라는 메시지가 표시됩니다. 이 새 계정은 운영 체제의 네트워크 관리자 계정이 됩니다. 관리자 계정 및 자동 로그온이 비활성화되었습니다. 품질 보증 테스트를 위해 cfg.ini 파일을 사용하여 이 프로세스를 자동화할 수 있습니다.  
  
-   unattend.xml 파일을 만드는 방법에 대한 자세한 내용은 [Windows 8 ADK](https://go.microsoft.com/fwlink/?LinkId=248694) 설명서를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  

 [Windows Server ESSENTIALS ADK를 사용 하 여 시작](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [이미지  만들기 및 사용자 지정](Creating-and-Customizing-the-Image.md)  
 [추가 사용자 지정](Additional-Customizations.md)   
 [배포할 이미지를 준비 하는 중](Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](Testing-the-Customer-Experience.md)

 [Windows Server ESSENTIALS ADK를 사용 하 여 시작](../install/Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [이미지  만들기 및 사용자 지정](../install/Creating-and-Customizing-the-Image.md)  
 [추가 사용자 지정](../install/Additional-Customizations.md)   
 [배포할 이미지를 준비 하는 중](../install/Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](../install/Testing-the-Customer-Experience.md)

