---
ms.assetid: d282bb4e-38a0-4c7c-83d8-f6ea89278057
title: AD FS 2016 이상에서 Openid connect Connect를 사용 하 여 웹 응용 프로그램 빌드
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 49d952a49cf474708f57a0ae2a7760d2470af607
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857496"
---
# <a name="build-a-web-application-using-openid-connect-with-ad-fs-2016-and-later"></a>AD FS 2016 이상에서 Openid connect Connect를 사용 하 여 웹 응용 프로그램 빌드

## <a name="pre-requisites"></a>필수 구성 요소  
이 문서를 완료 하기 전에 필요한 필수 구성 요소 목록은 다음과 같습니다. 이 문서는 AD FS 설치 되어 있고 AD FS 팜에 만들어진 가정 합니다.  

-   GitHub 클라이언트 도구  

-   AD FS Windows Server 2016 t p 4 이상  

-   Visual Studio 2013 이상입니다.  

## <a name="create-an-application-group-in-ad-fs-2016-and-later"></a>AD FS 2016 이상에서 응용 프로그램 그룹 만들기
다음 섹션에서는 AD FS 2016 이상에서 응용 프로그램 그룹을 구성 하는 방법을 설명 합니다.  

#### <a name="create-application-group"></a>응용 프로그램 그룹 만들기  

1.  AD FS 관리에서 응용 프로그램 그룹을 마우스 오른쪽 단추로 클릭 하 고 선택 **응용 프로그램 그룹 추가**합니다.  

2.  응용 프로그램 그룹 마법사에서 이름에 **ADFSSSO** 를 입력 하 고 **클라이언트-서버 응용 프로그램** 에서 웹 **응용 프로그램 템플릿에 액세스 하는 웹 브라우저** 를 선택 합니다.  **다음**을 클릭합니다.

    ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_1.PNG)  

3.  복사는 **클라이언트 식별자** 값입니다.  그는 나중에 값으로 ida: ClientId 애플리케이션 web.config 파일에 대 한 합니다.  

4.  **리디렉션 URI:**  -  **https://localhost:44320/** 에 대해 다음을 입력 합니다.  **추가**를 클릭합니다. **다음**을 클릭합니다.  

    ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_2.PNG)  

5.  에 **요약** 화면에서 **다음**합니다.  

    ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_3.PNG)

6.  에 **Complete** 화면에서 **닫기**합니다.  

## <a name="download-and-modify-sample-application-to-authenticate-via-openid-connect-and-ad-fs"></a>Openid connect Connect 및 AD FS를 통해 인증 하기 위한 샘플 응용 프로그램 다운로드 및 수정  
이 섹션에서는 샘플 웹 앱을 다운로드 하 고 Visual Studio에서 수정 하는 방법을 설명 합니다.   Azure AD 된 샘플을 사용 합니다 [여기](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)합니다.  

샘플 프로젝트를 다운로드 하려면 Git Bash를 사용 하 고 다음을 입력 합니다.  

```  
git clone https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect  
```  

![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_8.PNG)  

#### <a name="to-modify-the-app"></a>응용 프로그램을 수정 하려면  

1.  Visual Studio를 사용 하 여 샘플을 엽니다.  

2.  누락 된 Nuget가 모두 복원 되도록 앱을 다시 빌드합니다.  

3.  Web.config 파일을 엽니다.  모양은 다음 하므로 다음 값을 수정 합니다.  

    ```  
    <add key="ida:ClientId" value="[Replace this Client Id from #3 in above section]" />  
    <add key="ida:ADFSDiscoveryDoc" value="https://[Your ADFS hostname]/adfs/.well-known/openid-configuration" />  
    <!--<add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" />      
    <add key="ida:AADInstance" value="https://login.microsoftonline.com/{0}" />-->  
    <add key="ida:PostLogoutRedirectUri" value="[Replace this with Redirect URI from #4 in the above section]" />  
    ```  

    ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_9.PNG)  

4.  Startup.Auth.cs 파일을 열고 다음과 같이 변경 합니다.  

    -   다음 주석 처리 합니다.  

        ```  
        //string Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);  
        ```  

    -   다음 변경 내용으로 OpenId Connect 미들웨어 초기화 논리를 조정 합니다.  

        ```  
        private static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];  
        //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];  
        //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];  
        private static string metadataAddress = ConfigurationManager.AppSettings["ida:ADFSDiscoveryDoc"];  
        private static string postLogoutRedirectUri = ConfigurationManager.AppSettings["ida:PostLogoutRedirectUri"];  
        ```  

        ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_10.PNG)  

    -   아래와 같이 Openid connect Connect 미들웨어 옵션을 수정 합니다.  

        ```  
        app.UseOpenIdConnectAuthentication(  
            new OpenIdConnectAuthenticationOptions  
            {  
                ClientId = clientId,  
                //Authority = authority,  
                MetadataAddress = metadataAddress,  
                PostLogoutRedirectUri = postLogoutRedirectUri,
                RedirectUri = postLogoutRedirectUri
        ```  

        ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_11.PNG)  

        위의 변경 하 여 다음 수행 하는 합니다.  

        -   신뢰할 수 있는 발급자에 대 한 데이터를 전달 하기 위한 권한을 사용 하는 대신 MetadataAddress를 통해 직접 검색 문서 위치를 지정 합니다.  

        -   Azure AD는 요청에 redirect_uri의 존재를 적용 하지 않는 않지만 ADFS 합니다. 따라서 먼저 여기에 추가 하려면  

## <a name="verify-the-app-is-working"></a>앱이 작동 확인  
내용이 변경 되 면 f5 키를 누릅니다.  이 샘플 페이지를 표시 합니다.  로그인을 클릭 합니다.  

![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_12.PNG)  

AD FS 로그인 페이지로 리디렉션될 수 있습니다.  계속 해 서 로그인 합니다.  

![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_13.PNG)  

이 작업이 성공 되 면 이제으로 로그인 됩니다 표시 됩니다.  

![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_14.PNG)  

## <a name="next-steps"></a>다음 단계
[AD FS 개발](../../ad-fs/AD-FS-Development.md)  
