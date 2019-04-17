---
ms.assetid: 1df78c2a-5054-4b54-8310-c48ea62e6e0b
title: "ADFS 로그인 페이지에 대 한 사용자 지정 오류 메시지"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3a015c27f784d5b1f488f984450612820d4a06b1
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="custom-error-messages-for-ad-fs-sign-in-page"></a>ADFS 로그인 페이지에 대 한 사용자 지정 오류 메시지  

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

조직에 맞게 조정할 수 있는 사용자 지정 오류 메시지를 구성할 수 있습니다. 다음 그림 사용자 지정 된 오류 페이지 설명 하 고 일반 오류 메시지가 표시 됩니다. 다음과 같은 Windows PowerShell cmdlet을 사용 오류 메시지를 사용자 지정할 수 있습니다.  
  
![사용자 지정 오류](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom3.png)  
  
## <a name="customize-the-error-page-description"></a>오류 페이지 설명 사용자 지정  
오류 페이지 설명을 사용자 지정 하려면 다음 Windows PowerShell cmdlet와 구문을 사용 합니다.  
  

`Set-AdfsGlobalWebContent -ErrorPageDescriptionText "This is Contoso's error page description" ` 

  
## <a name="customize-a-generic-error-message"></a>일반적인 오류 메시지를 사용자 지정  
일반적인 오류 메시지를 사용자 지정 하려면 다음 Windows PowerShell cmdlet와 구문을 사용 합니다.  
  
 
`Set-AdfsGlobalWebContent -ErrorPageGenericErrorMessage "This is a generic error message.  Contact Contoso IT for assistance." ` 

  
## <a name="customize-an-authorization-error-message"></a>인증 오류 메시지를 사용자 지정  
인증 오류 메시지를 사용자 지정 하려면 다음 Windows PowerShell cmdlet와 구문을 사용 합니다.  
  

    Set-AdfsGlobalWebContent -ErrorPageAuthorizationErrorMessage "You have received an Authorization error.  Contact Contoso IT for assistance."  

  
## <a name="customize-a-device-authentication-error-message"></a>장치 인증 오류 메시지를 사용자 지정  
장치 인증 오류 메시지를 사용자 지정 하려면 다음 Windows PowerShell cmdlet와 구문을 사용 합니다.  
  
 
`Set-AdfsGlobalWebContent -ErrorPageDeviceAuthenticationErrorMessage "Your device is not authorized.  Contact Contoso IT for assistance."`  
 
  
## <a name="customize-a-support-email-error-message"></a>지원 메일 오류 메시지를 사용자 지정  
Adfs의 지원 메일 주소를 구성할 수 있습니다. ADFS 구성 하 고, 최종 사용자가 메일 오류 세부 정보에 대 한 링크를 자동으로 표시 됩니다.  
  
지원 메일 오류 메시지를 사용자 지정 하려면 다음 Windows PowerShell cmdlet와 구문을 사용 합니다.  
  

    Set-AdfsGlobalWebContent -ErrorPageSupportEmail  "admin@contoso.com"  

  
## <a name="customize-a-relying-party-authorization-message"></a>신뢰 자 인증 메시지를 사용자 지정  
Adfs의 신뢰 자 인증 오류 메시지를 구성할 수 있습니다.  
  
신뢰 파티 오류 메시지를 사용자 지정 하려면 다음 Windows PowerShell cmdlet와 구문을 사용 합니다.  

    Set-AdfsRelyingPartyWebContent -Name fedpassive -ErrorPageAuthorizationErrorMessage "<p> You need to be a member of Security Auditors to access this site. Click <A href='http://accessrequest/'>here</A> for more information.</p>“  


## <a name="additional-references"></a>추가 참조 
[광고 FS 사용자 지정 로그인](AD-FS-user-sign-in-customization.md)    
