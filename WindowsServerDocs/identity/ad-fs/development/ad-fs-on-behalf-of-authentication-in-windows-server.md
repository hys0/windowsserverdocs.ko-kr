---
ms.assetid: 5052f13c-ff35-471d-bff5-00b5dd24f8aa
title: AD FS 2016 이상에서 OAuth를 사용 하 여 OBO ()를 사용 하는 다중 계층 응용 프로그램 빌드
description: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 028396bffff6449a296e2922846fe2fc379fe624
ms.sourcegitcommit: 2a15de216edde8b8e240a4aa679dc6d470e4159e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77465617"
---
# <a name="build-a-multi-tiered-application-using-on-behalf-of-obo-using-oauth-with-ad-fs-2016-or-later"></a>AD FS 2016 이상에서 OAuth를 사용 하 여 OBO ()를 사용 하는 다중 계층 응용 프로그램 빌드


이 연습에서는 Windows Server 2016 T P 5 이상에서 AD FS를 사용 하 여 (OBO) 인증을 구현 하기 위한 지침을 제공 합니다. OBO 인증에 대 한 자세한 내용은 [Openid connect Connect/OAuth 흐름 및 응용 프로그램 시나리오 AD FS](../../ad-fs/overview/ad-fs-openid-connect-oauth-flows-scenarios.md) 읽어 보세요.

>경고: 여기 빌드할 수 있는 예제는 교육용 으로만입니다. 이러한 지침은 모델의 필수 요소를 노출할 수 가장 간단 하 고 가장 최소한의 구현에 대 한 것입니다. 예제에서는 오류 처리의 모든 측면을 포함 되지 않아야 하 고 다른 관련 기능에 성공적으로 OBO 인증을 가져오는 중점을 두고 있습니다.

## <a name="overview"></a>개요

이 샘플에는 인증 흐름 여기서 중간 계층 웹 서비스 클라이언트 액세스 하 고 웹 서비스 액세스 토큰 인증된 된 클라이언트를 대신 하 여 헤드 만드는데 합니다.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO28.png)

다음은 샘플 작업을 수행 합니다 하는 인증 흐름
1. 클라이언트는 AD FS 권한 부여 끝점을 인증 하 고 권한 부여 코드를 요청 합니다.
2. 클라이언트에 인증 코드를 반환 하는 권한 부여 엔드포인트
3. 클라이언트 인증 코드를 사용 하 고 WebAPI로 중간 계층 웹 서비스에 대 한 액세스 토큰 요청에 AD FS 토큰 엔드포인트에 표시
4. AD FS는 중간 계층 웹 서비스에 액세스 토큰을 반환합니다. 추가 기능을 사용 하려면 중간 계층 서비스에서 백 엔드 WebAPI 액세스 해야 합니다.
5. 클라이언트는 중간 계층 서비스를 사용 하 여 액세스 토큰을 사용 합니다.
6. AD FS 토큰 끝점에 대 한 액세스 토큰을 제공 하는 중간 계층 서비스 및 요청 액세스 토큰에 대 한 대리 백 엔드 WebAPI 인증된 된 사용자
7. AD FS actiing 중간 계층 서비스를 클라이언트로 WebAPI 백 엔드에 대 한 액세스 토큰을 반환
8. 클라이언트로 WebAPI 백 엔드에 액세스 하 고 필요한 기능을 수행 하려면 7 단계에서 AD FS에서 제공 된 액세스 토큰을 사용 하는 중간 계층 서비스

## <a name="sample-structure"></a>샘플 구조

다음 세 가지 모듈로 구성 하는 샘플


모듈 | 설명
-------|------------
ToDoClient | 사용자 상호 작용 하는 네이티브 클라이언트
ToDoService | 중간 계층 웹 WebAPI 백 엔드에 대 한 클라이언트 역할을 하는 API
WebAPIOBO | 백 엔드 웹 ToDoService 사용자 ToDoItem을 추가할 때 필요한 작업을 수행 하는 데 사용 되는 api




## <a name="setting-up-the-development-box"></a>개발 상자를 설정합니다.

이 연습에서는 Visual Studio 2015를 사용합니다. 프로젝트는 과도 하 게 Active Directory 인증 라이브러리 (ADAL)를 사용합니다. 읽으십시오 ADAL에 대 한 자세한 [Active Directory 인증 라이브러리.NET](https://msdn.microsoft.com/library/azure/mt417579.aspx)

이 샘플에는 또한 SQL LocalDB v11.0을 사용합니다. 이 샘플에서 일 하기 전에 SQL LocalDB를 설치 합니다.

## <a name="setting-up-the-environment"></a>환경 설정
여기서의 기본 설정을 작업할 수 있습니다.

1. **DC**: AD FS은 호스트 도메인에 대 한 도메인 컨트롤러
2. **AD FS 서버**: 도메인에 대 한 AD FS 서버
3. **개발 컴퓨터**:에서는 Visual Studio를 설치 하 고 컴퓨터 개발 샘플

사용할 수 있습니다, 원하는 경우 컴퓨터가 두 대만. DC/ADFS와 샘플을 개발 하기 위한 기타 하나입니다.

도메인 컨트롤러와 AD FS를 설정 하는 방법이 기사의 범위를 벗어납니다. 추가 배포 정보를 참조 하십시오.

- [AD DS 배포](../../ad-ds/deploy/AD-DS-Deployment.md)
- [AD FS 배포](../AD-FS-Deployment.md)

샘플은 azure Vittorio Bertocci에서 만든 기존 OBO 샘플에 기반 하 고 사용 가능한 [여기](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof)합니다. 개발 컴퓨터에서 프로젝트를 복제 하 고 작업을 시작 하려면이 샘플의 복사본을 만드는 지침을 따릅니다.

## <a name="clone-or-download-this-repository"></a>이 리포지토리 복제 또는 다운로드

셸 또는 명령줄:

    git clone https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof.git

## <a name="modifying-the-sample"></a>이 샘플을 수정합니다.

WebAPI-OnBehalfOf-DotNet 솔루션을 열면 바로 솔루션에 두 개의 프로젝트가 있는 것을 알 수 있습니다.

* **ToDoListClient**:이 역할을 사용자와 상호 작용 하기는 OpenID 클라이언트
* **ToDoListService**: 중간 계층 웹 서버 응용 프로그램 / 서비스에이 인증된 된 사용자 다른 백 엔드 WebAPI OBO 상호 작용 합니다

여기에서 볼 수 있듯이 다른 프로젝트 나중에 역할을 중간 계층 ToDoListService에서 액세스할 수 있는 리소스를 추가 해야 합니다.

### <a name="configuring-ad-fs-for-the-client-and-webserver-app"></a>클라이언트와 웹 서버 응용 프로그램에 대 한 AD FS를 구성합니다.

이 샘플의 현재 형태로 인증은 Azure AD에 대해 수행 될으로 구성 됩니다. 직접 AD FS에 대해 배포 온-프레미스 및 인증 메커니즘을 변경 해야 합니다. 이렇게 하려면 샘플에서 클라이언트를 인식 하도록 AD FS 및 마련 하는 웹 서버 응용 프로그램을 구성 해야 합니다.

**응용 프로그램 그룹 만들기**

AD FS 관리 MMC를 열고 새 애플리케이션 그룹을 추가 합니다. WebAPI-네이티브-응용 프로그램 템플릿을 선택 합니다.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO2.PNG)

다음에 클릭 하 고 클라이언트 응용 프로그램에 대 한 정보를 제공 하기 위한 페이지와 함께 나타납니다. AD FS에서 응용 프로그램 클라이언트는 적절 한 이름을 제공 합니다. 클라이언트 식별자를 복사 하 고이 visual studio에서 애플리케이션 구성에 필요한 수 만큼 나중에 액세스할 수 어딘가에 저장 합니다.

>참고: 리디렉션 URI도 가능 임의의 URI 실제로 사용 되지 않는 네이티브 클라이언트의 경우

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO11.PNG)

다음에 클릭 하 고 WebAPI에 대 한 정보를 제공 하기 위한 페이지와 함께 나타납니다. WebAPI 위해 AD FS 항목에 대 한 적절 한 이름을 지정 하 고 ToDoListService에 대 한 Visual Studio에서 참조 하는 URI와 리디렉션 URI를 입력 합니다.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO16.PNG)

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO18.PNG)

다음에 클릭 하 고 액세스 제어 정책 선택 페이지가 표시 됩니다. "Everyone"에서 허용 정책 섹션을 참조를 확인 합니다.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO1.PNG)

다음에 클릭 하 고 구성 응용 프로그램 사용 권한 페이지 나타납니다. 이 페이지에서는 openid (기본적으로 선택 됨) 및 user_impersonation으로 허용 된 범위를 선택 합니다. 범위 'user_impersonation' 성공적으로 AD FS에서 대 한 대리 액세스 토큰을 요청할 수 있게 하는 데 필요한입니다.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO12.PNG)

다음 클릭 하 여 요약 페이지가 표시 됩니다. 마법사의 나머지 부분에서 이동한 다음 구성을 완료 합니다.

한 대리 인증을 사용 하기 위해 AD FS 클라이언트로 범위가 user_impersonation와 액세스 토큰을 반환 하는지 확인 해야 합니다. 다음 세 가지 사용자 지정 규칙을 포함 시키려면 ToDoListServiceWebApi에 대 한 클레임 발급을 수정 합니다.

    @RuleName = "All claims"
    c:[]
    => issue(claim = c);

    @RuleName = "Issue user_impersonation scope"
    => issue(Type = "http://schemas.microsoft.com/identity/claims/scope", Value = "user_impersonation");

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO10.PNG)

**응용 프로그램 그룹에서 클라이언트로 ToDoListService 추가**

이 단계에서 리소스 뿐만 아니라 클라이언트와 작동 하도록 웹 서버 응용 프로그램에 대 한 AD FS에서 추가 항목을 확인 해야 합니다. 방금 만든 애플리케이션 그룹을 열고 애플리케이션 추가 클릭 합니다.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO15.PNG)

"MySampleGroup 새 애플리케이션 추가" 페이지와 함께 나타납니다. 이 페이지에서 "서버 애플리케이션 또는 웹 사이트" 독립 실행형 애플리케이션으로 선택

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO19.PNG)

다음을 클릭 하 고 애플리케이션 정보를 제공 하는 페이지와 함께 나타납니다. 구성 항목의 이름 섹션에 대 한 적절 한 이름을 제공 합니다. 클라이언트 식별자는 ToDoListServiceWebAPI에 대 한 식별자와 같음 인지 확인

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO20.PNG)

다음에 클릭 하 고 애플리케이션 자격 증명을 구성 하는 페이지와 함께 나타납니다. "공유 암호 생성" 클릭 합니다. 자동으로 생성 되는 암호와 나타납니다. 로 서이 필요한 ToDoListService visual studio에서 구성 하는 동안 동일한 위치에서 암호를 복사 합니다.


![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO17.PNG)

다음에 클릭 하 고 마법사를 완료 합니다.

### <a name="modifying-the-todolistclient-code"></a>ToDoListClient 코드 수정

#### <a name="modify-the-application-config"></a>응용 프로그램 구성 수정

이동 하면 WebAPI-영문 솔루션의 ToDoListClient 프로젝트 된 것입니다. App.config 파일을 열고 다음과 같이 수정

* Ida: 테 넌 트 키 항목 설명
* Ida: RedirectURI는 MySampleGroup_ClientApplication AD FS에서 구성 하는 동안 제공 되는 임의의 URI를 입력 합니다.
* Ida: ClientID 키에 대 한 클라이언트 ID 식별자는 MySampleGroup_ClientApplication를 구성 하는 동안 지정한 AD FS를 제공 합니다.
* AD FS에는 ToDoListServiceWebApi를 구성 하는 동안 지정한 ida: ToDoListResourceID 리소스 ID 제공
* 키 ida: AADInstance 주석
* Ida: ToDoListBaseAddress는 ToDoListServiceWebApi의 리소스 ID를 입력 합니다. ToDoList WebAPI를 호출 하는 동안 사용 됩니다.
* Ida: 기관 키를 추가 하 고 AD FS에 대 한 URI로 값을 제공 합니다.

프로그램 **appSettings** App.Config는 모양이이 비슷합니다.

    <appSettings>
    <!--<add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" />-->
    <add key="ida:ClientId" value="c7f7b85c-497c-4589-877f-b17a0bd13398" />
    <add key="ida:RedirectUri" value="https://arbitraryuri.com/" />
    <add key="ida:TodoListResourceId" value="https://localhost:44321/" />
    <!--<add key="ida:AADInstance" value="https://login.microsoftonline.com/{0}" />-->
    <add key="ida:TodoListBaseAddress" value="https://localhost:44321" />
    <add key="ida:Authority" value="https://fs.anandmsft.com/adfs/"/>
    </appSettings>

#### <a name="modifying-the-code"></a>코드 수정

**MainWindow.xaml.cs**

애플리케이션 구성에서 테 넌 트 정보를 읽는 줄을 주석

    //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];
    //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];

권한 문자열의 값 변경

    private static string authority = ConfigurationManager.AppSettings["ida:Authority"];

ToDoListResourceId 및 ToDoListBaseAddress의 올바른 값을 읽는 코드를 변경 합니다.

    private static string todoListResourceId = ConfigurationManager.AppSettings["ida:TodoListResourceId"];
    private static string todoListBaseAddress = ConfigurationManager.AppSettings["ida:TodoListBaseAddress"];

함수에서 mainwindow ()로 authcontext 초기화를 변경 합니다.

    authContext = new AuthenticationContext(authority, false);

### <a name="adding-the-backend-resource"></a>백엔드 리소스를 추가합니다.

한 대리 ToDoListService에 액세스 하는 백 엔드 리소스를 만들 필요가 대 한 대리 흐름을 완료 하려면 인증된 된 사용자입니다. 백엔드 리소스의 선택은 요구 사항에 따라 달라질 수 있지만이 샘플에서는 기본 WebAPI를 만들 수 있습니다.

* 솔루션 탐색기에서 ' WebAPI-영문 ' 솔루션을 마우스 오른쪽 단추로 클릭 하 고 추가 선택-> 새 프로젝트
* ASP.NET 웹 응용 프로그램 템플릿을 선택 합니다.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO4.PNG)

* 다음 프롬프트 클릭 ' 인증 변경 '
* '회사 및 학교 계정'을 선택 하 고 오른쪽의 드롭다운 목록에서 ' 온-프레미스 '를 선택 합니다.
* AD FS 배포에 대 한 federationmetadata.xml 경로 입력 하 고 응용 프로그램 URI를 제공 (지금은 모든 URI를 제공 하 고 나중에 변경 됩니다) 솔루션에 프로젝트를 추가 하려면 확인을 클릭 합니다.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO9.PNG)

* 마우스 오른쪽 단추로 새 프로젝트가 만들어지면 솔루션 탐색기에서 컨트롤러 클릭 합니다. 선택-> 컨트롤러 추가
* 템플릿 선택 영역에 'Web API 2 컨트롤러-비어 있음을'를 선택 하 고 확인을 클릭 합니다.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO3.PNG)

* 컨트롤러에 적절 한 이름을 지정 합니다.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO13.PNG)

* 컨트롤러에 다음 코드를 추가 합니다.

```cs
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Net;
    using System.Net.Http;
    using System.Web.Http;
    namespace WebAPIOBO.Controllers
    {
        [Authorize]
        public class WebAPIOBOController : ApiController
        {
            public IHttpActionResult Get()
            {
                return Ok($"WebAPI via OBO (user: {User.Identity.Name}");
            }
        }
    }
```

이 코드는 WebAPI WebAPIOBO에 대 한 Get 요청을 전환할 누구 든 지 때 문자열 반환 단순히

### <a name="adding-the-new-backend-webapi-to-ad-fs"></a>AD FS에 새 WebAPI 백 엔드를 추가합니다.

MySampleGroup 애플리케이션 그룹을 엽니다. 추가 애플리케이션 및 Web API 템플릿 선택을 클릭 하 고 클릭 합니다.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO6.PNG)

웹 API 구성 페이지에서 WebAPI 항목 및 식별자에 대 한 적절 한 이름을 제공 합니다. 식별자는 (BackendWebAPIAdfsAdd에 대해 수행한 것과 비슷함) visual studio에서 WebAPIOBO 프로젝트에서 SSL URL 값을 이어야 합니다.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO8.PNG)

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO7.PNG)

마법사의 나머지 부분에서 동일한으로 계속 ToDoListService WebAPI을 구성 했습니다. 끝에 애플리케이션 그룹 아래 같이 표시 됩니다.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO5.PNG)


### <a name="modifying-the-todolistservice-code"></a>ToDoListService 코드 수정

#### <a name="modifying-the-application-config"></a>애플리케이션 구성 수정

* Web.config 파일을 열으십시오
* 다음 키를 수정 합니다.

| Key                      | 값                                                                                                                                                                                                                   |
|:-------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ida: 대상             | ToDoListService WebAPI를 구성 하는 동안 AD FS에 지정 된 ToDoListService의 ID (예: https://localhost:44321/                                                                                         |
| ida: ClientID             | ToDoListService WebAPI를 구성 하는 동안 AD FS에 지정 된 ToDoListService의 ID (예: <https://localhost:44321/> </br>**Ida: 대상 그룹과 ida: ClientID는 서로 일치 해야 합니다.** |
| ida: ClientSecret         | 이 AD FS에는 AD FS에서 ToDoListService 클라이언트 구성할 때 생성 되는 암호                                                                                                                   |
| ida: AdfsMetadataEndpoint | AD FS 메타 데이터에 대 한 URL (예: https://fs.anandmsft.com/federationmetadata/2007-06/federationmetadata.xml                                                                                             |
| ida: OBOWebAPIBase        | 백 엔드 API를 호출 하는 데 사용 하는 기본 주소 (예: https://localhost:44300                                                                                                                     |
| ida: 기관            | AD FS 서비스에 대 한 URL입니다 (예 https://fs.anandmsft.com/adfs/                                                                                                                                          |

모든 다른 ida: XXXXXXX에 키의 **appsettings** 노드를 주석으로 처리 하거나 삭제 수

#### <a name="change-authentication-from-azure-ad-to-ad-fs"></a>Azure AD에 AD FS의 인증을 변경 합니다.

* Startup.Auth.cs 파일을 엽니다
* 다음 코드를 제거 합니다.

        app.UseWindowsAzureActiveDirectoryBearerAuthentication(
            new WindowsAzureActiveDirectoryBearerAuthenticationOptions
            {
                Audience = ConfigurationManager.AppSettings["ida:Audience"],
                Tenant = ConfigurationManager.AppSettings["ida:Tenant"],
                TokenValidationParameters = new TokenValidationParameters{ SaveSigninToken = true }
            });

의 태그 값을

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

System.Web.Extensions에 대 한 참조를 추가 합니다. 아래 코드를 대체 하 여 클래스 멤버를 수정 합니다.

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

의 태그 값을

    //
    // The Client ID is used by the application to uniquely identify itself to Azure AD.
    // The client secret is the credentials for the WebServer Client

    private static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];
    private static string clientSecret = ConfigurationManager.AppSettings["ida:ClientSecret"];
    private static string authority = ConfigurationManager.AppSettings["ida:Authority"];

    // Base address of the WebAPI
    private static string OBOWebAPIBase = ConfigurationManager.AppSettings["ida:OBOWebAPIBase"];

**이름에 사용 된 클레임 수정**

AD FS에서 Nmae 클레임을 실행 하는 것 하지만 하지 NameIdentifier 클레임을 실행 하는 것입니다. 샘플 할 일 항목의 고유 키를 NameIdentifier를 사용합니다. 간단히 하기 위해 코드에서 이름 클레임을 가진 NameIdentifier를 안전 하 게 제거할 수 있습니다. NameIdentifier의 모든 항목을 찾아 이름으로 바꿉니다.

**Post 루틴 및 CallGraphAPIOnBehalfOfUser 수정 ()**

복사 ToDoListController.cs에 아래 코드를 붙여 넣은 Post 및 CallGraphAPIOnBehalfOfUser에 대 한 코드를 바꿉니다

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
        // The Resource ID of the service we want to call.
        // The current user's access token, from the current request's authorization header.
        // The credentials of this application.
        // The username (UPN or email) of the user calling the API
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
                    result = await authContext.AcquireTokenAsync(OBOWebAPIBase, clientCred, userAssertion);
                    //result = await authContext.AcquireTokenAsync(...);
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

## <a name="running-the-solution"></a>솔루션을 실행합니다.


기본적으로 visual studio는 실행 하는 디버그 적중 되 면 한 프로젝트를 실행 하도록 구성 됩니다.

* 마우스 오른쪽 단추로 클릭 솔루션 및 속성을 선택 합니다.
* 속성 페이지에서 여러 개의 시작 프로젝트를 선택 하 고 모든 세 가지 항목에 대 한 시작 하는 작업을 변경 합니다.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO14.PNG)

솔루션을 실행 하 고 f5 키를 누릅니다

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO24.PNG)

로그인 단추를 클릭 합니다. 로그인 할 AD FS를 사용 하 여 나타납니다.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO25.PNG)

한 후 로그인, 목록에 ToDo 항목을 추가 합니다. 뒷 이야기 하겠습니다 ToDoListService 추가 될 지 WebAPIOBO 웹 API에 게시 하는 Post 작업을 수행 합니다.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO26.PNG)

작업 성공에 OBO 인증 흐름을 사용 하 여 액세스 하는 웹 API 백 엔드에서 추가 메시지를 사용 하 여 목록에 항목 추가 되어 있는지 표시 됩니다.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO27.PNG)

또한 Fiddler에 자세한 추적을 볼 수 있습니다. Fiddler를 시작 하 고 HTTPS 암호 해독을 설정 합니다. /Adfs/oautincludes 엔드포인트에 두 개의 요청을 수행할 것을 볼 수 있습니다.
첫 번째 상호 작용에서 토큰 끝점에 대 한 액세스 코드를 제공 하 고 https://localhost:44321/ ![AD FS OBO에 대 한 액세스 토큰을 가져옵니다](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO22.PNG)

두 번째 토큰 끝점과의 상호 작용에서 **on_behalf_of** 로 설정 된 **requested_token_use** 를 확인 하 고, 중간 계층 웹 서비스에 대해 획득 한 액세스 토큰 (예:)을 사용 하 여 토큰을 사용 하 여 토큰을 가져올 수 있습니다 https://localhost:44321/.
![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO23.PNG)

## <a name="next-steps"></a>다음 단계
[AD FS 개발](../../ad-fs/AD-FS-Development.md)  
