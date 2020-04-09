---
ms.assetid: 28043fc4-a34d-4710-ac3b-5c9d4d6a895c
title: AD FS 로그인 페이지에서 회사 이름을 변경 합니다.
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 378979825c0e8e505c3996cf8cbcdb471a0c7d79
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859966"
---
# <a name="change-the-company-name-on-the-ad-fs-sign-in-page"></a>AD FS 로그인 페이지에서 회사 이름을 변경 합니다.
 
페이지의 부호\-에 표시 되는 회사 이름을 변경 하려면 다음 Windows PowerShell cmdlet 및 구문을 사용 합니다. 이 값은 기본적으로 설치하는 동안 입력한 페더레이션 서비스 표시 이름 값을 사용하여 설정됩니다.  

![이름 변경](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1.png)
  
  
    Set-AdfsGlobalWebContent –CompanyName "Contoso Corp"  
 
  
> [!NOTE]  
> Windows PowerShell 통합 스크립팅 환경에 사용할 수도 있습니다 \(ISE\) 회사 이름을 변경할 수 있습니다. Windows PowerShell ISE를 사용 하 여 유니코드에서 콘텐츠를 표시할 수 있습니다\-호환 환경입니다. 추가 정보는 [Windows PowerShell ISE 소개](https://technet.microsoft.com/library/dd315244.aspx)를 참조하세요.  

## <a name="additional-references"></a>추가 참조 
[사용자 로그인 사용자 지정 AD FS](AD-FS-user-sign-in-customization.md)  
  
