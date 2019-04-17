---
ms.assetid: a4526500-24b3-423d-805c-24b0d8061aba
title: "그림 ADFS 로그인 페이지에 변경"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: ac5e60aaad864248b58a3908e7aa9622165fbc14
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="change-the-illustration-on-the-ad-fs-sign-in-page"></a>그림 ADFS 로그인 페이지에 변경

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

## <a name="change-the-illustration"></a>그림 변경  


왼쪽에서 sign\ 페이지에 표시 되는 그래픽 그림을 변경 하려면 다음과 같은 Windows PowerShell PowerShell cmdlet 및 구문을 사용 합니다.  

![그림 변경](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)
  
> [!IMPORTANT]  
> 파일 크기 200 KB 보다 더 큰의 96 DPI @ 1420 x 1080 픽셀 그림에 대 한 크기를 것이 좋습니다.  
  
 
    Set-AdfsWebTheme -TargetName default -Illustration @{path="c:\Contoso\illustration.png"}  

## <a name="additional-references"></a>추가 참조 
[광고 FS 사용자 지정 로그인](AD-FS-user-sign-in-customization.md)  
  
  
