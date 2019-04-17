---
ms.assetid: 1ca6f87f-7272-4767-b609-3e295ac7d32f
title: "개인 정보 보호 링크 추가"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 81a453b45693b8222bdfc0231885b506fdfcd2fc
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="add-privacy-link"></a>개인 정보 보호 링크 추가 

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

sign\ 페이지에 표시 되는 개인 정보 링크를 추가 하려면 다음 Windows PowerShell cmdlet와 구문을 사용 합니다.  

![개인 정보 보호 링크 추가](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png) 
  
 
`Set-AdfsGlobalWebContent -PrivacyLink https://fs1.contoso.com/privacy/ -PrivacyLinkText Privacy`  
 
  
> [!IMPORTANT]  
> `linkText`는 기본적으로 보다 다른 값을 사용 하지 않는 경우이 cmdlet에 매개 필요 하지 않습니다 *개인 정보 보호*합니다. 기본값 사용 페이지 모든 클라이언트 로캘에 지역화는입니다. 사용자가 우선; sign\에서 페이지를 사용자 지정 된 후 따라서 지원 하 고 모든 언어에 대해 사용자 지정 해야 합니다. 사용자 지정 된 모든 내용이 로캘 매개 변수를 사용 합니다. 지역화 된 콘텐츠를 구성 구성 해야 country\ 덜 로캘 먼저 예를 들어, "en" 구성 하기 전에 국가 및 region\ 특정 지역와 같은 "en\-해 주세요" 합니다.  

## <a name="additional-references"></a>추가 참조 
[광고 FS 사용자 지정 로그인](AD-FS-user-sign-in-customization.md)  
