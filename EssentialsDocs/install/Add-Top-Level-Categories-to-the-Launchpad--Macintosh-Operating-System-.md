---
title: "최상위 범주 (Macintosh 운영 체제) 실행 창에 추가"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ee2173c3-e464-4001-9f43-6d926a575092
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: ae4eb5943d37b4a9d3b554af28cb425420782cf8
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="add-top-level-categories-to-the-launchpad-macintosh-operating-system"></a>최상위 범주 (Macintosh 운영 체제) 실행 창에 추가

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

최상위 범주 Macintosh 운영 체제를 실행 하는 컴퓨터에서 실행 패드에 추가할 수 있습니다. 실행 패드 추가 기능에 최상위 범주를 추가 하는 만들려면이 페이지에서 및 방법 항목에서 정보를 함께 사용할 수: 추가 작업 및 범주를 실행 하 고 패드? 에 [Windows Server 솔루션 SDK](https://go.microsoft.com/fwlink/?LinkID=248648)합니다.  
  
 이때 실행 패드 항목.launchpad 파일의 최상위 범주를 지정 하는 방법을 보여 줍니다.  
  
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
  
 최상위 범주 수 있는 항목에 대 한 범주 요소 Id 특성 "Microsoft.Launchpad.HomeCategory" 여야 합니다.  
  
## <a name="see-also"></a>참조 하십시오  
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](Testing-the-Customer-Experience.md)