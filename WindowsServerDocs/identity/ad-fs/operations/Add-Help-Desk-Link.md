---
ms.assetid: 2bac7744-9de3-491a-b0a2-4e843cec7344
title: "추가 도움말 센터 링크"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 6d16cc0a75bfe636c29b44687b669e87f31b69ce
ms.sourcegitcommit: 76e57a5453d6ee9a04dcff6a8cca087132cb1d5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/20/2018
---
# <a name="add-help-desk-link"></a>추가 도움말 센터 링크 

>적용 대상: Windows Server 2016, Windows Server 2012 r 2


## <a name="to-add-a-help-desk-link"></a>도움말 센터 링크를 추가 하려면  
Sign\에 페이지에 표시 되는 도움말 센터 링크를 추가 하려면 다음 Windows PowerShell PowerShell cmdlet와 구문을 사용 합니다.  

![추가 지원 센터](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)
  

`Set-AdfsGlobalWebContent -HelpDeskLink https://fs1.contoso.com/help/ -HelpDeskLinkText Help`  
 
  
> [!IMPORTANT]  
> `linkText`는 기본적으로 보다 다른 값을 사용 하지 않는 경우이 cmdlet에 매개 필요 하지 않습니다 *도움말*합니다. 기본값 사용 되는 모든 클라이언트 로캘에 지역화 된입니다. 사용자가 우선; 페이지를 사용자 지정 된 후 따라서 지원 하 고 모든 언어에 대해 사용자 지정 해야 합니다.  


## <a name="additional-references"></a>추가 참조 
[광고 FS 사용자 지정 로그인](AD-FS-user-sign-in-customization.md)  
