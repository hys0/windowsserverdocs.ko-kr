---
title: 도구 확장 개발
description: Windows Admin Center SDK (Project Honolulu) 도구 확장 개발
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 7dd213f7032ab77021bbfcbdc966c9c2307b86eb
ms.sourcegitcommit: be0144eb59daf3269bebea93cb1c467d67e2d2f1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/20/2018
ms.locfileid: "4081060"
---
# 도구 확장 개발

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

도구 확장에 서버 또는 클러스터 등의 연결을 관리 하는 Windows Admin Center를 사용 하 여 사용자가 상호 작용 하는 기본 방법입니다. Windows Admin Center 홈 화면에서 연결을 클릭 하 고 연결의 왼쪽된 탐색 창의 도구 목록을 표시 한 다음 됩니다. 도구를 클릭 하면 도구 확장 로드 되 고 오른쪽 창에 표시 됩니다.

도구 확장을 로드할 때 대상 서버 또는 클러스터에서 WMI 호출 또는 PowerShell 스크립트를 실행 하 고 UI에 정보를 표시 하거나 사용자 입력에 따라 명령을 실행할 수 있습니다 것. 도구 확장 것을 표시할지, 다른 각 솔루션에 대 한 도구 집합을 생성 하는 솔루션을 정의 합니다.

> [!NOTE]
> 익숙하지 다른 확장 형식? [확장성 아키텍처 및 확장 형식](understand-extensions.md)에 대해 알아봅니다.

## 사용자 환경 준비

아직, 모든 프로젝트에 필요한 전역 필수 구성 요소 및 종속성을 설치 하 여 [환경을 준비](prepare-development-environment.md) 를 합니다.

## Windows Admin Center CLI를 사용 하 여 새 도구 확장 만들기 ##

설치 된 모든 종속성을 구성한 후에 새 도구 확장을 만들 준비가 됩니다.  또는 프로젝트 파일이 포함 된 폴더로 이동, 명령 프롬프트를 열고 만들고 작업 디렉터리와 해당 폴더를 설정 합니다.  이전에 설치 된 Windows Admin Center CLI를 사용 하 여 다음 구문을 사용 하 여 새로운 확장을 만듭니다.

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

## 확장에 콘텐츠 추가

Windows Admin Center CLI를 사용 하 여 확장을 만든 했으므로 콘텐츠를 사용자 지정할 준비가 되었습니다.  수행할 수 있는 작업의 예제를 보려면 다음이 가이드를 참조 하세요.

- [빈 모듈](guides\add-module.md) 추가
- [iFrame](guides\add-iframe.md) 추가
 
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