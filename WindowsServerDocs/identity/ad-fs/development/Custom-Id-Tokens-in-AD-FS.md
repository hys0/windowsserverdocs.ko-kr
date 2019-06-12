---
title: Ad FS 2016 OpenID Connect 또는 OAuth를 사용 하는 경우 id_token에서 내보낸 이상 이어야 하는 클레임을 사용자 지정
description: AD FS 2016 이상에서 사용자 지정 id 토큰 개념의 기술 개요
author: anandyadavmsft
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.reviewer: anandy
ms.technology: identity-adfs
ms.openlocfilehash: 04573aa13689a0e6744b01a0fbf8b11b622b2706
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445474"
---
# <a name="customize-claims-to-be-emitted-in-idtoken-when-using-openid-connect-or-oauth-with-ad-fs-2016-or-later"></a>Ad FS 2016 OpenID Connect 또는 OAuth를 사용 하는 경우 id_token에서 내보낸 이상 이어야 하는 클레임을 사용자 지정

## <a name="overview"></a>개요
이 문서 [여기](native-client-with-ad-fs.md) 로그온 OpenID Connect에 대 한 AD FS를 사용 하는 앱을 빌드하는 방법을 보여 줍니다. 그러나 기본적으로 가지 고정된 된 집합의 클레임은 id_token에서 사용할 수 있습니다. AD FS 2016 및 이후 릴리스에서 OpenID Connect 시나리오의 id_token을 사용자 지정 하는 기능을 있습니다.

## <a name="when-are-custom-id-token-used"></a>사용자 지정 ID를 때 사용 되는 토큰?
특정 시나리오에서 클라이언트 응용 프로그램 액세스를 시도 하는 리소스 없이 됩니다. 따라서 액세스 토큰이 필요 실제로 하지 않습니다. 이러한 경우 클라이언트 응용 프로그램 에서만 ID 토큰 하지만 기능을 돕는 몇 가지 추가 클레임을 사용 하 여 기본적으로 해야 합니다.

## <a name="what-are-the-restrictions-on-getting-custom-claims-in-id-token"></a>토큰을 가져오는 데 사용자 지정 클레임 id에서에 대 한 제한 이란?

### <a name="scenario-1"></a>시나리오 1

![제한](media/Custom-Id-Tokens-in-AD-FS/res1.png)

1.  response_mode는 form_post로 설정
2.  공용 클라이언트만 수는 사용자 지정 클레임 ID에서 토큰 가져오기
3.  신뢰 당사자 식별자 (Web API 식별자)는 클라이언트 식별자와 동일 해야 합니다.

### <a name="scenario-2"></a>시나리오 2

![제한](media/Custom-Id-Tokens-in-AD-FS/restrict2.png)

사용 하 여 [KB4019472](https://support.microsoft.com/help/4019472/windows-10-update-kb4019472) AD FS 서버에 설치
1.  response_mode는 form_post로 설정
2.  공용 및 기밀 클라이언트 수는 사용자 지정 클레임 ID에서 토큰 가져오기
3.  클라이언트-RP 쌍에 범위 allatclaims를 할당 합니다.
아래 예제에 표시 된 대로 권한 부여 ADFSApplicationPermission cmdlet을 사용 하 여 범위를 할당할 수 있습니다.

``` powershell
Grant-AdfsApplicationPermission -ClientRoleIdentifier "https://my/privateclient" -ServerRoleIdentifier "https://rp/fedpassive" -ScopeNames "allatclaims","openid"
```

## <a name="creating-and-configuring-an-oauth-application-to-handle-custom-claims-in-id-token"></a>만들기 및 ID 토큰의 사용자 지정 클레임을 처리 하는 OAuth 응용 프로그램 구성
만들기 및 사용자 지정 클레임을 사용 하 여 ID 토큰을 수신 하기 위한 AD FS에서 응용 프로그램을 구성 하려면 다음 단계를 수행 합니다.

### <a name="create-and-configure-an-application-group-in-ad-fs-2016-or-later"></a>만들기 및 AD FS 2016 이상에서 응용 프로그램 그룹 구성

1. AD FS 관리에서 응용 프로그램 그룹을 마우스 오른쪽 단추로 클릭 하 고 선택 **응용 프로그램 그룹 추가**합니다.

2. 응용 프로그램 그룹 마법사에서 이름을 입력 **ADFSSSO** 고 클라이언트-서버에서 응용 프로그램을 선택 합니다 **웹 응용 프로그램에 액세스 하는 네이티브 응용 프로그램** 템플릿. **다음**을 클릭합니다.

   ![클라이언트](media/Custom-Id-Tokens-in-AD-FS/clientsnap1.png)

3. 복사는 **클라이언트 식별자** 값입니다.  그는 나중에 값으로 ida: ClientId 응용 프로그램 web.config 파일에 대 한 합니다.

4. 에 다음과 같이 입력 **리디렉션 URI:**  -  **https://localhost:44320/** 합니다.  **추가**를 클릭합니다. **다음**을 클릭합니다.

   ![클라이언트](media/Custom-Id-Tokens-in-AD-FS/clientsnap2.png)

5. 에 **Web API 구성** 화면에서 입력 한 다음 **식별자** -  **https://contoso.com/WebApp** 합니다.  **추가**를 클릭합니다. **다음**을 클릭합니다.  이 값은 나중에 사용할 **ida: ResourceID** 응용 프로그램 web.config 파일에서입니다.

   ![클라이언트](media/Custom-Id-Tokens-in-AD-FS/clientsnap3.png)

6. 에 **액세스 제어 정책 선택** 화면에서 **모든 사용자 허용** 클릭 **다음**합니다.

   ![클라이언트](media/Custom-Id-Tokens-in-AD-FS/clientsnap4.png)

7. 에 **응용 프로그램 사용 권한 구성** 화면, 반드시 **openid** 하 고 **allatclaims** 선택 하 고 클릭 **다음**합니다.

   ![클라이언트](media/Custom-Id-Tokens-in-AD-FS/clientsnap5.png)

8. 에 **요약** 화면에서 **다음**합니다.  

   ![클라이언트](media/Custom-Id-Tokens-in-AD-FS/clientsnap6.png)

9. 에 **Complete** 화면에서 **닫기**합니다.

10. AD FS 관리에서 모든 응용 프로그램 그룹의 목록을 가져오려면 응용 프로그램 그룹을 클릭 합니다. 마우스 오른쪽 단추로 클릭 **ADFSSSO** 선택한 **속성**합니다. 선택 **ADFSSSO-Web API** 를 클릭 하 고 **편집...**

    ![클라이언트](media/Custom-Id-Tokens-in-AD-FS/clientsnap7.png)

11. 온 **ADFSSSO-웹 API 속성** 화면에서 **발급 변환 규칙** 탭을 클릭 **규칙 추가...**

    ![클라이언트](media/Custom-Id-Tokens-in-AD-FS/clientsnap8.png)

12. 온 **변환 클레임 규칙 추가 마법사** 화면에서 **사용자 지정 규칙을 사용 하 여 클레임 보내기** 드롭다운 목록에서 클릭 하 고 **다음**

    ![클라이언트](media/Custom-Id-Tokens-in-AD-FS/clientsnap9.png)

13. 온 **변환 클레임 규칙 추가 마법사** 화면에서 입력 **ForCustomIDToken** 에서 **클레임 규칙 이름** 다음 클레임에 대 한 규칙 및 **사용자 지정 규칙**. **마침** 클릭

    ```  
    x:[]
    => issue(claim=x);  
    ```

    ![클라이언트](media/Custom-Id-Tokens-in-AD-FS/clientsnap10.png)

```

>[!NOTE]
>You can also use PowerShell to assign the allatclaims and openid scopes
>``` powershell
Grant-AdfsApplicationPermission -ClientRoleIdentifier "[Client ID from #3 above]" -ServerRoleIdentifier "[Identifier from #5 above]" -ScopeNames "allatclaims","openid"
```

### <a name="download-and-modify-the-sample-application-to-emit-custom-claims-in-idtoken"></a>다운로드 하 고 id_token의 사용자 지정 클레임을 내보낼 샘플 응용 프로그램 수정

이 섹션에서는 샘플 웹 앱을 다운로드 하 고 Visual Studio에서 수정 하는 방법을 설명 합니다.   Azure AD 된 샘플을 사용 합니다 [여기](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)합니다.  

샘플 프로젝트를 다운로드 하려면 Git Bash를 사용 하 고 다음을 입력 합니다.  

```  
git clone https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect  
```  

![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_1.PNG)

#### <a name="to-modify-the-app"></a>응용 프로그램을 수정 하려면

1.  Visual Studio를 사용 하 여 샘플을 엽니다.  

2.  모든 누락 된 Nuget 복원 되도록 앱을 다시 작성 합니다.  

3.  Web.config 파일을 엽니다.  모양은 다음 하므로 다음 값을 수정 합니다.  

    ```  
    <add key="ida:ClientId" value="[Replace this Client Id from #3 above under section Create and configure an Application Group in AD FS 2016 or later]" />  
    <add key="ida:ResourceID" value="[Replace this with the Web API Identifier from #5 above]"  />
    <add key="ida:ADFSDiscoveryDoc" value="https://[Your ADFS hostname]/adfs/.well-known/openid-configuration" />  
    <!--<add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" />      
    <add key="ida:AADInstance" value="https://login.microsoftonline.com/{0}" />-->  
    <add key="ida:PostLogoutRedirectUri" value="[Replace this with the Redirect URI from #4 above]" />  
    ```  

    ![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_2.PNG)  

4.  Startup.Auth.cs 파일을 열고 다음과 같이 변경 합니다.  

    -   다음 변경 내용으로 OpenId Connect 미들웨어 초기화 논리를 조정 합니다.  

        ```  
        private static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];  
        //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];  
        //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];  
        private static string metadataAddress = ConfigurationManager.AppSettings["ida:ADFSDiscoveryDoc"];
        private static string resourceId = ConfigurationManager.AppSettings["ida:ResourceID"];
        private static string postLogoutRedirectUri = ConfigurationManager.AppSettings["ida:PostLogoutRedirectUri"];  
        ```  

    -   다음 주석 처리 합니다.  

            ```  
            //string Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);  
            ```

          ![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_3.PNG)

    -   추가로, 다음과 같이 OpenId Connect 미들웨어 옵션을 수정 합니다.  

        ```  
        app.UseOpenIdConnectAuthentication(  
            new OpenIdConnectAuthenticationOptions  
            {  
                ClientId = clientId,  
                //Authority = authority,  
                Resource = resourceId,
                MetadataAddress = metadataAddress,  
                PostLogoutRedirectUri = postLogoutRedirectUri,
                RedirectUri = postLogoutRedirectUri
        ```  

        ![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_4.PNG)

5.  HomeController.cs 파일을 열고 다음과 같이 변경 합니다.  

    -   다음을 추가합니다.  

            ```  
            using System.Security.Claims;  
            ```

    -   아래와 같이 about () 메서드를 업데이트 합니다.  

        ```  
        [Authorize]
        public ActionResult About()
        {
            ClaimsPrincipal cp = ClaimsPrincipal.Current;
            string userName = cp.FindFirst(ClaimTypes.WindowsAccountName).Value;
            ViewBag.Message = String.Format("Hello {0}!", userName);
            return View();
        }
        ```  

        ![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_5.PNG)

### <a name="test-the-custom-claims-in-id-token"></a>ID 토큰에서 사용자 지정 클레임을 테스트 합니다.

내용이 변경 되 면 f5 키를 누릅니다. 이 샘플 페이지를 표시 합니다. 로그인을 클릭 합니다.

![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_6.PNG)

AD FS 로그인 페이지로 리디렉션될 수 있습니다. 계속 해 서 로그인 합니다.

![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_7.PNG)

이 작업이 성공 되 면 이제으로 로그인 됩니다 표시 됩니다.

![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_8.PNG)

링크에 대 한 클릭 합니다. ID 토큰의 사용자 이름 클레임에서 검색 되는 Hello [Username]이 표시 됩니다.

![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_9.PNG)

## <a name="next-steps"></a>다음 단계
[AD FS 개발](../../ad-fs/AD-FS-Development.md)  
