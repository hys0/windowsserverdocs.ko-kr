---
title: 도구 확장 개발
description: 개발 도구 확장 Windows Admin Center SDK (프로젝트 브라 티)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 092a97c1166f1090dd7c556f1ab86d42a1f46ee4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889274"
---
# <a name="develop-a-tool-extension"></a>도구 확장 개발

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

도구 확장에는 서버 또는 클러스터 등의 연결을 관리 하려면 Windows Admin Center 사용 하 여 사용자 상호 작용 하는 기본 방법입니다. Windows Admin Center 홈 화면에서 연결을 클릭 하 고 연결 하는 경우 목록이 왼쪽된 탐색 창에서 도구를 사용 하 여 표시 한 다음 됩니다. 도구를 클릭 하면 도구 확장 로드 되 고 오른쪽 창에 표시 합니다.

도구 확장을 로드 되 면 대상 서버 또는 클러스터에서 WMI 호출 또는 PowerShell 스크립트를 실행 하 및 UI에서 정보를 표시 하거나 사용자 입력을 기반으로 하는 명령을 실행할 수 있습니다 것. 도구 확장 표시할을 다른 각 솔루션에 대 한 도구 집합을 생성 하는 솔루션을 정의 합니다.

> [!NOTE]
> 에 익숙하지 않는 다양 한 확장 형식? 에 대 한 자세한 정보는 [확장성 아키텍처 및 확장 형식](understand-extensions.md)합니다.

## <a name="prepare-your-environment"></a>사용자 환경 준비

이미 않았다면 [환경을 준비](prepare-development-environment.md) 종속성 및 모든 프로젝트에 필요한 전체 필수 구성 요소를 설치 하 여 합니다.

## <a name="create-a-new-tool-extension-with-the-windows-admin-center-cli"></a>Windows Admin Center CLI를 사용 하 여 새 도구 확장명 만들기 ##

설치 된 모든 종속성을 만든 후 새 도구 확장을 만들 준비가 되었습니다.  또는 프로젝트 파일이 포함 된 폴더로 이동, 명령 프롬프트를 열고 만들고 해당 폴더의 작업 디렉터리를 설정 합니다.  이전에 설치 된 Windows Admin Center CLI를 사용 하 여, 다음 구문을 사용 하 여 새 확장을 만듭니다.

``` cmd
wac create --company "{!Company Name}" --tool "{!Tool Name}"
```

| 값 | 설명 | 예제 |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | 회사 이름 (공백 포함) | ```Contoso Inc``` |
| ```{!Tool Name}``` | 사용자 도구 이름 (공백 포함) | ```Manage Foo Works``` |

사용 예제는 다음과 같습니다.

``` cmd
wac create --company "Contoso Inc" --tool "Manage Foo Works"
```

이 도구에 대해 지정 된 프로젝트에 모든 필요한 템플릿 파일을 복사 및 파일에 회사 이름과 도구를 사용 하 여 구성 이름을 사용 하 여 현재 작업 디렉터리 내에서 새 폴더를 만듭니다.  

방금 만든 폴더로 디렉터리를 변경 합니다. 그런 다음, 다음 명령을 실행 하 여 필요한 로컬 종속성을 설치 합니다.

``` cmd
npm install
```

이 완료 되 면 Windows Admin Center 새 확장을 로드 하는 데 필요한 모든 구성 설정 했습니다. 

## <a name="add-content-to-your-extension"></a>확장 프로그램에 콘텐츠 추가

Windows Admin Center CLI를 사용 하 여 확장을 만든 했으므로 콘텐츠를 사용자 지정할 준비가 되었습니다.  수행할 수 있는 예가 다음이 가이드를 참조 하세요.

- 추가 [빈 모듈](guides\add-module.md)
- 추가 [iFrame](guides\add-iframe.md)
 
더 많은 예제를 찾을 수 있습니다 우리의 [GitHub SDK 사이트](https://aka.ms/wacsdk):
-  [개발자 도구](https://github.com/Microsoft/windows-admin-center-sdk/tree/master/windows-admin-center-developer-tools) 는 Windows Admin Center 테스트용으로 로드 될 수 있는 완벽 한 기능의 확장으로, 탐색 하 고 고유한 확장에서 사용할 수 있는 샘플 기능 및 도구 예제가 다양 한 컬렉션을 포함 합니다.

## <a name="customize-your-extensions-icon"></a>확장 프로그램의 아이콘을 사용자 지정

도구 목록에서 확장 프로그램에 대해 표시 되는 아이콘을 사용자 지정할 수 있습니다.  이렇게 하려면 모든 수정 ```icon``` 항목에서 ```manifest.json``` 확장 프로그램에 대해:

``` json
"icon": "{!icon-uri}",
```

| 값 | 설명 | 예제에서는 uri |
| ----- | ----------- | ------- |
| ```{!icon-uri}``` | 아이콘 리소스의 위치 | ```assets/foo-icon.svg``` |

참고: 현재 사용자 지정 아이콘 쪽 개발 모드에서 확장을 로드 하는 경우에 표시 되지 않습니다.  해결 방법으로의 콘텐츠를 제거 ```target``` 다음과 같습니다.

``` json
"target": "",
```

이 구성에만 유효 개발 모드에서 테스트용 로드에 포함 된 값을 유지 해야 하므로 ```target``` 후 확장 프로그램을 게시 하기 전에 복원 합니다.

## <a name="build-and-side-load-your-extension"></a>빌드 및 쪽에 확장을 로드합니다.

다음으로 빌드 및 쪽 확장을 Windows Admin Center 로드합니다.  명령 창을 열고, 빌드할 준비가 되었습니다. 그런 다음 원본 디렉터리에 디렉터리를 변경 합니다.

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

## <a name="target-a-different-version-of-the-windows-admin-center-sdk"></a>다른 버전의 Windows Admin Center SDK를 대상

확장 SDK 변경 내용 및 플랫폼 변경 내용을 사용 하 여 최신 상태로 유지 하는 것은 쉽습니다.  방법에 대해 알아보세요 [다른 버전을 대상](target-sdk-version.md) Windows Admin Center SDK입니다.