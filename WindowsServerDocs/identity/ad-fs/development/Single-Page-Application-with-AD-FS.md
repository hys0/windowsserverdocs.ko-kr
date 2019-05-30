---
title: OAuth 및 ADAL을 사용 하 여 단일 페이지 웹 응용 프로그램을 빌드하십시오. AD FS 2016 이상의 버전을 사용 하 여 JS
description: AngularJS를 보안 하 JavaScript 용 ADAL를 사용 하 여 AD FS에 대 한 인증에 대 한 지침을 제공 하는 연습은 기반 단일 페이지 응용 프로그램
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 06/12/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: active-directory-federation-services
ms.openlocfilehash: 24a9caba7a2745973d7c69c3bd7bc42717e7a06c
ms.sourcegitcommit: d84dc3d037911ad698f5e3e84348b867c5f46ed8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66266690"
---
# <a name="build-a-single-page-web-application-using-oauth-and-adaljs-with-ad-fs-2016-or-later"></a>OAuth 및 ADAL을 사용 하 여 단일 페이지 웹 응용 프로그램을 빌드하십시오. AD FS 2016 이상의 버전을 사용 하 여 JS

이 연습에서는 AngularJS를 보호 하는 JavaScript 용 ADAL을 사용 하 여 AD FS에 대 한 인증에 대 한 지침 기반 단일 페이지 응용 프로그램에서 ASP.NET Web API 백 엔드를 사용 하 여 구현 합니다.

이 시나리오에서는 사용자가 로그인 할 때 JavaScript 프런트 엔드 사용 [Active Directory 인증 라이브러리 (ADAL JavaScript 용. JS)](https://github.com/AzureAD/azure-activedirectory-library-for-js) 및 Azure AD에서 ID 토큰 (id_token)을 가져오려면 암시적 권한 부여 합니다. 토큰이 캐시 되 고 클라이언트 연결 요청에 전달자 토큰으로 백 엔드 OWIN 미들웨어를 사용 하 여 보호 되는 웹 api 호출을 수행할 때.

>경고: 여기 빌드할 수 있는 예제는 교육용 으로만입니다. 이러한 지침은 모델의 필수 요소를 노출할 수 가장 간단 하 고 가장 최소한의 구현에 대 한 것입니다. 이 예제에서는 오류 처리의 모든 측면을 포함 하지 않은 하 고 다른 관련 기능입니다.

>[!NOTE]
>이 연습에서는 적용 됩니다 **만** AD FS 서버 2016 이상 

## <a name="overview"></a>개요
이 샘플에서 우리가 만들는 인증 흐름을 백 엔드 WebAPI 리소스에 대 한 액세스를 보호 하려면 AD FS에 대해 단일 페이지 응용 프로그램 클라이언트를 인증 하는 위치입니다. 다음은 전체 인증 흐름


![AD FS 권한 부여](media/Single-Page-Application-with-AD-FS/authenticationflow.PNG)

단일 페이지 응용 프로그램을 사용 하는 경우 사용자가 탐색할 시작 위치에서 페이지 및 JavaScript 파일의 컬렉션을 시작 하는 경우 및 HTML 보기 로드 됩니다. AD FS에 대 한 인증을 보낼 수 있도록는 인증 라이브러리 ADAL (Active Directory) 응용 프로그램에 AD FS 인스턴스 즉, 클라이언트 ID에 대 한 중요 한 정보를 알아야를 구성 해야 합니다.

ADAL 인증에 대 한 트리거를 인식 하는 경우 응용 프로그램에서 제공 하는 정보를 사용 하 고 AD FS STS에 대 한 인증을 보냅니다.  암시적 허용 흐름에 대 한 AD FS에서 공용 클라이언트를 등록 하는 단일 페이지 응용 프로그램을 자동으로 구성 됩니다. #Fragment을 통해 응용 프로그램에 다시 반환 되는 ID 토큰의 권한 부여 요청 결과입니다. 백 엔드에 대 한 추가 호출이 WebAPI WebAPI에 액세스 하는 헤더에서 전달자 토큰으로이 ID 토큰을 전달 됩니다.

## <a name="setting-up-the-development-box"></a>개발 상자를 설정합니다.
이 연습에서는 Visual Studio 2015를 사용합니다. 프로젝트는 ADAL JS 라이브러리를 사용합니다. 읽으십시오 ADAL에 대 한 자세한 [Active Directory 인증 라이브러리.NET.](https://msdn.microsoft.com/library/azure/mt417579.aspx)

## <a name="setting-up-the-environment"></a>환경 설정
이 연습에 대 한 기본 설치를 사용 합니다.

1.  DC: AD FS은 호스트 도메인의 도메인 컨트롤러
2.  AD FS 서버: 도메인에 대 한 AD FS 서버
3.  개발 컴퓨터: 여기서 Visual Studio를 설치 하 고 샘플 개발 컴퓨터

사용할 수 있습니다, 원하는 경우 컴퓨터가 두 대만. DC/AD FS 및 샘플을 개발 하기 위한 기타 하나입니다.

도메인 컨트롤러와 AD FS를 설정 하는 방법이 기사의 범위를 벗어납니다. 추가 배포 정보를 참조 하십시오.

- [AD DS 배포](../../ad-ds/deploy/AD-DS-Deployment.md) 
- [AD FS 배포](../AD-FS-Deployment.md)



## <a name="clone-or-download-this-repository"></a>이 리포지토리 복제 또는 다운로드
AngularJS 단일 페이지 앱에 Azure AD 통합을 수정 하는 것에 대 한 만든 샘플 응용 프로그램 대신 AD FS를 사용 하 여 백 엔드 리소스를 보호 하려면 사용 합니다.

셸 또는 명령줄:

    git clone https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp.git

## <a name="about-the-code"></a>코드에 대 한
키 파일 인증 논리를 포함 하는 다음과 같습니다.

**App.js** -ADAL 모듈 종속성 주입, AAD 사용 하 여 프로토콜 상호 작용을 촉진에 대 한 ADAL에서 사용 되는 앱 구성 값을 제공 및 경로 이전 인증 없이 액세스할 수 없습니다 나타냅니다.

**index.html** -adal.js에 대 한 참조를 포함 합니다.

**HomeController.js**-ADAL의 login () 및 logOut() 메서드를 활용 하는 방법을 보여 줍니다.

**UserDataController.js** -캐시 된 id_token에서 사용자 정보를 추출 하는 방법을 보여 줍니다.

**Startup.Auth.cs** -전달자 인증에 대 한 Active Directory Federation Service를 사용 하 여 WebAPI에 대 한 구성이 포함 되어 있습니다.

## <a name="registering-the-public-client-in-ad-fs"></a>AD FS에서 공용 클라이언트 등록
이 샘플에서는 WebAPI에서 수신 하도록 구성 되어 https://localhost:44326/입니다. 응용 프로그램 그룹 **웹 응용 프로그램에 액세스 하는 웹 브라우저** 암시적 허용 흐름 응용 프로그램을 구성 하는 데 사용할 수 있습니다.

1. AD FS 관리 콘솔을 열고 클릭 **응용 프로그램 그룹 추가**합니다. 에 **응용 프로그램 그룹 추가 마법사** 응용 프로그램, 설명 및 선택의 이름을 입력 합니다 **웹 응용 프로그램에 액세스 하는 웹 브라우저** 템플릿에서 **클라이언트-서버 응용 프로그램** 아래와 같이 섹션

    ![새 응용 프로그램 그룹 만들기](media/Single-Page-Application-with-AD-FS/appgroup_step1.png)

2. 다음 페이지에서 **네이티브 응용 프로그램**응용 프로그램 클라이언트 id를 제공 하 고 아래와 같이 리디렉션 URI

    ![새 응용 프로그램 그룹 만들기](media/Single-Page-Application-with-AD-FS/appgroup_step2.png)

3. 다음 페이지에서 **액세스 제어 정책 적용** 권한으로 둡니다 *모든 사용자 허용*

4. 요약 페이지는 아래와 같아야 합니다.

    ![새 응용 프로그램 그룹 만들기](media/Single-Page-Application-with-AD-FS/appgroup_step3.png)

5. 클릭할 **다음** 응용 프로그램 그룹 추가 완료 하 고 마법사를 닫습니다.

## <a name="modifying-the-sample"></a>이 샘플을 수정합니다.
ADAL JS를 구성 합니다.

엽니다는 **app.js** 파일을 변경 합니다 **adalProvider.init** 정의:

    adalProvider.init(
        {
            instance: 'https://fs.contoso.com/', // your STS URL
            tenant: 'adfs',                      // this should be adfs
            clientId: 'https://localhost:44326/', // your client ID of the
            //cacheLocation: 'localStorage', // enable this for IE, as sessionStorage does not work for localhost.
        },
        $httpProvider
        );

|Configuration|설명
|--------|--------
|instance|STS URL, 예: https://fs.contoso.com/
|테넌트(tenant)|'Adfs'로 유지
|clientID|이 단일 페이지 응용 프로그램에 대 한 공용 클라이언트를 구성 하는 동안 지정 된 클라이언트 ID

## <a name="configure-webapi-to-use-ad-fs"></a>AD FS를 사용 하는 WebAPI를 구성 합니다.
열기는 **Startup.Auth.cs** 샘플에서 파일을 시작 부분에 다음을 추가 합니다. 

    using System.IdentityModel.Tokens;

제거 합니다.

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

|매개 변수|설명
|--------|--------
|ValidAudience|이 구성의 'audience' 값이 검사에 대 한 토큰의
|ValidIssuer|이 구성의 값 ' 토큰에 대 한 확인 되는 발급자
|MetadataEndpoint|이 STS의 메타 데이터 정보를 가리키는

## <a name="add-application-configuration-for-ad-fs"></a>추가 AD FS에 대 한 응용 프로그램 구성
아래와 같이 appsettings를 변경 합니다.

    <appSettings>
    <add key="ida:Audience" value="https://localhost:44326/" />
    <add key="ida:AdfsMetadataEndpoint" value="https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml" />
    <add key="ida:Issuer" value="https://fs.contoso.com/adfs" />
      </appSettings>

## <a name="running-the-solution"></a>솔루션을 실행합니다.
솔루션을 정리 하 고 솔루션을 다시 실행 합니다. 자세한 추적을 보려는 경우 Fiddler를 시작 하 고 HTTPS 암호 해독을 설정 합니다.

브라우저 (Chrome 브라우저 사용)가 SPA를 로드 하 고 다음 화면이 표시 됩니다.

![클라이언트 등록](media/Single-Page-Application-with-AD-FS/singleapp3.PNG)

로그인을 클릭 합니다.  인증 흐름을 트리거할 할 일 목록 및 ADAL JS 인증 AD FS 안내 합니다.

![로그인](media/Single-Page-Application-with-AD-FS/singleapp4a.PNG)

Fiddler에서 # 조각에서 보았듯이 URL의 일부로 반환 되는 토큰을 볼 수 있습니다.

![Fiddler](media/Single-Page-Application-with-AD-FS/singleapp5a.PNG)

이제 백 엔드에 로그인 한 사용자의 할 일 목록 항목을 추가 하는 API를 호출 할 수 있습니다.

![Fiddler](media/Single-Page-Application-with-AD-FS/singleapp6.PNG)

## <a name="next-steps"></a>다음 단계
[AD FS 개발](../../ad-fs/AD-FS-Development.md)  
