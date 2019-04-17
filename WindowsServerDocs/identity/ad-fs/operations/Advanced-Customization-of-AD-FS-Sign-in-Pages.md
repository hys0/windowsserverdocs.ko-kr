---
ms.assetid: 882abec8-0189-4f73-99c5-792987168080
title: "고급 사용자 지정 AD FS 로그인 페이지"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/13/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: ea01d0ff2a38c4fef2f68091608d777d8412e91b
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="advanced-customization-of-ad-fs-sign-in-pages"></a>고급 사용자 지정 AD FS 로그인 페이지

>적용 대상: Windows Server 2016, Windows Server 2012 r 2
  
## <a name="advanced-customization-of-ad-fs-sign-in-pages"></a>페이지에서 FS Sign\ AD 고급 사용자 지정  
Windows Server 2012 r 2에서 ADFS sign\에서 환경 사용자 지정 built\에서 지원을 제공 합니다. 대부분의 이러한 시나리오에 대 한 built\에서 Windows PowerShell cmdlet 필요한 모든 됩니다.  Adfs의 sign\ 환경을 가능할 때마다 표준 요소를 사용자 지정할 built\에서 Windows PowerShell 명령을 사용 하는 것이 좋습니다.  참조 [-ADFS 사용자 지정 로그인](AD-FS-user-sign-in-customization.md) 에 대 한 자세한 내용은 합니다.  
  
일부 경우에 ADFS 관리자를 통해 Adfs와 in\ 기본 제공 되는 기존 PowerShell 명령을 가능 하지 않은 추가 sign\-환경을 제공 하기 위해 할 수 있습니다. 경우에서 가능는 \ (내에서 제공 되는 지침 below\) 환경을 사용자 지정할 sign\에 추가 하는 논리가 추가 추가 하 여 관리자 **onload.js** Adfs에서 제공 하 고 모든 ADFS 페이지에서 실행 됩니다.  
  
## <a name="things-to-know-before-you-start"></a>시작 하기 전에 알아야 할 사항  
  
-   이동 흐름 영향을 주는 또는 함께 작동 ADFS 프로토콜 매개 변수를 수정 하는 모든 변경 지원 되지 않습니다.
  
-   기본 웹 테마와 함께 제공 된 기존 onload.js 다른 폼 요소에 대 한 페이지가 렌더링 처리 하는 코드 포함 되어 있습니다. 하지 원래 onload.js 내용을 수정 있지만 사용자 지정 논리를 처리 하는 기존 onload.js에 코드를 추가 하는 것이 좋습니다.  
  
-   ADFS 기본 라고 하는 웹에서 built\ 테마 함께 제공 됩니다. 기본 웹 테마 onload.js를 수정할 수 없습니다. Onload.js를 업데이트 하려면 만들고 테마를 사용자 지정 웹 페이지에서 sign\ Adfs에 대 한 사용 해야 합니다.  참조 [-ADFS 사용자 지정 로그인](AD-FS-user-sign-in-customization.md) 사용자 지정 웹 테마를 만드는 방법에 대 한 정보입니다.  
  
-   동일한 onload.js 모든 ADFS 페이지 \(ex.에서 실행 될 로그온 form\ 기반 페이지, 홈 영역 검색 페이지 및 등. \). 코드가 스크립트에만 가져옵니다 실행 하도록 설계 되어 있으며 예기치 않게 실행 되지 않는 있는지 확인 해야 합니다.  
  
-   HTML 요소를 참조 하는 경우 확인 하는 항상 요소 작업을 수행 하기 전에 요소 있는지 확인 합니다. 안정성을 제공 하 고 사용자 지정 하는 논리가이 요소 포함 되지 않은 페이지에서 실행 되지 것입니다. 간단 하 게 HTML 소스 기존 요소 보려면 ADFS sign\에 페이지에서 볼 수 있습니다.  
  
-   암호 확인용 환경에서 사용자 지정을 확인 하 고 롤링 테스트해 프로덕션에 ADFS 서버 전에 테스트 하는 것이 좋습니다. 최종 사용자가 이러한 사용자 지정 전에 유효성 검사에 노출 될 가능성이 줄입니다.  
  
## <a name="customizing-the-ad-fs-sign-in-experience-by-using-onloadjs"></a>Adfs의 sign\ 환경을 onload.js를 사용 하 여 사용자 지정  
ADFS 서비스에 대 한 onload.js 사용자 지정 하는 경우 다음 단계를 사용 합니다.  
  
#### <a name="customizing-onloadjs-for-the-ad-fs-service"></a>ADFS 서비스에 대 한 onload.js 사용자 지정  
  
1.  사용자 지정 논리 onload.js을 추가 하려면 먼저 사용자 지정 웹 테마를 만들 수 있어야 합니다. 출시 out\ of\-the\-기본이 테마 기본을 라고 합니다. 기본 테마 내보낸 빠르게 시작할 수 있도록 사용할 수 있습니다. 다음 cmdlet 중복 기본 웹 테마 지정 웹 테마를 만듭니다.  
  
    ```  
    New-AdfsWebTheme –Name custom –SourceName default  
  
    ```  
  
2.  그런 다음 사용자 지정 내보내거나 기본 웹 테마로 onload.js 파일을 가져올 수 있습니다. 웹 테마를 내보내려면 다음 cmdlet 사용:  
  
    ```  
    Export-AdfsWebTheme –Name default –DirectoryPath c:\theme  
  
    ```  
  
    있습니다 onload.js 스크립트 폴더 디렉터리에 위의 내보내기 cmdlet에 지정 하 고 사용자 지정 논리 스크립트 추가 \ (참조 경우 예제 섹션 below\에서 사용).  
  
3.  필요에 따라 onload.js 사용자 지정 하는 데 필요한를 수정 합니다.  
  
4.  테마 수정된 onload.js로 업데이트 합니다. 다음 cmdlet를 사용 하 여 업데이트 onload.js 사용자 지정 웹 테마를 적용할 수 있습니다.  
  
    ```  
    Set-AdfsWebTheme -TargetName custom -AdditionalFileResource @{Uri=’/adfs/portal/script/onload.js’;path="c:\theme\script\onload.js"}  
  
    ```  
  
5.  사용자 지정 웹 테마 Adfs를 적용 하려면 다음 cmdlet 사용:  
  
    ```  
    Set-AdfsWebConfig -ActiveThemeName custom  
    ```  
  
## <a name="additional-customization-examples"></a>사용자 지정 추가적인 예시  
다른 fine\ 목소리 목적을 위해 onload.js에 추가한 사용자 지정 코드의 예는 다음과 같습니다. 사용자 지정 코드를 추가할 때 하세요 항상 추가 사용자 지정 코드는 onload.js 맨 아래에 있습니다.  
  
### <a name="example-1-change-sign-in-with-organizational-account-string"></a>예제 1: "조직 계정으로 로그인" 문자열 변경  
광고 기본 FS form\ 기반 sign\에 페이지에 "조직 계정으로 로그인"의 제목 사용자 입력 상자 위에서 합니다.  
  
이 문자열 문자열을 직접으로 대체 하려는 경우 다음 코드 onload.js에 추가할 수 있습니다.  
  
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
  
### <a name="example-2-accept-sam-account-name-as-a-login-format-on-an-ad-fs-form-based-sign-in-page"></a>예제 2: ADFS form\ 기반 sign\에서 페이지에 로그인 형식으로 SAM\ 계정 이름에 동의  
사용자 계정 이름을 \(UPNs\) \(for example, ** johndoe@contoso.com **\) 또는 도메인 ADFS 페이지에서 sign\ form\ 기반 지원 로그인 형식 기본 된 sam\ 계정 이름 \ (**contoso\\johndoe** 또는 **contoso.com\\johndoe**\). 동일한 도메인 모든 사용자에 게 제공 하 고 sam\ 계정 이름에 대해 알고 있더라도, sam\ 계정 이름만 사용에 사용자가 로그인 할 수 시나리오를 지원 수도 있습니다. 다음 코드가이 시나리오를 지원,만 도메인을 사용 하는 도메인 "contoso.com" 예제에서 아래 바꿉니다 onload.js를 추가할 수 있습니다.  
  
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
[광고 FS 사용자 지정 로그인](AD-FS-user-sign-in-customization.md)  
  

