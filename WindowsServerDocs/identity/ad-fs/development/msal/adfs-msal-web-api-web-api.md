---
title: 웹 API를 호출 하는 AD FS MSAL Web API (시나리오 대신)
description: 다른 Web API를 호출 하는 Web API를 빌드하는 방법을 알아봅니다.
author: billmath
ms.author: billmath
manager: daveba
ms.date: 08/09/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 106262b63b5aad0eddb08618eb808d2d9ff5b425
ms.sourcegitcommit: b7f55949f166554614f581c9ddcef5a82fa00625
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/18/2019
ms.locfileid: "71407804"
---
# <a name="scenario-web-api-calling-web-api-on-behalf-of-scenario"></a>시나리오: web api를 호출 하는 web api (시나리오 대신) 
> 적용 대상: AD FS 2019 이상 
 
사용자를 대신 하 여 다른 웹 API를 호출 하는 Web API를 빌드하는 방법에 대해 알아봅니다.  
 
이 문서를 읽기 전에 [AD FS 개념과](../ad-fs-openid-connect-oauth-concepts.md) [Behalf_Of 흐름](../../overview/ad-fs-openid-connect-oauth-flows-scenarios.md#on-behalf-of-flow) 에 대해 잘 알고 있어야 합니다.

## <a name="overview"></a>개요 


- 클라이언트 (웹 앱)-아래 다이어그램에 표시 되지 않고 보호 된 웹 API를 호출 하 고 "Authorization" Http 헤더에 JWT 전달자 토큰을 제공 합니다. 
- 보호 된 웹 API는 토큰의 유효성을 검사 하 고 MSAL [AcquireTokenOnBehalfOf](https://docs.microsoft.com/en-us/dotnet/api/microsoft.identitymodel.clients.activedirectory.authenticationcontext.acquiretokenasync?view=azure-dotnet#Microsoft_IdentityModel_Clients_ActiveDirectory_AuthenticationContext_AcquireTokenAsync_System_String_Microsoft_IdentityModel_Clients_ActiveDirectory_ClientCredential_Microsoft_IdentityModel_Clients_ActiveDirectory_UserAssertion_) 메서드를 사용 하 여 다른 토큰을 요청 (AD FS) 하 여 사용자 대신 두 번째 웹 api (다운스트림 웹 api)를 호출할 수 있도록 합니다. 
- 보호 된 웹 API는이 토큰을 사용 하 여 다운스트림 API를 호출 합니다. AcquireTokenSilentlater를 호출 하 여 다른 다운스트림 Api에 대 한 토큰을 요청할 수도 있습니다 (동일한 사용자를 대신 하 여). AcquireTokenSilent는 필요한 경우 토큰을 새로 고칩니다.  
 
     ![개요](media/adfs-msal-web-api-web-api/webapi1.png)
 
ADFS의 인증 시나리오를 대신 하 여를 구성 하는 방법을 더 잘 이해 하려면 [여기](https://github.com/microsoft/adfs-sample-msal-dotnet-webapi-to-webapi-onbehalfof) 에 제공 된 샘플을 사용 하 고 앱 등록 및 코드 구성 단계를 연습 하겠습니다.  
 
## <a name="pre-requisites"></a>필수 구성 요소 

- GitHub 클라이언트 도구 
- AD FS 2019 이상 구성 되어 실행 되 고 있습니다. 
- Visual Studio 2013 이상 
 
## <a name="app-registration-in-ad-fs"></a>AD FS에서 앱 등록 

이 섹션에서는 네이티브 앱을 공용 클라이언트 및 웹 Api를의 RP (신뢰 당사자)로 등록 하는 방법을 보여 줍니다 AD FS 

  1. AD FS 관리에서 **응용 프로그램 그룹** 을 마우스 오른쪽 단추로 클릭 하 고 **응용 프로그램 그룹 추가**를 선택 합니다.  
  
  2. 응용 프로그램 그룹 마법사에서 **이름** 에 **WebApiToWebApi** 를 입력 하 고 **클라이언트-서버 응용 프로그램** 에서 **웹 API 템플릿에 액세스 하는 네이티브 응용 프로그램** 을 선택 합니다. **다음**을 클릭합니다.

      ![앱 등록](media/adfs-msal-web-api-web-api/webapi2.png)

  3. 복사는 **클라이언트 식별자** 값입니다. 이 파일은 나중에 응용 프로그램의 **app.config** 파일에서 **ClientId** 의 값으로 사용 됩니다. **리디렉션 URI:**  - https://ToDoListClient에 대해 다음을 입력 합니다. **추가**를 클릭합니다. **다음**을 클릭합니다. 
  
      ![앱 등록](media/adfs-msal-web-api-web-api/webapi3.png)
  
  4. 웹 API 구성 화면에서 https://localhost:44321/**식별자** 를 입력 합니다. **추가**를 클릭합니다. **다음**을 클릭합니다. 이 값은 응용 프로그램의 **app.config** 및 **web.config** 파일에서 나중에 사용 됩니다.  
 
      ![앱 등록](media/adfs-msal-web-api-web-api/webapi4.png)

  5. Access Control 정책 적용 화면에서 **Everyone 허용** 을 선택 하 고 **다음**을 클릭 합니다. 
  
      ![앱 등록](media/adfs-msal-web-api-web-api/webapi5.png)  

  6. 응용 프로그램 사용 권한 구성 화면에서 **openid connect** 및 **user_impersonation**를 선택 합니다. **다음**을 클릭합니다.  
  
      ![앱 등록](media/adfs-msal-web-api-web-api/webapi6.png)  

  7. 요약 화면에서 **다음**을 클릭 합니다. 

  8. 완료 화면에서 **닫기**를 클릭 합니다. 


  9. AD FS 관리에서 **응용 프로그램 그룹** 을 클릭 하 고 **WebApiToWebApi** 응용 프로그램 그룹을 선택 합니다. 마우스 오른쪽 단추를 클릭하고 **속성**을 선택합니다. 
  
      ![앱 등록](media/adfs-msal-web-api-web-api/webapi7.png)  

  10. WebApiToWebApi 속성 화면에서 **응용 프로그램 추가**...를 클릭 합니다. 
  
      ![앱 Reg](media/adfs-msal-web-api-web-api/webapi8.png)

  11. 독립 실행형 응용 프로그램에서 **서버 응용 프로그램**을 선택 합니다.  
  
      ![앱 Reg](media/adfs-msal-web-api-web-api/webapi9.png)

  12. 서버 응용 프로그램 화면에서 https://localhost:44321/를 **클라이언트 식별자** 및 **리디렉션 URI**로 추가 합니다. 
  
      ![앱 Reg](media/adfs-msal-web-api-web-api/webapi10.png)

  13. 응용 프로그램 자격 증명 구성 화면에서 **공유 암호 생성**을 선택 합니다. 나중에 사용 하기 위해 암호를 복사 합니다.
  
      ![앱 Reg](media/adfs-msal-web-api-web-api/webapi11.png)

  14. 요약 화면에서 **다음**을 클릭 합니다. 

  15. 완료 화면에서 **닫기**를 클릭 합니다. 

  16. AD FS 관리에서 **응용 프로그램 그룹** 을 클릭 하 고 **WebApiToWebApi** 응용 프로그램 그룹을 선택 합니다. 마우스 오른쪽 단추를 클릭하고 **속성**을 선택합니다. 
  
      ![앱 Reg](media/adfs-msal-web-api-web-api/webapi12.png)

  17. WebApiToWebApi 속성 화면에서 **응용 프로그램 추가**...를 클릭 합니다. 
  
      ![앱 Reg](media/adfs-msal-web-api-web-api/webapi13.png)

  18. 독립 실행형 응용 프로그램에서 **WEB API**를 선택 합니다. 
  
      ![앱 Reg](media/adfs-msal-web-api-web-api/webapi14.png)  

  19. 웹 API 구성에서 **식별자**로 https://localhost:44300을 추가 합니다.  
  
      ![앱 Reg](media/adfs-msal-web-api-web-api/webapi15.png)

  20. Access Control 정책 적용 화면에서 **Everyone 허용** 을 선택 하 고 **다음**을 클릭 합니다. 
  
      ![앱 Reg](media/adfs-msal-web-api-web-api/webapi16.png)

  21. 응용 프로그램 사용 권한 구성 화면에서 **다음**을 클릭 합니다. 
  
      ![앱 Reg](media/adfs-msal-web-api-web-api/webapi17.png)

  22. 요약 화면에서 **다음**을 클릭 합니다.

  23. 완료 화면에서 **닫기**를 클릭 합니다.  

  24. WebApiToWebApi – Web API 2 속성 화면에서 확인을 클릭 합니다.  

  25. WebApiToWebApi 속성 화면에서 **WebApiToWebApi – WEB API** 를 선택 하 고 **편집 ...** 을 클릭 합니다.  
  
      ![앱 Reg](media/adfs-msal-web-api-web-api/webapi18.png)

  26. WebApiToWebApi – Web API 속성 화면에서 **발급 변환 규칙** 탭을 선택 하 고 **규칙 추가**...를 클릭 합니다. 
  
      ![앱 Reg](media/adfs-msal-web-api-web-api/webapi19.png)

  27. 변환 클레임 규칙 추가 마법사에서 드롭다운에서 **사용자 지정 규칙을 사용 하 여 클레임 보내기** 를 선택 하 고 **다음**을 클릭 합니다. 
  
      ![앱 Reg](media/adfs-msal-web-api-web-api/webapi20.png)

  28. **클레임 규칙 이름:** 필드 및 **x: [] = > issue (클레임 = x),** 사용자 지정 규칙의 클레임 규칙: 필드에 **PassAllClaims** 를 입력 하 고 마침을 클릭 합니다.  
   
      ![앱 Reg](media/adfs-msal-web-api-web-api/webapi21.png)

  29. WebApiToWebApi – Web API 속성 화면에서 확인을 클릭 합니다.

  30. WebApiToWebApi 속성 화면에서 WebApiToWebApi – Web API 2를 선택 하 고 편집 ...을 클릭 합니다.</br> 
  ![앱 Reg](media/adfs-msal-web-api-web-api/webapi22.png)

  31. WebApiToWebApi – Web API 2 속성 화면에서 발급 변환 규칙 탭을 선택 하 고 규칙 추가 ...를 클릭 합니다. 

  32. 변환 클레임 규칙 추가 마법사에서 dopdown의 사용자 지정 규칙을 사용 하 여 클레임 보내기를 선택 하 고 다음 ![앱 Reg를 클릭](media/adfs-msal-web-api-web-api/webapi23.png)

  33. 클레임 규칙 이름: 필드 및 **x: [] = > issue (클레임 = x),** **사용자 지정 규칙** 의 클레임 규칙: 필드에 PassAllClaims를 입력 하 고 **마침**을 클릭 합니다.  
   
      ![앱 Reg](media/adfs-msal-web-api-web-api/webapi24.png)

  34.  WebApiToWebApi – Web API 2 속성 화면에서 확인을 클릭 한 다음 WebApiToWebApi 속성 화면에서 확인을 클릭 합니다.  
 

## <a name="code-configuration"></a>코드 구성 

이 섹션에서는 Web API를 구성 하 여 다른 Web API를 호출 하는 방법을 보여 줍니다. 

  1. [여기](https://github.com/microsoft/adfs-sample-msal-dotnet-webapi-to-webapi-onbehalfof) 에서 샘플을 다운로드 합니다.  
  
  2. Visual Studio를 사용 하 여 샘플 열기 
  
  3. App.config 파일을 엽니다. 다음을 수정 합니다. 
       - ida: Authority- https://[your AD FS hostname]/adfs/를 입력 합니다.
       - ida: ClientId-위의 AD FS 섹션에서 앱 등록의 #3 값을 입력 합니다. 
       - ida: RedirectUri-위의 AD FS 섹션에서 앱 등록의 #3 값을 입력 합니다. 
       - todo: TodoListResourceId – 위의 AD FS 섹션에서 앱 등록 #4의 식별자 값을 입력 합니다. 
       - ida: todo: TodoListBaseAddress-위의 AD FS 섹션에서 앱 등록의 #4에서 식별자 값을 입력 합니다. 
      
            ![앱 Reg](media/adfs-msal-web-api-web-api/webapi25.png)

  4. ToDoListService 아래에서 web.config 파일을 엽니다. 다음을 수정 합니다. 
       - ida: 대상-위의 AD FS 섹션에서 앱 등록 #12의 클라이언트 식별자 값을 입력 합니다.
       - ida: ClientId-위의 AD FS 섹션에서 앱 등록 #12의 클라이언트 식별자 값을 입력 합니다. 
       - Ida: ClientSecret-위의 AD FS 섹션에서 앱 등록의 #13 복사 된 공유 비밀을 입력 합니다.
       - ida: RedirectUri-위의 AD FS 섹션에서 앱 등록의 #12에서 RedirectUri 값을 입력 합니다. 
       - ida: AdfsMetadataEndpoint-enter https://[your AD FS hostname]/federationmetadata/2007-06/federationmetadata.xml 
       - ida: OBOWebAPIBase-위의 AD FS 섹션에서 앱 등록의 #19에서 식별자 값을 입력 합니다. 
       - ida: Authority- https://[your AD FS hostname]/ds를 입력 합니다. 
  
          ![앱 Reg](media/adfs-msal-web-api-web-api/webapi26.png) 

 5. WebAPIOBO 아래에서 web.config 파일을 엽니다. 다음을 수정 합니다. 
       - ida: AdfsMetadataEndpoint-enter https://[your AD FS hostname]/federationmetadata/2007-06/federationmetadata.xml 
       - ida: 대상-위의 AD FS 섹션에서 앱 등록 #12의 클라이언트 식별자 값을 입력 합니다. 
 
          ![앱 Reg](media/adfs-msal-web-api-web-api/webapi27.png)
 
## <a name="test-the-sample"></a>샘플 테스트 

이 섹션에서는 위에서 구성한 샘플을 테스트 하는 방법을 보여 줍니다. 

코드가 변경 되 면 솔루션을 다시 빌드합니다. 
 
  1. Visual Studio에서 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **시작 프로젝트 설정** ...을 선택 합니다. 
      
      ![앱 Reg](media/adfs-msal-web-api-web-api/webapi28.png)

  2. 속성 페이지에서 TodoListSPA를 제외 하 고 각 프로젝트에 대해 **작업** 이 **시작** 으로 설정 되어 있는지 확인 합니다.  
  
      ![앱 Reg](media/adfs-msal-web-api-web-api/webapi29.png)
  
  3. Visual Studio 위쪽에서 녹색 화살표를 클릭 합니다.  
  
      ![앱 Reg](media/adfs-msal-web-api-web-api/webapi30.png)

  4. 네이티브 앱의 주 화면에서 **로그인**을 클릭 합니다. 
  
      ![앱 Reg](media/adfs-msal-web-api-web-api/webapi31.png)

     네이티브 앱 화면이 표시 되지 않으면 프로젝트 리포지토리가 시스템에 저장 된 폴더에서 * msalcache. bin 파일을 검색 하 여 제거 합니다. 
  
  5. AD FS 로그인 페이지로 리디렉션될 수 있습니다. 계속 해 서 로그인 합니다. 
  
      ![앱 Reg](media/adfs-msal-web-api-web-api/webapi32.png)

  6. 로그인 한 후 **에는 할 일 항목 만들기**에서 web Api to Web api 호출을 입력 합니다. **항목 추가**를 클릭 합니다.  이렇게 하면 web api (할 일 목록 서비스)를 호출 하 여 Web API 2 (WebAPIOBO)를 호출 하 고 캐시에 항목을 추가 합니다.  
 
      ![앱 Reg](media/adfs-msal-web-api-web-api/webapi33.png)
 
 ## <a name="next-steps"></a>다음 단계
[AD FS OpenID Connect/OAuth 흐름 및 애플리케이션 시나리오](../../overview/ad-fs-openid-connect-oauth-flows-scenarios.md)
 
 
