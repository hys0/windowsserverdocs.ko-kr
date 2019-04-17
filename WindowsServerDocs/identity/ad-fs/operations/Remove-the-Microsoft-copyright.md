---
ms.assetid: c89a977c-b09f-44ec-be42-41e76a6cf3ad
title: "Microsoft 저작권 제거"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: c2e6f9445e53a5b5867a763d58ad4a6ca3600cbe
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="remove-the-microsoft-copyright"></a>Microsoft 저작권 제거 

>적용 대상: Windows Server 2016, Windows Server 2012 r 2
 
기본적으로 ADFS 페이지 Microsoft 저작권을 포함 됩니다. 사용자 지정 된 페이지에서이 저작권을 제거 하려면 다음 절차를 사용할 수 있습니다. 

![저작권 제거](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1.png) 
  
## <a name="to-remove-the-microsoft-copyright"></a>Microsoft 저작권을 제거 하려면  
  
1.  사용자 지정 테마 기본 설정에 따라를 만듭니다.  
  

    `New-AdfsWebTheme –Name custom –SourceName default ` 
 
  
2.  출력 폴더 지정 하 여 테마를 내보냅니다.  

    `Export-AdfsWebTheme -Name custom -DirectoryPath C:\customWebTheme ` 

  
3.  출력 폴더에 있는 Style.css 파일을 찾습니다. 위 예제를 사용 하 여 경로 C:\\CustomWebTheme\\Css\\Style.css 것입니다.  
  
4.  메모장과 같은 편집기 Style.css 파일을 엽니다.  
  
5.  찾아는 `#copyright` 부분을 하 고 다음으로 변경 합니다.  
  `#copyright {color:#696969; display:none;} ` 
 
6.  새 Style.css 파일에 따라 테마를 사용자 지정을 만듭니다.  
  
    `Set-AdfsWebTheme -TargetName custom -StyleSheet @{locale="";path="C:\customWebTheme\css\style.css"}  `

7.  새로운 테마를 활성화 합니다.  
  

    `Set-AdfsWebConfig -ActiveThemeName custom ` 


이제 저작권 로그인 페이지의 아래쪽에 더 이상 표시 됩니다.

![저작권 제거](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1a.png) 

## <a name="additional-references"></a>추가 참조 
[광고 FS 사용자 지정 로그인](AD-FS-user-sign-in-customization.md) 
