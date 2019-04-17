---
ms.assetid: f7f6bac2-1100-4b00-a248-4ca3eb3cdbe9
title: "회사 로고 ADFS 로그인 페이지에 변경"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 03/08/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: ca54abe7fe852b22f2f4d9a717e38d219fa50694
ms.sourcegitcommit: a00fc4426dc4ad0098257f01f0124d6c733d1aef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/09/2018
---
# <a name="changing-the-company-logo-on-the-ad-fs-sign-in-page"></a>회사 로고 ADFS 로그인 페이지에 변경

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

#### <a name="change-company-logo"></a>변경 회사 로고  
회사에서 sign\ 페이지에 표시 되는 로고를 변경 하려면 다음 PowerShell Windows PowerShell cmdlet와 구문을 사용 합니다.  

![로고 변경](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)
  
> [!IMPORTANT]  
> 크기를 로고 260 x 350 @ 10 KB 보다 더 큰 파일 크기를으로 96 dpi를 사용 하는 것이 좋습니다.  
  
    
    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.png"}  

  
> [!NOTE]  
> `TargetName`매개가 필요 합니다. ADFS 함께 출시 기본 테마 라는 *기본*합니다.  

## <a name="additional-references"></a>추가 참조 
[광고 FS 사용자 지정 로그인](AD-FS-user-sign-in-customization.md)  
