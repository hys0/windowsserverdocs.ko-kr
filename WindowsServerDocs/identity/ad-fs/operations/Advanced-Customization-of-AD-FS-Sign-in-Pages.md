---
ms.assetid: 882abec8-0189-4f73-99c5-792987168080
title: AD FS 로그인 페이지에 대 한 고급 사용자 지정
author: billmath
ms.author: billmath
manager: femila
ms.date: 01/16/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: a4a70632ea4c1db39c020327bbe135f4798e6970
ms.sourcegitcommit: 2cc251eb5bc3069bf09bc08e06c3478fcbe1f321
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/03/2020
ms.locfileid: "84333894"
---
# <a name="advanced-customization-of-ad-fs-sign-in-pages"></a>AD FS 로그인 페이지에 대 한 고급 사용자 지정

  
## <a name="advanced-customization-of-ad-fs-sign-in-pages"></a>AD FS 로그인 페이지의 고급 사용자 지정 \-  
Windows Server 2012 r 2의 AD FS에서는 \- 로그인 환경을 사용자 지정 하는 기능을 기본적으로 지원 합니다 \- . 대부분의 시나리오에서는 기본 제공 \- Windows PowerShell cmdlet이 모두 필요 합니다.  가능 하면 기본 제공 \- Windows PowerShell 명령을 사용 하 여 AD FS 로그인 환경에 대 한 표준 요소를 사용자 지정 하는 것이 좋습니다 \- .  자세한 내용은 [AD FS 사용자 로그인 사용자 지정](AD-FS-user-sign-in-customization.md) 을 참조 하세요.  
  
경우에 따라 AD FS 관리자는 \- AD FS와 함께 제공 되는 기존 PowerShell 명령을 통해 불가능 한 추가 로그인 환경을 제공할 수 있습니다 \- . 특정 한 경우에는 아래에 \( 제공 된 지침에 따라 \) 사용자가 \- AD FS에서 제공 하는 **onload** 에 논리를 추가 하 여 로그인 환경을 사용자 지정 하 고 모든 AD FS 페이지에서 실행할 수 있습니다.  
  
## <a name="things-to-know-before-you-start"></a>시작 하기 전에 알아두어야 할 사항  
  
-   리디렉션 흐름에 영향을 주는 변경 내용 또는 AD FS 작동 하는 프로토콜 매개 변수를 수정 하는 것은 지원 되지 않습니다.
  
-   기본 웹 테마와 함께 제공 되는 원래 onload .js에는 다양 한 폼 팩터를 위한 페이지 렌더링을 처리 하는 코드가 포함 되어 있습니다. 원래 onload .js 콘텐츠를 수정 하지 않는 것이 좋으며, 사용자 지정 논리를 처리 하는 기존 onload에만 코드를 추가 합니다.  
  
-   AD FS 기본 제공 웹 테마와 함께 제공 \- 됩니다 .이 테마는 기본값 이라고 합니다. 기본 웹 테마의 onload는 수정할 수 없습니다. Onload를 업데이트 하려면 AD FS 로그인 페이지에 대 한 사용자 지정 웹 테마를 만들고 사용 해야 \- 합니다.  사용자 지정 웹 테마를 만드는 방법에 대 한 자세한 내용은 [AD FS 사용자 로그인 사용자 지정](AD-FS-user-sign-in-customization.md) 을 참조 하세요.  
  
-   모든 ADFS 페이지 (예:)에서 동일한 onload를 실행 합니다 \( . 양식 \- 기반 로그온 페이지, 홈 영역 검색 페이지 등 \) 스크립트의 코드는 디자인 될 때만 실행 되 고 예기치 않게 실행 되지 않는지 확인 해야 합니다.  
  
-   HTML 요소를 참조할 때 요소에 대 한 동작을 수행 하기 전에 항상 요소가 있는지 확인 해야 합니다. 이를 통해 견고성을 제공 하 고이 요소를 포함 하지 않는 페이지에서 사용자 지정 논리를 실행 하지 않도록 합니다. AD FS 로그인 페이지에서 HTML 소스를 확인 \- 하 여 기존 요소를 볼 수 있습니다.  
  
-   대체 환경에서 사용자 지정 항목의 유효성을 검사 하 고 프로덕션 AD FS 서버에 롤아웃하기 전에 테스트 하는 것이 좋습니다. 이렇게 하면 최종 사용자가 유효성 검사를 수행 하기 전에 이러한 사용자 지정에 노출 될 가능성을 줄일 수 있습니다.  
  
## <a name="customizing-the-ad-fs-sign-in-experience-by-using-onloadjs"></a>\-Onload를 사용 하 여 AD FS 로그인 환경 사용자 지정  
AD FS 서비스에 대 한 onload를 사용자 지정할 때 다음 단계를 사용 합니다.  
  
#### <a name="customizing-onloadjs-for-the-ad-fs-service"></a>AD FS 서비스에 대 한 onload 사용자 지정  
  
1.  사용자 지정 논리를 onload에 추가 하려면 먼저 사용자 지정 웹 테마를 만들어야 합니다. Out 제공 되는 테마\-의\-는\-상자 기본 테마 라고 합니다. 기본 테마를 내보내 이를 사용하여 빠르게 시작할 수 있습니다. 다음 cmdlet은 기본 웹 테마를 복제 하는 사용자 지정 웹 테마를 만듭니다.  
  
    ```  
    New-AdfsWebTheme –Name custom –SourceName default  
  
    ```  
  
2.  그런 다음 사용자 지정 또는 기본 웹 테마를 내보내 onload .js 파일을 가져올 수 있습니다. 웹 테마를 내보내려면 다음 cmdlet을 사용 합니다.  
  
    ```  
    Export-AdfsWebTheme –Name default –DirectoryPath c:\theme  
  
    ```  
  
    위의 내보내기 cmdlet에서 지정한 디렉터리의 스크립트 폴더 아래에 있는 onload를 찾고 사용자 지정 논리를 스크립트에 추가 \( 합니다. 아래 예제 섹션의 사용 사례를 참조 하세요 \) .  
  
3.  필요에 따라 onload를 사용자 지정 하기 위해 필요한 수정 작업을 수행 합니다.  
  
4.  수정 된 onload를 사용 하 여 테마를 업데이트 합니다. 다음 cmdlet을 사용 하 여 사용자 지정 웹 테마에 onload 업데이트를 적용 합니다.  

     Windows Server 2012 r 2에 대 한 AD FS:  

    ```  
    Set-AdfsWebTheme -TargetName custom -AdditionalFileResource @{Uri='/adfs/portal/script/onload.js';path="c:\theme\script\onload.js"}  
  
    ```  
    Windows Server 2016에 대 한 AD FS:

     ```  
    Set-AdfsWebTheme -TargetName custom -OnLoadScriptPath "c:\theme\script\onload.js"   
  
    ```  
  
5.  AD FS에 사용자 지정 웹 테마를 적용 하려면 다음 cmdlet을 사용 합니다.  
  
    ```  
    Set-AdfsWebConfig -ActiveThemeName custom  
    ```  
  
## <a name="additional-customization-examples"></a>추가 사용자 지정 예제  
다음은 다른 미세 조정을 위해 onload에 추가 된 사용자 지정 코드의 예입니다. \- 사용자 지정 코드를 추가 하는 경우 항상 사용자 지정 코드를 onload의 맨 아래에 추가 하세요.  
  
### <a name="example-1-change-sign-in-with-organizational-account-string"></a>예 1: "조직 계정으로 로그인" 문자열 변경  
기본 AD FS 폼 \- 기반 로그인 페이지에는 \- 사용자 입력 상자 위의 "조직 계정으로 로그인" 제목이 있습니다.  
  
이 문자열을 사용자 고유의 문자열로 바꾸려는 경우에는 다음 코드를 onload에 추가할 수 있습니다.  
  
```  
// Sample code to change "Sign in with organizational account" string.  
  
// Check whether the loginMessage element is present on this page.  
var loginMessage = document.getElementById('loginMessage');  
if (loginMessage)  
{  
       // loginMessage element is present, modify its properties.  
       loginMessage.innerHTML = 'Your company description text';  
}  
  
```  
  
### <a name="example-2-accept-sam-account-name-as-a-login-format-on-an-ad-fs-form-based-sign-in-page"></a>예 2: \- AD FS 양식 \- 기반 로그인 페이지에서 SAM 계정 이름을 로그인 형식으로 허용 \-  
기본 AD FS 양식 \- 기반 로그인 \- 페이지는 Upn (사용자 계정 이름)의 로그인 \( 형식 \) \( (예: <strong>johndoe@contoso.com</strong> \) 또는 도메인 정규화 된 sam \- 계정 이름 \( **contoso \\ johndoe** 또는 **contoso.com \\ johndoe** \) )을 지원 합니다. 모든 사용자가 동일한 도메인에서 들어오고 sam 계정 이름만 알고 있는 경우 \- 사용자가 sam 계정 이름만 사용 하 여 로그인 할 수 있는 시나리오를 지원할 수 있습니다 \- . 다음 코드를 onload에 추가 하 여이 시나리오를 지원할 수 있습니다. 아래 예제에서 "contoso.com" 도메인을 사용 하려는 도메인으로 바꿉니다.  
  
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
[사용자 로그인 사용자 지정 AD FS](AD-FS-user-sign-in-customization.md)  
  

