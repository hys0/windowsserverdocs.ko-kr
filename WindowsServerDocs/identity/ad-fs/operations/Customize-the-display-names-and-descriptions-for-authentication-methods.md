---
ms.assetid: 309d6358-777d-496a-856d-728246c7d9a1
title: 표시 이름 및 인증 방법에 대 한 설명을 사용자 지정
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: cc0da10858ca6924a516fbf825206e376294209d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407564"
---
# <a name="customize-the-display-names-and-descriptions-for-authentication-methods"></a>표시 이름 및 인증 방법에 대 한 설명을 사용자 지정 


인증 방법에 대한 표시 이름 및 설명을 사용자 지정하려면 `Set-AdfsAuthenticationProviderWebContent` PowerShell cmdlet을 사용하면 됩니다.  이 cmdlet을 사용하려면 먼저 사용자 지정하려는 인증 방법의 이름을 얻어야 합니다.  `Get-AdfsGlobalAuthenticationPolicy`를 사용하여 이 작업을 수행할 수 있습니다.  아래 예제에서는 있다는 것을 알, 우리의 기호\-다음 페이지에 표시 됩니다: "X.509 인증서를 사용 하 여 로그인"입니다.  사용자의 경우 이 작업을 간소화할 수 있습니다.  
  
![displayname을 사용자 지정](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update1.PNG)  
  
먼저 인증 방법의 이름을 가져온 다음 표시된 텍스트를 편집합니다.  
  
 
    Get-AdfsGlobalAuthenticationPolicy  
      
    AdditionalAuthenticationProvider  : {}  
    DeviceAuthenticationEnabled   : False  
    PrimaryIntranetAuthenticationProvider : {FormsAuthentication, CertificateAuthentication}  
    PrimaryExtranetAuthenticationProvider : {FormsAuthentication, CertificateAuthentication}  
    WindowsIntegratedFallbackEnabled  : True  
      
    Set-AdfsAuthenticationProviderWebContent -Name CertificateAuthentication -DisplayName "Sign in with a certificate"  
  
  
![displayname을 사용자 지정](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update2.PNG)  
  
이제 표시 메시지가 변경되었습니다.  
  
![displayname을 사용자 지정](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update3.PNG)  

## <a name="additional-references"></a>추가 참조 
[사용자 로그인 사용자 지정 AD FS](AD-FS-user-sign-in-customization.md) 
