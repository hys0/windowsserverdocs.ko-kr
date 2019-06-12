---
title: 네이티브 클라이언트 OAuth 공용 클라이언트를 사용 하 여 AD FS 2016을 사용 하 여 응용 프로그램 또는 이후 빌드
description: 공용 클라이언트 OAuth 및 AD FS 2016을 사용 하 여 응용 프로그램 이상 네이티브 클라이언트를 작성 하는 지침을 제공 하는 연습
author: billmath
ms.author: billmath
ms.reviewer: anandy
manager: mtillman
ms.date: 07/17/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: active-directory-federation-services
ms.openlocfilehash: 15bb6f1e39f64ff19ebb5515188ee944e277d3b7
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445482"
---
# <a name="build-a-native-client-application-using-oauth-public-clients-with-ad-fs-2016-or-later"></a>네이티브 클라이언트 OAuth 공용 클라이언트를 사용 하 여 AD FS 2016을 사용 하 여 응용 프로그램 또는 이후 빌드

## <a name="overview"></a>개요

이 문서에는 이상 AD FS 2016에서 보호 된 Web API를 사용 하 여 상호 작용 하는 네이티브 응용 프로그램을 빌드하는 방법을 보여 줍니다.

1. .NET TodoListClient WPF 응용 프로그램에서 Active Directory 인증 라이브러리 (ADAL)를 사용 하 여 OAuth 2.0 프로토콜을 통해 Azure Active Directory (Azure AD)에서 JWT 액세스 토큰을 가져오려면
2. 액세스 토큰은 TodoListService web API의 /todolist 였습니다. 그리고 끝점을 호출할 때 사용자를 인증 하는 전달자 토큰으로 사용 됩니다.
 에서는 여기에서 Azure AD에 대 한 응용 프로그램 예제를 사용 하 여 되며 다음 AD FS 2016 이상에 대 한 수정 합니다.

![응용 프로그램 개요](media/native-client-with-ad-fs-2016/appoverview.png)

## <a name="pre-requisites"></a>필수 구성 요소
이 문서를 완료 하기 전에 필요한 필수 구성 요소 목록은 다음과 같습니다. 이 문서는 AD FS 설치 되어 있고 AD FS 팜에 만들어진 가정 합니다.

* GitHub 클라이언트 도구
* AD FS Windows Server 2016 이상
* Visual Studio 2013 이상

## <a name="creating-the-sample-walkthrough"></a>이 연습에서는 샘플 만들기

### <a name="create-the-application-group-in-ad-fs"></a>AD FS에서 응용 프로그램 그룹을 만들려면

1. AD FS 관리에서 마우스 오른쪽 단추로 클릭 **응용 프로그램 그룹** 선택한 **응용 프로그램 그룹 추가**합니다.

2. 응용 프로그램 그룹 마법사에서 이름에 대 한 사용자가 원하는 이름 예: NativeToDoListAppGroup를 입력 합니다. 선택 된 **web API에 액세스 하는 네이티브 응용 프로그램** 템플릿. **다음**을 클릭합니다.
 ![응용 프로그램 그룹 추가](media/native-client-with-ad-fs-2016/addapplicationgroup1.png)

3. 에 **네이티브 응용 프로그램** 페이지에서 AD FS에서 생성 된 식별자를 확인 합니다. AD FS에서 공용 클라이언트 앱을 인식 하는 데는 id입니다. 복사는 **클라이언트 식별자** 값입니다. 나중에 대 한 값으로 사용 됩니다 **ida: ClientId** 응용 프로그램 코드에서입니다. 원하는 경우 여기에 모든 사용자 지정 식별자를 지정할 수 있습니다. 리디렉션 URI가 있는 임의의 값 예제에서는 put https://ToDoListClient ![네이티브 앱](media/native-client-with-ad-fs-2016/addapplicationgroup2.png)

4. 에 **Web API 구성** 페이지, 웹 API에 대 한 식별자 값을 설정 합니다. 이 예제에서는이 값 이어야 합니다는 **SSL URL** 웹 앱은 실행 중 이어야 할 위치. 솔루션의 TooListServer 프로젝트의 속성을 클릭 하 여이 값을 가져올 수 있습니다. 으로 나중에 사용 됩니다 합니다 **todo:TodoListResourceId** 값 **App.config** 네이티브 클라이언트 응용 프로그램 및 파일을 **todo:TodoListBaseAddress**합니다.
![Web API](media/native-client-with-ad-fs-2016/addapplicationgroup3.png)

5. 통해 이동 합니다 **액세스 제어 정책을 적용** 및 **응용 프로그램 사용 권한 구성** 위치에서 기본값을 사용 하 여 합니다. 요약 페이지는 다음과 같이 표시 됩니다.
![요약](media/native-client-with-ad-fs-2016/addapplicationgroupsummary.png)

다음을 클릭 하 고 마법사를 완료 합니다.

### <a name="add-the-nameidentifier-claim-to-the-list-of-claims-issued"></a>NameIdentifier 클레임 발급 된 클레임 목록에 추가
데모 응용 프로그램에서 다양 한 위치에서 NameIdentifier 클레임 값을 사용합니다. Azure AD와 달리 AD FS 기본적으로 NameIdentifier 클레임을 발급 하지 않습니다. 따라서 응용 프로그램에 올바른 값을 사용할 수 있도록 NameIdentifier 클레임을 실행 하는 클레임 규칙을 추가 해야 합니다. 이 예제에서는 지정 된 이름은 사용자의 사용자 토큰의 NameIdentifier 값으로 발급 됩니다.
클레임 규칙을 구성 하려면 방금 만든 응용 프로그램 그룹을 열고 Web API를 두 번 클릭 합니다. 발급 변환 규칙 탭을 선택 하 고 규칙 추가 단추를 클릭 합니다. 클레임 규칙의 유형에 사용자 지정 클레임 규칙을 선택 하 고 아래 표시 된 대로 클레임 규칙을 추가 합니다.

```  
c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"]
 => issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier"), query = ";givenName;{0}", param = c.Value);
```

![NameIdentifier 클레임 규칙](media/native-client-with-ad-fs-2016/addnameidentifierclaimrule.png)

### <a name="modify-the-application-code"></a>응용 프로그램 코드를 수정 합니다.

이 섹션에서는 웹 API 샘플을 다운로드 하 고 Visual Studio에서 수정 하는 방법을 설명 합니다.   Azure AD 된 샘플을 사용 합니다 [여기](https://github.com/Azure-Samples/active-directory-dotnet-native-desktop)합니다.  

샘플 프로젝트를 다운로드 하려면 Git Bash를 사용 하 고 다음을 입력 합니다.  

```  
git clone https://github.com/Azure-Samples/active-directory-dotnet-native-desktop  
```  

#### <a name="modify-todolistclient"></a>Modify ToDoListClient

솔루션에서이 프로젝트는 네이티브 클라이언트 응용 프로그램을 나타냅니다. 클라이언트 응용 프로그램 알고 있는지 확인 해야 합니다.

1. 사용자가 필요한 경우 인증 어 려는 위치
2. 인증 기관 (AD FS)을 제공 해야 해당 클라이언트 ID는 무엇입니까?
3. 액세스 토큰을 요청 하는 리소스의 ID 란?
4. Web API의 기준 주소는 무엇입니까?

네이티브 클라이언트 응용 프로그램에 위의 정보를 얻으려면 다음 코드 변경 내용이 필요 합니다.

**App.config**

* 키를 추가 **ida: 기관** AD FS 서비스를 나타내는 값을 사용 하 여 합니다. 예를 들어 IPv4 주소를 사용하는 경우 https://fs.contoso.com/adfs/
* 수정할 **ida: ClientId** 에서 값을 사용 하 여 키 **클라이언트 식별자** 에 **네이티브 응용 프로그램** AD FS에서 응용 프로그램 그룹을 만드는 동안 페이지입니다. 예를 들어 3f07368b-6efd-4f50-a330-d93853f4c855
* 수정 합니다 **todo:todo:TodoListResourceId** 의 값으로 **식별자** 에 **웹 API 구성** AD FS에서 응용 프로그램 그룹을 만드는 동안 페이지. 예를 들어 IPv4 주소를 사용하는 경우 https://localhost:44321/
* 수정 합니다 **todo:TodoListBaseAddress** 의 값으로 **식별자** 에 **웹 API 구성** AD FS에서 응용 프로그램 그룹을 만드는 동안 페이지. 예를 들어 IPv4 주소를 사용하는 경우 https://localhost:44321/
* 값을 설정할 **ida: RedirectUri** 의 값으로 **리디렉션 URI** 에 **네이티브 응용 프로그램** AD FS에서 응용 프로그램 그룹을 만드는 동안 페이지입니다. 예를 들어 IPv4 주소를 사용하는 경우 https://ToDoListClient
* 읽기 쉽도록 제거 / 키에 대 한 주석 수 있습니다 **ida: 테 넌 트** 하 고 **ida: AADInstance**합니다.

  ![앱 구성](media/native-client-with-ad-fs-2016/app_configfile.PNG)


**MainWindow.xaml.cs**

* 아래와 같이 aadInstance에 대 한 줄을 주석

        // private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];

* 아래와 같이 기관에 대 한 값을 추가 합니다.

        private static string authority = ConfigurationManager.AppSettings["ida:Authority"];

* 만들기에 대 한 줄을 삭제 합니다 **기관** aadInstance 및 테 넌 트의 값

        private static string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);

* 함수의 **MainWindow**, authContext 인스턴스화를 변경 합니다.

        authContext = new AuthenticationContext(authority,false);

    ADAL 기관으로 AD FS를 유효성 검사 지원 하지 않으며 따라서 validateAuthority 매개 변수에 대 한 값이 false 플래그를 전달 해야 합니다.

  ![주 창](media/native-client-with-ad-fs-2016/mainwindow.PNG)

#### <a name="modify-todolistservice"></a>TodoListService를 수정 합니다.
두 파일에는 Web.config 및 Startup.Auth.cs이이 프로젝트에서 변경 해야합니다. 매개 변수의 올바른 값을 얻으려면 Web.Config 변경 해야 합니다. Startup.Auth.cs 변경 내용은 Azure AD를 사용 하지 않고 AD FS에 대해 인증 하 여 WebAPI를 설정 해야 합니다.

**Web.config**

* 키 주석 **ida: 테 넌 트** 필요 하지 않은 것으로
* 키를 추가 합니다 **ida: 기관** 페더레이션 FQDN을 나타내는 값을 사용 하 여 서비스, 예 https://fs.contoso.com/adfs/
* 키를 수정 **ida: 대상** 에 지정 된 웹 API 식별자의 값을 **웹 API 구성** AD FS에서 응용 프로그램 그룹을 추가 하는 동안 페이지.
* 키 추가 **ida: AdfsMetadataEndpoint** 의 AD FS 페더레이션 메타 데이터 URL로 해당 값을 사용 하 여 서비스에 대 한 예: https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml

![웹 구성](media/native-client-with-ad-fs-2016/webconfig.PNG)


**Startup.Auth.cs**

아래와 같이 ConfigureAuth 함수 수정

    public void ConfigureAuth(IAppBuilder app)
    {
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
    }

기본적으로, AD FS를 사용 하 여 추가 메타 데이터를 AD FS에 대 한 정보를 제공 하 고 토큰 유효성 검사 인증을 구성 하는 것, 대상 그룹 클레임에는 웹 API에 필요한 값 이어야 합니다.
응용 프로그램 실행

1. Nativeclient-dotnet 솔루션을 마우스 오른쪽 단추로 클릭 하 고 속성으로 이동 합니다. 여러 개의 시작 프로젝트에 아래 표시 된 것 처럼 시작 프로젝트를 변경 하 고 시작 TodoListClient와 TodoListService를 설정 합니다.
![솔루션 속성](media/native-client-with-ad-fs-2016/solutionproperties.png)

2.  F5 키를 누르거나 디버그 선택 > 메뉴에서 계속 합니다. 네이티브 응용 프로그램과 WebAPI 시작 됩니다. 네이티브 응용 프로그램에서 로그인 단추를 클릭할 고 팝업 대화형 로그온 AD AL에서 AD FS 서비스 리디렉션됩니다. 유효한 사용자의 자격 증명을 입력 합니다.
![Sign-in](media/native-client-with-ad-fs-2016/sign-in.png)

이 단계에서는 네이티브 응용 프로그램이 AD fs 및 웹 API에 대 한 ID 토큰 및 액세스 토큰을 가져왔습니다.

3. 입력을을 텍스트 상자에 항목 추가 항목을 클릭 합니다. 이 단계에서는 응용 프로그램에 도달 추가 하는 웹 API는 할 일 항목 및이 위해 AD FS에서 얻은 WebAPI에 액세스 토큰을 제공 합니다. Web API는 토큰에 대 한 것 이며 페더레이션 메타 데이터에서 정보를 사용 하 여 토큰 서명을 확인 되도록 대상 값을 찾습니다.

![로그인](media/native-client-with-ad-fs-2016/clienttodoadd.png)

## <a name="next-steps"></a>다음 단계
[AD FS 개발](../../ad-fs/AD-FS-Development.md)  
