---
ms.assetid: da035189-e87f-4597-9933-49bf391a8d5d
title: 홈 링크 추가
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: a9a043390f5bfb412e549779ed4a9048d1c8a0b5
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190185"
---
# <a name="add-home-link"></a>홈 링크 추가 

로그인에 표시 되는 홈 링크를 추가 하려면\-페이지에서 다음 Windows PowerShell cmdlet 및 구문을 사용 합니다. 


![홈 링크 추가](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png) 
  

`Set-AdfsGlobalWebContent -HomeLink https://fs1.contoso.com/home/ -HomeLinkText Home ` 
 
  
> [!IMPORTANT]  
> 이 cmdlet의 `linkText` 매개 변수는 기본값( *Home*)이 아닌 다른 값을 사용하는 경우에만 필요합니다. 기본값을 사용하면 모든 클라이언트 로캘로 지역화된다는 점이 장점입니다. 로그인 한 후\-페이지는 사용자 정의 사용자 지정 항목이 우선적; 이므로 지원 하려는 모든 언어에 대 한 사용자 지정 해야 합니다.

## <a name="additional-references"></a>추가 참조 
[AD FS 사용자 로그인 사용자 지정](AD-FS-user-sign-in-customization.md)  
