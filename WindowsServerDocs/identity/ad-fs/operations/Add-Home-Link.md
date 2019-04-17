---
ms.assetid: da035189-e87f-4597-9933-49bf391a8d5d
title: "홈 링크 추가"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fb903c62e717e36099934e64e1c939a502f691a3
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="add-home-link"></a>홈 링크 추가 

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

sign\ 페이지에 표시 되는 집 링크를 추가 하려면 다음 Windows PowerShell cmdlet와 구문을 사용 합니다. 


![홈 링크 추가](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png) 
  

`Set-AdfsGlobalWebContent -HomeLink https://fs1.contoso.com/home/ -HomeLinkText Home ` 
 
  
> [!IMPORTANT]  
> `linkText`는 기본적으로 보다 다른 값을 사용 하지 않는 경우이 cmdlet에 매개 필요 하지 않습니다 *Home*합니다. 기본값 사용 되는 모든 클라이언트 로캘에 지역화 된입니다. 사용자가 우선; sign\에서 페이지를 사용자 지정 된 후 따라서 지원 하 고 모든 언어에 대해 사용자 지정 해야 합니다.

## <a name="additional-references"></a>추가 참조 
[광고 FS 사용자 지정 로그인](AD-FS-user-sign-in-customization.md)  
