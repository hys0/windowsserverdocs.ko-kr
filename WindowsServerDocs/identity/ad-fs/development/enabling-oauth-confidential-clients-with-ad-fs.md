---
ms.assetid: 5a64e790-6725-4099-aa08-8067d57c3168
title: AD FS 2016 이상에서 OAuth 기밀 클라이언트를 사용 하 여 서버 쪽 응용 프로그램 빌드
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 8a8567a497e10df66f77fb996c937791b4aa9e08
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857566"
---
# <a name="build-a-server-side-application-using-oauth-confidential-clients-with-ad-fs-2016-or-later"></a>AD FS 2016 이상에서 OAuth 기밀 클라이언트를 사용 하 여 서버 쪽 응용 프로그램 빌드


AD FS 2016 이상 릴리스는 웹 서버에서 실행 되는 응용 프로그램 또는 서비스와 같이 자체 암호를 유지 관리할 수 있는 클라이언트에 대 한 지원을 제공 합니다.  이러한 클라이언트는 기밀 클라이언트 라고 합니다.
다음은 웹 서버에서 실행 되 고 AD FS에 기밀 클라이언트로 웹 애플리케이션의 개요입니다.  

## <a name="pre-requisites"></a>필수 구성 요소  
이 문서를 완료 하기 전에 필요한 필수 구성 요소 목록은 다음과 같습니다. 이 문서에서는 AD FS 설치 되어 있다고 가정 합니다.  

-   GitHub 클라이언트 도구  

-   AD FS Windows Server 2016 t p 4 이상  

-   Visual Studio 2013 이상입니다.  

## <a name="create-an-application-group-in-ad-fs-2016-or-later"></a>AD FS 2016 이상에서 응용 프로그램 그룹 만들기
다음 섹션에서는 AD FS 2016 이상에서 응용 프로그램 그룹을 구성 하는 방법을 설명 합니다.  

#### <a name="create-the-application-group"></a>응용 프로그램 그룹 만들기  

1.  AD FS 관리에서 응용 프로그램 그룹을 마우스 오른쪽 단추로 클릭 하 고 선택 **응용 프로그램 그룹 추가**합니다.  

2.  응용 프로그램 그룹 마법사에서 **이름** 에 대해 **Adfsoauthcc** 를 입력 하 고 **클라이언트-서버 응용 프로그램** 에서 **웹 API 템플릿에 액세스 하는 서버 응용 프로그램** 을 선택 합니다.  **다음**을 클릭합니다.  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_2.PNG)  

3.  복사는 **클라이언트 식별자** 값입니다.  나중에 대 한 값으로 사용 **ida: ClientId** 응용 프로그램 web.config 파일에 있습니다.  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_3.PNG)  

4.  **리디렉션 URI:**  -  **https://localhost:44323** 에 대해 다음을 입력 합니다.  **추가**를 클릭합니다. **다음**을 클릭합니다.  

5.  에 **응용 프로그램 자격 증명 구성** 화면에서에 체크 **공유 암호를 생성** secret을 복사 합니다.  이는 나중에 응용 프로그램 web.config 파일에서 **ida: ClientSecret** 의 값으로 사용 됩니다.  **다음**을 클릭합니다.  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_4.PNG)   

6. **웹 API 구성** 화면에서 **식별자** -  **https://contoso.com/WebApp** 에 대해 다음을 입력 합니다.  **추가**를 클릭합니다. **다음**을 클릭합니다.  이 값은 나중에 사용할 **ida: GraphResourceId** 응용 프로그램 web.config 파일에 있습니다.  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_9.PNG)  

7. **Access Control 정책 적용** 화면에서 **everyone 허용** 을 선택 하 고 **다음**을 클릭 합니다.  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_7.PNG)  

8. **응용 프로그램 사용 권한 구성** 화면에서 **openid connect** 및 **user_impersonation** 가 선택 되어 있는지 확인 하 고 **다음**을 클릭 합니다.  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_8.PNG)  

9. 에 **요약** 화면에서 **다음**합니다.  

10. 에 **Complete** 화면에서 **닫기**합니다.  

## <a name="upgrade-the-database"></a>데이터베이스 업그레이드  
Visual Studio 2015가이 연습을 만드는 데 사용 합니다.   Visual Studio 2015를 사용 하는 예제를 가져오기 위해 데이터베이스 파일을 업데이트 해야 합니다.  다음 절차를 사용 하 여이 작업을 수행 합니다.  

이 섹션에서는 샘플 웹 API를 다운로드 하 고 Visual Studio 2015의 데이터베이스를 업그레이드 하는 방법을 설명 합니다.   Azure AD 된 샘플을 사용 합니다 [여기](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity)합니다.  

샘플 프로젝트를 다운로드 하려면 Git Bash를 사용 하 고 다음을 입력 합니다.  

```  
git clone https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity.git  
```  

![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_10.PNG)  

#### <a name="to-upgrade-the-database-file"></a>데이터베이스 파일을 업그레이드 하려면  

1.  Visual Studio에서 프로젝트를 열면 앱에 SQL Server 2012 Express가 필요 하거나 데이터베이스를 업그레이드 해야 한다는 팝업이 표시 됩니다.  확인을 클릭합니다.  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_12.PNG)  

2.  다음 컴파일 빌드를 선택 하 여 응용 프로그램 맨 위에 있는 솔루션 빌드-> 합니다.  이렇게 하면 모든 NuGet 패키지 복원 됩니다.  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_13.PNG)  

3.  이제 맨 위에 있는 선택 **보기** -> **서버 탐색기**합니다.  아래에서 열리는 면 **데이터 연결**, 를 마우스 오른쪽 단추로 클릭 **DefaultConnection** 선택한 **연결 수정**합니다.  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_14.PNG)  

4.  **연결 수정**의 **데이터베이스 파일 이름 (신규 또는 기존)** 에서 **찾아보기** 를 선택 하 고 **path\filename.mdf**를 제공 합니다. 대화 상자에서 **예** 를 클릭 합니다.

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_6.PNG)

5.  **연결 수정**,  **고급**합니다.  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_15.PNG)  

6.  고급 속성에서 데이터 원본을 찾고 드롭다운을 사용 하 여 **(Localdb\v11.0)** 에서 **(LocalDb) \MSSQLLocalDB**로 변경 합니다.  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_16.PNG)  

7.  확인을 클릭합니다. 확인을 클릭합니다.  예를 클릭 하 여 데이터베이스를 업그레이드 합니다.  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_17.PNG)  

8.  이 완료 되 면 넘는 오른쪽 값을 복사 상자에서 옆에 **연결 문자열입니다.**  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_18.PNG)  

9.  이제 Web.config 파일을 열고 위에서 복사한 값으로 연결 문자열에 있는 값을 바꿉니다.  Web.config 파일을 저장합니다.  

    > [!NOTE]  
    > 위의 단계는 새 연결 문자열을 얻을 수 있도록 필요 합니다.  그렇지 않은 경우 데이터베이스 업데이트 아래 실행 하면를 오류가 발생을 합니다.  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_19.PNG)  

10. Visual Studio의 맨 선택 **보기** -> **다른 창** -> **패키지 관리자 콘솔**합니다.  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_20.PNG)  

11. 아래에 패키지 관리자 콘솔에서 입력:  `Enable-Migrations` 및 입력 키를 누릅니다.  

    > [!NOTE]  
    > Enable-migrations 나타내는 오류가 cmdlet으로 인식 되지 않습니다 발생 하는 경우 entity Framework를 업데이트 하려면 entity Framework 설치 패키지를 입력 합니다.  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_21.PNG)  

12. 아래에 패키지 관리자 콘솔에서 입력:  `Add-Migration <anynamehere>` 및 입력 키를 누릅니다.  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_22.PNG)  

13. 아래에 패키지 관리자 콘솔에서 입력:  `Update-Database` 및 입력 키를 누릅니다.  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_23.PNG)  

## <a name="modify-the-webapi-in-visual-studio"></a>Visual Studio에서 WebApi 수정  

#### <a name="to-modify-the-sample-web-api"></a>샘플 웹 API를 수정 하려면  

1.  Visual Studio를 사용 하 여 샘플을 엽니다.  

2.  Web.config 파일을 엽니다.  다음 값을 수정 합니다.  

    -   ida: ClientId-위의 응용 프로그램 그룹 만들기 섹션에서 #3 값을 입력 합니다.  

    -   ida: ClientSecret-위의 응용 프로그램 그룹 만들기 섹션에서 #5 값을 입력 합니다.  

    -   ida: GraphResourceId-위의 응용 프로그램 그룹 만들기 섹션에 있는 #6의 값을 입력 합니다.  

    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_24.PNG)  

3.  App_Start에서 Startup.Auth.cs 파일을 열고 다음과 같이 변경 합니다.  

    -   다음 줄을 주석 처리 합니다.  

        ```  
        //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];  
        //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];  
        //public static readonly string Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);  
        ```  

    -   다음 그 위치에 추가 합니다.  

        ```  
        public static readonly string Authority = "https://<your_fsname>/adfs";  
        ```  

        여기서 < your_fsname > 페더레이션 서비스 url, 예를 들어 adfs.contoso.com의 DNS 부분으로 바뀝니다  

        ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_25.PNG)  

4.  UserProfileController.cs 파일을 열고 다음과 같이 변경 합니다.  

    -   다음 주석 처리 합니다.  

        ```  
        //authContext = new AuthenticationContext(Startup.Authority, new TokenDbCache(userObjectID));  
        ```  

    -   다음으로 두 항목을 바꿉니다.  

        ```  
        authContext = new AuthenticationContext(Startup.Authority, false, new TokenDbCache(userObjectID));  
        ```  

        ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_27.PNG)  

    -   다음 주석 처리 합니다.  

        ```  
        //authContext = new AuthenticationContext(Startup.Authority);  
        ```  

    -   다음으로 두 항목을 바꿉니다.  

        ```  
        authContext = new AuthenticationContext(Startup.Authority, false);  
        ```  

        ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_28.PNG)  

    -   이제을 주석으로 처리는 다음의 모든 인스턴스입니다.  

        ```  
        Uri redirectUri = new Uri(Request.Url.GetLeftPart(UriPartial.Authority).ToString() + "/OAuth");  
        ```  

    -   다음 항목을 모두 바꿉니다.  

        ```  
        Uri redirectUri = new Uri(Request.Url.GetLeftPart(UriPartial.Authority).ToString());  
        ```  

        ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_34.PNG)  

## <a name="test-the-solution"></a>솔루션 테스트  
이 섹션에서는 기밀 클라이언트 솔루션을 테스트 합니다.  다음 절차를 사용 하 여 솔루션을 테스트 합니다.  

#### <a name="testing-the-confidential-client-solution"></a>기밀 클라이언트 솔루션 테스트  

1. Visual Studio 맨 위에 있는 Internet Explorer가 선택 되어 있는지 확인 하 고 녹색 화살표를 클릭 합니다.  

   ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_36.png)  

2. ASP.Net 페이지가 시작 되 면 페이지의 오른쪽 위에서 **등록** 을 클릭 합니다.  사용자 이름 및 암호를 입력 한 다음 **등록** 단추를 클릭 합니다.  이 SQL 데이터베이스에 로컬 계정을 만듭니다.  

   ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_31.PNG)  

3. 이제 ASP.NET 사이트가 Hello abby@contoso.com! 라고 표시 됩니다.  **프로필**을 클릭합니다.  

   ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_32.PNG)  

4. 이 정보 없이 페이지를 시작 하 고는 우리 해야 여기를 클릭에 로그인 합니다.  클릭 **여기**합니다.  

   ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_33.PNG)  

5. AD FS에 로그인 하 라는 메시지가 표시 됩니다.  

   ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_35.PNG)  

## <a name="next-steps"></a>다음 단계
[AD FS 개발](../../ad-fs/AD-FS-Development.md)  
