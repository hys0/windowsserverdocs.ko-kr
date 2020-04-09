---
ms.assetid: f7f6bac2-1100-4b00-a248-4ca3eb3cdbe9
title: AD FS 로그인 페이지에 회사 로고 변경
author: billmath
ms.author: billmath
manager: femila
ms.date: 03/08/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: d12429b22265495cb8168ce3e5993a5cf3e74a0c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859976"
---
# <a name="changing-the-company-logo-on-the-ad-fs-sign-in-page"></a>AD FS 로그인 페이지에 회사 로고 변경

#### <a name="change-company-logo"></a>회사 로고 변경  
로그인에 표시 되는 회사의 로고를 변경 하려면\-페이지에서 다음 PowerShell Windows PowerShell cmdlet 및 구문을 사용 합니다.  

![로고 변경](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)
  
> [!IMPORTANT]  
> 로고 크기는 96dpi에서 260x35이고, 파일 크기는 10KB 이내인 것이 좋습니다.  
  
    
    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.png"}  

  
> [!NOTE]  
> `TargetName` 매개 변수는 필수입니다. AD FS와 함께 출시 되는 기본 테마 라고 *기본*합니다.  

## <a name="additional-references"></a>추가 참조 
[사용자 로그인 사용자 지정 AD FS](AD-FS-user-sign-in-customization.md)  
