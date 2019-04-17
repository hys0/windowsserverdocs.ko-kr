---
ms.assetid: 38bbc002-a8fa-4211-9328-4ef67fca0acf
title: "지역화 용 사용자 지정"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: ac206d5aa8af970b65a014955ac66a8cf2835eb6
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="customization-for-localization"></a>지역화 용 사용자 지정 

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

웹 콘텐츠 영어 이외 언어 지역화 가능 합니다. 지역화 경우 다음과 같은 고려 주의 해야 합니다.  
  
사용자가 우선; 콘텐츠를 사용자 지정 된 후 따라서 지원 하 고 모든 언어에 대해 사용자 지정 해야 합니다. 사용자 지정 된 모든 내용이 로캘 매개 변수를 사용 합니다. 지역화 된 콘텐츠를 구성으로 구성 country\ 덜 로캘 먼저 예를 들어, "en" 구성 하기 전에 국가 및 region\ 특정 지역와 같은 "en\-해 주세요" 합니다.  
  
다음 몇 가지 예가 추가 코드입니다.  
  
    
    Set-AdfsWebTheme -TargetName default -Logo @{Locale="";Path="c:\contoso.png"}  
      
    Set-AdfsWebTheme -TargetName default -Illustration @{Locale="";Path="c:\illustration.png"}  

  
다음 몇 가지 예가 추가 코드입니다.  
  
 
    Set-AdfsGlobalWebContent -ErrorPageDescriptionText "This is Contoso's error page description" –locale "en"  
  
  

    Set-AdfsGlobalWebContent -ErrorPageDescriptionText "Il s'agit de description de page erreur de Contoso" –locale "fr"  
 
  
유니코드의 입력 해야 하는 영어 이외 언어 웹 콘텐츠를 사용자 지정 하려면 Windows PowerShell ISE 사용 하는 것이 좋습니다. 자세한 내용은 참조 [ISE Windows PowerShell 소개](https://technet.microsoft.com/library/dd315244.aspx)합니다.  

## <a name="additional-references"></a>추가 참조 
[광고 FS 사용자 지정 로그인](AD-FS-user-sign-in-customization.md) 
