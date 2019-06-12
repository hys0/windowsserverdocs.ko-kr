---
title: 게이트웨이 플러그 인 개발
description: 게이트웨이 플러그 인 Windows Admin Center SDK (프로젝트 브라 티) 개발
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 66e36a349fc6bd38a77ccf4f00d380788ea4b422
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445950"
---
# <a name="develop-a-gateway-plugin"></a>게이트웨이 플러그 인 개발

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows Admin Center 게이트웨이 플러그 인 API에서에서 통신을 UI 도구 또는 솔루션의 대상 노드 수 있습니다.  Windows Admin Center 대상 노드에서 실행 될 명령 및 게이트웨이 플러그 인에서 스크립트를 릴레이 하는 게이트웨이 서비스를 호스팅합니다. 게이트웨이 서비스는 기본 색이 아닌 프로토콜을 지 원하는 사용자 지정 게이트웨이 플러그 인을 포함 하도록 확장할 수 있습니다.

이러한 게이트웨이 플러그 인은 Windows Admin Center 사용 하 여 기본적으로 포함 됩니다.

* PowerShell 게이트웨이 플러그 인
* WMI 게이트웨이 플러그 인

PowerShell 또는 WMI 이외의 프로토콜을 사용 하 여 통신 하려는 경우와 같은 REST를 사용 하 여 빌드할 수 있습니다 게이트웨이 플러그 인.  게이트웨이 플러그 인 기존 게이트웨이 프로세스에서 별도 AppDomain에 로드 되지만 권한 같은 권한 상승 수준을 사용 합니다.

> [!NOTE]
> 에 익숙하지 않는 다양 한 확장 형식? 에 대 한 자세한 정보는 [확장성 아키텍처 및 확장 형식](understand-extensions.md)합니다.

## <a name="prepare-your-environment"></a>사용자 환경 준비

이미 않았다면 [환경을 준비](prepare-development-environment.md) 종속성 및 모든 프로젝트에 필요한 전체 필수 구성 요소를 설치 하 여 합니다.

## <a name="create-a-gateway-plugin-c-library"></a>게이트웨이 플러그 인 만들기 (C# 라이브러리)

플러그 인을 사용자 지정 게이트웨이 만들려면 새로 만들기 C# 를 구현 하는 클래스를 ```IPlugIn``` 에서 인터페이스를 ```Microsoft.ManagementExperience.FeatureInterfaces``` 네임 스페이스입니다.  

> [!NOTE]
> ```IFeature``` SDK의 이전 버전에서 사용할 수 있는 인터페이스 플래그가 지정으로 사용 되지 않습니다.  모든 게이트웨이 플러그 인 개발 IPlugIn (또는 필요에 따라 HttpPlugIn 추상 클래스)를 사용 해야 합니다.

### <a name="download-sample-from-github"></a>GitHub에서 샘플을 다운로드 합니다.

사용자 지정 게이트웨이 플러그 인을 사용 하 여 신속 하 게 시작 하려면 복제 또는 다운로드 수 우리의 [샘플 C# 플러그 인 프로젝트](https://github.com/Microsoft/windows-admin-center-sdk/tree/master/GatewayPluginExample/Plugin) Windows Admin Center SDK에서 [GitHub 사이트](https://aka.ms/wacsdk)합니다.

### <a name="add-content"></a>콘텐츠 추가

복제 된 복사본을 새 콘텐츠를 추가 합니다 [샘플 C# 플러그 인 프로젝트](https://github.com/Microsoft/windows-admin-center-sdk/tree/master/GatewayPluginExample/Plugin) 사용자 지정 Api를 포함 하 고 사용자 지정 게이트웨이 플러그 인 DLL을 빌드할 프로젝트 (또는 프로젝트를) 다음 단계에서 사용할 파일입니다.

### <a name="deploy-plugin-for-testing"></a>배포 테스트에 대 한 플러그 인

Windows Admin Center 게이트웨이 프로세스에 로드 하 여 사용자 지정 게이트웨이 플러그 인 DLL을 테스트 합니다.

Windows Admin Center 모든 플러그 인을 찾고를 ```plugins``` (Environment.SpecialFolder 열거형 CommonApplicationData 값 사용) 현재 컴퓨터의 응용 프로그램 데이터 폴더의 폴더입니다. Windows 10에서이 위치는 ```C:\ProgramData\Server Management Experience```합니다.  경우는 ```plugins``` 폴더가 없습니다. 그러나 직접 폴더를 만들 수 있습니다.

> [!NOTE]
> "StaticsFolder" 구성 값을 업데이트 하 여 디버그 빌드에 플러그 인 위치를 재정의할 수 있습니다. 로컬로 디버그 하는 경우이 설정은 데스크톱 솔루션의 App.Config에서입니다. 

플러그 인 폴더 안에 (이 예제에서는 ```C:\ProgramData\Server Management Experience\plugins```)

* 동일한 이름의 새 폴더를 만듭니다는 ```Name``` 속성 값을 ```Feature``` 사용자 지정 게이트웨이 플러그 인 DLL에서 (샘플 프로젝트에서는 ```Name``` "샘플 Uno"는)
* 새 폴더에 사용자 지정 게이트웨이 플러그 인 DLL 파일을 복사 합니다.
* Windows Admin Center 프로세스를 다시 시작

Windows 관리 프로세스를 다시 시작 되 면 GET을 실행 하 여 사용자 지정 게이트웨이 플러그 인 DLL에서 Api를 실행 하는 일을 할 수는 PUT, PATCH, DELETE 또는 게시 ```http(s)://{domain|localhost}/api/nodes/{node}/features/{feature name}/{identifier}```

### <a name="optional-attach-to-plugin-for-debugging"></a>선택 사항: 디버깅에 대 한 플러그 인에 연결

Visual Studio 2017에서 디버그 메뉴에서 "프로세스에 연결"을 선택 합니다. 다음 창에서 사용 가능한 프로세스 목록을 스크롤하여 SMEDesktop.exe를 선택 하 고 "연결"을 클릭 합니다. 한 번 후 디버거를 시작, 기능 코드 및 위의 URL 형식을 통해 다음 연습에서 중단점을 배치할 수 있습니다. 샘플 프로젝트에 대 한 (기능 이름: URL은 "샘플 Uno"): "<http://localhost:6516/api/nodes/fake-server.my.domain.com/features/Sample%20Uno>"

## <a name="create-a-tool-extension-with-the-windows-admin-center-cli"></a>Windows Admin Center CLI를 사용 하 여 도구 확장명 만들기 ##

이제 사용자 지정 게이트웨이 플러그 인을 호출할 수 있습니다 도구 확장을 생성 해야 합니다.  페이지를 만들거나 프로젝트 파일을 저장 하 고 명령 프롬프트를 열고 작업 디렉터리로 해당 폴더를 설정 하려는 폴더를 찾습니다.  이전에 설치 된 Windows Admin Center CLI를 사용 하 여, 다음 구문을 사용 하 여 새 확장을 만듭니다.

```
wac create --company "{!Company Name}" --tool "{!Tool Name}"
```

| 값 | 설명 | 예제 |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | 회사 이름 (공백 포함) | ```Contoso Inc``` |
| ```{!Tool Name}``` | 사용자 도구 이름 (공백 포함) | ```Manage Foo Works``` |

사용 예제는 다음과 같습니다.

```
wac create --company "Contoso Inc" --tool "Manage Foo Works"
```

이 도구에 대해 지정 된 프로젝트에 모든 필요한 템플릿 파일을 복사 및 파일에 회사 이름과 도구를 사용 하 여 구성 이름을 사용 하 여 현재 작업 디렉터리 내에서 새 폴더를 만듭니다.  

방금 만든 폴더로 디렉터리를 변경 합니다. 그런 다음, 다음 명령을 실행 하 여 필요한 로컬 종속성을 설치 합니다.

```
npm install
```

이 완료 되 면 Windows Admin Center 새 확장을 로드 하는 데 필요한 모든 구성 설정 했습니다. 

## <a name="connect-your-tool-extension-to-your-custom-gateway-plugin"></a>도구 확장 사용자 지정 게이트웨이 플러그 인에 연결

Windows Admin Center CLI를 사용 하 여 확장을 만든 했으므로 다음이 단계를 수행 하 여 사용자 지정 게이트웨이 플러그 인에 도구 확장을 연결할 수 있습니다.

- 추가 [빈 모듈](guides/add-module.md)
- 사용 하 여 사용자 [사용자 지정 게이트웨이 플러그 인](guides/use-custom-gateway-plugin.md) 도구 확장의
 
## <a name="build-and-side-load-your-extension"></a>빌드 및 쪽에 확장을 로드합니다.

다음으로 빌드 및 쪽 확장을 Windows Admin Center 로드합니다.  명령 창을 열고, 빌드할 준비가 되었습니다. 그런 다음 원본 디렉터리에 디렉터리를 변경 합니다.

* Gulp로 빌드 및 제공:

    ```
    gulp build
    gulp serve -p 4201
    ```

현재 사용되지 않는 포트를 선택해야 합니다. Windows Admin Center를 실행하는 포트를 사용하지 마십시오.

테스트를 위해 로컬로 제공되는 프로젝트를 Windows Admin Center에 연결하여 사용자 프로젝트는 Windows Admin Center의 로컬 인스턴스에 사이드로드할 수 있습니다.

* 웹 브라우저에서 Windows Admin Center 실행
* 디버거 열기(F12)
* 콘솔을 열고 다음 명령을 입력합니다.

    ```
    MsftSme.sideLoad("http://localhost:4201")
    ```

*   웹 브라우저를 새로 고침

그러면 사용자 프로젝트가 이름 옆에 있는 (사이드로드된) 도구 목록에 표시됩니다.

## <a name="target-a-different-version-of-the-windows-admin-center-sdk"></a>다른 버전의 Windows Admin Center SDK를 대상

확장 SDK 변경 내용 및 플랫폼 변경 내용을 사용 하 여 최신 상태로 유지 하는 것은 쉽습니다.  방법에 대해 알아보세요 [다른 버전을 대상](target-sdk-version.md) Windows Admin Center SDK입니다.