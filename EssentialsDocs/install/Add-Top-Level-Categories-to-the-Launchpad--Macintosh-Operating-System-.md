---
title: 실행 패드에 최상위 범주 추가(Macintosh 운영 체제)
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ee2173c3-e464-4001-9f43-6d926a575092
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 3b16cadc14999e041dc6b1661689787e434460eb
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80310223"
---
# <a name="add-top-level-categories-to-the-launchpad-macintosh-operating-system"></a>실행 패드에 최상위 범주 추가(Macintosh 운영 체제)

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Macintosh 운영 체제를 실행하는 컴퓨터의 실행 패드에 최상위 범주를 추가할 수 있습니다. 최상위 범주를 추가 하는 실행 패드 추가 기능을 만들려면이 페이지의 정보와 방법: 실행 패드에 작업 및 범주 추가 라는 주제를 사용 하면 됩니다. [Windows Server SOLUTIONS SDK](https://go.microsoft.com/fwlink/?LinkID=248648).  
  
 다음 예제에서는 .launchpad 파일에서 최상위 범주로 사용할 실행 패드 항목을 지정하는 방법을 보여 줍니다.  
  
```  
  
<?xml version="1.0" encoding="utf-8" ?>  
<LaunchPad resFile="Localizable">  
   <Category id="Microsoft.Launchpad.HomeCategory" name="SampleAddin"  image="SampleImage01.png">  
      <Task id="Microsoft.Launchpad.SampleAddin.Pictures"   
          name="Pictures"       
           src="smb://%ServerAddress%/Pictures"   
         image="SampleImage02.png"/>  
   </Category>  
</LaunchPad>  
```  
  
 최상위 범주로 사용할 항목의 경우 범주 요소의 ID 특성이 "Microsoft.Launchpad.HomeCategory"여야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [이미지  만들기 및 사용자 지정](Creating-and-Customizing-the-Image.md)  
 [추가 사용자 지정](Additional-Customizations.md)   
 [배포할 이미지를 준비 하는 중](Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](Testing-the-Customer-Experience.md)