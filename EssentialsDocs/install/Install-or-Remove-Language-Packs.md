---
title: 언어 팩 설치 또는 제거
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860094"
---
# <a name="install-or-remove-language-packs"></a>언어 팩 설치 또는 제거

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

> [!NOTE]
>  에 설명 된 대로 다국어 Windows 이미지를을 먼저 만들어야 합니다 [언어 팩 및 배포](https://technet.microsoft.com/library/hh824829) Windows Server Essentials 언어 팩을 추가 하기 전에 합니다.  
  
 언어 팩은 다국어 이미지를 만드는 데에만 사용할 수 있습니다. 이 섹션의 정보는 설치 또는 Windows Server Essentials에서 언어 팩을 제거 하는 데 관련이 있습니다.  
  
> [!NOTE]
>  동아시아어(예: ja-jp)를 지원하지 않는 클라이언트 컴퓨터에서 IC(초기 구성)를 실행하려는 경우나 영어가 서버의 다국어 이미지에 포함되어 있지 않은 경우 IC 웹 페이지가 사각형으로 표시됩니다. IC 웹 페이지를 기본적으로 영어로 표시하려면 만드는 다국어 이미지에 영어가 포함되어야 합니다.  
  
## <a name="adding-language-packs-to-an-image"></a>언어 팩을 이미지에 추가  
 언어 팩을 OEM 사용자 지정 DVD에서 사용할 수 있습니다. 이미지에 언어 팩을 추가하기 전에 기술자 컴퓨터에 언어 팩을 복사하는 것이 좋습니다.  
  
 언어 팩을 설치하려면 다음 명령을 사용해야 합니다.  
  
 **dism.exe /online /Add-Package /packagepath:\\< 전체 경로 파일 디렉터리를\>\lp.cab**  
  
 예를 들어, 다음 명령은 독일어 언어 팩을 추가하는 방법을 보여 줍니다.  
  
 **dism.exe /online /Add-Package /PackagePath:C:\Users\Administrator\Desktop\WindowsHomeServer-Product-r\de-de\lp.cab**  
  
> [!IMPORTANT]
>  운영 체제를 완전히 지역화 하려면 Windows Server Essentials 용 언어 팩도 적용 해야 합니다.  
  
## <a name="removing-language-packs-from-an-image"></a>이미지에서 언어 팩 제거  
 다음 명령을 사용하여 더 이상 이미지에 포함시키지 않을 언어 팩을 제거할 수 있습니다.  
  
 **dism.exe /online /Remove-Package /packagepath:\\< 전체 경로 파일 디렉터리를\>\lp.cab**  
  
 예를 들어, 다음 명령은 독일어 언어 팩을 제거하는 방법을 보여 줍니다.  
  
 **dism.exe /online /Remove-Package /PackagePath:C:\Users\Administrator\Desktop\WindowsHomeServer-Product-r\de-de\lp.cab**  
  
## <a name="see-also"></a>관련 항목  

 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가 사용자 지정](Additional-Customizations.md)   
 [배포용 이미지 준비](Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](Testing-the-Customer-Experience.md)

 [만들기 및 이미지를 사용자 지정](../install/Creating-and-Customizing-the-Image.md)   
 [추가 사용자 지정](../install/Additional-Customizations.md)   
 [배포용 이미지 준비](../install/Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](../install/Testing-the-Customer-Experience.md)

