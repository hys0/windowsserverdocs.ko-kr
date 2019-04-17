---
ms.assetid: 25f5aff1-6abf-4dea-b531-f1d9943bc181
title: "Windows Server 2016에에서 AD FS 사용자 지정"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 2e4d463f5f25fe85dc95d767c9c75b722e60b012
ms.sourcegitcommit: a2699e93a0a19cb138c1fde0c9af36774a12f865
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/20/2017
---
# <a name="ad-fs-customization-in-windows-server-2016"></a>Windows Server 2016에에서 AD FS 사용자 지정

>Windows Server 2016 적용 됩니다.

ADFS 사용 하는 조직에서 피드백에 응답을 사용자 지정 하는 추가 도구 Adfs에 의해 보호 개별 응용 프로그램에 대 한 경험에 로그인 추가 되었습니다.  
이제 설명 텍스트 및 링크 등의 응용 프로그램 웹 콘텐츠를 지정 하는 것 외에도 전체 웹 테마 응용 프로그램에 따라 지정할 수 있습니다.  로고, 그림, 스타일 시트를 또는 전체 onload.js 파일이 포함 됩니다.  
  
## <a name="global-settings"></a>전 세계 설정    
글로벌 일반 설정에 대 한를 참조 [AD FS 로그인 페이지 사용자 지정](https://technet.microsoft.com/library/dn280950.aspx) ADFS Windows Server 2012 r 2에서와 함께 제공 되는 합니다.  
  
## <a name="pre-requisites"></a>필수  
이 문서에 설명 된 절차 하기 전에 다음과 같은 필수 필요 합니다.  
  
-   Windows Server 2016 t p 4 이상 ADFS  
  
## <a name="configure-ad-fs-relying-parties"></a>당사자 광고 FS 의존 구성  
웹 로그인 신뢰 파티 별로 요소 및 테마 구성할 수 있습니다 아래의 PowerShell 예제를 사용 하 여 다음과 같습니다.  
  
### <a name="customize-messages"></a>메시지를 사용자 지정  
  
```  
PS C:\>Set-AdfsRelyingPartyWebContent  
    -TargetRelyingPartyName "<RP trust Name>"  
    -CompanyName "This text appears in place of the federation service display name"  
    -OrganizationalNameDescriptionText "This text appears right below the company name"  
    -SignInPageDescription "This text appears below the credential prompt"  
```  
  
### <a name="customize-company-name-logo-and-image"></a>회사 이름과 로고 이미지를 사용자 지정  
  
```  
PS C:\>Set-AdfsRelyingPartyWebTheme  
    -TargetRelyingPartyName "<RP trust Name>"  
    -Logo @{path="C:\Images\applogo.png"}  
    -Illustration @{path="C:\Images\appillustration.jpg"}  
```  
  
### <a name="customize-entire-page"></a>전체 페이지가 사용자 지정  
  
```  
PS C:\>Set-AdfsRelyingPartyWebTheme  
    -TargetRelyingPartyName "<RP trust Name>"  
    -OnLoadScriptPath @{path="c:\scripts\adfstheme\onload.js"}  
```  
  
## <a name="custom-themes-and-advanced-custom-themes"></a>사용자 지정 테마 및 고급 사용자 지정 테마  
  
사용자 지정 테마 참조 [AD FS 로그인 페이지 사용자 지정](https://technet.microsoft.com/library/dn280950.aspx) 및 [광고 FS 로그인 페이지 고급 사용자 지정 합니다.](https://technet.microsoft.com/library/dn636121.aspx)  
  
## <a name="assigning-custom-web-themes-per-rp"></a>별로 RP 사용자 지정 웹 테마를 지정 하는 방법  
  
할당 하려면 RP 당 테마를 사용자 지정 다음 절차 합니다.  
  
1. 새 테마 복사본 Adfs의 글로벌 테마 기본으로 만들기  
<code>New-AdfsWebTheme -Name AppSpecificTheme -SourceName default</code>  
2.  사용자 지정 주제 내보내기 <code>Export-AdfsWebTheme -Name AppSpecificTheme -DirectoryPath c:\appspecifictheme</code> 3. 테마 파일 (이미지를 위해 css, onload.js)-좋아하는 편집기에 사용자 지정 하거나 파일 4 교체 합니다. ADFS (새로운 테마를 대상으로)를 사용자 지정 된 파일이 파일 시스템에서 가져오기 <code>Set-AdfsWebTheme -TargetName AppSpecificTheme -AdditionalFileResource @{Uri='/adfs/portal/script/onload.js';Path="c:\appspecifictheme\script\onload.js"}</code> 5. 특정 RP (또는 RP의)을 새, 사용자 지정 된 테마 적용
<code>Set-AdfsRelyingPartyWebTheme -TargetRelyingPartyName urn:app1 -SourceWebThemeName AppSpecificTheme</code>  
  
## <a name="home-realm-discovery"></a>홈 영역 검색  
홈 영역 dicovery 사용자 지정 참조 [AD FS 로그인 페이지 사용자 지정](https://technet.microsoft.com/library/dn280950.aspx)합니다.  
  
## <a name="updated-password-page"></a>업데이트 암호 페이지  
사용자 지정 업데이트 암호 페이지에 대 한 내용은 [FS 로그인 페이지 광고를 사용자 지정](https://technet.microsoft.com/library/dn280950.aspx)합니다.  
  
## <a name="customizing-and-alternate-ids"></a>사용자 지정 하 고 암호 확인용 Id  
사용자가 로그인 할 수의 Active Directory Federation Services ADFS ()-방식의 Active Directory Domain Services (AD DS)에서 허용 되는 사용자 id 사용 하 여 응용 프로그램을 사용 하도록 설정 합니다. 여기에 (Upn) 사용자 이름 (johndoe@contoso.com) 또는 도메인 한정 (contoso\johndoe 또는 contoso.com\johndoe) 삼로 계정 이름입니다.  이 확인에 대 한 자세한 내용은 [대체 로그인 구성 id입니다.](Configuring-Alternate-Login-ID.md)  
  
일부 ID 대체 로그인에 대 한 힌트 최종 사용자에 게 ADFS 로그인 페이지를 사용자 지정 또한. 자세한 내용은 참조 사용자 지정 된 로그인 페이지 설명 추가 하 여 로그인 할 수도 있습니다 [FS 로그인 페이지 광고를 사용자 지정 합니다.](https://technet.microsoft.com/library/dn280950.aspx)   
  
사용자 이름 들판 위 문자열 "조직 계정으로 로그인" 사용자 지정 하 여 또한 수행할 수 있습니다.  이 확인에 대 한 내용은 [광고 FS 로그인 페이지 고급 사용자 지정](https://technet.microsoft.com/library/dn636121.aspx)합니다.  

## <a name="additional-references"></a>추가 참조 
[광고 FS 사용자 지정 로그인](AD-FS-user-sign-in-customization.md)  
