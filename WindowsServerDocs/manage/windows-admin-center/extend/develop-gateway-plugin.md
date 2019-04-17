---
title: 게이트웨이 플러그 인 개발
description: 게이트웨이 플러그 인 Windows Admin Center SDK (Project Honolulu) 개발
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 93cee5b8e3611a264119947103d22d9aa3b9a56b
ms.sourcegitcommit: be0144eb59daf3269bebea93cb1c467d67e2d2f1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/20/2018
ms.locfileid: "4081160"
---
# 게이트웨이 플러그 인 개발

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows Admin Center 게이트웨이 플러그 인 API의에서 커뮤니케이션을 UI 도구 또는 솔루션의 대상 노드에 수 있습니다.  Windows Admin Center 대상 노드에서 실행 되는 명령 및 게이트웨이 플러그 인에서 스크립트를 릴레이 하는 게이트웨이 서비스를 호스트 합니다. 게이트웨이 서비스는 기본 스타일 이외의 프로토콜을 지 원하는 사용자 지정 게이트웨이 플러그 인을 포함 하도록 확장할 수 있습니다.

이러한 게이트웨이 플러그 인 Windows Admin Center를 사용 하 여 기본적으로 포함 됩니다.

* PowerShell 게이트웨이 플러그 인
* WMI 게이트웨이 플러그 인

PowerShell 또는 WMI 아닌 프로토콜와 통신 하려는 경우와 같은 나머지를 작성할 수 있습니다 고유한 게이트웨이 플러그 인 합니다.  게이트웨이 플러그 인 기존 게이트웨이 프로세스에서 별도 AppDomain에 로드 되지만 권리에 대 한 권한 상승 동일한 수준을 사용 합니다.

> [!NOTE]
> 익숙하지 다른 확장 형식? [확장성 아키텍처 및 확장 형식](understand-extensions.md)에 대해 알아봅니다.

## 사용자 환경 준비

아직, 모든 프로젝트에 필요한 전역 필수 구성 요소 및 종속성을 설치 하 여 [환경을 준비](prepare-development-environment.md) 를 합니다.

## 게이트웨이 플러그 인 (C# 라이브러리) 만들기

사용자 지정 게이트웨이 플러그 인을 만들려면 새 클래스를 만듭니다 C#을 구현 하는 ```IPlugIn``` 에서 인터페이스는 ```Microsoft.ManagementExperience.FeatureInterfaces``` 네임 스페이스 합니다.  

> [!NOTE]
> ```IFeature``` 인터페이스는 SDK의 이전 버전에서 사용할 수 있는 플래그가 지정 사용 되지 않는 것입니다.  모든 게이트웨이 플러그 인 개발 IPlugIn (또는 선택적으로 HttpPlugIn 추상 클래스)를 사용 해야 합니다.

### GitHub에서 샘플을 다운로드 합니다.

사용자 지정 게이트웨이 플러그 인을 사용 하 여 빠르게 시작 하려면 복제 수도 있고 Windows Admin Center SDK [GitHub 사이트](https://aka.ms/wacsdk)에서 [플러그 인 샘플 C# 프로젝트](https://github.com/Microsoft/windows-admin-center-sdk/tree/master/GatewayPluginExample/Plugin) 의 복사본을 다운로드할 수 있습니다.

### 콘텐츠 추가

새 콘텐츠 복제 사본을 사용자 지정 Api를 포함 하도록 [플러그 인 샘플 C# 프로젝트](https://github.com/Microsoft/windows-admin-center-sdk/tree/master/GatewayPluginExample/Plugin) 프로젝트 (또는 프로젝트)를 추가 하 고 단계에서 사용 하도록 사용자 지정 게이트웨이 플러그 인 DLL 파일을 작성할 합니다.

### 배포 테스트를 위해 플러그 인

Windows Admin Center 게이트웨이 프로세스에 로드 하 여 사용자 지정 게이트웨이 플러그 DLL을 테스트 합니다.

Windows Admin Center에서 모든 플러그 인을 찾고는 ```plugins``` (Environment.SpecialFolder 열거형의 CommonApplicationData 값 사용) 현재 컴퓨터의 응용 프로그램 데이터 폴더에 폴더. Windows 10에서이 위치는 ```C:\ProgramData\Server Management Experience```.  하는 경우는 ```plugins``` 폴더 아직, 폴더를 직접 만들 수 있습니다.

> [!NOTE]
> "StaticsFolder" 구성 값을 업데이트 하 여 디버그 빌드에서 플러그 인 위치를 재정의할 수 있습니다. 로컬로 디버깅 하는 경우 데스크톱 솔루션의 App.Config에서이 설정이 이루어집니다. 

플러그 인 폴더 안에 (이 예제에서는 ```C:\ProgramData\Server Management Experience\plugins```)

* 동일한 이름으로 새 폴더를 만듭니다 합니다 ```Name``` 속성 값이는 ```Feature``` 에 사용자 지정 게이트웨이 플러그 인 DLL에 (우리의 샘플 프로젝트에는 ```Name``` "샘플 Uno"는)
* 이 새 폴더를 사용자 지정 게이트웨이 플러그 인 DLL 파일을 복사 합니다.
* Windows Admin Center 프로세스를 다시 시작

GET를 실행 하 여 사용자 지정 게이트웨이 플러그 DLL의에서 Api를 실행 하는 수 있게 됩니다 Windows Admin 프로세스를 다시 시작한 후 배치, 패치, 삭제 또는에 게시 ```http(s)://{domain|localhost}/api/nodes/{node}/features/{feature name}/{identifier}```

### 선택 사항: 디버깅에 대 한 플러그 인에 연결

Visual Studio 2017 디버그 메뉴에서 "프로세스에 연결"를 선택 합니다. 다음 창에서 SMEDesktop.exe, 사용 가능한 프로세스 목록을 스크롤할 선택한 "연결"을 클릭 합니다. 한 번 디버거 시작 기능 코드와 위의 URL 형식을 통해 다음 연습에서 중단점을 배치할 수 있습니다. 샘플 프로젝트에 대 한 (기능 이름: "샘플 Uno")의 URL은: "http://localhost:6516/api/nodes/fake-server.my.domain.com/features/Sample%20Uno"

## Windows Admin Center CLI를 사용 하 여 도구 확장 만들기 ##

이제 사용자 지정 게이트웨이 플러그를 호출할 수 있는 도구 확장을 만드는 해야 합니다.  만들거나 프로젝트 파일을 저장 하 고 명령 프롬프트를 열고 작업 디렉터리와 해당 폴더를 설정 하려는 폴더로 이동 합니다.  이전에 설치 된 Windows Admin Center CLI를 사용 하 여 다음 구문을 사용 하 여 새로운 확장을 만듭니다.

```
wac create --company "{!Company Name}" --tool "{!Tool Name}"
```

| 값 | 설명 | 예 |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | 회사 이름 (공백 포함) | ```Contoso Inc``` |
| ```{!Tool Name}``` | 사용자 도구 이름 (공백 포함) | ```Manage Foo Works``` |

사용 예제는 다음과 같습니다.

```
wac create --company "Contoso Inc" --tool "Manage Foo Works"
```

이 도구에 대해 지정한, 모든 필요한 템플릿 파일을 프로젝트에 복사 하 고 회사 및 도구 이름의 파일을 구성 이름을 사용 하 여 현재 작업 디렉터리 내에 새 폴더를 만듭니다.  

다음으로 방금 만든 폴더로 디렉터리를 변경한 후 다음 명령을 실행 하 여 필요한 로컬 종속성 설치:

```
npm install
```

이 완료 되 면 Windows Admin Center에 새로운 확장을 로드 하는 데 필요한 모든 설정을 마쳤으니 합니다. 

## 도구 확장에 사용자 지정 게이트웨이 플러그 인에 연결

확장 Windows Admin Center CLI를 사용 하 여 만든 했으므로 다음 단계를 수행 하 여 사용자 지정 게이트웨이 플러그 도구 확장 연결할 준비가 되었습니다.

- [빈 모듈](guides\add-module.md) 추가
- 도구 확장에서 [사용자 지정 게이트웨이 플러그 인](guides\use-custom-gateway-plugin.md) 을 사용 합니다.
 
## 빌드 및 사이드 로드 확장

다음으로 빌드 및 사이드 Windows Admin Center에는 확장을 로드 합니다.  명령 창을 열고, 빌드할 준비가 되었습니다. 그런 다음 원본 디렉터리에 디렉터리를 변경 합니다.

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

## Windows Admin Center SDK의 다른 버전을 대상으로 지정

확장 SDK와 변경 내용이 플랫폼을 사용 하 여 최신 상태로 유지 하는 것은 쉽습니다.  Windows Admin Center SDK의 [다른 버전을 대상](target-sdk-version.md) 하는 방법에 대해 알아봅니다.