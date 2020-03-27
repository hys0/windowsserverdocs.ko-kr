---
title: 사용자 지정된 단순 이미지 만들기
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 29f9a09f-e4e8-476d-ada1-ab9202a670d7
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 74a1729f9445710b6b9d279f1603295eff2a5d25
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312135"
---
# <a name="create-a-simple-customized-image"></a>사용자 지정된 단순 이미지 만들기

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

다음 절차에서는 사용자 지정된 단순 이미지를 만들 수 있습니다.  
  
#### <a name="to-create-the-image"></a>이미지를 만들려면  
  
1.  서버 설치 후 초기 구성 첫 페이지에서 Shift+F10을 눌러 cmd 창을 시작합니다.  
  
2.  시스템 드라이브 루트에서 SkipIC.txt 파일을 만듭니다.  
  
3.  서버를 다시 시작합니다.  
  
4.  unattend.xml 파일이 포함된 USB 플래시 드라이브 또는 DVD를 사용하여 서버를 시작합니다. 부팅 가능 USB 플래시 드라이브 만들기에 대한 자세한 내용은 [부팅 가능 USB 플래시 드라이브 만들기](Create-a-Bootable-USB-Flash-Drive.md)를 참조하세요.  
  
5.  대시보드에 로고 브랜딩을 추가합니다. 브랜딩 추가에 대한 자세한 내용은 [대시보드, 원격 웹 액세스 및 실행 패드에 브랜딩 추가](Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md)를 참조하세요.  
  
6.  OOBE.xml 파일을 만들어 회사 이름, 로고 및 EULA와 같은 사용자 지정 정보를 표시합니다. OOBE.xml 파일에 대한 자세한 내용은 [Create the Oobe.xml File Including Logo and EULA](Create-the-Oobe.xml-File-Including-Logo-and-EULA.md)를 참조하세요.  
  
7.  unattend.xml에 정의하지 않는 경우 기본 서버 이름을 변경합니다.  
  
8.  기본적으로 서버 이름은 임의의 문자열이 됩니다. 서버 이름을 다른 문자열(ContosoServer 등)로 변경한 다음 고객에게 새 서버 이름을 알립니다.  
  
9. [이미지 배포 준비](Preparing-the-Image-for-Deployment.md)의 설명과 같이 이미지 배포를 준비합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Windows Server ESSENTIALS ADK를 사용 하 여 시작](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [이미지  만들기 및 사용자 지정](Creating-and-Customizing-the-Image.md)  
 [추가 사용자 지정](Additional-Customizations.md)   
 [배포할 이미지를 준비 하는 중](Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](Testing-the-Customer-Experience.md)