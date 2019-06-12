---
title: 솔루션 확장 개발
description: 솔루션 확장 Windows Admin Center SDK (프로젝트 브라 티) 개발
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 268a7d2833f73e9fab006501e9b3dc261d1b1d9e
ms.sourcegitcommit: 48bb3e5c179dc520fa879b16c9afe09e07c87629
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66452568"
---
# <a name="develop-a-solution-extension"></a>솔루션 확장 개발

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

솔루션에는 주로 Windows Admin Center 통해 관리 하려는 개체의 고유 형식을 정의 합니다.  이러한 솔루션/연결 유형은 기본적으로 Windows Admin Center 사용 하 여 포함 합니다.

* Windows Server 연결
* Windows PC 연결
* 장애 조치 클러스터 연결
* 하이퍼 수렴 형 클러스터 연결

Windows Admin Center 연결 페이지에서 연결을 선택 하면 해당 연결의 유형에 대 한 솔루션 확장 로드 되 고 Windows Admin Center 대상 노드에 연결을 시도 합니다. 연결이 성공적 이면 솔루션 확장의 UI 로드 되 고, Windows Admin Center 왼쪽된 탐색 창에서 해당 솔루션에 대 한 도구를 표시 됩니다.

컴퓨터 이름으로 위의 기본 연결 유형, 이러한 네트워크 스위치를 또는 검색할 수 없는 다른 하드웨어에 의해 정의 되지 않은 서비스에 대 한 관리 GUI를 빌드 하려는 경우 사용자 고유의 솔루션 확장을 만드는 것이 좋습니다.

> [!NOTE]
> 에 익숙하지 않는 다양 한 확장 형식? 에 대 한 자세한 정보는 [확장성 아키텍처 및 확장 형식](understand-extensions.md)합니다.

## <a name="prepare-your-environment"></a>사용자 환경 준비

이미 않았다면 [환경을 준비](prepare-development-environment.md) 종속성 및 모든 프로젝트에 필요한 전체 필수 구성 요소를 설치 하 여 합니다.

## <a name="create-a-new-solution-extension-with-the-windows-admin-center-cli"></a>Windows Admin Center CLI를 사용 하 여 새 솔루션 확장 만들기 ##

설치 된 모든 종속성을 만든 후 새 솔루션 확장 프로그램을 만들 준비가 되었습니다.  또는 프로젝트 파일이 포함 된 폴더로 이동, 명령 프롬프트를 열고 만들고 해당 폴더의 작업 디렉터리를 설정 합니다.  이전에 설치 된 Windows Admin Center CLI를 사용 하 여, 다음 구문을 사용 하 여 새 확장을 만듭니다.

```
wac create --company "{!Company Name}" --solution "{!Solution Name}" --tool "{!Tool Name}"
```

| 값 | 설명 | 예제 |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | 회사 이름 (공백 포함) | ```Contoso Inc``` |
| ```{!Solution Name}``` | 솔루션 이름을 (공백 포함) | ```Contoso Foo Works Suite``` |
| ```{!Tool Name}``` | 사용자 도구 이름 (공백 포함) | ```Manage Foo Works``` |

사용 예제는 다음과 같습니다.

```
wac create --company "Contoso Inc" --solution "Contoso Foo Works Suite" --tool "Manage Foo Works"
```

이 솔루션에 대해 지정 된 프로젝트에 모든 필요한 템플릿 파일을 복사 및 회사, 솔루션 및 도구 이름을 사용 하 여 파일을 구성 하는 이름을 사용 하 여 현재 작업 디렉터리 내에서 새 폴더를 만듭니다.  

방금 만든 폴더로 디렉터리를 변경 합니다. 그런 다음, 다음 명령을 실행 하 여 필요한 로컬 종속성을 설치 합니다.

```
npm install
```

이 완료 되 면 Windows Admin Center 새 확장을 로드 하는 데 필요한 모든 구성 설정 했습니다. 

## <a name="add-content-to-your-extension"></a>확장 프로그램에 콘텐츠 추가

Windows Admin Center CLI를 사용 하 여 확장을 만든 했으므로 콘텐츠를 사용자 지정할 준비가 되었습니다.  수행할 수 있는 예가 다음이 가이드를 참조 하세요.

- 추가 [빈 모듈](guides/add-module.md)
- 추가 [iFrame](guides/add-iframe.md)
- 만들기는 [사용자 지정 연결 공급자](guides/create-connection-provider.md)
- 수정 [루트 탐색 동작](guides/modify-root-navigation.md)
 
더 많은 예제를 찾을 수 있습니다 우리의 [GitHub SDK 사이트](https://aka.ms/wacsdk):
-  [개발자 도구](https://github.com/Microsoft/windows-admin-center-sdk/tree/master/windows-admin-center-developer-tools) 는 Windows Admin Center 테스트용으로 로드 될 수 있는 완벽 한 기능의 확장으로, 탐색 하 고 고유한 확장에서 사용할 수 있는 샘플 기능 및 도구 예제가 다양 한 컬렉션을 포함 합니다.

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