---
title: "Windows Server Essentials ADK 사용에 대 한 중요 한 정보"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 26cb2992-1250-4672-98ee-8b870baa45d5
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 4dec1fdf01538ca119b991675f932d2d8ec1e097
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="important-information-for-using-the-windows-server-essentials-adk"></a>Windows Server Essentials ADK 사용에 대 한 중요 한 정보

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

을 만들고 Windows Server Essentials의 이미지를 사용자 지정 하려면 사용 대부분의 도구는 [Windows 8 ADK](https://go.microsoft.com/fwlink/?LinkId=248647), 몇 가지 중요 한 차이점이 ADK Windows 8 및 Windows Server Essentials ADK 간 하지만 합니다.  
  
 중요 한 다음과 같은 차이점이의 알고 있어야 합니다.  
  
-   일부 설정은에서 변경 된 **%windir%\setup\script\SetupComplete.cmd**합니다. 이 명령을 사용 하려면 추가 cmdlines 추가할 수 있지만 기존 줄을 제거 하지 않습니다.  
  
## <a name="working-with-passwords"></a>암호를 사용한 작업  
  
-   관리자 암호 설정 되어 Admin@123 자동 로그온은 Install.wim\unattend.xml에서 사용 됩니다. 따라서 암호 다시 입력 하 고 여러 번 서버 초기 구성 하는 동안 필요가 없습니다. 사용자 지정 된 unattend.xml 루트 이동식 미디어에에서는이 설정을 덮어씁니다, 하 고 설정 해야 합니다 암호 및 중 로그온 시작...  
  
-   초기 구성 하는 동안 최종 사용자 새 계정 및 암호를 만들 하 라는 메시지가 표시 됩니다. 이 새 계정을 운영 체제에 대 한 네트워크 관리자 계정이 됩니다. 관리자 계정 및 자동 로그온 다음 사용 하지 않도록 설정 합니다. 이 프로세스 품질 보증 테스트용 cfg.ini 파일을 사용 하 여 자동화 수 있습니다.  
  
-   참조는 [Windows 8 ADK](https://go.microsoft.com/fwlink/?LinkId=248694) 만들기 unattend.xml 파일에 대 한 설명서 합니다.  
  
## <a name="see-also"></a>참조 하십시오  

 [Windows Server Essentials ADK 시작](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](Testing-the-Customer-Experience.md)

 [Windows Server Essentials ADK 시작](../install/Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [만들기 및 이미지를 사용자 지정](../install/Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](../install/Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](../install/Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](../install/Testing-the-Customer-Experience.md)

