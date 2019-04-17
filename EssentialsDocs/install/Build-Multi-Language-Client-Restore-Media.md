---
title: "다국어 클라이언트 복원 미디어 빌드"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2fdbc016-d464-43cb-bd75-8a63e61588a2
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 1ad934d297c3092050bd6adbb6bb0f50d1ec6f36
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="build-multi-language-client-restore-media"></a>다국어 클라이언트 복원 미디어 빌드

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

> [!NOTE]
>  먼저 만들어야 다국어 Windows 이미지에 설명 된 대로 [연습: 다국어 Windows 이미지를 만들려면](https://technet.microsoft.com/library/jj126995) Windows Server Essentials langauage 팩 install.wim을 추가 하기 전에 합니다.  
  
 다국어 서버 설치 DVD을 만들 때 install.wim 서버에 대 한 언어 팩을 설치 됩니다. 지역화 복원 마법사는 언어 팩의 일환으로 설치 됩니다.  
  
### <a name="to-build-a-multi-language-client-restore-media"></a>다국어 클라이언트 복원 미디어를 만들려는  
  
1.  Install.wim 탑재 c:\mount에서 루트 클라이언트 복원 미디어로 c:\mount\Program Files\Windows Server\bin\ClientRestore 폴더 이라고: [RestoreMediaRoot] 아래:  
  
    ```  
    dism /mount-wim /wimfile:install.wim /index:1 /mountdir:c:\mount  
    ```  
  
2.  탑재 클라이언트 복원 WIM 파일 [RestoreMediaRoot]\Sources\Boot.wim (동일한 단계 boot_x86.wim에 대해 너무 수행 해야 할). 명령줄이 다음과 같습니다.  
  
    ```  
    dism /mount-wim /wimfile:boot.wim /index:1 /mountdir:c:\mountRestore  
    ```  
  
3.  WinPE Setup.cab 패키지 복원 미디어를 실행 하 여 추가:  
  
    ```  
    dism /image:c:\mountRestore /add-package /packagepath:WinPE-Setup.cab  
    ```  
  
4.  메모장을 사용 하 여 c:\mountRestore\windows\system32\winpeshl.ini 편집, 다음과 같은 콘텐츠를 채웁니다.  
  
    ```  
    [LaunchApp]  
    AppPath = %SYSTEMDRIVE%\sources\SelectLanguage.exe  
    ```  
  
5.  복원 미디어에 언어 팩을 추가 합니다. 다음 명령을 실행 하 여 추가 언어 팩을 수행할 수 있습니다.  
  
    ```  
    dism /image:c:\mountRestore /add-package /packagepath:[language pack path]  
    ```  
  
     다음과 같은 언어 팩이 추가 해야 합니다.  
  
    1.  언어 팩 WinPE (lp.cab)  
  
    2.  언어 팩 WinPE 설정 (예: WinPE-Setup_en-us.cab,.cab WinPE Setup_ [언어])  
  
    3.  글꼴 cn, 글꼴 지원, 글꼴 홍콩, 코 경기, ja jp 아시아 글꼴에 대 한 추가 글꼴 팩 설치 해야 할 (winpe-fontsupport-[언어].cab, 예를 들어, fontsupport 글꼴 cn.cab winpe)  
  
6.  새 Lang.ini 파일을 실행 하 여 생성 합니다.  
  
    ```  
    dism /image:c:\mountRestore /Gen-LangINI /distribution:mount  
    ```  
  
7.  적용 하 고 실행 하 여 이미지를 분리 합니다.  
  
    ```  
    dism /unmount-wim /mountdir:c:\mountRestore /commit  
    ```  
  
8.  [RestoreMediaroot]\Sources\Boot_x86.wim에 대 한 7 단계를 2 단계를 반복 합니다.  
  
9. 적용 하 고 실행 하 여 이미지를 분리 합니다.  
  
    ```  
    dism /unmount-wim /mountdir:c:\mount /commit  
    ```  
  
## <a name="see-also"></a>참조 하십시오  

 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](Testing-the-Customer-Experience.md)

 [만들기 및 이미지를 사용자 지정](../install/Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](../install/Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](../install/Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](../install/Testing-the-Customer-Experience.md)

