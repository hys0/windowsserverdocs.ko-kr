---
title: Openid connect Connect 또는 OAuth with AD FS 2016 이상을 사용할 때 id_token에서 내보낼 클레임 사용자 지정
description: AD FS 2016 이상에서 사용자 지정 id 토큰 개념의 기술 개요
author: anandyadavmsft
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server
ms.reviewer: anandy
ms.technology: identity-adfs
ms.openlocfilehash: 88ae6837872c5a6cf6bb1d8533a0aa14b82ca573
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358912"
---
# <a name="customize-claims-to-be-emitted-in-id_token-when-using-openid-connect-or-oauth-with-ad-fs-2016-or-later"></a>Openid connect Connect 또는 OAuth with AD FS 2016 이상을 사용할 때 id_token에서 내보낼 클레임 사용자 지정

## <a name="overview"></a>개요
이 문서에서는 Openid connect Connect 로그온을 위해 AD FS를 사용 하는 앱을 빌드하 [는 방법을 보여](native-client-with-ad-fs.md) 줍니다. 그러나 id_token에서는 기본적으로 고정 된 클레임 집합만 사용할 수 있습니다. AD FS 2016 이상 릴리스에는 Openid connect Connect 시나리오에서 id_token을 사용자 지정 하는 기능이 있습니다.

## <a name="when-are-custom-id-token-used"></a>사용자 지정 ID 토큰이 사용 되는 경우
특정 시나리오에서는 클라이언트 응용 프로그램에 액세스를 시도 하는 리소스가 없을 수 있습니다. 따라서 액세스 토큰이 정말로 필요 하지 않습니다. 이러한 경우 클라이언트 응용 프로그램은 기본적으로 ID 토큰만 필요 하지만 기능에 도움이 되는 몇 가지 추가 클레임이 필요 합니다.

## <a name="what-are-the-restrictions-on-getting-custom-claims-in-id-token"></a>ID 토큰의 사용자 지정 클레임 가져오기에 대 한 제한 사항은 무엇 인가요?

### <a name="scenario-1"></a>시나리오 1

![제한](media/Custom-Id-Tokens-in-AD-FS/res1.png)

1.  response_mode는 form_post로 설정 됩니다.
2.  공용 클라이언트만 ID 토큰에서 사용자 지정 클레임을 가져올 수 있습니다.
3.  신뢰 당사자 식별자 (웹 API 식별자)는 클라이언트 식별자와 동일 해야 합니다.

### <a name="scenario-2"></a>시나리오 2

![제한](media/Custom-Id-Tokens-in-AD-FS/restrict2.png)

AD FS 서버에 설치 된 [KB4019472](https://support.microsoft.com/help/4019472/windows-10-update-kb4019472)
1.  response_mode는 form_post로 설정 됩니다.
2.  공용 및 기밀 클라이언트는 모두 ID 토큰에서 사용자 지정 클레임을 가져올 수 있습니다.
3.  클라이언트에 범위 allatclaims 할당-RP 쌍.
아래 예제에 표시 된 것 처럼 ADFSApplicationPermission cmdlet을 사용 하 여 범위를 할당할 수 있습니다.

``` powershell
Grant-AdfsApplicationPermission -ClientRoleIdentifier "https://my/privateclient" -ServerRoleIdentifier "https://rp/fedpassive" -ScopeNames "allatclaims","openid"
```

## <a name="creating-and-configuring-an-oauth-application-to-handle-custom-claims-in-id-token"></a>ID 토큰에서 사용자 지정 클레임을 처리 하는 OAuth 응용 프로그램 만들기 및 구성
사용자 지정 클레임을 사용 하 여 ID 토큰을 수신 하기 위해 AD FS에서 응용 프로그램을 만들고 구성 하려면 다음 단계를 수행 합니다.

### <a name="create-and-configure-an-application-group-in-ad-fs-2016-or-later"></a>AD FS 2016 이상에서 응용 프로그램 그룹 만들기 및 구성

1. AD FS 관리에서 응용 프로그램 그룹을 마우스 오른쪽 단추로 클릭 하 고 선택 **응용 프로그램 그룹 추가**합니다.

2. 응용 프로그램 그룹 마법사에서 이름에 **ADFSSSO** 를 입력 하 고 클라이언트-서버 응용 프로그램에서 **웹 응용 프로그램 템플릿에 액세스 하는 네이티브 응용 프로그램** 을 선택 합니다. **다음**을 클릭합니다.

   ![클라이언트](media/Custom-Id-Tokens-in-AD-FS/clientsnap1.png)

3. 복사는 **클라이언트 식별자** 값입니다.  그는 나중에 값으로 ida: ClientId 응용 프로그램 web.config 파일에 대 한 합니다.

4. **리디렉션 URI** - **에대해다음을입력합니다. https://localhost:44320/**  **추가**를 클릭합니다. **다음**을 클릭합니다.

   ![클라이언트](media/Custom-Id-Tokens-in-AD-FS/clientsnap2.png)

5. **웹 API 구성** 화면에서 **https://contoso.com/WebApp** **식별자** -  에 대해 다음을 입력 합니다.  **추가**를 클릭합니다. **다음**을 클릭합니다.  이 값은 나중에 응용 프로그램 web.config 파일에서 **ida: ResourceID** 에 사용 됩니다.

   ![클라이언트](media/Custom-Id-Tokens-in-AD-FS/clientsnap3.png)

6. 에 **액세스 제어 정책 선택** 화면에서 **모든 사용자 허용** 클릭 **다음**합니다.

   ![클라이언트](media/Custom-Id-Tokens-in-AD-FS/clientsnap4.png)

7. **응용 프로그램 사용 권한 구성** 화면에서 **openid connect** 및 **allatclaims** 선택 되어 있는지 확인 하 고 **다음**을 클릭 합니다.

   ![클라이언트](media/Custom-Id-Tokens-in-AD-FS/clientsnap5.png)

8. 에 **요약** 화면에서 **다음**합니다.  

   ![클라이언트](media/Custom-Id-Tokens-in-AD-FS/clientsnap6.png)

9. 에 **Complete** 화면에서 **닫기**합니다.

10. AD FS 관리에서 응용 프로그램 그룹을 클릭 하 여 모든 응용 프로그램 그룹 목록을 가져옵니다. **ADFSSSO** 를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다. **ADFSSSO-WEB API** 를 선택 하 고 **편집 ...** 을 클릭 합니다.

    ![클라이언트](media/Custom-Id-Tokens-in-AD-FS/clientsnap7.png)

11. **ADFSSSO-WEB API 속성** 화면에서 **발급 변환 규칙** 탭을 선택 하 고 **규칙 추가** ...를 클릭 합니다.

    ![클라이언트](media/Custom-Id-Tokens-in-AD-FS/clientsnap8.png)

12. **변환 클레임 규칙 추가 마법사** 화면에서 드롭다운에서 **사용자 지정 규칙을 사용 하 여 클레임 보내기** 를 선택 하 고 **다음** 을 클릭 합니다.

    ![클라이언트](media/Custom-Id-Tokens-in-AD-FS/clientsnap9.png)

13. **변환 클레임 규칙 추가 마법사** 화면에서 **클레임 규칙 이름** 에 **ForCustomIDToken** 를 입력 하 고 **사용자 지정 규칙**에 다음 클레임 규칙을 입력 합니다. **마침** 클릭

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

### <a name="download-and-modify-the-sample-application-to-emit-custom-claims-in-id_token"></a>Id_token에서 사용자 지정 클레임을 내보내는 샘플 응용 프로그램 다운로드 및 수정

이 섹션에서는 샘플 웹 앱을 다운로드 하 고 Visual Studio에서 수정 하는 방법을 설명 합니다.   Azure AD 된 샘플을 사용 합니다 [여기](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)합니다.  

샘플 프로젝트를 다운로드 하려면 Git Bash를 사용 하 고 다음을 입력 합니다.  

```  
git clone https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect  
```  

![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_1.PNG)

#### <a name="to-modify-the-app"></a>응용 프로그램을 수정 하려면

1.  Visual Studio를 사용 하 여 샘플을 엽니다.  

2.  누락 된 Nuget가 모두 복원 되도록 앱을 다시 빌드합니다.  

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

    -   아래와 같이 Openid connect Connect 미들웨어 옵션을 수정 합니다.  

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

    -   아래와 같이 About () 메서드를 업데이트 합니다.  

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

### <a name="test-the-custom-claims-in-id-token"></a>ID 토큰에서 사용자 지정 클레임 테스트

내용이 변경 되 면 f5 키를 누릅니다. 이 샘플 페이지를 표시 합니다. 로그인을 클릭 합니다.

![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_6.PNG)

AD FS 로그인 페이지로 리디렉션될 수 있습니다. 계속 해 서 로그인 합니다.

![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_7.PNG)

이 작업이 성공 되 면 이제으로 로그인 됩니다 표시 됩니다.

![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_8.PNG)

정보 링크를 클릭 합니다. ID 토큰의 사용자 이름 클레임에서 검색 된 Hello [사용자 이름]이 표시 됩니다.

![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_9.PNG)

## <a name="next-steps"></a>다음 단계
[AD FS 개발](../../ad-fs/AD-FS-Development.md)  
