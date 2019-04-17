---
ms.assetid: 5a64e790-6725-4099-aa08-8067d57c3168
title: "빌드 FS 2016 ad OAuth 기밀 클라이언트를 사용 하는 서버 쪽 응용 프로그램"
description: 
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 175c683f9097aeba4c1f06e8671183476c98aa3f
ms.sourcegitcommit: c16a2bf1b8a48ff267e71ff29f18b5e5cda003e8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/28/2018
---
# <a name="build-a-server-side-application-using-oauth-confidential-clients-with-ad-fs-2016"></a>빌드 FS 2016 ad OAuth 기밀 클라이언트를 사용 하는 서버 쪽 응용 프로그램

>Windows Server 2016 적용 됩니다.

Windows Server 2012 r 2에서 Adfs의 초기 Oauth 지원의 개발 FS 2016 AD 수 있는 앱 이나 서비스에서 실행 하는 웹 서버에서 등 자체 비밀 정보를 유지 하는 클라이언트에 대 한 지원이 소개 합니다.  이러한 클라이언트 기밀 클라이언트도 알려져 있습니다.    
아래 구조 웹 서버에서 실행 되 고 Adfs에 대 한 기밀 클라이언트 역할 웹 응용 프로그램에 다음과 같습니다.  
  
## <a name="pre-requisites"></a>필수  
이 문서를 완료 하기 전에 필요한 필수 목록은 다음과 같습니다. 이 문서도 간주 ADFS 설치가 완료 된 후 ADFS 농장 만들었습니다.  
  
-   (무료 평가판 괜찮습니다)는 Azure AD 구독  
  
-   GitHub 클라이언트 도구  
  
-   Windows Server 2016 t p 4 이상 ADFS  
  
-   Visual Studio 2013 이상 합니다.  
  
## <a name="create-an-application-group-in-ad-fs-2016"></a>Adfs 2016 응용 프로그램 그룹 만들기  
다음 광고 FS 2016에 응용 프로그램 그룹 구성 하는 방법을 설명 합니다.  
  
#### <a name="create-the-application-group"></a>응용 프로그램 그룹 만들기  
  
1.  AD FS 관리에 응용 프로그램 그룹에서 마우스 오른쪽 단추로 클릭 한 다음 **응용 프로그램 그룹 추가**합니다.  
  
2.  응용 프로그램 그룹 마법사에서 이름을 입력 **ADFSOAUTHCC** 고 **독립 실행형 응용 프로그램** 선택는 **서버 응용 프로그램 또는 웹 사이트** 서식 합니다.  클릭 **다음**합니다.  
  
    ![광고 FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_2.PNG)  
  
3.  복사는 **클라이언트 식별자** 값 합니다.  나중에 대 한 값으로 사용 **ida: ClientId** 응용 프로그램 토큰과에 있습니다.  
  
    ![광고 FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_3.PNG)  
  
4.  입력에 대 한 다음 **리디렉션합니다 URI:** - **https://localhost:44323**합니다.  클릭 **추가**합니다. 클릭 **다음**합니다.  
  
5.  에 **응용 프로그램 자격 증명 구성** 화면에서의 확인란을 선택 **공유 암호를 생성**비밀 복사 하 고 있습니다.  이 나중에 사용에 대 한 값으로 **ida: AppKey** 응용 프로그램 토큰과에 있습니다.  클릭 **다음**합니다.  
  
    ![광고 FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_4.PNG)  
  
6.  에 **요약** 화면에서 클릭 **다음**합니다.  
  
7.  에 **Complete** 화면에서 클릭 **닫기**합니다.  
  
8.  지금 마우스 오른쪽 단추로 클릭 새 응용 프로그램 그룹에서 선택한 **속성**합니다.  
  
9. **ADFSOAUTHCC 속성** 클릭 **응용 프로그램 추가**합니다.  
  
10. 에 **샘플 응용 프로그램의 응용 프로그램 새로 추가** 선택 **웹 API**클릭 **다음**합니다.  
  
    ![광고 FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_6.PNG)  
  
11. 에 **구성 웹 API** 화면에서 대 한 다음 입력 **식별자** - **https://contoso.com/WebApp**합니다.  클릭 **추가**합니다. 클릭 **다음**합니다.  이 값은 사용할 나중에 대 한 **ida: GraphResourceId** 응용 프로그램 토큰과에 있습니다.  
  
    ![광고 FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_9.PNG)  
  
12. 에 **액세스 제어 정책 선택** 화면에서 **모든 허용** 클릭 **다음**합니다.  
  
    ![광고 FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_7.PNG)  
  
13. 에 **응용 프로그램 사용 권한 구성** 화면에서 확인**user_impersonation** 을 선택 하 고 클릭 **다음**합니다.  
  
    ![광고 FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_8.PNG)  
  
14. 에 **요약** 화면에서 클릭 **다음**합니다.  
  
15. 에 **Complete** 화면에서 클릭 **닫기**합니다.  
  
16. 에 **ADFSOAUTHCC 속성** 클릭 **확인**합니다.  
  
## <a name="upgrade-the-database"></a>데이터베이스를 업그레이드  
Visual Studio 2015이이 연습 만드는에 사용 되었습니다.   Visual Studio 2015와 협력 예제 얻기 위해 데이터베이스 파일을 업데이트 해야 합니다.  다음 절차를 사용 하 여이 작업을 수행 합니다.  
  
이 여기서 샘플 웹 API를 다운로드 하 고 데이터베이스에 Visual Studio 2015 업그레이드 하는 방법을 설명 합니다.   Azure AD 샘플을 사용 했습니다 [여기](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity)합니다.  
  
샘플 프로젝트를 다운로드 하려면 Git Bash를 사용 하 고 다음을 입력 합니다.  
  
```  
git clone https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity.git  
```  
  
![광고 FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_10.PNG)  
  
#### <a name="to-upgrade-the-database-file"></a>데이터베이스 파일을 업그레이드  
  
1.  Visual Studio에서 프로젝트 열거나 앱 SQL Server 2102 Express 해야 함을 알려주는 팝업 됩니다 데이터베이스를 업그레이드 해야 합니다.  확인을 클릭 합니다.  
  
    ![광고 FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_12.PNG)  
  
2.  다음 빌드를 선택 하 여 응용 프로그램 컴파일 위에 솔루션 빌드-> 합니다.  이렇게 하면 모든 NuGet 패키지 복원 됩니다.  
  
    ![광고 FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_13.PNG)  
  
3.  이제 맨 위에 있는 선택 **보기** -> **서버 탐색기**합니다.  열리는 되 면 **데이터 연결**를 마우스 오른쪽 단추로 클릭 **DefaultConnection** 선택한 **연결 수정**합니다.  
  
    ![광고 FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_14.PNG)  
  
4.  **연결 수정**선택 **고급**합니다.  
  
    ![광고 FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_15.PNG)  
  
5.  고급 속성에서 데이터 소스 찾아에서 설정을 변경 하려면 다음 드롭다운 메뉴를 사용 하 여 **(LocalDb\v11.0)** 에 **(LoaclDB) MSSQLLocalDB**합니다.  
  
    ![광고 FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_16.PNG)  
  
6.  확인을 클릭 합니다. 확인을 클릭 합니다.  예 데이터베이스를 클릭 합니다.  
  
    ![광고 FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_17.PNG)  
  
7.  이 완료 되 면 넘는 오른쪽에 값을 복사 상자에서 옆에 **연결 문자열 합니다.**  
  
    ![광고 FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_18.PNG)  
  
8.  이제는 토큰과 열고 값 위의 복사한 값으로 연결 문자열을 대체 합니다.  토큰과 저장 합니다.  
  
    > [!NOTE]  
    > 위의 단계는 새 연결 문자열 접속할 수 있도록 필요 합니다.  그렇지 않은 경우 Update-Database 아래 실행 하면 아웃 오류가 됩니다.  
  
    ![광고 FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_19.PNG)  
  
9. Visual Studio 맨 선택 **보기** -> **다른 창** -> **패키지 관리자 콘솔**합니다.  
  
    ![광고 FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_20.PNG)  
  
10. 아래에서 패키지 관리자 콘솔 입력: `Enable-Migrations`시작 하 고 입력 하 고 있습니다.  
  
    > [!NOTE]  
    > Enable-Migrations cmdlet으로 인식 되지 않는 한다는 오류 메시지가 Install-Package EntityFramework는 EntityFramework 업데이트를 입력 합니다.  
  
    ![광고 FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_21.PNG)  
  
11. 아래에서 패키지 관리자 콘솔 입력: `Add-Migration <anynamehere>`시작 하 고 입력 하 고 있습니다.  
  
    ![광고 FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_22.PNG)  
  
12. 아래에서 패키지 관리자 콘솔 입력: `Update-Database`시작 하 고 입력 하 고 있습니다.  
  
    ![광고 FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_23.PNG)  
  
## <a name="modify-the-webapi-in-visual-studio"></a>Visual Studio에서 WebApi 수정  
  
#### <a name="to-modify-the-sample-web-api"></a>샘플 웹 API 수정 하려면  
  
1.  Visual Studio를 사용 하 여 샘플을 엽니다.  
  
2.  토큰과를 엽니다.  다음 값 수정 합니다.  
  
    -   ida: ClientId-위의 # 3 값을 입력 합니다.  
  
    -   ida: AppKey-5 번 위의에서 값을 입력 합니다.  
  
    -   ida: GraphResourceId-위의 # 11에서 값을 입력 합니다.  
  
    ![광고 FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_24.PNG)  
  
3.  App_Start Startup.Auth.cs 파일 열고 다음과 같은 변경:  
  
    -   다음 줄을 설명 합니다.  
  
        ```  
        //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];  
        //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];  
        //public static readonly string Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);  
        ```  
  
        ![광고 FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_25.PNG)  
  
    -   다음의 위치에서 추가.  
  
        ```  
        public static readonly string Authority = "https://<your_fsname>/adfs";  
        ```  
  
        < your_fsname > 해당 federation 서비스 url 예를 들어 adfs.contoso.com DNS 부분으로 대체 됩니다 위치  
  
        ![광고 FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_26.PNG)  
  
4.  UserProfileController.cs 파일을 열고 다음과 같은 변경 합니다.  
  
    -   다음 의견을 다음과 같습니다.  
  
        ```  
        //authContext = new AuthenticationContext(Startup.Authority, new TokenDbCache(userObjectID));  
        ```  
  
    -   다음 두 번을 바꿉니다.  
  
        ```  
        authContext = new AuthenticationContext(Startup.Authority, false, new TokenDbCache(userObjectID));  
        ```  
  
        ![광고 FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_27.PNG)  
  
    -   다음 의견을 다음과 같습니다.  
  
        ```  
        //authContext = new AuthenticationContext(Startup.Authority);  
        ```  
  
    -   다음 두 번을 바꿉니다.  
  
        ```  
        authContext = new AuthenticationContext(Startup.Authority, false);  
        ```  
  
        ![광고 FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_28.PNG)  
  
    -   다음의 모든 인스턴스 메모 이제:  
  
        ```  
        Uri redirectUri = new Uri(Request.Url.GetLeftPart(UriPartial.Authority.ToString() + "/OAuth");  
        ```  
  
    -   모든 항목을 다음과 같은 바꿉니다.  
  
        ```  
        Uri redirectUri = new Uri(Request.Url.GetLeftPart(UriPartial.Authority.ToString());  
        ```  
  
        ![광고 FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_34.PNG)  
  
## <a name="test-the-solution"></a>테스트는 해결 방법  
이 섹션의 기밀 클라이언트 솔루션을 테스트 했습니다.  다음 절차 솔루션을 테스트할 수 있습니다.  
  
#### <a name="testing-the-confidential-client-solution"></a>테스트 기밀 클라이언트 해결 방법  
  
1.  Visual Studio 맨 위에 있는 Internet Explorer 선택 되어 있는지 확인 하 고 녹색에 있는 화살표를 클릭 합니다.  
  
    ![광고 FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_36.png)  
  
2.  클릭 ASP.Net 페이지를 되 면 **등록**합니다.  
  
    ![광고 FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_31.PNG)  
  
3.  사용자 이름 및 암호를 입력 한 다음 누르고 **등록**합니다.  이 SQL 데이터베이스에 로컬 계정을 만듭니다.  
  
    ![광고 FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_31.PNG)  
  
4.  이제, 공지 ASP.NET 사이트 Hello bsimon를 표시 아닙니다.  클릭 **프로필**합니다.  
  
    ![광고 FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_32.PNG)  
  
5.  이 정보 없이 페이지를 시작 하 고는 저희 해야 여기를 클릭에 로그인 합니다.  클릭 **여기**합니다.  
  
    ![광고 FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_33.PNG)  
  
6.  Adfs에 로그인 하 라는 메시지가 표시 됩니다.  
  
    ![광고 FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_35.PNG)  
  
## <a name="next-steps"></a>다음 단계
[광고 FS 개발](../../ad-fs/AD-FS-Development.md)  

