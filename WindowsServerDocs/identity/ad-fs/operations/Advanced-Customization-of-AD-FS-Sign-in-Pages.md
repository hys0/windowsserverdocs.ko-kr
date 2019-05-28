---
ms.assetid: 882abec8-0189-4f73-99c5-792987168080
title: AD FS 로그인 페이지의 고급 사용자 지정
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 01/16/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 73ff3fc6df872edd29735ee96c0918144250d5f1
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190044"
---
# <a name="advanced-customization-of-ad-fs-sign-in-pages"></a>AD FS 로그인 페이지의 고급 사용자 지정

  
## <a name="advanced-customization-of-ad-fs-sign-in-pages"></a>AD FS 로그인의 고급 사용자 지정\-페이지  
Windows Server 2012 R2에서 AD FS 제공 빌드된\-로그인 사용자 지정에 대 한 지원이\-환경에서. 이러한 시나리오에서는 기본 제공 되는 대부분\-Windows PowerShell cmdlet은 모든 필요한 것입니다.  기본 제공을 사용 하는 것이 좋습니다\-AD FS에 대 한 표준 요소를 사용자 지정 하려면 Windows PowerShell 명령에서 로그인\-환경이 가능 합니다.  참조 [AD FS 사용자 지정 로그인](AD-FS-user-sign-in-customization.md) 자세한 내용은 합니다.  
  
경우에 따라 AD FS 관리자 제공할 경우도 추가 기호\-되지 않은 환경에 기존를 통해 가능한 PowerShell 명령에서 제공 되는\-AD FS 사용 하 여 상자입니다. 특정 인스턴스에서 것이 가능한 \(아래에 제공 된 지침 내\) 기호를 사용자 지정 하는 관리자에 대 한\-환경에서 추가 논리를 추가 하 여 추가 **onload.js** 는 AD FS에서 제공 되 고 모든 AD FS 페이지에서 실행 됩니다.  
  
## <a name="things-to-know-before-you-start"></a>시작 하기 전에 알아야 할 사항  
  
-   리디렉션 흐름에 영향을 또는 AD FS를 사용 하는 프로토콜 매개 변수를 수정 하는 모든 변경 지원 되지 않습니다.
  
-   기본 웹 테마를 함께 제공 되는 원래 onload.js, 다양 한 폼 팩터 용 페이지 렌더링을 처리 하는 코드를 포함 합니다. 원래 onload.js 콘텐츠를 수정 하지만 코드에 사용자 지정 논리를 처리 하는 기존 onload.js을 추가할 필요가 것이 좋습니다.  
  
-   AD FS 포함 기본 제공\-기본 이라고 하는 웹 테마의 합니다. Onload.js의 기본 웹 테마를 수정할 수 없습니다. 만들기 및 AD FS 로그인에 대 한 사용자 지정 웹 테마를 사용 해야 onload.js를 업데이트 하려면\-페이지에서입니다.  참조 [AD FS 사용자 지정 로그인](AD-FS-user-sign-in-customization.md) 사용자 지정 웹 테마를 만드는 방법에 대 한 정보에 대 한 합니다.  
  
-   모든 ADFS 페이지에 동일한 onload.js 실행될지 \(예입니다. 폼\-로그온 페이지와 홈 영역 검색 페이지 등 기반\)입니다. 스크립트의 코드 에서만 가져옵니다 실행 설계 되었으며 예기치 않게 실행 되지 않는 있는지 확인 해야 합니다.  
  
-   모든 HTML 요소를 참조할 때 요소에 역할을 수행 하기 전에 요소의 있는지 항상 확인 하는 확인 합니다. 이 견고성을 제공 하 고이 요소를 포함 하지 않는 페이지에서 사용자 지정 논리를 실행 하지는 확인 합니다. AD FS 로그인에 HTML 소스를 간단히 볼 수 있습니다\-기존 요소를 보려면 페이지에서입니다.  
  
-   다른 환경에서 사용자 지정 유효성 검사 및 롤링 하 프로덕션에 AD FS 서버 하기 전에 테스트 하는 것이 좋습니다. 이렇게 하면 유효성 검사 하기 전에 이러한 사용자 지정에 노출 되는 최종 사용자의 가능성이 줄어듭니다.  
  
## <a name="customizing-the-ad-fs-sign-in-experience-by-using-onloadjs"></a>AD FS 로그인 사용자 지정\-onload.js를 사용 하 여 환경에서  
AD FS 서비스에 대 한 onload.js 사용자 지정 하는 경우 다음 단계를 사용 합니다.  
  
#### <a name="customizing-onloadjs-for-the-ad-fs-service"></a>Onload.js AD FS 서비스에 대 한 사용자 지정  
  
1.  사용자 지정 논리에 onload.js를 추가 하려면 먼저 사용자 지정 웹 테마를 만들 해야 합니다. Out 제공 되는 테마\-의\-는\-상자 기본 테마 라고 합니다. 기본 테마를 내보내 이를 사용하여 빠르게 시작할 수 있습니다. 다음 cmdlet은 기본 웹 테마를 복제 하는 사용자 지정 웹 테마를 만듭니다.  
  
    ```  
    New-AdfsWebTheme –Name custom –SourceName default  
  
    ```  
  
2.  그런 다음 사용자 지정 내보내거나 기본 웹 테마 onload.js 파일을 가져올 수 있습니다. 웹 테마를 내보내려면 다음 cmdlet을 사용 합니다.  
  
    ```  
    Export-AdfsWebTheme –Name default –DirectoryPath c:\theme  
  
    ```  
  
    보면 onload.js 스크립트 폴더 아래에 있는 디렉터리에 위의 export cmdlet에서 지정 하 고 스크립트에 사용자 지정 논리를 추가 \(참조 아래 예제 섹션의 사용 사례\)합니다.  
  
3.  Onload.js 필요에 따라 사용자 지정에 필요한 수정 사항을 확인 합니다.  
  
4.  수정 된 onload.js를 사용 하 여 테마를 업데이트 합니다. 업데이트 onload.js 사용자 지정 웹 테마를 적용 하려면 다음 cmdlet을 사용 합니다.  

     Windows Server 2012 R2에서 AD FS:  

    ```  
    Set-AdfsWebTheme -TargetName custom -AdditionalFileResource @{Uri=’/adfs/portal/script/onload.js’;path="c:\theme\script\onload.js"}  
  
    ```  
    Windows Server 2016에서 AD FS:

     ```  
    Set-AdfsWebTheme -TargetName custom -OnLoadScriptPath "c:\ADFStheme\script\onload.js"   
  
    ```  
  
5.  AD fs 사용자 지정 웹 테마를 적용 하려면 다음 cmdlet을 사용 합니다.  
  
    ```  
    Set-AdfsWebConfig -ActiveThemeName custom  
    ```  
  
## <a name="additional-customization-examples"></a>추가 사용자 지정 예제  
Onload.js 다른 미세에 대 한 추가 사용자 지정 코드의 예는\-목적으로 조정 합니다. 사용자 지정 코드를 추가할 때 하세요 항상 추가 사용자 지정 코드를 onload.js 맨 아래에 있습니다.  
  
### <a name="example-1-change-sign-in-with-organizational-account-string"></a>"조직 계정으로 로그인" 문자열을 변경 하는 예 1:  
기본 AD FS 폼\-로그인 기반\-위에서 사용자 입력된 상자에 "조직 계정으로 로그인"의 제목이 페이지에 있습니다.  
  
사용자 고유의 문자열을 사용 하 여이 문자열을 바꾸려는 경우 onload.js에 다음 코드를 추가할 수 있습니다.  
  
```  
// Sample code to change “Sign in with organizational account” string.  
  
// Check whether the loginMessage element is present on this page.  
var loginMessage = document.getElementById('loginMessage');  
if (loginMessage)  
{  
       // loginMessage element is present, modify its properties.  
       loginMessage.innerHTML = 'Your company description text';  
}  
  
```  
  
### <a name="example-2-accept-sam-account-name-as-a-login-format-on-an-ad-fs-form-based-sign-in-page"></a>예제 2: 수락 SAM\-AD FS 폼에서 로그인 형식으로 계정 이름을\-기반 sign\-페이지에서  
기본 AD FS 폼\-기반 sign\-페이지에서 사용자 계정 이름의 로그인 형식을 지원 \(Upn\) \(예를 들어 **johndoe@contoso.com** \) 또는 도메인 sam 한정\-계정 이름 \( **contoso\\johndoe** 하거나 **contoso.com\\johndoe**\)합니다. 경우에 동일한 도메인에서 가져와야 하는 모든 사용자가 sam만 알고\-sam 하를 사용 하 여 사용자에 서명할 수 있는 시나리오를 지원 하려는 계정 이름,\-계정 이름만 있습니다. 이 시나리오를 지원 하려면 사용 하려는 도메인을 사용 하 여 도메인 "contoso.com" 예에서 아래 바꾸기만 onload.js에 다음 코드를 추가할 수 있습니다.  
  
```  
if (typeof Login != 'undefined'){  
    Login.submitLoginRequest = function () {   
    var u = new InputUtil();  
    var e = new LoginErrors();  
    var userName = document.getElementById(Login.userNameInput);  
    var password = document.getElementById(Login.passwordInput);  
    if (userName.value && !userName.value.match('[@\\\\]'))   
    {  
        var userNameValue = 'contoso.com\\' + userName.value;  
        document.forms['loginForm'].UserName.value = userNameValue;  
    }  
  
    if (!userName.value) {  
       u.setError(userName, e.userNameFormatError);  
       return false;  
    }  
  
    if (!password.value)   
    {  
        u.setError(password, e.passwordEmpty);  
        return false;  
    }  
    document.forms['loginForm'].submit();  
    return false;  
};  
}  
  
```  
  
## <a name="additional-references"></a>추가 참조 
[AD FS 사용자 로그인 사용자 지정](AD-FS-user-sign-in-customization.md)  
  

