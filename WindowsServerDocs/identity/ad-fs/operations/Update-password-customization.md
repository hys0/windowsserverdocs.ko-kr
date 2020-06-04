---
ms.assetid: 7e804590-6d6c-4cca-ac14-02d4dff06cec
title: 사용자 지정 암호를 업데이트 합니다.
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: f43b3052d64c7a5766e014aa47063c7e17a7d2ab
ms.sourcegitcommit: 2cc251eb5bc3069bf09bc08e06c3478fcbe1f321
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/03/2020
ms.locfileid: "84333944"
---
# <a name="update-password-customization"></a>사용자 지정 암호를 업데이트 합니다. 


경우에 따라 사용자가 자신의 계정 암호를 변경하기 위해 회사 네트워크에 연결하지 못할 수도 있습니다. 이 요소는 가장 가까운 회사 사무실에서 멀리 떨어진 곳에 살고 있을 수 있는 원격 직원에게 특히 문제가 될 수 있습니다. 이 특정한 경우 인터넷에 연결하는 것만으로 암호 업데이트 페이지를 사용할 수 있습니다.  
  
페이지에 대한 고유한 설명을 제공하여 암호 업데이트 페이지를 사용자 지정할 수 있습니다.  
  
> 암호 업데이트 페이지를 사용하도록 설정하려면 AD FS 관리에서 엔드포인트로 이동합니다. 암호 업데이트 엔드포인트는 기타(/adfs/portal/updatepassword/)의 맨 아래에 있습니다. 엔드포인트를 사용하도록 설정한 후에는 AD FS 서비스를 다시 시작해야 합니다. 이 작업은 수동으로 수행해야 합니다. 외부에서 암호 업데이트 웹 페이지를 사용 하 고 웹 응용 프로그램 프록시를 사용 하는 경우 프록시 (프록시 사용)에서 사용 하도록 설정 해야 합니다. 그런 다음 작업 공간에 연결된 디바이스에서 https://<fqdn>/adfs/portal/updatepassword/로 이동하면 암호 업데이트 페이지를 볼 수 있습니다.  
  
![업데이트](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom5.png)  
  
## <a name="customize-the-update-password-page-description"></a>암호 업데이트 페이지 설명 사용자 지정  
암호 업데이트 페이지 설명을 사용자 지정 하려면 다음 Windows PowerShell cmdlet 및 구문을 사용 합니다.  
  

    Set-AdfsGlobalWebContent -UpdatePasswordPageDescriptionText "This is the Contoso Update Password page."  

## <a name="additional-references"></a>추가 참조 
[사용자 로그인 사용자 지정 AD FS](AD-FS-user-sign-in-customization.md)  
