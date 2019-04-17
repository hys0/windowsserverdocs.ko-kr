---
ms.assetid: 5052f13c-ff35-471d-bff5-00b5dd24f8aa
title: "응용 프로그램 다중 계층 On-Behalf-Of (OBO) OAuth FS 2016 광고를 사용 하 여 사용 하 여 빌드"
description: 
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 8940cde2b78ce3ead499263e6fba0fbe28aae695
ms.sourcegitcommit: c16a2bf1b8a48ff267e71ff29f18b5e5cda003e8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/28/2018
---
# <a name="build-a-multi-tiered-application-using-on-behalf-of-obo-using-oauth-with-ad-fs-2016"></a>응용 프로그램 다중 계층 On-Behalf-Of (OBO) OAuth FS 2016 광고를 사용 하 여 사용 하 여 빌드

>Windows Server 2016 적용 됩니다.

이 연습 Adfs을 사용 하 여 Windows Server 2016 TP5에서를 대신 하 여-의 (OBO) 인증을 구현 하기 위한 지침을 제공 합니다.  o 읽어보십시오 OBO 인증에 대 한 자세한 [개발자를 위해 광고 FS 시나리오](../../ad-fs/overview/AD-FS-Scenarios-for-Developers.md)

>경고: 교육 목적 으로만 여기 빌드할 수 있는 예가입니다. 필요한 요소 모델의 노출 될 수 간단한, 가장 최소 구현 위한이 지침입니다. 예제 오류 처리의 모든 측면 포함 되지 않을 수 및 기타 관련 기능에 성공 OBO 인증 가져오는 집중 하 고 있습니다.

## <a name="overview"></a>개요

이 샘플는 인증 흐름 클라이언트 중간 계층 웹 서비스에 액세스할 수는 장소와 웹 서비스 헤드를 액세스 토큰 인증된 클라이언트를 대표 하 여 만들 수는 예정 합니다.

![광고 FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO28.PNG)

다음은 샘플을 얻을 수 있는 인증 흐름
1. 클라이언트는 ADFS 승인 종료 지점으로 인증와 인증 코드를 요청
2. 승인 끝점 인증 코드 클라이언트를 반환
3. 클라이언트 인증 코드를 사용 하 여를 WebAPI로 가운데 계층 웹 서비스에 대 한 요청 액세스 토큰 ADFS 토큰 끝점에 게 제공
4. ADFS 중간 계층 웹 서비스에 대 한 액세스 토큰을 반환합니다. 추가 기능에 대 한 가운데 계층 서비스 백 엔드 WebAPI에 액세스 해야
5. 액세스 토큰 중간 계층 서비스를 사용 하 여 사용 합니다.
6. 가운데 계층 서비스 제공을 ADFS 토큰 끝점 액세스 토큰 하 고 요청 토큰에 대 한 액세스를 대신 하 여-의 백 엔드 WebAPI 인증된 된 사용자
7. ADFS 클라이언트로 백 엔드 WebAPI에 대 한 액세스 토큰 가운데 계층 서비스 actiing을 반환
8. 가운데 계층 서비스 ADFS 7 단계에서 제공한 액세스 토큰 클라이언트로 WebAPI 백 엔드 액세스 하 고 필요한 기능을 수행를 사용 하 여

## <a name="sample-structure"></a>샘플 구조

3 개의의 샘플 구성 하는


모듈 | 설명
-------|------------
ToDoClient | 사용자는와 상호 작용 하는 기본 클라이언트
ToDoService | 중간 계층 웹 백 엔드 WebAPI에 대 한 클라이언트 역할을 하는 API
WebAPIOBO | 백 엔드 웹 ToDoService 사용자는 ToDoItem 추가할 때 필요한 작업을 수행 하는 데 사용 되는 api




## <a name="setting-up-the-development-box"></a>개발 상자 설정

이 단계는 Visual Studio 2015 사용합니다. 프로젝트 Active Directory 인증 라이브러리 (ADAL)를 많이 사용합니다. 읽어보십시오 ADAL에 대해 자세히 알아보려면 [Active Directory 인증 라이브러리.NET](https://msdn.microsoft.com/library/azure/mt417579.aspx)

또한 샘플 SQL LocalDB v11.0를 사용합니다. 작업 하 고 샘플에서 이전 SQL LocalDB 설치 합니다.

## <a name="setting-up-the-environment"></a>환경 설정
저희의 기본 설정을 작업할 수 있습니다.

1. **DC**: ADFS 호스팅할 도메인 도메인 컨트롤러
2. **광고 FS 서버**: 도메인 광고 FS 서버
3. **개발 시스템**: 기계 Visual Studio가 설치 되어 저희와 샘플 개발

사용할 수 있습니다을 두 개만 컴퓨터 합니다. DC/ADFS 및 샘플 개발에 대 한 다른 하나입니다.

이 문서 범위를 벗어나는 도메인 컨트롤러 및 Adfs를 설정 하는 방법이입니다. 추가 배포 내용은 다음과 같습니다.

- [AD DS 배포](../../ad-ds/deploy/AD-DS-Deployment.md)
- [AD FS 배포](../AD-FS-Deployment.md)

샘플 Vittorio Bertocci 만든 Azure에 대 한 기존 OBO 샘플에 따라 되어 사용할 수 있는 [여기](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof)합니다. 개발 시스템에 프로젝트 복제 및 작업을 시작 하 고 샘플의 복사본을 만들 지침을 따릅니다.

## <a name="clone-or-download-this-repository"></a>이 저장소를 다운로드 하거나 복제

셸 또는 명령줄:

    git clone https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof.git

## <a name="modifying-the-sample"></a>샘플 수정

WebAPI-OnBehalfOf-DotNet.sln 솔루션을 열면 즉시 솔루션-에 두 개의 프로젝트 있는 경우 알 수 있습니다.

* **ToDoListClient**: 사용자와 상호 작용은 OpenID 클라이언트 역할은이
* **ToDoListService**: 중간 계층 웹 서버 앱 / 하는 서비스는이 인증된 된 사용자 다른 백 엔드 WebAPI OBO 상호 작용은

알 수 다른 프로젝트 나중에 역할을 중간 계층 ToDoListService 하 여 액세스할 수 있는이 리소스는 추가 해야 합니다.

### <a name="configuring-ad-fs-for-the-client-and-webserver-app"></a>ADFS 클라이언트와 웹 앱에 대 한 구성

현재 샘플 형태로 Azure AD에 대 한 작업을 수행 해야 하는 인증 구성 됩니다. 인증 메커니즘을 변경 하려고 하 고 직접 ADFS 주말로 가면서 배포 온-프레미스 합니다. 이렇게 하기 위해 샘플에서 ADFS 클라이언트 인식 하도록 및는 웹 서버 앱 구성 해야 합니다.

**응용 프로그램 그룹 만들기**

ADFS 관리 MMC 열고 새 응용 프로그램 그룹을 추가 합니다. 기본-응용 프로그램-WebAPI 템플릿을 선택 합니다.

![광고 FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO2.PNG)

다음 클릭 하 고 클라이언트 앱에 대 한 정보를 제공 하기 위해 페이지가 나타납니다. 적절 한 이름을 클라이언트 Adfs에서 앱을 제공 합니다. 클라이언트 식별자 복사한 visual studio에서 응용 프로그램 구성에서이 필요한 수 만큼 나중에 액세스할 수 장소를 저장 합니다.

>참고: 리디렉션합니다 URI도 가능 모든 임의의 URI 정말 사용 하지 않으면 기본 클라이언트의 경우

![광고 FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO11.PNG)

다음 클릭 하 고 WebAPI에 대 한 정보를 제공 하기 위해 페이지가 나타납니다. WebAPI에 대 한 ADFS 항목에 대 한 적절 한 이름을 지정 하 고 Visual Studio에서는 ToDoListService 표시 URI로 이동 URI 입력

![광고 FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO16.PNG)

![광고 FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO18.PNG)

다음 클릭 하 고 선택 액세스 제어 정책 페이지가 표시 됩니다. "허용 모든" 정책 섹션에 표시 되도록 합니다.

![광고 FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO1.PNG)

다음 클릭 하 고 구성 응용 프로그램 사용 권한 페이지가 나타납니다. 이 페이지에서 openid (기본적으로 선택) 및 user_impersonation으로 허가 된 범위를 선택 합니다. 'User_impersonation' 범위 성공적으로 Adfs의 액세스를 대신 하 여-의 토큰 요청할 수 있게 하는 데 필요한 됩니다.

![광고 FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO12.PNG)

다음 클릭 요약 페이지가 표시 됩니다. 마법사의 나머지 서 구성을 완료 합니다.

-를 대신 하 여-의 인증을 사용 하기 위해 ADFS 클라이언트로 범위 user_impersonation와 액세스 토큰을 반환 확인 해야 합니다. 클레임 발급 ToDoListServiceWebApi 포함 다음 세 가지 사용자 지정 규칙에 대 한 수정 합니다.

    @RuleName = "All claims"
    c:[]
    => issue(claim = c);

    @RuleName = "Issue open id scope"
    => issue(Type = "https://schemas.microsoft.com/identity/claims/scope", Value = "openid");

    @RuleName = "Issue user_impersonation scope"
    => issue(Type = "https://schemas.microsoft.com/identity/claims/scope", Value = "user_impersonation");

![광고 FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO10.PNG)

**응용 프로그램 그룹에서 클라이언트로 ToDoListService 추가**

이 단계에서 adfs 리소스와 뿐 아니라 클라이언트로 작동 하는 웹 서버 앱에 대해 추가 항목을 확인 해야 합니다. 방금 만든 응용 프로그램 그룹 열고 응용 프로그램 추가 클릭 합니다.

![광고 FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO15.PNG)

"새 MySampleGroup 응용 프로그램을 추가" 페이지와 함께 제공 됩니다. 이 페이지에서 "응용 프로그램이 나 웹 서버의" 실행형 응용 프로그램으로 선택

![광고 FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO19.PNG)

다음을 클릭 응용 프로그램 세부 정보를 제공 하기 위해 페이지와 함께 제공 됩니다. 이름 섹션에서 구성 항목에 대 한 적절 한 이름을 제공 합니다. 클라이언트 식별자는 ToDoListServiceWebAPI에 대 한 식별자와 같은 인지 확인

![광고 FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO20.PNG)

다음 클릭 하 고 응용 프로그램 자격 증명을 구성 하는 페이지와 함께 제공 됩니다. "공유 암호를 생성"를 클릭 합니다. 자동으로 생성 시크릿 표시 됩니다. 이 해야 하는 visual studio에는 ToDoListService 구성 하는 동안 일부 위치의 암호를 복사 합니다.


![광고 FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO17.PNG)

다음 클릭 하 고 마법사를 완료 합니다.

### <a name="modifying-the-todolistclient-code"></a>ToDoListClient 코드를 수정

#### <a name="modify-the-application-config"></a>응용 프로그램 구성 수정

이동 하는 WebAPI-OnBehalfOf-DotNet 솔루션 ToDoListClient 프로젝트 합니다. App.config 파일을 연 다음 수정

* 메모 ida: 테 주요 항목
* Ida: RedirectURI adfs에서의 MySampleGroup_ClientApplication 구성 하는 동안 제공 되는 임의의 URI 입력에 대 한 합니다.
* Ida: ClientID 키에 대 한 클라이언트는 MySampleGroup_ClientApplication 구성 하는 동안 ADFS 주었습니다 ID 식별자를 제공 합니다.
* Adfs에서의 ToDoListServiceWebApi 구성 하는 동안 제공한 ida: ToDoListResourceID 제공 리소스 ID
* 주요 ida: AADInstance 메모
* Ida: ToDoListBaseAddress에 대 한 리소스는 ToDoListServiceWebApi ID를 입력 합니다. 이 일 WebAPI 호출 하는 동안 사용 됩니다.
* 주요 ida: 기관 추가 하 고 adfs URI로 값을 제공 합니다.

사용자 **appSettings** App.Config에는 다음과 유사 합니다.

    <appSettings>
    <!--<add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" />-->
    <add key="ida:ClientId" value="c7f7b85c-497c-4589-877f-b17a0bd13398" />
    <add key="ida:RedirectUri" value="https://arbitraryuri.com/" />
    <add key="ida:TodoListResourceId" value="https://localhost:44321/" />
    <!--<add key="ida:AADInstance" value="https://login.microsoftonline.com/{0}" />-->
    <add key="ida:TodoListBaseAddress" value="https://localhost:44321" />
    <add key="ida:Authority" value="https://fs.anandmsft.com/adfs/"/>
    </appSettings>

#### <a name="modifying-the-code"></a>코드를 수정

**MainWindow.xaml.cs**

메모 응용 프로그램 구성에서 테 정보를 읽는 줄

    //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];
    //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];

권한 문자열이 값 변경

    private static string authority = ConfigurationManager.AppSettings["ida:Authority"];

코드를 ToDoListResourceId 및 ToDoListBaseAddress 올바르지 값 읽기 변경

    private static string todoListResourceId = ConfigurationManager.AppSettings["ida:TodoListResourceId"];
    private static string todoListBaseAddress = ConfigurationManager.AppSettings["ida:TodoListBaseAddress"];

함수 MainWindow()로 authcontext 초기화를 변경 합니다.

    authContext = new AuthenticationContext(authority, false);

### <a name="adding-the-backend-resource"></a>백 엔드 리소스 추가

백 엔드 리소스는 ToDoListService에 액세스 하는를 대신 하 여-의 만들 필요가를 대신 하 여-의 흐름을 완료 하려면 인증된 된 사용자 합니다. 백 엔드 리소스의 선택, 요구 사항에 따라 다를 수 있습니다 있지만이 샘플 함으로써 기본 WebAPI 만들 수 있습니다.

* ' WebAPI OnBehalfOf DotNet' 솔루션 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 하 고 선택 추가 새 프로젝트->
* 웹 응용 프로그램 서식 ASP.NET 선택

![광고 FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO4.PNG)

* 다음에서 프롬프트 ' 변경 인증 '를 클릭합니다
* '작업 및 학교 계정'를 선택합니다 하 고 올바른 드롭다운 목록에서 ' 온-프레미스 '을 선택합니다
* ADFS 배포 federationmetadata.xml 경로 입력 하 고 앱 URI 제공 (현재 모든 URI 제공 하 고 나중에 변경 됩니다) 솔루션을 프로젝트 추가 확인을 클릭 합니다.

![광고 FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO9.PNG)

* 마우스 오른쪽 단추로 클릭 컨트롤러 솔루션 탐색기 새 프로젝트를 만들 아래에 있습니다. 추가-> 컨트롤러를 선택
* 서식 파일 선택 '웹 API 2 컨트롤러-비우기'를 선택 하 고 확인을 클릭 합니다.

![광고 FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO3.PNG)

* 이름을 적절 한 컨트롤러

![광고 FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO13.PNG)

* 컨트롤러의 다음 코드 추가


        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Net;
        using System.Net.Http;
        using System.Web.Http;
        namespace WebAPIOBO.Controllers
        {
            public class WebAPIOBOController : ApiController
            {
                public IHttpActionResult Get()
                {
                    return Ok("WebAPI via OBO");
                }
            }
        }

Get 요청 WebAPI WebAPIOBO에 대 한 모드로 누구 든 지 때이 코드는 문자열을 반환 간단 하 게

### <a name="adding-the-new-backend-webapi-to-ad-fs"></a>새 백 엔드 WebAPI Adfs에 추가

MySampleGroup 응용 프로그램 그룹을 엽니다. 추가 응용 프로그램과 선택 하 고 웹 API 템플릿 클릭 하 고 클릭 합니다.

![광고 FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO6.PNG)

웹 API 구성 페이지 WebAPI 항목과 식별자에 대 한 적절 한 이름을 제공 합니다. 식별자 (BackendWebAPIAdfsAdd에 그랬던 것 비슷함) visual studio에서 WebAPIOBO 프로젝트에서 값 SSL URL 있어야 합니다.

![광고 FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO8.PNG)

![광고 FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO7.PNG)

계속 마법사의 나머지 부분을 동일 ToDoListService WebAPI를 구성 했습니다. 끝에 응용 프로그램 그룹 아래 같이 됩니다.

![광고 FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO5.PNG)


### <a name="modifying-the-todolistservice-code"></a>ToDoListService 코드를 수정

#### <a name="modifying-the-application-config"></a>응용 프로그램 구성 수정

* 토큰과 열기
* 다음과 같은 키를 수정

| 키 | 값 |
|:-----|:-------|
|관객 ida:| 가리키는 ADFS 예를 들어, ToDoListService WebAPI 구성 하는 동안 https://localhost:44321/ 대로 ToDoListService ID|
|ClientID ida:| 가리키는 ADFS 예를 들어, ToDoListService WebAPI 구성 하는 동안 https://localhost:44321/ 대로 ToDoListService ID </br>**것은 매우 중요 ida: 관객 및 ida: ClientID 일치 하는 다른 사용자**|
|ClientSecret ida:| 이 ADFS adfs에서 ToDoListService 클라이언트 구성 된 경우 발생 하는 암호|
|ADFSMetadata ida:| 예를 들어 https://fs.anandmsft.com/federationmetadata/2007-06/federationmetadata.xml에 대 한 ADFS 메타 데이터에 대 한 URL이|
|OBOWebAPIBase ida:| 예를 들어 https://localhost:44300에 대 한 API 백 엔드 전화를 사용 하 여는 경우 기본 주소|
|기관 ida:| 이 예제 https://fs.anandmsft.com/adfs/ ADFS 서비스에 대 한 URL|


모든 다른 ida:가지고 키의 **appsettings** 노드 주석으로 되거나 삭제 될 수 있습니다

#### <a name="change-authentication-from-azure-ad-to-ad-fs"></a>Azure AD에 Adfs의 인증 변경

* Startup.Auth.cs 파일 열기
* 다음은 제거

        app.UseWindowsAzureActiveDirectoryBearerAuthentication(
            new WindowsAzureActiveDirectoryBearerAuthenticationOptions
            {
                Audience = ConfigurationManager.AppSettings["ida:Audience"],
                Tenant = ConfigurationManager.AppSettings["ida:Tenant"],
                TokenValidationParameters = new TokenValidationParameters{ SaveSigninToken = true }
            });

사용

        app.UseActiveDirectoryFederationServicesBearerAuthentication(
            new ActiveDirectoryFederationServicesBearerAuthenticationOptions
            {
                MetadataEndpoint = ConfigurationManager.AppSettings["ida:AdfsMetadataEndpoint"],
                TokenValidationParameters = new TokenValidationParameters()
                {
                    SaveSigninToken = true,
                    ValidAudience = ConfigurationManager.AppSettings["ida:Audience"]
                }
            });

#### <a name="modifying-the-todolistcontroller"></a>ToDoListController 수정

System.Web에 대 한 언급을 추가 합니다. 확장 합니다. 아래에 있는 코드를 대체 하 여 클래스 회원 수정

    //
    // The Client ID is used by the application to uniquely identify itself to Azure AD.
    // The App Key is a credential used by the application to authenticate to Azure AD.
    // The Tenant is the name of the Azure AD tenant in which this application is registered.
    // The AAD Instance is the instance of Azure, for example public Azure or Azure China.
    // The Authority is the sign-in URL of the tenant.
    //
    private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];
    private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];
    private static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];
    private static string appKey = ConfigurationManager.AppSettings["ida:AppKey"];

    //
    // To authenticate to the Graph API, the app needs to know the Grah API's App ID URI.
    // To contact the Me endpoint on the Graph API we need the URL as well.
    //
    private static string graphResourceId = ConfigurationManager.AppSettings["ida:GraphResourceId"];
    private static string graphUserUrl = ConfigurationManager.AppSettings["ida:GraphUserUrl"];
    private const string TenantIdClaimType = "https://schemas.microsoft.com/identity/claims/tenantid";

사용

    //
    // The Client ID is used by the application to uniquely identify itself to Azure AD.
    // The client secret is the credentials for the WebServer Client

    private static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];
    private static string clientSecret = ConfigurationManager.AppSettings["ida:ClientSecret"];
    private static string authority = ConfigurationManager.AppSettings["ida:Authority"];

    // Base address of the WebAPI
    private static string OBOWebAPIBase = ConfigurationManager.AppSettings["ida:OBOWebAPIBase"];

**이름에 사용 되는 클레임 수정**

Adfs의 Nmae 클레임 발급는 저희 하지만 NameIdentifier 클레임 보내지 했습니다. 샘플 NameIdentifier 작업 항목의 고유 하 게 키를 사용합니다. 편의 위해 클레임와 NameIdentifier 코드에 안전 하 게 제거할 수 있습니다. 찾기 및 NameIdentifier 동일한 모든 이름을 바꿉니다.

**게시물 루틴 및 CallGraphAPIOnBehalfOfUser() 수정**

복사 하 고 아래 코드 ToDoListController.cs에 붙여 누르고 코드 게시물 및 CallGraphAPIOnBehalfOfUser

    // POST api/todolist
    public async Task Post(TodoItem todo)
    {
        if (!ClaimsPrincipal.Current.FindFirst("https://schemas.microsoft.com/identity/claims/scope").Value.Contains("user_impersonation"))
        {
            throw new HttpResponseException(new HttpResponseMessage { StatusCode = HttpStatusCode.Unauthorized, ReasonPhrase = "The Scope claim does not contain 'user_impersonation' or scope claim not found" });
        }

        //
        // Call the WebAPIOBO On Behalf Of the user who called the To Do list web API.
        //
        string augmentedTitle = null;
        string custommessage = await CallGraphAPIOnBehalfOfUser();
        if (custommessage != null)
        {
            augmentedTitle = String.Format("{0}, Message: {1}", todo.Title, custommessage);
        }
        else
        {
            augmentedTitle = todo.Title;
        }

        if (null != todo && !string.IsNullOrWhiteSpace(todo.Title))
        {
            db.TodoItems.Add(new TodoItem { Title = augmentedTitle, Owner = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Name).Value });
            db.SaveChanges();
        }
    }

    public static async Task<string> CallGraphAPIOnBehalfOfUser()
    {
        string accessToken = null;
        AuthenticationResult result = null;
        AuthenticationContext authContext = null;
        HttpClient httpClient = new HttpClient();
        string custommessage = "";

        //
        // Use ADAL to get a token On Behalf Of the current user.  To do this we will need:
        //      The Resource ID of the service we want to call.
        //      The current user's access token, from the current request's authorization header.
        //      The credentials of this application.
        //      The username (UPN or email) of the user calling the API
        //
        ClientCredential clientCred = new ClientCredential(clientId, clientSecret);
        var bootstrapContext = ClaimsPrincipal.Current.Identities.First().BootstrapContext as System.IdentityModel.Tokens.BootstrapContext;
        string userName = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Upn) != null ? ClaimsPrincipal.Current.FindFirst(ClaimTypes.Upn).Value : ClaimsPrincipal.Current.FindFirst(ClaimTypes.Email).Value;
        string userAccessToken = bootstrapContext.Token;
        UserAssertion userAssertion = new UserAssertion(bootstrapContext.Token, "urn:ietf:params:oauth:grant-type:jwt-bearer", userName);

        string userId = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Name).Value;
        authContext = new AuthenticationContext(authority, false);

        // In the case of a transient error, retry once after 1 second, then abandon.
        // Retrying is optional.  It may be better, for your application, to return an error immediately to the user and have the user initiate the retry.
        bool retry = false;
        int retryCount = 0;

        do
        {
            retry = false;
            try
            {
                result = authContext.AcquireToken(OBOWebAPIBase, clientCred, userAssertion);
                accessToken = result.AccessToken;
            }
            catch (AdalException ex)
            {
                if (ex.ErrorCode == "temporarily_unavailable")
                {
                    // Transient error, OK to retry.
                    retry = true;
                    retryCount++;
                    Thread.Sleep(1000);
                }
            }
        } while ((retry == true) && (retryCount < 1));

        if (accessToken == null)
        {
            // An unexpected error occurred.
            return (null);
        }

        // Once the token has been returned by ADAL, add it to the http authorization header, before making the call to access the To Do list service.
        httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

        // Call the WebAPIOBO.
        HttpResponseMessage response = await httpClient.GetAsync(OBOWebAPIBase + "/api/WebAPIOBO");


        if (response.IsSuccessStatusCode)
        {
            // Read the response and databind to the GridView to display To Do items.
            string s = await response.Content.ReadAsStringAsync();
            JavaScriptSerializer serializer = new JavaScriptSerializer();
            custommessage = serializer.Deserialize<string>(s);
            return custommessage;
        }
        else
        {
            custommessage = "Unsuccessful OBO operation : " + response.ReasonPhrase;
        }
        // An unexpected error occurred calling the Graph API.  Return a null profile.
        return (null);
    }

## <a name="running-the-solution"></a>실행 하는 해결 방법


기본적으로 visual studio 한 프로젝트 실행 디버그 누를 경우 실행 하도록 구성 됩니다.

* 마우스 오른쪽 단추로 클릭 솔루션을 속성을 선택 합니다.
* 속성 페이지에서 여러 시작 프로젝트를 선택 하 고 세 모든 항목을 시작 하는 작업 변경 합니다.

![광고 FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO14.PNG)

F5 키를 누르면 하 고 솔루션을 실행

![광고 FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO24.PNG)

로그인 단추를 클릭 합니다. 로그인에 사용 하 여 ADFS 하 라는 메시지가 표시 될

![광고 FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO25.PNG)

후 로그인을 할 일 항목 목록에 추가 합니다. 백그라운드에서 하겠습니다에 더 이상 게시물 WebAPIOBO 웹 API 구입 해야 합니다 ToDoListService 게시물 작업을 수행 합니다.

![광고 FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO26.PNG)

성공 작업에 대해 항목 OBO auth 흐름을 사용 하 여 액세스 하는 웹 API 백 엔드에서 추가 메시지를 목록에 추가 된 것 표시 됩니다.

![광고 FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO27.PNG)

또한 자세한 추적 Fiddler에서 볼 수 있습니다. Fiddler을 실행 하 고 암호를 해독 HTTPS를 사용 하도록 설정 합니다. /Adfs/oautincludes 끝점으로 요청 두 죠 있는지 확인할 수 있습니다.
첫 번째 상호 작용에서 우리 토큰 끝점에 액세스 코드는 대해 알아보고 토큰 https://localhost:44321/에 대 한 ![광고 FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO22.PNG)

토큰 끝점와 두 번째 상호 작용을 볼 수 있습니다는 **requested_token_use** 홈페이지로 설정할 **on_behalf_of** 얻은를 대신 하 여-의 토큰 얻는 설정으로 https://localhost:44321/ 즉, 중간 계층 웹 서비스에 대 한 액세스 토큰을 사용 하는 것입니다.
![광고 FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO23.PNG)

## <a name="next-steps"></a>다음 단계
[광고 FS 개발](../../ad-fs/AD-FS-Development.md)  
