---
ms.assetid: 38bbc002-a8fa-4211-9328-4ef67fca0acf
title: 지역화를 위한 사용자 지정
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3cf209756c27c72836c7e2e1e58e84f3f5af2ca9
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189180"
---
# <a name="customization-for-localization"></a>지역화를 위한 사용자 지정 


웹 콘텐츠를 영어 이외의 언어로 지역화할 수 있습니다. 지역화할 때 다음 사항을 고려해야 합니다.  
  
콘텐츠를 사용자 지정한 후에는 사용자 지정 항목이 우선적으로 적용되므로 지원하려는 모든 언어에 대해 사용자 지정해야 합니다. 사용자 지정된 모든 콘텐츠에는 로캘 매개 변수가 붙습니다. 지역화 된 콘텐츠를 구성할 때와 국가 구성\-덜 로캘 예를 들어, "en", 국가 및 지역 구성 하기 전에 먼저\-와 같은 특정 로캘 "en\-우리"입니다.  
  
다음은 몇 가지 추가 코드 예제입니다.  
  
    
    Set-AdfsWebTheme -TargetName default -Logo @{Locale="";Path="c:\contoso.png"}  
      
    Set-AdfsWebTheme -TargetName default -Illustration @{Locale="";Path="c:\illustration.png"}  

  
다음은 몇 가지 추가 코드 예제입니다.  
  
 
    Set-AdfsGlobalWebContent -ErrorPageDescriptionText "This is Contoso's error page description" –locale "en"  
  
  

    Set-AdfsGlobalWebContent -ErrorPageDescriptionText "Il s'agit de description de page erreur de Contoso" –locale "fr"  
 
  
웹 콘텐츠를 영어 이외의 유니코드 입력이 필요한 언어로 사용자 지정 하려는 경우에 Windows PowerShell ISE를 사용 하는 것이 좋습니다. 추가 정보는 [Windows PowerShell ISE 소개](https://technet.microsoft.com/library/dd315244.aspx)를 참조하세요.  

## <a name="additional-references"></a>추가 참조 
[AD FS 사용자 로그인 사용자 지정](AD-FS-user-sign-in-customization.md) 
