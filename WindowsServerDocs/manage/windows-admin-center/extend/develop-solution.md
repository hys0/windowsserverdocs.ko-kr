---
title: 솔루션 확장 개발
description: Windows Admin Center SDK (Project Honolulu) 솔루션 확장 개발
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: ed5ecddbaef91f127846825e408a9a6ec65ff741
ms.sourcegitcommit: be0144eb59daf3269bebea93cb1c467d67e2d2f1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/20/2018
ms.locfileid: "4081070"
---
# 솔루션 확장 개발

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

솔루션에는 기본적으로 Windows Admin Center를 통해 관리 하고자 하는 개체의 고유한 유형을 정의 합니다.  이러한 솔루션/연결 유형 기본적으로 Windows Admin Center로 포함 되어 있습니다.

* Windows Server 연결
* Windows PC 연결
* 장애 조치 클러스터 연결
* 하이퍼 컨 버 지 드 클러스터 연결

Windows Admin Center 연결 페이지에서 연결을 선택 하는 경우 해당 연결 형식에 대 한 솔루션 확장이 로드, 및 Windows Admin Center는 대상 노드에 연결 하려고 합니다. 연결에 성공 하면 솔루션 확장의 UI가 로드, 하 고 Windows Admin Center 왼쪽된 탐색 창에서 솔루션에 대 한 도구를 표시 합니다.

컴퓨터 이름으로 위에서 기본 연결 유형, 이러한 네트워크 스위치, 또는 기타 하드웨어 검색 되지 않는 정의 되지 않은 서비스에 대 한 관리 GUI를 빌드 하려는 경우 고유한 솔루션 확장을 만드는 것이 좋습니다.

> [!NOTE]
> 익숙하지 다른 확장 형식? [확장성 아키텍처 및 확장 형식](understand-extensions.md)에 대해 알아봅니다.

## 사용자 환경 준비

아직, 모든 프로젝트에 필요한 전역 필수 구성 요소 및 종속성을 설치 하 여 [환경을 준비](prepare-development-environment.md) 를 합니다.

## Windows Admin Center CLI를 사용 하 여 새로운 솔루션 확장 만들기 ##

설치 된 모든 종속성을 구성한 후에 새로운 솔루션 확장을 만들 준비가 됩니다.  또는 프로젝트 파일이 포함 된 폴더로 이동, 명령 프롬프트를 열고 만들고 작업 디렉터리와 해당 폴더를 설정 합니다.  이전에 설치 된 Windows Admin Center CLI를 사용 하 여 다음 구문을 사용 하 여 새로운 확장을 만듭니다.

```
wac create --company "{!Company Name}" --solution "{!Solution Name}" --tool "{!Tool Name}"
```

| 값 | 설명 | 예 |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | 회사 이름 (공백 포함) | ```Contoso Inc``` |
| ```{!Solution Name}``` | 사용자 솔루션 이름 (공백 포함) | ```Contoso Foo Works Suite``` |
| ```{!Tool Name}``` | 사용자 도구 이름 (공백 포함) | ```Manage Foo Works``` |

사용 예제는 다음과 같습니다.

```
wac create --company "Contoso Inc" --solution "Contoso Foo Works Suite" --tool "Manage Foo Works"
```

이 솔루션에 대해 지정 된 모든 필요한 템플릿 파일을 프로젝트에 복사 및 회사, 솔루션 및 도구 이름으로 파일을 구성 이름을 사용 하 여 현재 작업 디렉터리 내에 새 폴더를 만듭니다.  

다음으로 방금 만든 폴더로 디렉터리를 변경한 후 다음 명령을 실행 하 여 필요한 로컬 종속성 설치:

```
npm install
```

이 완료 되 면 Windows Admin Center에 새로운 확장을 로드 하는 데 필요한 모든 설정을 마쳤으니 합니다. 

## 확장에 콘텐츠 추가

Windows Admin Center CLI를 사용 하 여 확장을 만든 했으므로 콘텐츠를 사용자 지정할 준비가 되었습니다.  수행할 수 있는 작업의 예제를 보려면 다음이 가이드를 참조 하세요.

- [빈 모듈](guides\add-module.md) 추가
- [iFrame](guides\add-iframe.md) 추가
- [사용자 지정 연결 공급자](guides\create-connection-provider.md) 만들기
- [루트 탐색 동작](guides\modify-root-navigation.md) 을 수정합니다
 
훨씬 더 많은 예제는 [GitHub SDK 사이트](https://aka.ms/wacsdk)를 찾을 수 있습니다.
-  [개발자 도구](https://github.com/Microsoft/windows-admin-center-sdk/tree/master/windows-admin-center-developer-tools) 는 Windows Admin Center에 테스트용으로 로드 될 수 있는 완벽 하 게 작동 확장 하 고 풍부한 샘플 기능 및 찾아 자체 확장에서 사용할 수 있는 도구 예제 컬렉션을 포함 합니다.

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