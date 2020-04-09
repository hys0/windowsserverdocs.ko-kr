---
ms.assetid: 25f5aff1-6abf-4dea-b531-f1d9943bc181
title: Windows Server 2016에서에서 AD FS 사용자 지정 합니다.
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 3f46ea97034c382d1846ff95bb0974307943bbc5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860096"
---
# <a name="ad-fs-customization-in-windows-server-2016"></a>Windows Server 2016에서에서 AD FS 사용자 지정 합니다.


AD FS를 사용 하는 조직의 피드백에 대 한 응답으로 AD FS에서 보호 하는 개별 응용 프로그램에 대 한 사용자 로그인 환경을 사용자 지정 하는 추가 도구를 추가 했습니다.  
설명 텍스트 및 링크와 같은 응용 프로그램별 웹 콘텐츠를 지정 하는 것 외에, 이제 응용 프로그램당 전체 웹 테마를 지정할 수 있습니다.  여기에는 로고, 그림, 스타일 시트 또는 전체 onload .js 파일이 포함 됩니다.  
  
## <a name="global-settings"></a>전역 설정    
일반 전역 설정의 경우 Windows Server 2012 r 2의 AD FS와 함께 제공 되는 [AD FS 로그인 페이지를 사용자 지정](https://technet.microsoft.com/library/dn280950.aspx) 하는 방법을 참조할 수 있습니다.  
  
## <a name="pre-requisites"></a>필수 구성 요소  
이 문서에 설명 된 절차를 시도 하기 전에 다음과 같은 필수 구성 요소가 필요 합니다.  
  
-   AD FS Windows Server 2016 t p 4 이상  
  
## <a name="configure-ad-fs-relying-parties"></a>AD FS 신뢰 당사자 구성  
신뢰 당사자 로그인 웹 요소 및 테마는 아래의 PowerShell 예제를 사용 하 여 구성할 수 있습니다.  
  
### <a name="customize-messages"></a>메시지 사용자 지정  
  
```  
PS C:\>Set-AdfsRelyingPartyWebContent  
    -TargetRelyingPartyName "<RP trust Name>"  
    -CompanyName "This text appears in place of the federation service display name"  
    -OrganizationalNameDescriptionText "This text appears right below the company name"  
    -SignInPageDescription "This text appears below the credential prompt"  
```  
  
### <a name="customize-company-name-logo-and-image"></a>회사 이름, 로고 및 이미지 사용자 지정  
  
```  
PS C:\>Set-AdfsRelyingPartyWebTheme  
    -TargetRelyingPartyName "<RP trust Name>"  
    -Logo @{path="C:\Images\applogo.png"}  
    -Illustration @{path="C:\Images\appillustration.jpg"}  
```  
  
### <a name="customize-entire-page"></a>전체 페이지 사용자 지정  
  
```  
PS C:\>Set-AdfsRelyingPartyWebTheme  
    -TargetRelyingPartyName "<RP trust Name>"  
    -OnLoadScriptPath @{path="c:\scripts\adfstheme\onload.js"}  
```  
  
## <a name="custom-themes-and-advanced-custom-themes"></a>사용자 지정 테마 및 고급 사용자 지정 테마  
  
사용자 지정 테마의 경우 [AD FS 로그인 페이지를 사용자 지정](https://technet.microsoft.com/library/dn280950.aspx) 하 고 [AD FS 로그인 페이지의 고급 사용자 지정](https://technet.microsoft.com/library/dn636121.aspx) 을 참조 하세요.  
  
## <a name="assigning-custom-web-themes-per-rp"></a>RP 당 사용자 지정 웹 테마 할당  
  
RP 당 사용자 지정 테마를 할당 하려면 다음 절차를 사용 합니다.  
  
1. AD FS의 기본 전역 테마에 대 한 복사본으로 새 테마를 만듭니다.  
`New-AdfsWebTheme -Name AppSpecificTheme -SourceName default`  
2. 사용자 지정할 테마 내보내기  
`Export-AdfsWebTheme -Name AppSpecificTheme -DirectoryPath c:\appspecifictheme`  
3. 선호 하는 편집기에서 테마 파일 (이미지, css, onload)을 사용자 지정 하거나 파일을 바꿉니다.  
4. 새 테마를 대상으로 하는 AD FS 파일 시스템에서 사용자 지정 된 파일을 가져옵니다.  
`Set-AdfsWebTheme -TargetName AppSpecificTheme -AdditionalFileResource @{Uri='/adfs/portal/script/onload.js';Path="c:\appspecifictheme\script\onload.js"}`  
5. 사용자 지정 된 새 테마를 특정 RP (또는 RP)에 적용 합니다.  
`Set-AdfsRelyingPartyWebTheme -TargetRelyingPartyName urn:app1 -SourceWebThemeName AppSpecificTheme`  
  
## <a name="home-realm-discovery"></a>홈 영역 검색  
홈 영역 검색 사용자 지정에 대해서 [는 AD FS 로그인 페이지 사용자 지정](https://technet.microsoft.com/library/dn280950.aspx)을 참조 하세요.  
  
## <a name="updated-password-page"></a>업데이트 된 암호 페이지  
암호 업데이트 페이지를 사용자 지정 하는 방법에 대 한 자세한 내용은 [AD FS 로그인 페이지 사용자 지정](https://technet.microsoft.com/library/dn280950.aspx)을 참조 하세요.  
  
## <a name="customizing-and-alternate-ids"></a>사용자 지정 및 대체 Id  
사용자는 AD DS (Active Directory Domain Services)에서 허용 하는 모든 형태의 사용자 식별자를 사용 하 여 Active Directory Federation Services (AD FS) 사용 응용 프로그램에 로그인 할 수 있습니다. 여기에는 Upn (사용자 계정 이름) (johndoe@contoso.com) 또는 도메인 정규화 된 sam-계정 이름 (예 contoso\johndoe 또는 com\johndoe)이 포함 됩니다.  이에 대 한 자세한 내용은 [대체 로그인 ID 구성](Configuring-Alternate-Login-ID.md) 을 참조 하세요.  
  
일부 힌트가 대체 로그인 ID에 대 한 최종 사용자에 게 AD FS 로그인 페이지 사용자 지정 또한 하려는 경우 사용자 지정 된 로그인 페이지 설명을 추가 하 여이 작업을 수행할 수 있습니다. 자세한 내용은 [AD FS 로그인 페이지 사용자 지정](https://technet.microsoft.com/library/dn280950.aspx) 을 참조 하세요.   
  
사용자 이름 필드 위의 "조직 계정으로 로그인" 문자열을 사용자 지정 하 여이 작업을 수행할 수도 있습니다.  이에 대 한 자세한 내용은 [AD FS 로그인 페이지의 고급 사용자 지정](https://technet.microsoft.com/library/dn636121.aspx)을 참조 하세요.  

## <a name="additional-references"></a>추가 참조 
[사용자 로그인 사용자 지정 AD FS](AD-FS-user-sign-in-customization.md)  
