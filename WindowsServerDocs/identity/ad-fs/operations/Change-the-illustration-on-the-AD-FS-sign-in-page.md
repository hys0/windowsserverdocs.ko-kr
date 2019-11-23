---
ms.assetid: a4526500-24b3-423d-805c-24b0d8061aba
title: AD FS 로그인 페이지에서 그림을 변경 합니다.
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 3da7726ca625c32728fb0ae64d291ae599b6cd8d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358295"
---
# <a name="change-the-illustration-on-the-ad-fs-sign-in-page"></a>AD FS 로그인 페이지에서 그림을 변경 합니다.

## <a name="change-the-illustration"></a>그림을 변경 합니다.  


페이지의 부호\-에 표시 되는 왼쪽의 그림을 변경 하려면 다음 Windows PowerShell cmdlet 및 구문을 사용 합니다.  

![일러스트레이션 변경](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)
  
> [!IMPORTANT]  
> 일러스트레이션 크기는 96dpi에서 1420x1080픽셀이고, 파일 크기는 200KB 이내인 것이 좋습니다.  
  
 
    Set-AdfsWebTheme -TargetName default -Illustration @{path="c:\Contoso\illustration.png"}  

## <a name="additional-references"></a>추가 참조 
[사용자 로그인 사용자 지정 AD FS](AD-FS-user-sign-in-customization.md)  
  
  
