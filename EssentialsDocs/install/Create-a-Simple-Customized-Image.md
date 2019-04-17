---
title: "간단한 정의 이미지를 만들려면"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 29f9a09f-e4e8-476d-ada1-ab9202a670d7
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: e18ff5ded94127449072d28d00b98e17dbe63c3a
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="create-a-simple-customized-image"></a>간단한 정의 이미지를 만들려면

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

다음 절차 간단한 정의 이미지를 만들기 위한 사용할 수 있습니다.  
  
#### <a name="to-create-the-image"></a>이미지를 만들려면  
  
1.  초기 구성에서의 첫 번째 페이지 서버 설치 후 Shift + F10 cmd 창을 누릅니다.  
  
2.  드라이브 시스템의 루트 SkipIC.txt 파일을 만듭니다.  
  
3.  서버를 다시 시작 합니다.  
  
4.  서버를 USB 플래시 드라이브 또는 DVD, 파일이 포함 되어 있는 unattend.xml를 사용 하 여 시작 합니다. 부팅 가능한 USB 플래시 드라이브를 만드는 방법에 대해 내용은 [부팅 가능한 USB 플래시 드라이브를 만들](Create-a-Bootable-USB-Flash-Drive.md)합니다.  
  
5.  로고 브랜드 대시보드를 추가 합니다. 브랜드 추가 대 한 자세한 내용은 참조 [대시보드, 원격 Web Access 및 실행 패드 브랜드 추가](Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md)합니다.  
  
6.  회사 이름을, 로고 EULA 등 사용자 지정 정보를 표시 하려면 OOBE.xml 파일을 만듭니다. OOBE.xml 파일에 대 한 자세한 내용은 참조 [Oobe.xml 파일 등 로고 만들고 EULA](Create-the-Oobe.xml-File-Including-Logo-and-EULA.md)합니다.  
  
7.  하지 unattend.xml에서 정의 않으면 기본 서버 이름을 변경 합니다.  
  
8.  기본적으로 서버 이름 임의 문자열로 됩니다. 서버 이름 (예: ContosoServer), 다른 문자열을 변경 하 고 새 서버 이름에 대 한 고객을 알립니다.  
  
9. 이미지에 설명 된 대로 배포 준비 [이미지 배포 준비](Preparing-the-Image-for-Deployment.md)합니다.  
  
## <a name="see-also"></a>참조 하십시오  
 [Windows Server Essentials ADK 시작](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](Testing-the-Customer-Experience.md)