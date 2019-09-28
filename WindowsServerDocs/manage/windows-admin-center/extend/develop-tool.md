---
title: 도구 확장 개발
description: 도구 확장 Windows 관리 센터 SDK 개발 (Project Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: de2cbf3a47771555eef02cd7d18f93b2b33227b3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406905"
---
# <a name="develop-a-tool-extension"></a>도구 확장 개발

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

도구 확장은 사용자가 서버 또는 클러스터와 같은 연결을 관리 하기 위해 Windows 관리 센터와 상호 작용 하는 기본 방법입니다. Windows 관리 센터 홈 화면에서 연결을 클릭 하 고 연결 하면 왼쪽 탐색 창에 도구 목록이 표시 됩니다. 도구를 클릭 하면 도구 확장이 로드 되어 오른쪽 창에 표시 됩니다.

도구 확장이 로드 되 면 대상 서버 또는 클러스터에서 WMI 호출 또는 PowerShell 스크립트를 실행 하 고 UI에 정보를 표시 하거나 사용자 입력에 따라 명령을 실행할 수 있습니다. 도구 확장은 표시 되는 솔루션을 정의 하 여 각 솔루션에 대 한 다양 한 도구 집합을 생성 합니다.

> [!NOTE]
> 다른 확장 형식에 익숙하지 않나요? [확장성 아키텍처 및 확장 형식](understand-extensions.md)에 대해 자세히 알아보세요.

## <a name="prepare-your-environment"></a>사용자 환경 준비

아직 설치 하지 않은 경우 모든 프로젝트에 필요한 종속성 및 전역 필수 구성 요소를 설치 하 여 [환경을 준비](prepare-development-environment.md) 합니다.

## <a name="create-a-new-tool-extension-with-the-windows-admin-center-cli"></a>Windows 관리 센터 CLI를 사용 하 여 새 도구 확장 만들기 ##

모든 종속성이 설치 되 면 새 도구 확장을 만들 준비가 된 것입니다.  프로젝트 파일이 포함 된 폴더를 만들거나 찾은 다음 명령 프롬프트를 열고 해당 폴더를 작업 디렉터리로 설정 합니다.  이전에 설치 된 Windows 관리 센터 CLI를 사용 하 여 다음 구문을 사용 하 여 새 확장을 만듭니다.

``` cmd
wac create --company "{!Company Name}" --tool "{!Tool Name}"
```

| 값 | 설명 | 예제 |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | 회사 이름 (공백 포함) | ```Contoso Inc``` |
| ```{!Tool Name}``` | 도구 이름 (공백 포함) | ```Manage Foo Works``` |

사용 예제는 다음과 같습니다.

``` cmd
wac create --company "Contoso Inc" --tool "Manage Foo Works"
```

그러면 도구에 대해 지정한 이름을 사용 하 여 현재 작업 디렉터리 내에 새 폴더가 만들어지고, 필요한 모든 템플릿 파일을 프로젝트에 복사 하 고, 회사 및 도구 이름을 사용 하 여 파일을 구성 합니다.  

그런 다음, 디렉터리를 앞에서 만든 폴더로 변경 하 고 다음 명령을 실행 하 여 필요한 로컬 종속성을 설치 합니다.

``` cmd
npm install
```

이 작업이 완료 되 면 Windows 관리 센터에 새 확장을 로드 하는 데 필요한 모든 항목을 설정 했습니다. 

## <a name="add-content-to-your-extension"></a>확장에 콘텐츠 추가

이제 Windows 관리 센터 CLI를 사용 하 여 확장을 만들었으므로 콘텐츠를 사용자 지정할 준비가 되었습니다.  수행할 수 있는 작업에 대 한 예제는 다음 가이드를 참조 하세요.

- [빈 모듈](guides/add-module.md) 추가
- [IFrame](guides/add-iframe.md) 추가
 
[GITHUB SDK 사이트](https://aka.ms/wacsdk)에서 더 많은 예제를 찾을 수 있습니다.
-  [개발자 도구](https://github.com/Microsoft/windows-admin-center-sdk/tree/master/windows-admin-center-developer-tools) 은 Windows 관리 센터에 테스트용으로 로드할 수 있는 완전히 작동 하는 확장 이며, 사용자 고유의 확장에서 찾아보고 사용할 수 있는 다양 한 샘플 기능 모음 및 도구 예제를 포함 하 고 있습니다.

## <a name="customize-your-extensions-icon"></a>확장 아이콘 사용자 지정

도구 목록에서 확장에 대해 표시 되는 아이콘을 사용자 지정할 수 있습니다.  이렇게 하려면 확장에 대해 ```manifest.json```의 모든 ```icon``` 항목을 수정 합니다.

``` json
"icon": "{!icon-uri}",
```

| 값 | 설명 | 예제 uri |
| ----- | ----------- | ------- |
| ```{!icon-uri}``` | 아이콘 리소스의 위치 | ```assets/foo-icon.svg``` |

참고: 현재 개발 모드에서 확장을 로드 하는 경우 사용자 지정 아이콘은 표시 되지 않습니다.  해결 방법으로 다음과 같이 ```target```의 내용을 제거 합니다.

``` json
"target": "",
```

이 구성은 개발 모드에서의 테스트용 로드에만 유효 하므로 ```target```에 포함 된 값을 유지 한 다음 확장을 게시 하기 전에 복원 하는 것이 중요 합니다.

## <a name="build-and-side-load-your-extension"></a>확장을 빌드하고 로드 합니다.

다음으로 Windows 관리 센터에 확장을 빌드하고 로드 합니다.  명령 창을 열고 디렉터리를 원본 디렉터리로 변경한 다음 빌드할 준비가 되었습니다.

* Gulp로 빌드 및 제공:

    ``` cmd
    gulp build
    gulp serve -p 4201
    ```

현재 사용되지 않는 포트를 선택해야 합니다. Windows Admin Center를 실행하는 포트를 사용하지 마십시오.

테스트를 위해 로컬로 제공되는 프로젝트를 Windows Admin Center에 연결하여 사용자 프로젝트는 Windows Admin Center의 로컬 인스턴스에 사이드로드할 수 있습니다.

* 웹 브라우저에서 Windows Admin Center 실행
* 디버거 열기(F12)
* 콘솔을 열고 다음 명령을 입력합니다.

    ``` cmd
    MsftSme.sideLoad("http://localhost:4201")
    ```

*   웹 브라우저를 새로 고침

그러면 사용자 프로젝트가 이름 옆에 있는 (사이드로드된) 도구 목록에 표시됩니다.

## <a name="target-a-different-version-of-the-windows-admin-center-sdk"></a>다른 버전의 Windows 관리 센터 SDK를 대상으로 합니다.

SDK 변경 및 플랫폼 변경으로 확장을 최신 상태로 유지 하는 것은 쉽습니다.  [다른 버전](target-sdk-version.md) 의 Windows 관리 센터 SDK를 대상으로 하는 방법을 참조 하세요.