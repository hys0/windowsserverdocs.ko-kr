---
ms.assetid: 330c7b61-dde0-432f-9b74-d250ad9cc808
title: 기호를 추가\-페이지 설명
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 8d3cc69bde1c9126f97926802b53d049ed1ef501
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859996"
---
# <a name="add-sign-in-page-description"></a>기호를 추가\-페이지 설명


## <a name="to-add-sign-in-page-description"></a>추가 기호를\-페이지 설명  
페이지 설명의 부호\-를 추가 하려면 페이지의 부호\-페이지에서 다음 Windows PowerShell cmdlet 및 구문을 사용 합니다.  

![설명에 기호를 추가 합니다.](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>" 
 
  
> [!IMPORTANT]  
> `SignInPageDescriptionText` 매개 변수의 문자열은 태그가 있는 순수 HTML과 태그가 없는 순수 HTML을 둘 다 지원합니다. 따라서 실행할 수도 있습니다 다음 cmdlet을 사용 하지 않고는 &lt;p&gt; 태그입니다.  `Set-AdfsGlobalWebContent -SignInPageDescriptionText "Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information." ` 

로그인 한 후\-페이지는 사용자 정의 사용자 지정 항목이 우선적; 이므로 지원 하려는 모든 언어에 대 한 사용자 지정 해야 합니다. 사용자 지정된 모든 콘텐츠에는 로캘 매개 변수가 붙습니다. 지역화 된 콘텐츠를 구성할 때와 국가 구성 되어야 합니다\-덜 로캘 예를 들어, "en", 국가 및 지역 구성 하기 전에 먼저\-와 같은 특정 로캘 "en\-우리"입니다.  

## <a name="additional-references"></a>추가 참조 
[사용자 로그인 사용자 지정 AD FS](AD-FS-user-sign-in-customization.md)  
