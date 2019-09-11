---
title: 웹 Api를 호출 하는 AD FS MSAL 웹 앱 (서버 앱)
description: AD FS 2019에서 인증 된 웹 앱 로그인 사용자를 빌드하는 방법에 대해 알아봅니다.
author: billmath
ms.author: billmath
manager: daveba
ms.date: 08/09/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 03328ff8c94d96fcf34dcef29ac1a1daefc9d14a
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70867493"
---
# <a name="scenario-web-app-server-app-calling-web-api"></a>시나리오: 웹 앱 (서버 앱) 웹 API 호출 
>적용 대상: AD FS 2019 이상 
 
[Msal library](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet/wiki) 를 사용 하 여 웹 api를 호출 하는 AD FS 2019에서 인증 된 웹 앱 로그인 사용자를 빌드하는 방법에 대해 알아봅니다.  
 
이 문서를 읽기 전에 [AD FS 개념](../ad-fs-openid-connect-oauth-concepts.md) 및 [인증 코드 부여 흐름](../../overview/ad-fs-openid-connect-oauth-flows-scenarios.md#authorization-code-grant-flow) 에 대해 잘 알고 있어야 합니다.
 
## <a name="overview"></a>개요 
 
![Web api를 호출 하는 웹 앱 개요](media/adfs-msal-web-app-web-api/webapp1.png)

이 흐름에서는 웹 앱 (서버 앱)에 인증을 추가 하 여 사용자를 로그인 하 고 web API를 호출할 수 있습니다. 웹 앱에서 Web API를 호출 하려면 MSAL의 [AcquireTokenByAuthorizationCode](https://docs.microsoft.com/en-us/dotnet/api/microsoft.identity.client.acquiretokenbyauthorizationcodeparameterbuilder?view=azure-dotnet) token 취득 메서드를 사용 합니다. 토큰 캐시에 획득 된 토큰을 저장 하는 권한 부여 코드 흐름을 사용 합니다. 그러면 컨트롤러는 필요할 때 캐시에서 자동으로 토큰을 획득 합니다. 필요한 경우 MSAL에서 토큰을 새로 고칩니다. 

웹 Api를 호출 하는 Web Apps: 


- 기밀 클라이언트 응용 프로그램입니다. 
- 따라서 AD FS에 비밀 (응용 프로그램 공유 암호, 인증서 또는 AD 계정)을 등록 했습니다. 이 암호는 토큰을 가져오기 위해 AD FS를 호출 하는 동안 전달 됩니다.  

ADFS에서 웹 앱을 등록 하 고 웹 API를 호출 하는 토큰을 획득 하도록 구성 하는 방법을 더 잘 이해 하려면 [여기](https://github.com/microsoft/adfs-sample-msal-dotnet-webapp-to-webapi) 에 제공 된 샘플을 사용 하 고 앱 등록 및 코드 구성 단계를 연습 하겠습니다.  

 
## <a name="pre-requisites"></a>필수 구성 요소 

- GitHub 클라이언트 도구 
- AD FS 2019 이상 구성 되어 실행 되 고 있습니다. 
- Visual Studio 2013 이상 
 
## <a name="app-registration-in-ad-fs"></a>AD FS에서 앱 등록 
이 섹션에서는 AD FS에서 RP (신뢰 당사자)로 웹 앱을 기밀 클라이언트 및 Web API로 등록 하는 방법을 보여 줍니다. 

  1. AD FS 관리에서 **응용 프로그램 그룹** 을 마우스 오른쪽 단추로 클릭 하 고 **응용 프로그램 그룹 추가**를 선택 합니다.  
  2. 응용 프로그램 그룹 마법사에서 **이름** 에 **WebAppToWebApi** 를 입력 하 고 **클라이언트-서버 응용 프로그램** 에서 **웹 API 템플릿에 액세스 하는 서버 응용 프로그램** 을 선택 합니다. **다음**을 클릭합니다.  
  
      ![응용 프로그램 그룹 추가](media/adfs-msal-web-app-web-api/webapp2.png)
  
  3. 복사는 **클라이언트 식별자** 값입니다. 나중에 응용 프로그램 **web.config** 파일에서 **ida: ClientId** 의 값으로 사용 됩니다. **리디렉션 URI** - 에대해다음을입력합니다. https://localhost:44326 추가를 클릭합니다. **다음**을 클릭합니다. 
  
      ![응용 프로그램 그룹 추가](media/adfs-msal-web-app-web-api/webapp3.png)
  
  4. 응용 프로그램 자격 증명 구성 화면에서 체크 인을 선택 하 여 **공유 암호를 생성** 하 고 암호를 복사 합니다. 이는 나중에 응용 프로그램 **web.config** 파일에서 **ida: ClientSecret** 의 값으로 사용 됩니다. **다음**을 클릭합니다.  
  
      ![응용 프로그램 그룹 추가](media/adfs-msal-web-app-web-api/webapp4.png)
  
  5. 웹 API 구성 화면에서 **식별자** https://webapi 를 입력 합니다. **추가**를 클릭합니다. **다음**을 클릭합니다. 이 값은 나중에 응용 프로그램 **web.config** 파일에서 **Ida: graphresourceid** 에 사용 됩니다. 
  
      ![응용 프로그램 그룹 추가](media/adfs-msal-web-app-web-api/webapp5.png)
  
  6. Access Control 정책 적용 화면에서 everyone **허용** 을 선택 하 고 **다음**을 클릭 합니다. 
  
      ![응용 프로그램 그룹 추가](media/adfs-msal-web-app-web-api/webapp6.png)
  
  7. 응용 프로그램 사용 권한 구성 화면에서 **openid connect** 및 **user_impersonation** 가 선택 되어 있는지 확인 하 고 **다음**을 클릭 합니다. 
  
      ![응용 프로그램 그룹 추가](media/adfs-msal-web-app-web-api/webapp7.png)
  
  8. 요약 화면에서 **다음**을 클릭 합니다. 
  
  9. 완료 화면에서 **닫기**를 클릭 합니다.



## <a name="code-configuration"></a>코드 구성 

이 섹션에서는 로그인 사용자로 ASP.NET 웹 앱을 구성 하 고 Web API를 호출 하는 토큰을 검색 하는 방법을 보여 줍니다. 

  1. [여기](https://github.com/microsoft/adfs-sample-msal-dotnet-webapp-to-webapi) 에서 샘플을 다운로드 합니다.   
  
  2. Visual Studio를 사용 하 여 샘플 열기 
  
  3. Web.config 파일을 엽니다. 다음을 수정 합니다. 
       - ida: ClientId-위의 AD FS 섹션에서 앱 등록 #3의 **클라이언트 식별자** 값을 입력 합니다. 
       - ida: ClientSecret-위의 AD FS 섹션에서 앱 등록의 #4 **비밀** 값을 입력 합니다. 
       - ida: RedirectUri-위의 AD FS 섹션에서 앱 등록의 #3에서 **리디렉션 uri** 값을 입력 합니다. 
       - ida: Authority- https://[your AD FS hostname]/adfs.를 입력 합니다. 예: https://adfs.contoso.com/adfs 
       - ida: 리소스-위의 AD FS 섹션에서 앱 등록의 #5에서 **식별자** 값을 입력 합니다. 
      
          ![응용 프로그램 그룹 추가](media/adfs-msal-web-app-web-api/webapp8.png)
 
 
### <a name="test-the-sample"></a>샘플 테스트 
이 섹션에서는 위에서 구성한 샘플을 테스트 하는 방법을 보여 줍니다. 

  1. 코드가 변경 되 면 솔루션을 다시 빌드합니다. 
  
  2. Visual Studio 맨 위에 있는 Internet Explorer가 선택 되어 있는지 확인 하 고 녹색 화살표를 클릭 합니다. 
  
      ![응용 프로그램 그룹 추가](media/adfs-msal-web-app-web-api/webapp9.png)

  3. 홈 페이지에서 로그인을 클릭 합니다. 
  
      ![응용 프로그램 그룹 추가](media/adfs-msal-web-app-web-api/webapp10.png)

  4. AD FS 로그인 페이지로 리디렉션될 수 있습니다. 계속 해 서 로그인 합니다. 
  
      ![응용 프로그램 그룹 추가](media/adfs-msal-web-app-web-api/webapp11.png)

  5. 로그인 한 후 액세스 토큰을 클릭 합니다.  
  
      ![응용 프로그램 그룹 추가](media/adfs-msal-web-app-web-api/webapp12.png)

  6. 액세스 토큰을 클릭 하면 웹 API를 호출 하 여 액세스 토큰 정보가 수신 됩니다. 
  
      ![응용 프로그램 그룹 추가](media/adfs-msal-web-app-web-api/webapp13.png)
 
 ## <a name="next-steps"></a>다음 단계
[AD FS OpenID Connect/OAuth 흐름 및 애플리케이션 시나리오](../../overview/ad-fs-openid-connect-oauth-flows-scenarios.md)
 