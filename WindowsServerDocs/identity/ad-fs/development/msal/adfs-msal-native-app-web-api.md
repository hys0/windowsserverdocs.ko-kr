---
title: Web API를 호출 하는 AD FS MSAL 네이티브 앱
description: MSAL library를 사용 하 여 웹 Api를 호출 하는 AD FS 2019으로 인증 된 네이티브 앱 로그인 사용자를 빌드하는 방법을 알아봅니다.
author: billmath
ms.author: billmath
manager: daveba
ms.date: 08/09/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 8b27097ac64f981343c1d455c826fa1b9004133e
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2020
ms.locfileid: "75949580"
---
# <a name="scenario-native-app-calling-web-api"></a>시나리오: Web API를 호출 하는 네이티브 앱 
>적용 대상: AD FS 2019 이상 
 
[Msal library](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet/wiki) 를 사용 하 여 웹 api를 호출 하는 AD FS 2019에서 인증 된 네이티브 앱 로그인 사용자를 빌드하는 방법에 대해 알아봅니다.  
 
이 문서를 읽기 전에 [AD FS 개념](../ad-fs-openid-connect-oauth-concepts.md) 및 [인증 코드 부여 흐름](../../overview/ad-fs-openid-connect-oauth-flows-scenarios.md#authorization-code-grant-flow) 에 대해 잘 알고 있어야 합니다.
 
## <a name="overview"></a>개요 
 
 ![개요](media/adfs-msal-native-app-web-api/native1.png)

이 흐름에서는 네이티브 앱 (공용 클라이언트)에 인증을 추가 하 여 사용자를 로그인 하 고 Web API를 호출할 수 있습니다. 사용자를 로그인 하는 네이티브 앱에서 Web API를 호출 하려면 MSAL의 [AcquireTokenInteractive](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.ipublicclientapplication.acquiretokeninteractive?view=azure-dotnet#Microsoft_Identity_Client_IPublicClientApplication_AcquireTokenInteractive_System_Collections_Generic_IEnumerable_System_String__) token 취득 메서드를 사용할 수 있습니다. 이 상호 작용을 설정하기 위해 MSAL은 웹 브라우저를 활용합니다. 

 
액세스 토큰을 대화형으로 얻기 위해 ADFS에서 네이티브 앱을 구성 하는 방법을 더 잘 이해 하려면 [여기](https://github.com/microsoft/adfs-sample-msal-dotnet-native-to-webapi) 에 제공 된 샘플을 사용 하 고 앱 등록 및 코드 구성 단계를 연습 하겠습니다.  
 

## <a name="pre-requisites"></a>필수 구성 요소 


- GitHub 클라이언트 도구 
- AD FS 2019 이상 구성 되어 실행 되 고 있습니다. 
- Visual Studio 2013 이상 
 

## <a name="app-registration-in-ad-fs"></a>AD FS에서 앱 등록 
이 섹션에서는에서 네이티브 앱을 공용 클라이언트 및 웹 API로 등록 하는 방법을 보여 줍니다 AD FS 

  1. **AD FS 관리**에서 **응용 프로그램 그룹** 을 마우스 오른쪽 단추로 클릭 하 고 **응용 프로그램 그룹 추가**를 선택 합니다.   
  
  2. 응용 프로그램 그룹 마법사에서 **이름** 에 **NativeAppToWebApi** 를 입력 하 고 **클라이언트-서버 응용 프로그램** 에서 **웹 API 템플릿에 액세스 하는 네이티브 응용 프로그램** 을 선택 합니다. 클릭 하 여 **다음**.  
  
      ![앱 Reg](media/adfs-msal-native-app-web-api/native2.png)  

  3. 복사는 **클라이언트 식별자** 값입니다. 이 파일은 나중에 응용 프로그램의 **app.config** 파일에서 **ClientId** 의 값으로 사용 됩니다. **리디렉션 URI:** https://ToDoListClient 에 대해 다음을 입력 합니다. **추가**를 클릭합니다. 클릭 하 여 **다음**.  
 
     ![앱 Reg](media/adfs-msal-native-app-web-api/native3.png) 

  4. 웹 API 구성 화면에서 https://localhost:44321/**식별자** 를 입력 합니다. **추가**를 클릭합니다. 클릭 하 여 **다음**. 이 값은 응용 프로그램의 **app.config** 및 **web.config** 파일에서 나중에 사용 됩니다.
 
     ![앱 Reg](media/adfs-msal-native-app-web-api/native4.png)   
  
  5. Access Control 정책 적용 화면에서 **Everyone 허용** 을 선택 하 고 **다음**을 클릭 합니다. 
  
     ![앱 Reg](media/adfs-msal-native-app-web-api/native5.png)   
  
  6. 응용 프로그램 사용 권한 구성 화면에서 **openid connect** 이 선택 되어 있는지 확인 하 고 **다음**을 클릭 합니다.  
     
     ![앱 Reg](media/adfs-msal-native-app-web-api/native6.png) 

  7. 요약 화면에서 **다음**을 클릭 합니다.
  
  8. 완료 화면에서 **닫기**를 클릭 합니다. 
  
  9. AD FS 관리에서 **응용 프로그램 그룹** 을 클릭 하 고 **NativeAppToWebApi** 응용 프로그램 그룹을 선택 합니다. 마우스 오른쪽 단추를 클릭하고 **속성**을 선택합니다.
  
      ![앱 Reg](media/adfs-msal-native-app-web-api/native7.png)

  10. NativeAppToWebApi 속성 화면에서 **WEB api** 아래의 **NATIVEAPPTOWEBAPI – web api** 를 선택 하 고 **편집 ...** 을 클릭 합니다. 
  
      ![앱 Reg](media/adfs-msal-native-app-web-api/native8.png) 

  11. NativeAppToWebApi – Web API 속성 화면에서 **발급 변환 규칙** 탭을 선택 하 고 **규칙 추가** ...를 클릭 합니다. 
  
      ![앱 Reg](media/adfs-msal-native-app-web-api/native9.png) 

  12. 변환 클레임 규칙 추가 마법사에서 **클레임 규칙 템플릿에서** **들어오는 클레임 변환** : 드롭다운을 선택 하 고 **다음**을 클릭 합니다.  
  
      ![앱 Reg](media/adfs-msal-native-app-web-api/native10.png) 

  13. **클레임 규칙 이름:** 필드에 **NameID** 를 입력 합니다. **들어오는 클레임 유형:** , **보내는 클레임 유형에** 대 한 **이름 id** 및 **나가는 이름 id 형식**에 대 한 **일반 이름** **을 선택 합니다** . **마침**을 클릭 합니다.
  
      ![앱 Reg](media/adfs-msal-native-app-web-api/native11.png) 

  14. NativeAppToWebApi – Web API Properties 화면에서 확인을 클릭 한 다음 NativeAppToWebApi Properties 화면을 클릭 합니다.  
 
## <a name="code-configuration"></a>코드 구성 
이 섹션에서는 네이티브 앱을 로그인 사용자로 구성 하 고 웹 API를 호출 하는 토큰을 검색 하는 방법을 보여 줍니다. 

1. [여기](https://github.com/microsoft/adfs-sample-msal-dotnet-native-to-webapi) 에서 샘플을 다운로드 합니다. 

2. Visual Studio를 사용 하 여 샘플 열기 

3. App.config 파일을 엽니다. 다음을 수정 합니다. 
   - ida: Authority- https://[your AD FS hostname]/ds를 입력 합니다.
   - ida: ClientId-위의 AD FS 섹션에서 앱 등록 #3의 **클라이언트 식별자** 값을 입력 합니다. 
   - ida: RedirectUri-위의 AD FS 섹션에서 앱 등록의 #3에서 **리디렉션 uri** 값을 입력 합니다.
   - todo: TodoListResourceId – 위의 AD FS 섹션에서 앱 등록 #4의 **식별자** 값을 입력 합니다. 
   - ida: todo: TodoListBaseAddress-위의 AD FS 섹션에서 앱 등록의 #4에서 **식별자** 값을 입력 합니다. 
 
     ![코드 구성](media/adfs-msal-native-app-web-api/native12.png)

 4. Web.config 파일을 엽니다. 다음을 수정 합니다. 
    - ida: 대상-위의 AD FS 섹션에서 앱 등록의 #4에서 **식별자** 값을 입력 합니다. 
    - ida: AdfsMetadataEndpoint-enter https://[your AD FS hostname]/federationmetadata/2007-06/federationmetadata.xml 
    
      ![코드 구성](media/adfs-msal-native-app-web-api/native13.png)
 
  
## <a name="test-the-sample"></a>샘플 테스트 
이 섹션에서는 위에서 구성한 샘플을 테스트 하는 방법을 보여 줍니다. 

  1. 코드가 변경 되 면 솔루션을 다시 빌드합니다. 
 
  2. Visual Studio에서 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **시작 프로젝트 설정** ...을 선택 합니다.  
 
     ![앱 테스트](media/adfs-msal-native-app-web-api/native14.png)

  3. 속성 페이지에서 각 프로젝트에 대해 **작업** 이 **시작** 으로 설정 되어 있는지 확인 합니다. 
      
     ![앱 테스트](media/adfs-msal-native-app-web-api/native15.png)

  4. Visual Studio 위쪽에서 녹색 화살표를 클릭 합니다.  
 
     ![앱 테스트](media/adfs-msal-native-app-web-api/native16.png)

  5. 네이티브 앱의 주 화면에서 **로그인**을 클릭 합니다.  
  
     ![앱 테스트](media/adfs-msal-native-app-web-api/native17.png)

    네이티브 앱 화면이 표시 되지 않으면 프로젝트 리포지토리가 시스템에 저장 된 폴더에서 * msalcache. bin 파일을 검색 하 여 제거 합니다. 

  6. AD FS 로그인 페이지로 리디렉션될 수 있습니다. 계속 해 서 로그인 합니다. 
  
      ![앱 테스트](media/adfs-msal-native-app-web-api/native18.png)

  7. 로그인 한 후 **에는 할 일 항목 만들기**에서 **웹 Api에 네이티브 앱 빌드를** 입력 합니다. **항목 추가**를 클릭 합니다.  이렇게 하면 **To Do List Service (WEB API)** 가 호출 되 고 캐시에 항목이 추가 됩니다. 
    
       ![앱 테스트](media/adfs-msal-native-app-web-api/native19.png)
 
## <a name="next-steps"></a>다음 단계
[AD FS OpenID Connect/OAuth 흐름 및 애플리케이션 시나리오](../../overview/ad-fs-openid-connect-oauth-flows-scenarios.md)
 