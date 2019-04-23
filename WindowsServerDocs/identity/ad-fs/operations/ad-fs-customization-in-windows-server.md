---
ms.assetid: 25f5aff1-6abf-4dea-b531-f1d9943bc181
title: Windows Server 2016에서에서 AD FS 사용자 지정 합니다.
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 2e4d463f5f25fe85dc95d767c9c75b722e60b012
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852034"
---
# <a name="ad-fs-customization-in-windows-server-2016"></a>Windows Server 2016에서에서 AD FS 사용자 지정 합니다.

>적용 대상: Windows Server 2016

AD FS를 사용 하 여 조직에서 피드백에 응답으로 사용자에 맞게 추가 도구 AD FS로 보호 하는 개별 응용 프로그램에 대 한 환경에 로그인 추가 했습니다.  
이제 설명 텍스트 및 링크와 같은 응용 프로그램별 웹 콘텐츠를 지정 하는 것 외에도 전체 웹 테마 응용 프로그램 별로 지정할 수 있습니다.  이 로고, 그림, 스타일 시트 또는 전체 onload.js 파일을 포함 합니다.  
  
## <a name="global-settings"></a>전역 설정    
일반 전역 설정에 대 한를 참조할 수 있습니다 [Customizing the AD FS sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx) Windows Server 2012 R2에서 AD FS와 함께 제공 되는 합니다.  
  
## <a name="pre-requisites"></a>필수 구성 요소  
이 문서에 설명 된 절차를 시도 하기 전에 다음 필수 필요 합니다.  
  
-   AD FS Windows Server 2016 t p 4 이상  
  
## <a name="configure-ad-fs-relying-parties"></a>AD FS 신뢰 당사자를 구성 합니다.  
웹 로그인 신뢰 당사자 별 요소 및 테마 구성할 수 있습니다 다음 PowerShell 예제를 사용 하 여:  
  
### <a name="customize-messages"></a>메시지를 사용자 지정  
  
```  
PS C:\>Set-AdfsRelyingPartyWebContent  
    -TargetRelyingPartyName "<RP trust Name>"  
    -CompanyName "This text appears in place of the federation service display name"  
    -OrganizationalNameDescriptionText "This text appears right below the company name"  
    -SignInPageDescription "This text appears below the credential prompt"  
```  
  
### <a name="customize-company-name-logo-and-image"></a>회사 이름, 로고 및 이미지를 사용자 지정  
  
```  
PS C:\>Set-AdfsRelyingPartyWebTheme  
    -TargetRelyingPartyName "<RP trust Name>"  
    -Logo @{path="C:\Images\applogo.png"}  
    -Illustration @{path="C:\Images\appillustration.jpg"}  
```  
  
### <a name="customize-entire-page"></a>전체 페이지를 사용자 지정  
  
```  
PS C:\>Set-AdfsRelyingPartyWebTheme  
    -TargetRelyingPartyName "<RP trust Name>"  
    -OnLoadScriptPath @{path="c:\scripts\adfstheme\onload.js"}  
```  
  
## <a name="custom-themes-and-advanced-custom-themes"></a>사용자 지정 테마 및 고급 사용자 지정 테마  
  
사용자 지정 테마를 참조 하세요 [Customizing the AD FS sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx) 고 [Advanced Customization of AD FS 로그인 페이지입니다.](https://technet.microsoft.com/library/dn636121.aspx)  
  
## <a name="assigning-custom-web-themes-per-rp"></a>RP 별로 사용자 지정 웹 테마를 할당합니다.  
  
RP 별로 사용자 지정 테마를 할당 하려면 다음 절차를 따르십시오.  
  
1. 기본적으로 AD FS에서 전역 테마에 대 한 복사본으로 새 테마 만들기  
<code>New-AdfsWebTheme -Name AppSpecificTheme -SourceName default</code> 2.  사용자 지정 테마를 내보내려면 <code>Export-AdfsWebTheme -Name AppSpecificTheme -DirectoryPath c:\appspecifictheme</code>  
3. 테마 파일 (이미지, css, onload.js)-좋아하는 편집기에서 사용자 지정 또는 4 파일을 대체 합니다. AD FS (새 테마를 대상)에 파일 시스템에서 사용자 지정된 파일 가져오기 <code>Set-AdfsWebTheme -TargetName AppSpecificTheme -AdditionalFileResource @{Uri='/adfs/portal/script/onload.js';Path="c:\appspecifictheme\script\onload.js"}</code>  
5. 특정 RP (또는 RP의)에 새, 사용자 지정 테마 적용 <code>Set-AdfsRelyingPartyWebTheme -TargetRelyingPartyName urn:app1 -SourceWebThemeName AppSpecificTheme</code>  
  
## <a name="home-realm-discovery"></a>홈 영역 검색  
홈 영역 검색 사용자 지정 참조 [Customizing the AD FS sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx)합니다.  
  
## <a name="updated-password-page"></a>업데이트 된 암호 페이지  
암호 업데이트 페이지를 사용자 지정 하는 방법은 [AD FS 로그인 페이지 사용자 지정](https://technet.microsoft.com/library/dn280950.aspx)합니다.  
  
## <a name="customizing-and-alternate-ids"></a>사용자 지정 및 대체 Id  
Active Directory Federation Services (AD FS)에 로그인 한 사용자 수-Active Directory Domain Services (AD DS)에서 허용 되는 사용자 식별자의 모든 형태를 사용 하 여 응용 프로그램을 사용 하도록 설정 합니다. 여기에 사용자 계정 이름 (Upn) 포함 됩니다. (johndoe@contoso.com) 또는 도메인 sam 계정 이름 (예: contoso\johndoe 나 contoso.com \johndoe)를 한정 합니다.  이 참조에 대 한 자세한 내용은 [구성 대체 로그인 id입니다.](Configuring-Alternate-Login-ID.md)  
  
일부 힌트가 대체 로그인 ID에 대 한 최종 사용자에 게 AD FS 로그인 페이지 사용자 지정 또한 하려는 경우 자세한 내용은 사용자 지정된 로그인 페이지 설명을 추가 하 여 수행할 수 있습니다 [AD FS 로그인 페이지 사용자 지정 합니다.](https://technet.microsoft.com/library/dn280950.aspx)   
  
사용자 이름 필드 위 "조직 계정으로 로그인" 문자열을 사용자 지정 하 여이 수행할 수도 있습니다.  이 참조에 대 한 내용은 [Advanced Customization of AD FS 로그인 페이지](https://technet.microsoft.com/library/dn636121.aspx)합니다.  

## <a name="additional-references"></a>추가 참조 
[AD FS 사용자 로그인 사용자 지정](AD-FS-user-sign-in-customization.md)  
