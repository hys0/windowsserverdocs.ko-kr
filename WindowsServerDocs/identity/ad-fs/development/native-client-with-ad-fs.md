---
title: AD FS 2016 이상에서 OAuth 공용 클라이언트를 사용 하 여 네이티브 클라이언트 응용 프로그램 빌드
description: OAuth 공용 클라이언트를 사용 하 여 네이티브 클라이언트 응용 프로그램을 빌드하는 방법 및 2016 이상 AD FS 하는 지침을 제공 하는 연습
author: billmath
ms.author: billmath
ms.reviewer: anandy
manager: mtillman
ms.date: 07/17/2018
ms.topic: article
ms.prod: windows-server
ms.technology: active-directory-federation-services
ms.openlocfilehash: 442aef6daccda2ab3e95690a82f43f642e5a3f73
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358752"
---
# <a name="build-a-native-client-application-using-oauth-public-clients-with-ad-fs-2016-or-later"></a>AD FS 2016 이상에서 OAuth 공용 클라이언트를 사용 하 여 네이티브 클라이언트 응용 프로그램 빌드

## <a name="overview"></a>개요

이 문서에서는 AD FS 2016 이상으로 보호 되는 Web API와 상호 작용 하는 네이티브 응용 프로그램을 빌드하는 방법을 보여 줍니다.

1. .Net TodoListClient WPF 응용 프로그램은 Active Directory 인증 라이브러리 (ADAL)를 사용 하 여 OAuth 2.0 프로토콜을 통해 Azure Active Directory (Azure AD)에서 JWT 액세스 토큰을 가져옵니다.
2. 액세스 토큰은 TodoListService web API의/todolist 끝점을 호출할 때 사용자를 인증 하는 전달자 토큰으로 사용 됩니다.
 여기에서 Azure AD에 대 한 응용 프로그램 예제를 사용 하 고 AD FS 2016 이상에 대해 수정 합니다.

![응용 프로그램 개요](media/native-client-with-ad-fs-2016/appoverview.png)

## <a name="pre-requisites"></a>필수 구성 요소
이 문서를 완료 하기 전에 필요한 필수 구성 요소 목록은 다음과 같습니다. 이 문서는 AD FS 설치 되어 있고 AD FS 팜에 만들어진 가정 합니다.

* GitHub 클라이언트 도구
* Windows Server 2016 이상에서 AD FS
* Visual Studio 2013 이상

## <a name="creating-the-sample-walkthrough"></a>샘플 연습 만들기

### <a name="create-the-application-group-in-ad-fs"></a>AD FS에서 응용 프로그램 그룹 만들기

1. AD FS 관리에서 **응용 프로그램 그룹** 을 마우스 오른쪽 단추로 클릭 하 고 **응용 프로그램 그룹 추가**를 선택 합니다.

2. 응용 프로그램 그룹 마법사에서 이름에 대해 원하는 이름을 입력 합니다 (예: NativeToDoListAppGroup). **웹 API 템플릿에 액세스 하는 네이티브 응용 프로그램** 을 선택 합니다. **다음**을 클릭합니다.
 ![응용 프로그램 그룹 추가](media/native-client-with-ad-fs-2016/addapplicationgroup1.png)

3. **네이티브 응용 프로그램** 페이지에서 AD FS에 의해 생성 된 식별자를 확인 합니다. AD FS에서 공용 클라이언트 앱을 인식 하는 데 사용 하는 id입니다. 복사는 **클라이언트 식별자** 값입니다. 나중에 응용 프로그램 코드에서 **ida: ClientId** 의 값으로 사용 됩니다. 원하는 경우 여기에서 사용자 지정 식별자를 제공할 수 있습니다. 리디렉션 URI는 임의의 값입니다. 예를 들어 네이티브 https://ToDoListClient 앱을 배치 ![ 합니다.](media/native-client-with-ad-fs-2016/addapplicationgroup2.png)

4. **웹 Api 구성** 페이지에서 web api에 대 한 식별자 값을 설정 합니다. 이 예제에서이 값은 웹 앱이 실행 되 고 있는 **SSL URL** 의 값 이어야 합니다. 솔루션에서 TooListServer 프로젝트의 속성을 클릭 하 여이 값을 가져올 수 있습니다. 이는 나중에 native client 응용 프로그램의 **app.config** 파일에서 **todo: TodoListResourceId** 값으로 사용 되 고 **todo: TodoListBaseAddress**로도 사용 됩니다.
![웹 API](media/native-client-with-ad-fs-2016/addapplicationgroup3.png)

5. 기본 값을 사용 하 여 **Access Control 정책 적용** 및 **응용 프로그램 구성 권한** 을 참조 하세요. 요약 페이지는 다음과 같습니다.
![요약](media/native-client-with-ad-fs-2016/addapplicationgroupsummary.png)

다음을 클릭 하 고 마법사를 완료 합니다.

### <a name="add-the-nameidentifier-claim-to-the-list-of-claims-issued"></a>발급 된 클레임 목록에 NameIdentifier 클레임을 추가 합니다.
데모 응용 프로그램은 다양 한 위치에서 NameIdentifier 클레임의 값을 사용 합니다. Azure AD와 달리 AD FS는 기본적으로 NameIdentifier 클레임을 발급 하지 않습니다. 따라서 응용 프로그램에서 올바른 값을 사용할 수 있도록 NameIdentifier 클레임을 발급 하는 클레임 규칙을 추가 해야 합니다. 이 예제에서는 사용자의 지정 된 이름이 토큰의 사용자에 대 한 NameIdentifier 값으로 발급 됩니다.
클레임 규칙을 구성 하려면 앞서 만든 응용 프로그램 그룹을 열고 Web API를 두 번 클릭 합니다. 발급 변환 규칙 탭을 선택한 다음 규칙 추가 단추를 클릭 합니다. 클레임 규칙 유형에서 사용자 지정 클레임 규칙을 선택 하 고 아래와 같이 클레임 규칙을 추가 합니다.

```  
c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"]
 => issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier"), query = ";givenName;{0}", param = c.Value);
```

![NameIdentifier 클레임 규칙](media/native-client-with-ad-fs-2016/addnameidentifierclaimrule.png)

### <a name="modify-the-application-code"></a>응용 프로그램 코드 수정

이 섹션에서는 웹 API 샘플을 다운로드 하 고 Visual Studio에서 수정 하는 방법을 설명 합니다.   Azure AD 된 샘플을 사용 합니다 [여기](https://github.com/Azure-Samples/active-directory-dotnet-native-desktop)합니다.  

샘플 프로젝트를 다운로드 하려면 Git Bash를 사용 하 고 다음을 입력 합니다.  

```  
git clone https://github.com/Azure-Samples/active-directory-dotnet-native-desktop  
```  

#### <a name="modify-todolistclient"></a>ToDoListClient 수정

이 솔루션의 프로젝트는 native client 응용 프로그램을 나타냅니다. 클라이언트 응용 프로그램에서 다음을 인식 하는지 확인 해야 합니다.

1. 필요할 때 사용자를 인증 받기 위해 어디로 이동 해야 하나요?
2. 클라이언트에서 인증 기관 (AD FS)에 제공 해야 하는 ID는 무엇입니까?
3. 액세스 토큰을 요청 하는 리소스의 ID는 무엇 인가요?
4. Web API의 기본 주소는 무엇 인가요?

Native client 응용 프로그램에 위의 정보를 가져오기 위해 다음 코드를 변경 해야 합니다.

**App.config**

* AD FS 서비스를 나타내는 값을 사용 하 여 **ida: Authority** 키를 추가 합니다. 예를 들어 IPv4 주소를 사용하는 경우 https://fs.contoso.com/adfs/
* AD FS에서 응용 프로그램 그룹을 만드는 동안 **네이티브 응용 프로그램** 페이지의 **클라이언트 식별자** 값을 사용 하 여 **ida: ClientId** 키를 수정 합니다. 예: 3f07368b-6efd-4f50-a330-d93853f4c855
* AD FS에서 응용 프로그램 그룹을 만드는 동안 **웹 API 구성** 페이지에서 **식별자** 의 값으로 **todo: todo: TodoListResourceId** 를 수정 합니다. 예를 들어 IPv4 주소를 사용하는 경우 https://localhost:44321/
* AD FS에서 응용 프로그램 그룹을 만드는 동안 **웹 API 구성** 페이지에서 **식별자** 의 값으로 **todo: TodoListBaseAddress** 을 수정 합니다. 예를 들어 IPv4 주소를 사용하는 경우 https://localhost:44321/
* AD FS에서 응용 프로그램 그룹을 만드는 동안 **네이티브 응용 프로그램** 페이지에서 **리디렉션 uri** 값을 사용 하 여 **ida: redirecturi** 값을 설정 합니다. 예를 들어 IPv4 주소를 사용하는 경우 https://ToDoListClient
* 쉽게 읽을 수 있도록 **ida: Tenant** 및 **ida: AADInstance**의 키를 제거/주석으로 처리 하면 됩니다.

  ![앱 구성](media/native-client-with-ad-fs-2016/app_configfile.PNG)


**MainWindow.xaml.cs**

* 아래와 같이 aadInstance에 대 한 줄을 주석으로 처리 합니다.

        // private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];

* 아래와 같이 authority의 값을 추가 합니다.

        private static string authority = ConfigurationManager.AppSettings["ida:Authority"];

* AadInstance 및 테 넌 트에서 **기관** 값을 만들기 위한 줄을 삭제 합니다.

        private static string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);

* **Mainwindow.xaml**함수에서 authcontext 인스턴스화를로 변경 합니다.

        authContext = new AuthenticationContext(authority,false);

    ADAL은 AD FS의 유효성 검사를 권한으로 지원 하지 않으므로 validateAuthority 매개 변수에 대 한 false 값 플래그를 전달 해야 합니다.

  ![기본 창](media/native-client-with-ad-fs-2016/mainwindow.PNG)

#### <a name="modify-todolistservice"></a>TodoListService 수정
이 프로젝트에서는 Web.config 및 Startup.Auth.cs의 두 파일을 변경 해야 합니다. 매개 변수의 올바른 값을 가져오려면 web.config를 변경 해야 합니다. Azure AD가 아닌 AD FS에 대해 인증 하도록 WebAPI를 설정 하려면 Startup.Auth.cs를 변경 해야 합니다.

**Web.config**

* 키 **ida: 테 넌 트** 를 주석으로 처리 합니다.
* 페더레이션 서비스의 FQDN (예:)을 나타내는 값이 포함 된 **ida: Authority** 의 키를 추가 합니다. https://fs.contoso.com/adfs/
* Modify key **ida: 대상 사용자** 는 응용 프로그램 그룹 추가 중에 **웹 api 구성** 페이지에서 지정한 웹 api 식별자의 값을 사용 하 여 AD FS 합니다.
* **Ida: AdfsMetadataEndpoint** AD FS의 페더레이션 메타 데이터 URL에 해당 하는 값을 포함 하는 키를 추가 합니다 (예: https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml

![웹 구성](media/native-client-with-ad-fs-2016/webconfig.PNG)


**Startup.Auth.cs**

ConfigureAuth 함수를 아래와 같이 수정 합니다.

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

기본적으로 AD FS를 사용 하도록 인증을 구성 하 고 AD FS 메타 데이터에 대 한 정보를 추가로 제공 하 고, 토큰의 유효성을 검사 하기 위해 대상 클레임은 Web API에서 예상 하는 값 이어야 합니다.
응용 프로그램 실행

1. 솔루션 NativeClient에서 마우스 오른쪽 단추를 클릭 하 고 속성으로 이동 합니다. 아래와 같이 시작 프로젝트를 여러 개의 시작 프로젝트로 변경 하 고 TodoListClient 및 TodoListService를 모두 시작으로 설정 합니다.
![솔루션 속성](media/native-client-with-ad-fs-2016/solutionproperties.png)

2.  F5 단추를 누르거나 메뉴 모음에서 디버그 > 계속을 선택 합니다. 이렇게 하면 네이티브 응용 프로그램과 WebAPI 모두 시작 됩니다. 네이티브 응용 프로그램에서 로그인 단추를 클릭 하면 AD AL에서 대화형 로그온이 팝업 되 고 AD FS 서비스로 리디렉션됩니다. 유효한 사용자의 자격 증명을 입력 합니다.
![로그인](media/native-client-with-ad-fs-2016/sign-in.png)

이 단계에서는 네이티브 응용 프로그램이 AD FS으로 리디렉션되고 웹 API에 대 한 ID 토큰 및 액세스 토큰을 가져왔습니다.

3. 텍스트 상자에 할 일 항목을 입력 하 고 항목 추가를 클릭 합니다. 이 단계에서 응용 프로그램은 Web API에 도달 하 여 할 일 항목을 추가 하 고,이를 위해 AD FS에서 가져온 WebAPI 액세스 토큰을 표시 합니다. Web API는 대상 값과 일치 하 여 토큰이 대상 인지 확인 하 고 페더레이션 메타 데이터의 정보를 사용 하 여 토큰 서명을 확인 합니다.

![로그인](media/native-client-with-ad-fs-2016/clienttodoadd.png)

## <a name="next-steps"></a>다음 단계
[AD FS 개발](../../ad-fs/AD-FS-Development.md)  
