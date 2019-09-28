---
ms.assetid: 1ca6f87f-7272-4767-b609-3e295ac7d32f
title: 개인정보취급방침 링크 추가
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: cd559e38c38e96d1417257fe7d6ff8ccfa180c6b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358425"
---
# <a name="add-privacy-link"></a>개인정보취급방침 링크 추가 


로그인에 표시 되는 개인 정보 취급 방침 링크를 추가 하려면\-페이지에서 다음 Windows PowerShell cmdlet 및 구문을 사용 합니다.  

![개인 정보 취급 방침 링크 추가](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png) 
  
 
`Set-AdfsGlobalWebContent -PrivacyLink https://fs1.contoso.com/privacy/ -PrivacyLinkText Privacy`  
 
  
> [!IMPORTANT]  
> 이 cmdlet의 `linkText` 매개 변수는 기본값( *Privacy*)이 아닌 다른 값을 사용하는 경우에만 필요합니다. 기본값을 사용하면 페이지가 모든 클라이언트 로캘로 지역화된다는 점이 장점입니다. 로그인 한 후\-페이지는 사용자 정의 사용자 지정 항목이 우선적; 이므로 지원 하려는 모든 언어에 대 한 사용자 지정 해야 합니다. 사용자 지정된 모든 콘텐츠에는 로캘 매개 변수가 붙습니다. 지역화 된 콘텐츠를 구성할 때와 국가 구성 해야\-적은 로캘 예를 들어, "en", 국가 및 지역 구성 하기 전에 먼저\-특정 로캘에 같은 "en\-우리"입니다.  

## <a name="additional-references"></a>추가 참조 
[사용자 로그인 사용자 지정 AD FS](AD-FS-user-sign-in-customization.md)  
