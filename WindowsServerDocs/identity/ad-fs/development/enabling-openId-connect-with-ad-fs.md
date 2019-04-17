---
ms.assetid: d282bb4e-38a0-4c7c-83d8-f6ea89278057
title: "빌드 FS 2016 ad OpenID 연결을 사용 하는 웹 응용 프로그램"
description: 
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f8040b19576ac9de4ced43e6313cad69276a3d27
ms.sourcegitcommit: c16a2bf1b8a48ff267e71ff29f18b5e5cda003e8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/28/2018
---
# <a name="build-a-web-application-using-openid-connect-with-ad-fs-2016"></a>빌드 FS 2016 ad OpenID 연결을 사용 하는 웹 응용 프로그램

>Windows Server 2016 적용 됩니다.

Windows Server 2012 r 2에서 Adfs의 초기 Oauth 지원의 개발 FS 2016 광고는 OpenId 연결 로그온 사용에 대 한 지원이 소개 합니다.  
  
## <a name="pre-requisites"></a>필수  
이 문서를 완료 하기 전에 필요한 필수 목록은 다음과 같습니다. 이 문서도 간주 ADFS 설치가 완료 된 후 ADFS 농장 만들었습니다.  
  
-   (무료 평가판 괜찮습니다)는 Azure AD 구독  
  
-   GitHub 클라이언트 도구  
  
-   Windows Server 2016 t p 4 이상 ADFS  
  
-   Visual Studio 2013 이상 합니다.  
  
## <a name="create-an-application-group-in-ad-fs-2016"></a>Adfs 2016 응용 프로그램 그룹 만들기  
다음 광고 FS 2016에 응용 프로그램 그룹 구성 하는 방법을 설명 합니다.  
  
#### <a name="create-application-group"></a>응용 프로그램 그룹 만들기  
  
1.  AD FS 관리에 응용 프로그램 그룹에서 마우스 오른쪽 단추로 클릭 한 다음 **응용 프로그램 그룹 추가**합니다.  
  
2.  응용 프로그램 그룹 마법사에서 이름을 입력 **ADFSSSO** 고 **독립 실행형 응용 프로그램**선택는 **서버 응용 프로그램 또는 웹 사이트** 서식 합니다.  클릭 **다음**합니다.  
  
    ![광고 FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_1.PNG)  
  
3.  복사는 **클라이언트 식별자** 값 합니다.  그 나중에 값으로에 사용할 ida: ClientId 응용 프로그램 토큰과에 있습니다.  
  
4.  입력에 대 한 다음 **리디렉션합니다 URI:** - **https://localhost:44320/**합니다.  클릭 **추가**합니다. 클릭 **다음**합니다.  
  
    ![광고 FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_2.PNG)  
  
5.  에 **응용 프로그램 자격 증명 구성** 화면에서의 확인란을 선택 **공유 암호를 생성** 비밀 복사 하 고 있습니다. 클릭 **다음**  
  
    ![광고 FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_3.PNG)  
  
6.  에 **요약** 화면에서 클릭 **다음**합니다.  
  
7.  에 **Complete** 화면에서 클릭 **닫기**합니다.  
  
8.  지금 마우스 오른쪽 단추로 클릭 새 응용 프로그램 그룹에서 선택한 **속성**합니다.  
  
9. 에 **ADFSSSO 속성** 클릭 **응용 프로그램 추가**합니다.  
  
10. 에 **샘플 응용 프로그램의 응용 프로그램 새로 추가** 선택 **웹 API** 클릭 **다음**합니다.  
  
    ![광고 FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_4.PNG)  
  
11. 에 **구성 웹 API** 화면에서 대 한 다음 입력 **식별자** - **https://contoso.com/WebApp**합니다.  클릭 **추가**합니다. 클릭 **다음**합니다.  
  
    ![광고 FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_7.PNG)  
  
12. 에 **액세스 제어 정책 선택** 화면에서 **모든 허용** 클릭 **다음**합니다.  
  
    ![광고 FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_Confidential_7.PNG)  
  
13. 에 **응용 프로그램 사용 권한 구성** 화면에서 확인 **openid** 을 선택 하 고 클릭 **다음**합니다.  
  
    ![광고 FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_7.PNG)  
  
14. 에 **요약** 화면에서 클릭 **다음**합니다.  
  
15. 에 **Complete** 화면에서 클릭 **닫기**합니다.  
  
16. 에 **샘플 응용 프로그램 속성** 클릭 **확인**합니다.  
  
## <a name="download-and-modify-mvp-app-to-authenticate-via-openid-connect-and-ad-fs"></a>다운로드 및 MVP 앱을 통해 OpenId 인증 수정 연결 및 ADFS  
이 여기서 샘플 웹 API를 다운로드 하 고 Visual Studio에서 수정 하는 방법을 설명 합니다.   Azure AD 샘플을 사용 했습니다 [여기](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)합니다.  
  
샘플 프로젝트를 다운로드 하려면 Git Bash를 사용 하 고 다음을 입력 합니다.  
  
```  
git clone https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect  
```  
  
![광고 FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_8.PNG)  
  
#### <a name="to-modify-the-app"></a>앱을 수정 하려면  
  
1.  Visual Studio를 사용 하 여 샘플을 엽니다.  
  
2.  복원 모든 누락 NuGets 되도록 앱을 컴파일할 합니다.  
  
3.  토큰과를 엽니다.  다음과 같은 모양 되므로 다음 값 수정 다음과 같습니다.  
  
    ```  
    <add key="ida:ClientId" value="8219ab4a-df10-4fbd-b95a-8b53c1d8669e" />  
    <add key="ida:ADFSDiscoveryDoc" value="https://adfs.contoso.com/adfs/.well-known/openid-configuration" />  
    <!--<add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" />      
    <add key="ida:ResourceID" value="https://contoso.com/WebApp"  
    <add key="ida:AADInstance" value="https://login.microsoftonline.com/{0}" />-->  
    <add key="ida:PostLogoutRedirectUri" value="https://localhost:44320/" />  
    ```  
  
    ![광고 FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_9.PNG)  
  
4.  Startup.Auth.cs 파일을 열고 다음과 같은 변경 합니다.  
  
    -   다음 의견을 다음과 같습니다.  
  
        ```  
        //public static readonly string Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);  
        ```  
  
    -   다음과 같은 변경 OpenId 연결 미들웨어 초기화 논리를 조정 합니다.  
  
        ```  
        private static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];  
        //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];  
        //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];  
        private static string metadataAddress = ConfigurationManager.AppSettings["ida:ADFSDiscoveryDoc"];  
        private static string postLogoutRedirectUri = ConfigurationManager.AppSettings["ida:PostLogoutRedirectUri"];  
        ```  
  
        ![광고 FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_10.PNG)  
  
    -   멀리 아래쪽, 수정, OpenId 연결 미들웨어 옵션은 다음과 같이 합니다.  
  
        ```  
        app.UseOpenIdConnectAuthentication(  
            new OpenIdConnectAuthenticationOptions  
            {  
                ClientId = clientId,  
                //Authority = authority,  
                MetadataAddress = metadataAddress,  
                RedirectUri = postLogoutRedirectUri,  
                PostLogoutRedirectUri = postLogoutRedirectUri 
        ```  
  
        ![광고 FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_11.PNG)  
  
        위의 변경 하 여 다음 수행 하는 다음과 같습니다.  
  
        -   직접 MetadataAddress 통해 검색 문서 위치를 지정 했습니다 권한을 통신 신뢰할 수 있는 발행인이 대 한 데이터를 사용 하지 않고  
  
        -   Azure AD 요청을 redirect_uri의 존재를 적용 하지 하지만 ADFS 않습니다. 따라서 먼저 여기에 추가 하려면  
  
## <a name="verify-the-app-is-working"></a>앱 작동 하는지 확인  
위의 변경 나면 f5 키를 누릅니다.  이러한 샘플 페이지를 표시 합니다.  로그인을 클릭 합니다.  
  
![광고 FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_12.PNG)  
  
ADFS 로그인 페이지에 리디렉션된 됩니다.  진행 하 고 로그인 합니다.  
  
![광고 FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_13.PNG)  
  
이 완료 되 면 지금에 기록 됩니다 표시 됩니다.  
  
![광고 FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_14.PNG)  
  
## <a name="next-steps"></a>다음 단계
[광고 FS 개발](../../ad-fs/AD-FS-Development.md)  

