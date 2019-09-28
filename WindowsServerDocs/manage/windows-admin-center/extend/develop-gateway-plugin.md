---
title: 게이트웨이 플러그 인 개발
description: 게이트웨이 플러그 인 Windows 관리 센터 SDK 개발 (Project Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 2b096b226190ad1ca3fd07c38b7b939d019ee30f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406937"
---
# <a name="develop-a-gateway-plugin"></a>게이트웨이 플러그 인 개발

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows 관리 센터 게이트웨이 플러그 인을 사용 하면 도구 또는 솔루션의 UI에서 대상 노드로 API를 통신할 수 있습니다.  Windows 관리 센터는 대상 노드에서 실행할 게이트웨이 플러그 인의 명령과 스크립트를 릴레이 하는 게이트웨이 서비스를 호스팅합니다. 게이트웨이 서비스는 기본 프로토콜 이외의 프로토콜을 지 원하는 사용자 지정 게이트웨이 플러그 인을 포함 하도록 확장할 수 있습니다.

이러한 게이트웨이 플러그 인은 기본적으로 Windows 관리 센터에 포함 되어 있습니다.

* PowerShell 게이트웨이 플러그 인
* WMI 게이트웨이 플러그 인

REST를 사용 하는 경우와 같이 PowerShell 또는 WMI 이외의 프로토콜을 사용 하 여 통신 하려면 고유한 게이트웨이 플러그 인을 빌드할 수 있습니다.  게이트웨이 플러그 인은 기존 게이트웨이 프로세스와는 별개의 AppDomain에 로드 되지만 동일한 권한 상승 수준을 사용 합니다.

> [!NOTE]
> 다른 확장 형식에 익숙하지 않나요? [확장성 아키텍처 및 확장 형식](understand-extensions.md)에 대해 자세히 알아보세요.

## <a name="prepare-your-environment"></a>사용자 환경 준비

아직 설치 하지 않은 경우 모든 프로젝트에 필요한 종속성 및 전역 필수 구성 요소를 설치 하 여 [환경을 준비](prepare-development-environment.md) 합니다.

## <a name="create-a-gateway-plugin-c-library"></a>게이트웨이 플러그 인 만들기 (C# 라이브러리)

사용자 지정 게이트웨이 플러그 인을 만들려면 ```Microsoft.ManagementExperience.FeatureInterfaces``` C# 네임 스페이스에서 ```IPlugIn``` 인터페이스를 구현 하는 새 클래스를 만듭니다.  

> [!NOTE]
> 이전 버전의 SDK에서 사용할 수 있는 ```IFeature``` 인터페이스는 이제 사용 되지 않는 것으로 플래그가 지정 됩니다.  모든 게이트웨이 플러그 인 개발에서는 IPlugIn (또는 선택적으로 HttpPlugIn 추상 클래스)를 사용 해야 합니다.

### <a name="download-sample-from-github"></a>GitHub에서 샘플 다운로드

사용자 지정 게이트웨이 플러그 인을 빠르게 시작 하려면 Windows 관리 센터 SDK [GitHub 사이트](https://aka.ms/wacsdk)에서 [샘플 C# 플러그 인 프로젝트](https://github.com/Microsoft/windows-admin-center-sdk/tree/master/GatewayPluginExample/Plugin) 의 복사본을 복제 하거나 다운로드할 수 있습니다.

### <a name="add-content"></a>콘텐츠 추가

사용자 지정 Api를 포함 하도록 [ C# 샘플 플러그 인 프로젝트](https://github.com/Microsoft/windows-admin-center-sdk/tree/master/GatewayPluginExample/Plugin) 프로젝트의 복제 된 복사본에 새 콘텐츠를 추가 하 고 다음 단계에서 사용할 사용자 지정 게이트웨이 플러그 인 DLL 파일을 빌드합니다.

### <a name="deploy-plugin-for-testing"></a>테스트용 플러그 인 배포

Windows 관리 센터 게이트웨이 프로세스에 로드 하 여 사용자 지정 게이트웨이 플러그 인 DLL을 테스트 합니다.

Windows 관리 센터는 System.environment.specialfolder 열거형의 CommonApplicationData 값을 사용 하 여 현재 컴퓨터의 응용 프로그램 데이터 폴더에 있는 ```plugins``` 폴더의 모든 플러그 인을 찾습니다. Windows 10에서이 위치는 ```C:\ProgramData\Server Management Experience```입니다.  @No__t-0 폴더가 아직 존재 하지 않는 경우 폴더를 직접 만들 수 있습니다.

> [!NOTE]
> "StaticsFolder" 구성 값을 업데이트 하 여 디버그 빌드에서 플러그 인 위치를 재정의할 수 있습니다. 로컬로 디버깅 하는 경우이 설정은 데스크톱 솔루션의 app.config에 있습니다. 

플러그 인 폴더 내부 (이 예제에서는 ```C:\ProgramData\Server Management Experience\plugins```)

* 사용자 지정 게이트웨이 플러그 인 DLL에서 ```Feature```의 ```Name``` 속성 값과 같은 이름으로 새 폴더를 만듭니다 (샘플 프로젝트에서 ```Name```는 "Sample Uno").
* 사용자 지정 게이트웨이 플러그 인 DLL 파일을이 새 폴더에 복사 합니다.
* Windows 관리 센터 프로세스 다시 시작

Windows 관리자 프로세스가 다시 시작 된 후에는 ```http(s)://{domain|localhost}/api/nodes/{node}/features/{feature name}/{identifier}```에 대 한 GET, PUT, PATCH, DELETE 또는 POST를 실행 하 여 사용자 지정 게이트웨이 플러그 인 DLL에서 Api를 실행할 수 있습니다.

### <a name="optional-attach-to-plugin-for-debugging"></a>선택 사항: 디버깅을 위해 플러그 인에 연결

Visual Studio 2017의 디버그 메뉴에서 "프로세스에 연결"을 선택 합니다. 다음 창에서 사용 가능한 프로세스 목록을 스크롤하여 SMEDesktop를 선택 하 고 "연결"을 클릭 합니다. 디버거를 시작 하면 기능 코드에 중단점을 배치한 다음 위의 URL 형식을 통해 연습을 수행할 수 있습니다. 샘플 프로젝트의 경우 (기능 이름: "Sample Uno": URL은 "<http://localhost:6516/api/nodes/fake-server.my.domain.com/features/Sample%20Uno>"입니다.

## <a name="create-a-tool-extension-with-the-windows-admin-center-cli"></a>Windows 관리 센터 CLI를 사용 하 여 도구 확장 만들기 ##

이제 사용자 지정 게이트웨이 플러그 인을 호출할 수 있는 도구 확장을 만들어야 합니다.  프로젝트 파일을 저장 하려는 폴더를 만들거나 찾은 다음 명령 프롬프트를 열고 해당 폴더를 작업 디렉터리로 설정 합니다.  이전에 설치 된 Windows 관리 센터 CLI를 사용 하 여 다음 구문을 사용 하 여 새 확장을 만듭니다.

```
wac create --company "{!Company Name}" --tool "{!Tool Name}"
```

| 값 | 설명 | 예제 |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | 회사 이름 (공백 포함) | ```Contoso Inc``` |
| ```{!Tool Name}``` | 도구 이름 (공백 포함) | ```Manage Foo Works``` |

사용 예제는 다음과 같습니다.

```
wac create --company "Contoso Inc" --tool "Manage Foo Works"
```

그러면 도구에 대해 지정한 이름을 사용 하 여 현재 작업 디렉터리 내에 새 폴더가 만들어지고, 필요한 모든 템플릿 파일을 프로젝트에 복사 하 고, 회사 및 도구 이름을 사용 하 여 파일을 구성 합니다.  

그런 다음, 디렉터리를 앞에서 만든 폴더로 변경 하 고 다음 명령을 실행 하 여 필요한 로컬 종속성을 설치 합니다.

```
npm install
```

이 작업이 완료 되 면 Windows 관리 센터에 새 확장을 로드 하는 데 필요한 모든 항목을 설정 했습니다. 

## <a name="connect-your-tool-extension-to-your-custom-gateway-plugin"></a>사용자 지정 게이트웨이 플러그 인에 도구 확장 연결

이제 Windows 관리 센터 CLI를 사용 하 여 확장을 만들었으므로 다음 단계를 수행 하 여 사용자 지정 게이트웨이 플러그 인에 도구 확장을 연결할 준비가 되었습니다.

- [빈 모듈](guides/add-module.md) 추가
- 도구 확장에서 [사용자 지정 게이트웨이 플러그 인](guides/use-custom-gateway-plugin.md) 사용
 
## <a name="build-and-side-load-your-extension"></a>확장을 빌드하고 로드 합니다.

다음으로 Windows 관리 센터에 확장을 빌드하고 로드 합니다.  명령 창을 열고 디렉터리를 원본 디렉터리로 변경한 다음 빌드할 준비가 되었습니다.

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

## <a name="target-a-different-version-of-the-windows-admin-center-sdk"></a>다른 버전의 Windows 관리 센터 SDK를 대상으로 합니다.

SDK 변경 및 플랫폼 변경으로 확장을 최신 상태로 유지 하는 것은 쉽습니다.  [다른 버전](target-sdk-version.md) 의 Windows 관리 센터 SDK를 대상으로 하는 방법을 참조 하세요.