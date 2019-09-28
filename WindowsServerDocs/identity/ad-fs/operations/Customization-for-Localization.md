---
ms.assetid: 38bbc002-a8fa-4211-9328-4ef67fca0acf
title: 지역화를 위한 사용자 지정
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: ba3441d362960e054791ca3d6872dba6c7bd9a12
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357985"
---
# <a name="customization-for-localization"></a>지역화를 위한 사용자 지정 


웹 콘텐츠를 영어 이외의 언어로 지역화할 수 있습니다. 지역화할 때 다음 사항을 고려해야 합니다.  
  
콘텐츠를 사용자 지정한 후에는 사용자 지정 항목이 우선적으로 적용되므로 지원하려는 모든 언어에 대해 사용자 지정해야 합니다. 사용자 지정된 모든 콘텐츠에는 로캘 매개 변수가 붙습니다. 지역화 된 콘텐츠를 구성 하는 경우 국가 및 지역 @ no__t-1specific (예: "en @ no__t-2us")를 구성 하기 전에 먼저 country @-0less 로캘로 구성 합니다 (예: "en").  
  
다음은 몇 가지 추가 코드 예제입니다.  
  
    
    Set-AdfsWebTheme -TargetName default -Logo @{Locale="";Path="c:\contoso.png"}  
      
    Set-AdfsWebTheme -TargetName default -Illustration @{Locale="";Path="c:\illustration.png"}  

  
다음은 몇 가지 추가 코드 예제입니다.  
  
 
    Set-AdfsGlobalWebContent -ErrorPageDescriptionText "This is Contoso's error page description" –locale "en"  
  
  

    Set-AdfsGlobalWebContent -ErrorPageDescriptionText "Il s'agit de description de page erreur de Contoso" –locale "fr"  
 
  
유니코드 입력이 필요한 영어 이외의 언어로 웹 콘텐츠를 사용자 지정 하려는 경우 Windows PowerShell ISE를 사용 하는 것이 좋습니다. 추가 정보는 [Windows PowerShell ISE 소개](https://technet.microsoft.com/library/dd315244.aspx)를 참조하세요.  

## <a name="additional-references"></a>추가 참조 
[사용자 로그인 사용자 지정 AD FS](AD-FS-user-sign-in-customization.md) 
