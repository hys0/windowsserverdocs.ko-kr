---
title: "언어 팩을 제거 하거나 설치"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98f13f63-4480-40ba-a7ef-d1d9b7582e5f
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: a41b491bbe4b4a8ee7f9743dc85e5bdaffb08496
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="install-or-remove-language-packs"></a>언어 팩을 제거 하거나 설치

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

> [!NOTE]
>  먼저 만들어야 다국어 Windows 이미지에 설명 된 대로 [언어 팩 및 배포](https://technet.microsoft.com/library/hh824829) Windows Server Essentials 언어 팩을 추가 하기 전에 합니다.  
  
 언어 팩은 다국어 이미지를 만들기 위한 사용할 수만 있습니다. 이 섹션의 정보는 설치 또는 Windows Server Essentials에서 언어 팩을 제거 합니다.  
  
> [!NOTE]
>  초기 구성 (회사 간) ja jp 등-아시아 언어를 지원 하지 않는 클라이언트 컴퓨터에서 실행 하도록 하려는 경우 하 고 영어 서버에 다국어 이미지에 포함 되지 않은 회사 간 웹 페이지 사각형 표시 됩니다. 사용자가 만든 다국어 이미지를 기본 영어로 회사 간 웹 페이지에 대 한 영어 포함 해야 합니다.  
  
## <a name="adding-language-packs-to-an-image"></a>이미지를 팩 언어 추가  
 언어 팩 OEM 사용자 지정 DVD에서 사용할 수 있습니다. 언어 팩 이미지를 추가 하기 전에 언어 팩을 기술자 컴퓨터에 복사 하는 것이 좋습니다.  
  
 언어 팩을 설치 하려면 다음 명령을 사용 해야 합니다.  
  
 **dism.exe /online /Add-Package /PackagePath:C: \\ < 전체 경로 파일 directory\ cab를 > \lp.cab**  
  
 예를 들어 다음 명령을 독일 언어 팩을 추가 하는 방법을 보여 줍니다.  
  
 **dism.exe /online /Add-Package /PackagePath:C:\Users\Administrator\Desktop\WindowsHomeServer-Product-r\de-de\lp.cab**  
  
> [!IMPORTANT]
>  Windows Server Essentials 운영 체제를 완전히 지역화 하도록 용 언어 팩도 적용 해야 합니다.  
  
## <a name="removing-language-packs-from-an-image"></a>이미지에서 언어 팩을 제거  
 더 이상 이미지를 포함 하 여 원하는 언어 팩을 제거 하려면 다음 명령을 사용할 수 없습니다.  
  
 **dism.exe /online /Remove-Package /PackagePath:C: \\ < 전체 경로 파일 directory\ cab를 > \lp.cab**  
  
 예를 들어 다음 명령을 독일 언어 팩을 제거 하는 방법을 보여 줍니다.  
  
 **dism.exe /online /Remove-Package /PackagePath:C:\Users\Administrator\Desktop\WindowsHomeServer-Product-r\de-de\lp.cab**  
  
## <a name="see-also"></a>참조 하십시오  

 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](Testing-the-Customer-Experience.md)

 [만들기 및 이미지를 사용자 지정](../install/Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](../install/Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](../install/Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](../install/Testing-the-Customer-Experience.md)

