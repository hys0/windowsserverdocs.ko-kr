---
ms.assetid: 0379abc3-25c7-46ab-9a6b-80a5152365b0
title: AD FS에서 사용자 지정 웹 테마
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 2bce52a5704706ad72799d00879e2f4e48f9d703
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189250"
---
# <a name="custom-web-themes-in-ad-fs"></a>AD FS에서 사용자 지정 웹 테마 

Out 제공 되는 테마\-의\-는\-상자 기본 테마 라고 합니다. 기본 테마를 내보내 이를 사용하여 빠르게 시작할 수 있습니다. .css 파일을 수정하여 레이아웃을 변경하고, 이 새 테마를 가져와 적용하는 등 모양 및 동작을 사용자 지정한 다음 사용자 지정된 모양과 동작을 사용할 수 있습니다. 또한 .css 파일을 사용하면 웹 디자이너와 함께 보다 쉽게 작업할 수 있습니다.  
  
다음 cmdlet은 기본 웹 테마를 복제하는 사용자 지정 웹 테마를 만듭니다.  
  
  
`New-AdfsWebTheme –Name custom –SourceName default ` 

  
.css 파일을 수정하고 새 .css 파일을 사용하여 새 웹 테마를 구성할 수 있습니다. 웹 테마를 내보내려면 다음 cmdlet을 사용합니다.  
  

    Export-AdfsWebTheme –Name default –DirectoryPath c:\theme  

  
새 테마에 .css 파일을 적용하려면 다음 cmdlet을 사용합니다.  
  

    Set-AdfsWebTheme –TargetName custom –StyleSheet @{path=”c:\NewTheme.css”}  
  
  
다음 cmdlet은 새 스타일시트에서 사용자 지정 웹 테마를 만듭니다.  
  
  
`New-AdfsWebTheme –Name custom –StyleSheet @{path=”c:\NewTheme.css”} –RTLStyleSheetPath c:\NewRtlTheme.css ` 
  
  
  
AD fs 사용자 지정 웹 테마를 적용 하려면 다음 cmdlet을 사용 합니다.  
  

`Set-AdfsWebConfig -ActiveThemeName custom`  

  
AD FS에 JavaScript를 추가 하려면 다음 cmdlet을 사용 합니다.  
  
 
    Set-AdfsWebTheme -TargetName custom -AdditionalFileResource @{Uri=’ /adfs/portal/script/onload.js’;path="D:\inetpub\adfsassets\script\onload.js"}  


## <a name="additional-references"></a>추가 참조 
[AD FS 사용자 로그인 사용자 지정](AD-FS-user-sign-in-customization.md)  
