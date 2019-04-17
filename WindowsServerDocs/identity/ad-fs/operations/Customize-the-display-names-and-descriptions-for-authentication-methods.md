---
ms.assetid: 309d6358-777d-496a-856d-728246c7d9a1
title: "표시 이름 및 인증 방법에 대 한 설명을 사용자 지정"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 699622a8a075dd6c78ab1b536dce2abfee642e9e
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="customize-the-display-names-and-descriptions-for-authentication-methods"></a>표시 이름 및 인증 방법에 대 한 설명을 사용자 지정 

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

표시 이름 및 사용할 수 있는 인증 방법에 대 한 설명을 사용자 지정 하 고 `Set-AdfsAuthenticationProviderWebContent` PowerShell cmdlt 합니다.  이 cmdlt를 사용 하려면 먼저 인증 방법 사용자 지정 하려면 이름을 가져와야 합니다.  이렇게 사용 `Get-AdfsGlobalAuthenticationPolicy`합니다.  아래의 예제 우리 표시, 우리의 sign\-페이지에 다음이 표시 되는지: "X.509 인증서를 사용 하 여 로그인" 합니다.  이 사용자의 간소화 하려고 합니다.  
  
![표시 이름 사용자 지정](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update1.PNG)  
  
따라서 먼저 인증 방법의 이름을 연락할 한 다음 표시 되는 텍스트를 편집 했습니다.  
  
 
    Get-AdfsGlobalAuthenticationPolicy  
      
    AdditionalAuthenticationProvider  : {}  
    DeviceAuthenticationEnabled   : False  
    PrimaryIntranetAuthenticationProvider : {FormsAuthentication, CertificateAuthentication}  
    PrimaryExtranetAuthenticationProvider : {FormsAuthentication, CertificateAuthentication}  
    WindowsIntegratedFallbackEnabled  : True  
      
    Set-AdfsAuthenticationProviderWebContent -Name CertificateAuthentication -DisplayName "Sign in with a certificate"  
  
  
![표시 이름 사용자 지정](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update2.PNG)  
  
이제 디스플레이 메시지 변경 된 표시 됩니다.  
  
![표시 이름 사용자 지정](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update3.PNG)  

## <a name="additional-references"></a>추가 참조 
[광고 FS 사용자 지정 로그인](AD-FS-user-sign-in-customization.md) 
