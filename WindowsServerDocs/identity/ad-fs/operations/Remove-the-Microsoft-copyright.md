---
ms.assetid: c89a977c-b09f-44ec-be42-41e76a6cf3ad
title: Microsoft 저작권 정보를 제거 합니다.
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: aa27a014b0803712a20fdd23f075486dc35f33c2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820984"
---
# <a name="remove-the-microsoft-copyright"></a>Microsoft 저작권 정보를 제거 합니다. 

>적용 대상: Windows Server 2016, Windows Server 2012 R2
 
기본적으로 AD FS 페이지는 Microsoft 저작권 정보를 포함 합니다. 사용자 지정된 페이지에서 이 저작권 정보를 제거하려면 다음 절차를 따르면 됩니다. 

![저작권 정보를 제거 합니다.](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1.png) 
  
## <a name="to-remove-the-microsoft-copyright"></a>Microsoft 저작권 정보를 제거하려면  
  
1. 기본값을 기반으로 하는 사용자 지정 테마를 만듭니다.

   ```powershell
   New-AdfsWebTheme –Name custom –SourceName default
   ```

2. 출력 폴더를 지정하여 테마를 내보냅니다.  

   ```powershell
   Export-AdfsWebTheme -Name custom -DirectoryPath C:\CustomWebTheme
   ```

3. 찾을 `Style.css` 출력 폴더에 있는 파일입니다. 앞의 예제를 사용 하 여 경로 것 `C:\CustomWebTheme\Css\Style.css.`
  
4. 열기는 `Style.css` 메모장과 같은 편집기를 사용 하 여 파일입니다.  
  
5. `#copyright` 부분을 찾아서 다음으로 변경합니다.  

   ```css
   #copyright {color:#696969; display:none;}
   ```

6. 새의 기반이 되는 사용자 지정 테마를 만들려면 `Style.css` 파일입니다.  

   ```powershell
   Set-AdfsWebTheme -TargetName custom -StyleSheet @{locale="";path="C:\customWebTheme\css\style.css"}
   ```

7. 새 테마를 활성화합니다.  

   ```powershell
   Set-AdfsWebConfig -ActiveThemeName custom
   ```

이제 로그인 페이지의 맨 아래에 저작권은 더 이상 표시 됩니다.

![저작권 정보를 제거 합니다.](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1a.png) 

## <a name="additional-references"></a>추가 참조 
[AD FS 사용자 로그인 사용자 지정](AD-FS-user-sign-in-customization.md) 
