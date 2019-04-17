---
ms.assetid: 0379abc3-25c7-46ab-9a6b-80a5152365b0
title: "Adfs의 사용자 지정 웹 테마"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 300c9fda84285ddfc52a4f47ea0198deb6fd33ef
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="custom-web-themes-in-ad-fs"></a>Adfs의 사용자 지정 웹 테마 

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

출시 out\ of\-the\-기본이 테마 기본을 라고 합니다. 기본 테마 내보낸 빠르게 시작할 수 있도록 사용할 수 있습니다. 모양과.css 파일을 수정 하 여 레이아웃을 포함 하는 문제를 사용자 지정, 가져오기 및이 새로운 테마를 적용할 수 있고 사용자 지정 된 모양과 동작을 사용할 수 있습니다. .Css 파일을 사용 하 여 또한 쉽게 웹 디자이너 작업할 수 있습니다.  
  
다음 cmdlet 중복 기본 웹 테마 지정 웹 테마를 만듭니다.  
  
  
`New-AdfsWebTheme –Name custom –SourceName default ` 

  
.Css 파일을 수정 하 고 새.css 파일을 사용 하 여 새 웹 테마를 구성할 수 있습니다. 웹 테마를 내보내려면 다음 cmdlet을 사용 합니다.  
  

    Export-AdfsWebTheme –Name default –DirectoryPath c:\theme  

  
.Css 파일 새로운 테마를 적용 하려면 다음 cmdlet을 사용 합니다.  
  

    Set-AdfsWebTheme –TargetName custom –StyleSheet @{path=”c:\NewTheme.css”}  
  
  
다음 cmdlet 스타일 시트를 사용자 지정 웹 테마를 만듭니다.  
  
  
`New-AdfsWebTheme –Name custom –StyleSheet @{path=”c:\NewTheme.css”} –RTLStyleSheetPath c:\NewRtlTheme.css ` 
  
  
  
사용자 지정 웹 테마 Adfs를 적용 하려면 다음 cmdlet을 사용 합니다.  
  

`Set-AdfsWebConfig -ActiveThemeName custom`  

  
JavaScript Adfs을 추가 하려면 다음 cmdlet을 사용 합니다.  
  
 
    Set-AdfsWebTheme -TargetName custom -AdditionalFileResource @{Uri=’ /adfs/portal/script/onload.js’;path="D:\inetpub\adfsassets\script\onload.js"}  


## <a name="additional-references"></a>추가 참조 
[광고 FS 사용자 지정 로그인](AD-FS-user-sign-in-customization.md)  
