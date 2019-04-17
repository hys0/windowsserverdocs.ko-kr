---
ms.assetid: 28043fc4-a34d-4710-ac3b-5c9d4d6a895c
title: "회사 이름을 ADFS 로그인 페이지에 변경"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 8e99f6fed8922ed15bf78a98b207b6f46767763a
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="change-the-company-name-on-the-ad-fs-sign-in-page"></a>회사 이름을 ADFS 로그인 페이지에 변경

>적용 대상: Windows Server 2016, Windows Server 2012 r 2
 
회사에서 sign\ 페이지에 표시 되는 이름을 변경 하려면 다음과 같은 Windows PowerShell PowerShell cmdlet와 구문을 사용 합니다. 이 값은 설치 하는 동안 입력 Federation 서비스 표시 이름에서 값을 사용 하 여 기본적으로 설정 됩니다.  

![이름 변경](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1.png)
  
  
    Set-AdfsGlobalWebContent –CompanyName "Contoso Corp"  
 
  
> [!NOTE]  
> 회사 이름을 변경 하려면 Windows PowerShell 스크립트 통합 환경 \(ISE\)도 사용할 수 있습니다. ISE Windows PowerShell를 사용 하 여 Unicode\ 준수 환경에서 콘텐츠를 표시할 수 있습니다. 자세한 내용은 참조 [ISE Windows PowerShell 소개](https://technet.microsoft.com/library/dd315244.aspx)합니다.  

## <a name="additional-references"></a>추가 참조 
[광고 FS 사용자 지정 로그인](AD-FS-user-sign-in-customization.md)  
  
