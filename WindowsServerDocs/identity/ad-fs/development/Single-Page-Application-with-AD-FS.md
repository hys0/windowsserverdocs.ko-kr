---
title: OAuth 및 ADAL을 사용 하 여 단일 페이지 웹 응용 프로그램을 빌드합니다. AD FS 2016 이상 버전
description: JavaScript 용 ADAL을 사용 하 여 AD FS에 대 한 인증을 위한 지침을 제공 하는 연습은 AngularJS 기반 단일 페이지 응용 프로그램을 보호 합니다.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 06/13/2018
ms.topic: article
ms.prod: windows-server
ms.technology: active-directory-federation-services
ms.openlocfilehash: f62b6ad288e2733083d535260f0b3f5ffb5b50bf
ms.sourcegitcommit: f829a48b9b0c7b9ed6e181b37be828230c80fb8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "82173628"
---
# <a name="build-a-single-page-web-application-using-oauth-and-adaljs-with-ad-fs-2016-or-later"></a>OAuth 및 ADAL을 사용 하 여 단일 페이지 웹 응용 프로그램을 빌드합니다. AD FS 2016 이상 버전

이 연습에서는 ASP.NET Web API 백 엔드로 구현 된 AngularJS 기반 단일 페이지 응용 프로그램을 보호 하는 JavaScript 용 ADAL을 사용 하 여 AD FS에 대 한 인증을 위한 지침을 제공 합니다.

이 시나리오에서는 사용자가 로그인하면 JavaScript 프런트 엔드에서 [JavaScript용 Active Directory 인증 라이브러리(ADAL.JS)](https://github.com/AzureAD/azure-activedirectory-library-for-js) 및 암시적 권한 부여를 사용하여 Azure AD로부터 ID 토큰(id_token)을 가져옵니다. 토큰이 캐시되고, 클라이언트가 웹 API 백 엔드에 대해 호출할 때 이 토큰을 요청에 전달자 토큰으로 첨부합니다. 그러면 OWIN 미들웨어를 사용하여 보안됩니다.

>[!IMPORTANT]
>여기에서 빌드할 수 있는 예제는 교육용 으로만 사용 됩니다. 이러한 지침은 모델의 필수 요소를 노출할 수 가장 간단 하 고 가장 최소한의 구현에 대 한 것입니다. 이 예제에는 오류 처리 및 기타 관련 기능의 모든 측면이 포함 되지 않을 수 있습니다.

>[!NOTE]
>이 연습은 AD FS Server 2016 이상에 **만** 적용 됩니다. 

## <a name="overview"></a>개요
이 샘플에서는 단일 페이지 응용 프로그램 클라이언트가 백 엔드의 WebAPI 리소스에 대 한 액세스를 보호 하기 위해 AD FS에 대해 인증 하는 인증 흐름을 만듭니다. 전체 인증 흐름은 다음과 같습니다.


![AD FS 권한 부여](media/Single-Page-Application-with-AD-FS/authenticationflow.PNG)

단일 페이지 응용 프로그램을 사용 하는 경우 사용자가 시작 페이지로 이동 하 여 시작 페이지로 이동 하 여 JavaScript 파일 및 HTML 뷰의 컬렉션이 로드 됩니다. 응용 프로그램에 대 한 중요 한 정보 (예: AD FS 인스턴스, 클라이언트 ID)를 파악 하도록 ADAL (Active Directory 인증 라이브러리)을 구성 하 여 인증을 AD FS에 전달할 수 있도록 해야 합니다.

ADAL이 인증에 대 한 트리거를 발견 하면 응용 프로그램에서 제공 하는 정보를 사용 하 여 인증을 AD FS STS로 보냅니다.  AD FS에서 공용 클라이언트로 등록 된 단일 페이지 응용 프로그램은 암시적 권한 부여 흐름에 대해 자동으로 구성 됩니다. 권한 부여 요청은 #fragment를 통해 응용 프로그램으로 다시 반환 되는 ID 토큰을 생성 합니다. 백 엔드 WebAPI에 대 한 추가 호출은 WebAPI에 대 한 액세스 권한을 얻기 위해 헤더의 전달자 토큰으로이 ID 토큰을 전달 합니다.

## <a name="setting-up-the-development-box"></a>개발 상자를 설정합니다.
이 연습에서는 Visual Studio 2015를 사용합니다. 프로젝트는 ADAL JS 라이브러리를 사용 합니다. ADAL에 대 한 자세한 내용은 [.net Active Directory 인증 라이브러리](https://msdn.microsoft.com/library/azure/mt417579.aspx) 를 참조 하세요.

## <a name="setting-up-the-environment"></a>환경 설정
이 연습에서는의 기본 설정을 사용 합니다.

1.    DC: AD FS은 호스트 도메인에 대 한 도메인 컨트롤러
2.    AD FS 서버: 도메인에 대 한 AD FS 서버
3.    개발 컴퓨터:에서는 Visual Studio를 설치 하 고 컴퓨터 개발 샘플

사용할 수 있습니다, 원하는 경우 컴퓨터가 두 대만. 하나는 DC/AD FS이 고 다른 하나는 샘플을 개발 하는 데 사용할입니다.

도메인 컨트롤러와 AD FS를 설정 하는 방법이 기사의 범위를 벗어납니다. 추가 배포 정보를 참조 하십시오.

- [AD DS 배포](../../ad-ds/deploy/AD-DS-Deployment.md)
- [AD FS 배포](../AD-FS-Deployment.md)



## <a name="clone-or-download-this-repository"></a>리포지토리 복제 또는 다운로드
Azure AD를 AngularJS 단일 페이지 앱에 통합 하기 위해 만든 샘플 응용 프로그램을 사용 하 고, AD FS를 사용 하 여 백 엔드 리소스를 대신 보호 하도록 수정 합니다.

셸 또는 명령줄에서 다음 명령을 실행합니다.

    git clone https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp.git

## <a name="about-the-code"></a>코드 정보
인증 논리를 포함 하는 키 파일은 다음과 같습니다.

**Node.js** -adal 모듈 종속성을 삽입 하 고, AAD와의 프로토콜 상호 작용을 위한 adal에서 사용 되는 앱 구성 값을 제공 하 고, 이전 인증 없이는 액세스할 수 없는 경로를 나타냅니다.

**index .html** -adal에 대 한 참조를 포함 합니다.

**HomeController**-ADAL에서 login () 및 logOut () 메서드를 활용 하는 방법을 보여 줍니다.

**Userdatacontroller** -캐시 된 id_token에서 사용자 정보를 추출 하는 방법을 보여 줍니다.

**Startup.Auth.cs** -전달자 인증을 위해 Active Directory 페더레이션 서비스를 사용 하는 WebAPI에 대 한 구성을 포함 합니다.

## <a name="registering-the-public-client-in-ad-fs"></a>AD FS에서 공용 클라이언트 등록
이 샘플에서 WebAPI는에서 https://localhost:44326/수신 대기 하도록 구성 됩니다. **웹 응용 프로그램에 액세스 하** 는 응용 프로그램 그룹 웹 브라우저는 암시적 허용 흐름 응용 프로그램을 구성 하는 데 사용할 수 있습니다.

1. AD FS management console을 열고 **응용 프로그램 그룹 추가**를 클릭 합니다. **응용 프로그램 그룹 추가 마법사** 에서 응용 프로그램의 이름을 입력 하 고 아래와 같이 **클라이언트-서버 응용 프로그램** 섹션에서 **웹 응용 프로그램 템플릿에 액세스 하는 웹 브라우저** 를 선택 합니다.

    ![새 응용 프로그램 그룹 만들기](media/Single-Page-Application-with-AD-FS/appgroup_step1.png)

2. 다음 페이지 **네이티브 응용 프로그램**에서 아래와 같이 응용 프로그램 클라이언트 식별자 및 리디렉션 URI를 제공 합니다.

    ![새 응용 프로그램 그룹 만들기](media/Single-Page-Application-with-AD-FS/appgroup_step2.png)

3. 다음 페이지에서 **Access Control 정책 적용** everyone 사용 권한을 *모두 허용* 으로 그대로 둡니다.

4. 요약 페이지는 아래와 같이 표시 됩니다.

    ![새 응용 프로그램 그룹 만들기](media/Single-Page-Application-with-AD-FS/appgroup_step3.png)

5. **다음** 을 클릭 하 여 응용 프로그램 그룹 추가를 완료 하 고 마법사를 닫습니다.

## <a name="modifying-the-sample"></a>이 샘플을 수정합니다.
ADAL JS 구성

**응용 프로그램 .js** 파일을 열고 **adalProvider** 정의를 다음과 같이 변경 합니다.

    adalProvider.init(
        {
            instance: 'https://fs.contoso.com/', // your STS URL
            tenant: 'adfs',                      // this should be adfs
            clientId: 'https://localhost:44326/', // your client ID of the
            //cacheLocation: 'localStorage', // enable this for IE, as sessionStorage does not work for localhost.
        },
        $httpProvider
    );

|구성|Description|
|--------|--------|
|인스턴스|STS URL (예:https://fs.contoso.com/|
|tenant|' Adfs '로 유지|
|clientID|단일 페이지 응용 프로그램에 대 한 공용 클라이언트를 구성 하는 동안 지정한 클라이언트 ID입니다.|

## <a name="configure-webapi-to-use-ad-fs"></a>AD FS를 사용 하도록 WebAPI 구성
샘플에서 **Startup.Auth.cs** 파일을 열고 시작 부분에 다음을 추가 합니다.

    using System.IdentityModel.Tokens;

삭제

    app.UseWindowsAzureActiveDirectoryBearerAuthentication(
        new WindowsAzureActiveDirectoryBearerAuthenticationOptions
        {
            Audience = ConfigurationManager.AppSettings["ida:Audience"],
            Tenant = ConfigurationManager.AppSettings["ida:Tenant"]
        }
    );

다음을 추가 합니다.

    app.UseActiveDirectoryFederationServicesBearerAuthentication(
        new ActiveDirectoryFederationServicesBearerAuthenticationOptions
        {
            MetadataEndpoint = ConfigurationManager.AppSettings["ida:AdfsMetadataEndpoint"],
            TokenValidationParameters = new TokenValidationParameters()
            {
                ValidAudience = ConfigurationManager.AppSettings["ida:Audience"],
                ValidIssuer = ConfigurationManager.AppSettings["ida:Issuer"]
            }
        }
    );

|매개 변수|설명|
|--------|--------|
|유효한 대상|토큰에서 확인 되는 ' 대상 '의 값을 구성 합니다.|
|ValidIssuer|그러면 토큰에서 확인할 발급자의 값이 구성 됩니다.|
|MetadataEndpoint|STS의 메타 데이터 정보를 가리킵니다.|

## <a name="add-application-configuration-for-ad-fs"></a>AD FS에 대 한 응용 프로그램 구성 추가
아래와 같이 appsettings를 변경 합니다.
```xml
    <appSettings>
        <add key="ida:Audience" value="https://localhost:44326/" />
        <add key="ida:AdfsMetadataEndpoint" value="https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml" />
        <add key="ida:Issuer" value="https://fs.contoso.com/adfs" />
    </appSettings>
    ```

## Running the solution
Clean the solution, rebuild the solution and run it. If you want to see detailed traces, launch Fiddler and enable HTTPS decryption.

The browser (use Chrome browser) will load the SPA and you will be presented with the following screen:

![Register the client](media/Single-Page-Application-with-AD-FS/singleapp3.PNG)

Click on Login.  The ToDo List will trigger the authentication flow and ADAL JS will direct the authentication to AD FS

![Login](media/Single-Page-Application-with-AD-FS/singleapp4a.PNG)

In Fiddler you can see the token being returned as part of the URL in the # fragment.

![Fiddler](media/Single-Page-Application-with-AD-FS/singleapp5a.PNG)

You will be able to now call the backend API to add ToDo List items for the logged-in user:

![Fiddler](media/Single-Page-Application-with-AD-FS/singleapp6.PNG)

## Next Steps
[AD FS Development](../../ad-fs/AD-FS-Development.md)  
