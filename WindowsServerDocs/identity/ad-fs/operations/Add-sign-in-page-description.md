---
ms.assetid: 330c7b61-dde0-432f-9b74-d250ad9cc808
title: "페이지에서 sign\\ 설명 추가"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 128a4ffd8d4b9dfcfe5f0e8e2df8a0e1505cbb24
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="add-sign-in-page-description"></a>페이지에서 sign\ 설명 추가

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

## <a name="to-add-sign-in-page-description"></a>페이지에서 sign\ 설명 추가 하려면  
페이지에서 sign\ 설명 sign\에서 페이지를 추가 하려면 다음 Windows PowerShell PowerShell cmdlet와 구문을 사용 합니다.  

![로그 설명에 추가](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>" 
 
  
> [!IMPORTANT]  
> 에 대 한 문자열의 `SignInPageDescriptionText`매개 모두 순수한 HTML 태그 하거나 사용 하지 않고을 지원 합니다. 따라서 실행할 수도 있습니다 다음 cmdlet 사용 하지 않고는 &lt;p&gt; 태그 합니다.  `Set-AdfsGlobalWebContent -SignInPageDescriptionText "Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information." ` 

사용자가 우선; sign\에서 페이지를 사용자 지정 된 후 따라서 지원 하 고 모든 언어에 대해 사용자 지정 해야 합니다. 사용자 지정 된 모든 내용이 로캘 매개 변수를 사용 합니다. 지역화 된 콘텐츠를 구성 것으로 설정 해야 country\ 덜 로캘 먼저 예를 들어, "en" 구성 하기 전에 국가 및 지역 region\ 관련와 같은 "en\-해 주세요" 합니다.  

## <a name="additional-references"></a>추가 참조 
[광고 FS 사용자 지정 로그인](AD-FS-user-sign-in-customization.md)  
