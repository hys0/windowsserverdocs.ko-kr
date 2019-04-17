---
title: "한 페이지 웹 응용 프로그램 OAuth 및 ADAL.JS JS"
description: 
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: active-directory-federation-services
ms.openlocfilehash: 7b3d48e1e38baffeb84b1f236efb43cfda5048c0
ms.sourcegitcommit: c16a2bf1b8a48ff267e71ff29f18b5e5cda003e8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/28/2018
---
# <a name="build-a-single-page-web-application-using-oauth-and-adaljs-with-ad-fs-2016"></a>한 페이지 웹 응용 프로그램 OAuth 및 ADAL.JS JS

>Windows Server 2016 적용 됩니다.

이 연습 ADFS ADAL를 사용 하 여에 대해 JavaScript AngularJS는 보안 유지를 인증에 대 한 명령 기반 ASP.NET 웹 API 백 엔드 프로그램을 사용 하 여 구현 단일 페이지 응용 프로그램을 제공 합니다.

>경고: 교육 목적 으로만 여기 빌드할 수 있는 예가입니다. 필요한 요소 모델의 노출 될 수 간단한, 가장 최소 구현 위한이 지침입니다. 기타 관련 기능 및 예와 오류 처리의 모든 측면 포함 되어 있지 않을 수 있습니다.

>[!NOTE]
>This walkthrough is applicable **only** to AD FS Server 2016 and higher 

## <a name="overview"></a>개요
이 샘플 보안 백 엔드 WebAPI 리소스에 액세스 하려면 Adfs에 대해 단일 페이지 응용 프로그램 클라이언트는 인증 하는 되는 인증 흐름을 만들 수는 했습니다. 다음은 전체적인 인증 흐름


![광고 FS 인증](media/Single-Page-Application-with-AD-FS/authenticationflow.PNG)

한 페이지 응용 프로그램을 사용 하는 경우 사용자로 이동 시작 위치에서 페이지 및 JavaScript 파일 컬렉션을 시작 하는 경우 되 고 HTML 보기 로드 됩니다. 인증 하면 ADFS 보낼 수 있도록 클라이언트 ID ADFS 인스턴스 즉, 응용 프로그램에 대 한 중요 한 정보를 알고 Active Directory 인증 라이브러리 (ADAL)는를 구성 해야 합니다.

ADAL 인증을 위한 트리거를 인식 하 고 응용 프로그램에서 제공 하는 정보를 사용 하 여 및 인증 AD FS STS을 보냅니다.  암묵적인 허가 흐름 Adfs의 공개 클라이언트로 등록 한 페이지 응용 프로그램을 자동으로 구성 됩니다. 권한 요청에 #fragment 통해 응용 프로그램에 다시 반환 된 ID 토큰 발생 합니다. 백 엔드에 통화 추가 WebAPI는 WebAPI에 액세스 하는 헤더에 전달자 토큰이 ID 토큰을 전달 됩니다.

## <a name="setting-up-the-development-box"></a>개발 상자 설정
이 단계는 Visual Studio 2015 사용합니다. 프로젝트 ADAL JS 라이브러리를 사용합니다. 읽어보십시오 ADAL에 대해 자세히 알아보려면 [Active Directory 인증 라이브러리.NET 합니다.](https://msdn.microsoft.com/library/azure/mt417579.aspx)

## <a name="setting-up-the-environment"></a>환경 설정
이 연습의 기본 설정을 사용 합니다.

1.  ADFS 호스팅할 도메인에 대 한 DC: 도메인 컨트롤러
2.  광고 FS 서버:는 도메인의 광고 FS 서버
3.  Visual Studio가 설치 되어 저희와 샘플 개발 컴퓨터 개발 컴퓨터:

사용할 수 있습니다을 두 개만 컴퓨터 합니다. DC ADFS 및 샘플 개발에 대 한 다른 하나입니다.

이 문서 범위를 벗어나는 도메인 컨트롤러 및 Adfs를 설정 하는 방법이입니다. 추가 배포 내용은 다음과 같습니다.

- [AD DS 배포](../../ad-ds/deploy/AD-DS-Deployment.md) 
- [AD FS 배포](../AD-FS-Deployment.md)



## <a name="clone-or-download-this-repository"></a>이 저장소를 다운로드 하거나 복제
Azure AD AngularJS 단일 페이지 앱에 통합 하 고 수정에 대 한 만든 샘플 응용 프로그램 Adfs을 사용 하 여 대신 보안 백 엔드 리소스를 사용 합니다.

셸 또는 명령줄:

    git clone https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp.git

## <a name="about-the-code"></a>코드에 대 한
주요 인증 논리가 포함 된 파일 다음과 같습니다.

**App.js** -ADAL 모듈 종속성 삽입, ADAL 하 여 운전 프로토콜 AAD와의 상호 작용에 사용 되는 앱 구성 값을 제공 하 고 이전 인증 없이 경로 액세스 하지 합니다.

**index.html** -포함 adal.js에 대 한 참조

**HomeController.js**-ADAL login() 및 logOut() 방법의 활용 하는 방법을 보여 줍니다.

**UserDataController.js** -캐시 된 id_token에서 사용자 정보를 추출 하는 방법을 보여 줍니다.

**Startup.Auth.cs** -전달자 인증에 대 한 Active Directory Federation 서비스를 사용 하 여 WebAPI 구성을 포함 됩니다.

## <a name="registering-the-public-client-in-ad-fs"></a>Adfs의 공개 클라이언트 등록
샘플을 듣기 시작 https://localhost:44326/에는 WebAPI 구성 됩니다. 응용 프로그램 그룹 **웹 응용 프로그램에 액세스 하는 웹 브라우저** 암묵적인 허가 흐름 응용 프로그램을 구성 하는 데 사용할 수 있습니다.

1. 클릭 하 고 ADFS management console을 엽니다 **응용 프로그램 그룹 추가**합니다. 에 **응용 프로그램 그룹 추가 마법사** 선택, 설명 응용 프로그램의 이름을 입력 하는 **웹 응용 프로그램에 액세스 하는 웹 브라우저** 에서 템플릿을 **서버 클라이언트 응용 프로그램** 섹션 아래와 같이
    <br>![새 응용 그룹 만들기](media/Single-Page-Application-with-AD-FS/appgroup_step1.png)

2. 다음 페이지에서 **기본 응용 프로그램**응용 프로그램 클라이언트 id를 제공 하 고 다음과 같이 URI 리디렉션합니다,
    <br>![새 응용 그룹 만들기](media/Single-Page-Application-with-AD-FS/appgroup_step2.png)

3. 다음 페이지에서 **액세스 제어 정책이 적용** 권한으로 유지 *모든 허용*

4. 요약 페이지 아래와 같습니다.
    <br>![새 응용 그룹 만들기](media/Single-Page-Application-with-AD-FS/appgroup_step3.png)

5. 클릭 **다음** 응용 프로그램 그룹 완료 하 고 마법사 닫습니다.

## <a name="modifying-the-sample"></a>샘플 수정
ADAL JS 구성

열려 있는 **app.js** 파일을 변경는 **adalProvider.init** 정의를:

    adalProvider.init(
        {
            instance: 'https://fs.contoso.com/', // your STS URL
            tenant: 'adfs',                      // this should be adfs
            clientId: 'https://localhost:44326/', // your client ID of the
            //cacheLocation: 'localStorage', // enable this for IE, as sessionStorage does not work for localhost.
        },
        $httpProvider
        );

|구성|설명
|--------|--------
|인스턴스|예를 들어 https://fs.contoso.com/ STS URL을
|테|'Adfs'로 계속
|clientID|한 페이지 응용 프로그램에 대 한 클라이언트 공개 구성 하는 동안 지정 클라이언트 id

## <a name="configure-webapi-to-use-ad-fs"></a>ADFS 사용 하 여 WebAPI 구성
열려 있는 **Startup.Auth.cs** 고 샘플에서 파일을 처음에 다음 추가: 

    using System.IdentityModel.Tokens;

제거:

                app.UseWindowsAzureActiveDirectoryBearerAuthentication(
    new WindowsAzureActiveDirectoryBearerAuthenticationOptions
    {
    Audience = ConfigurationManager.AppSettings["ida:Audience"],
    Tenant = ConfigurationManager.AppSettings["ida:Tenant"]
    });

추가 합니다.

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

|매개|설명
|--------|--------
|ValidAudience|이렇게 하면 '관객' 값 구성 하는 여부를 검사 토큰
|ValidIssuer|이렇게 하면 구성 하는 가치에 ' 토큰에서 검사는 발행인이
|MetadataEndpoint|이 STS의 메타 데이터 정보 가리키는

## <a name="add-application-configuration-for-ad-fs"></a>Adfs 응용 프로그램 구성 추가
아래와 같이 appsettings를 변경 합니다.

    <appSettings>
    <add key="ida:Audience" value="https://localhost:44326/" />
    <add key="ida:AdfsMetadataEndpoint" value="https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml" />
    <add key="ida:Issuer" value="https://fs.contoso.com/adfs" />
      </appSettings>

## <a name="running-the-solution"></a>실행 하는 해결 방법
새로 솔루션을 솔루션을 다시 작성 하 고 실행 합니다. 자세한 추적 표시 하려는 경우 Fiddler을 실행 하 고 암호를 해독 HTTPS를 사용 하도록 설정 합니다.

브라우저에서 SPA 로드 됩니다 하 고 다음 화면이 나타납니다 합니다.

![클라이언트 등록](media/Single-Page-Application-with-AD-FS/singleapp3.PNG)

로그인을 클릭 합니다.  작업 목록 인증 흐름을 트리거하 및 ADAL JS ADFS 인증 안내해

![로그인](media/Single-Page-Application-with-AD-FS/singleapp4a.PNG)

Fiddler # 조각에 URL의 일환으로 반환 되 고 토큰을 확인할 수 있습니다.

![Fiddler](media/Single-Page-Application-with-AD-FS/singleapp5a.PNG)

이제 작업 목록 항목에 로그인 한 사용자에 대 한 추가 하는 API 백 엔드 호출할 수 있습니다.

![Fiddler](media/Single-Page-Application-with-AD-FS/singleapp6.PNG)

## <a name="next-steps"></a>다음 단계
[광고 FS 개발](../../ad-fs/AD-FS-Development.md)  
