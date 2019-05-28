---
ms.assetid: 2bac7744-9de3-491a-b0a2-4e843cec7344
title: 지원 센터 링크 추가
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fb186c3ba5cfb3acb9bfd0c3139b09b992fb8863
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190212"
---
# <a name="add-help-desk-link"></a>지원 센터 링크 추가 


## <a name="to-add-a-help-desk-link"></a>지원 센터 링크를 추가 하려면  
로그인에 표시 되는 지원 센터 링크를 추가할\-페이지에서 다음 Windows PowerShell cmdlet 및 구문을 사용 합니다.  

![기술 지원 서비스를 추가 합니다.](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)
  

`Set-AdfsGlobalWebContent -HelpDeskLink https://fs1.contoso.com/help/ -HelpDeskLinkText Help`  
 
  
> [!IMPORTANT]  
> 이 cmdlet의 `linkText` 매개 변수는 기본값( *Help*)이 아닌 다른 값을 사용하는 경우에만 필요합니다. 기본값을 사용하면 모든 클라이언트 로캘로 지역화된다는 점이 장점입니다. 페이지를 사용자 지정한 후에는 사용자 지정 항목이 우선적으로 적용되므로 지원하려는 모든 언어에 대해 사용자 지정해야 합니다.  


## <a name="additional-references"></a>추가 참조 
[AD FS 사용자 로그인 사용자 지정](AD-FS-user-sign-in-customization.md)  
