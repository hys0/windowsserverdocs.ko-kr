---
ms.assetid: 7e804590-6d6c-4cca-ac14-02d4dff06cec
title: "업데이트 암호 사용자 지정"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4b06992bfb398b66988ad4882217a8a83738365e
ms.sourcegitcommit: 78d8839ccafa9530784cb9e38c3127ed2c215423
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="update-password-customization"></a>업데이트 암호 사용자 지정 

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

경우에 따라 사용자가 자신의 계정 암호를 변경 하 여 회사 네트워크에 연결할 수 되지 않을 수 있습니다. 이 팩터 가장 가까운에서 라이브 수 있는 직원 원격 특히 문제가 발생할 수 있습니다 본사 합니다. 이러한 특정 경우에 대 한 업데이트 암호 페이지만 인터넷에 연결 하 여 사용할 수 있습니다.  
  
직접 설명 페이지에 제공 하 여 업데이트 암호 페이지를 사용자 지정할 수 있습니다.  
  
> 암호 업데이트 페이지를 사용 하려면 아래 끝점 AD FS 관리로 이동 합니다. 암호 업데이트에 대 한 끝점은 기타-/ adfs/포털/updatepassword/에서 맨 아래에 있습니다. 끝점 설정한 후 ADFS 서비스 다시 시작 해야 합니다. 이 수동으로 수행 해야 합니다. Https://로 이동할 수 있습니다<fqdn>/adfs/포털/updatepassword/회사에서 디바이스를 연결 하 고 업데이트 암호 페이지가 표시 됩니다.  
  
![업데이트](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom5.png)  
  
## <a name="customize-the-update-password-page-description"></a>업데이트 암호 페이지 설명 사용자 지정  
업데이트 암호 페이지 설명을 사용자 지정 하려면 다음 Windows PowerShell cmdlet와 구문을 사용 합니다.  
  

    Set-AdfsGlobalWebContent -UpdatePasswordPageDescriptionText "This is the Contoso Update Password page."  

## <a name="additional-references"></a>추가 참조 
[광고 FS 사용자 지정 로그인](AD-FS-user-sign-in-customization.md)  
