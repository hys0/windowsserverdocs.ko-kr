---
ms.assetid: 1df78c2a-5054-4b54-8310-c48ea62e6e0b
title: AD FS 로그인 페이지에 대 한 사용자 지정 오류 메시지
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 8bcc653cc9eb9adb6d31331463d01774d4faec1a
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189223"
---
# <a name="custom-error-messages-for-ad-fs-sign-in-page"></a>AD FS 로그인 페이지에 대 한 사용자 지정 오류 메시지  


조직에 맞게 조정할 수 있는 사용자 지정 오류 메시지를 구성할 수 있습니다. 다음 그림에는 사용자 지정된 오류 페이지 설명과 일반 오류 메시지가 나와 있습니다. 다음 Windows PowerShell cmdlet을 사용 하 여 오류 메시지를 사용자 지정할 수 있습니다.  
  
![사용자 지정 오류](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom3.png)  
  
## <a name="customize-the-error-page-description"></a>오류 페이지 설명 사용자 지정  
오류 페이지 설명을 사용자 지정 하려면 다음 Windows PowerShell cmdlet 및 구문을 사용 합니다.  
  

`Set-AdfsGlobalWebContent -ErrorPageDescriptionText "This is Contoso's error page description" ` 

  
## <a name="customize-a-generic-error-message"></a>일반 오류 메시지 사용자 지정  
일반 오류 메시지를 사용자 지정 하려면 다음 Windows PowerShell cmdlet 및 구문을 사용 합니다.  
  
 
`Set-AdfsGlobalWebContent -ErrorPageGenericErrorMessage "This is a generic error message.  Contact Contoso IT for assistance." ` 

  
## <a name="customize-an-authorization-error-message"></a>권한 부여 오류 메시지 사용자 지정  
권한 부여 오류 메시지를 사용자 지정 하려면 다음 Windows PowerShell cmdlet 및 구문을 사용 합니다.  
  

    Set-AdfsGlobalWebContent -ErrorPageAuthorizationErrorMessage "You have received an Authorization error.  Contact Contoso IT for assistance."  

  
## <a name="customize-a-device-authentication-error-message"></a>장치 인증 오류 메시지 사용자 지정  
장치 인증 오류 메시지를 사용자 지정 하려면 다음 Windows PowerShell cmdlet 및 구문을 사용 합니다.  
  
 
`Set-AdfsGlobalWebContent -ErrorPageDeviceAuthenticationErrorMessage "Your device is not authorized.  Contact Contoso IT for assistance."`  
 
  
## <a name="customize-a-support-email-error-message"></a>지원 메일 오류 메시지 사용자 지정  
AD FS에서 지원 전자 메일 주소를 구성할 수 있습니다. 를 구성 하는 경우 AD FS는 전자 메일 오류 세부 정보에 최종 사용자에 대 한 링크를 자동으로 나타납니다.  
  
지원 전자 메일 오류 메시지를 사용자 지정 하려면 다음 Windows PowerShell cmdlet 및 구문을 사용 합니다.  
  

    Set-AdfsGlobalWebContent -ErrorPageSupportEmail  "admin@contoso.com"  

  
## <a name="customize-a-relying-party-authorization-message"></a>신뢰 당사자 권한 부여 메시지 사용자 지정  
AD FS에서 신뢰 당사자 권한 부여 오류 메시지를 구성할 수 있습니다.  
  
신뢰 당사자 오류 메시지를 사용자 지정 하려면 다음 Windows PowerShell cmdlet 및 구문을 사용 합니다.  

    Set-AdfsRelyingPartyWebContent -Name fedpassive -ErrorPageAuthorizationErrorMessage "<p> You need to be a member of Security Auditors to access this site. Click <A href='http://accessrequest/'>here</A> for more information.</p>“  


## <a name="additional-references"></a>추가 참조 
[AD FS 사용자 로그인 사용자 지정](AD-FS-user-sign-in-customization.md)    
