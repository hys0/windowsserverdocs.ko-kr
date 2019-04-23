---
title: Windows Admin Center SDK 0.1에서 1.0에서 마이그레이션
description: 이 가이드에서는 Windows Admin Center SDK 0.1에서 1.0 버전에서 마이그레이션
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 02/26/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: ba0e8cda35c51763b5c10b89c76e2bf07e064dfd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886474"
---
# <a name="migrate-from-windows-admin-center-sdk-01-to-10"></a>Windows Admin Center SDK 0.1에서 1.0에서 마이그레이션

>적용 대상: Windows Admin Center 미리 보기

이 가이드는 Windows Admin Center SDK 0.1에서 1.0 버전에서에서 마이그레이션하는 데 도움이 됩니다.  

## <a name="1-learn-about-new-controls-with-the-dev-guide-extension"></a>1. 개발자 가이드 확장을 사용 하 여 새 컨트롤에 알아봅니다

Windows Admin Center 1902 이상 버전에 포함 된 **개발자 가이드** 컨트롤 (새로 사용 가능한 컨트롤 포함) 및 고유한 확장을 빌드할 수 있도록 하는 시나리오의 예제를 찾는 데 사용할 수 있는 확장.  개발자 가이드를 대체 합니다 **개발자 도구** 이전 버전의 SDK에서 확장 합니다.

### <a name="use-the-dev-guide-in-windows-admin-center"></a>개발자 가이드를 사용 하 여 Windows Admin Center

개발자 가이드 Windows Admin Center 버전 1902 솔루션으로 제공 되며 이후입니다.  개발자 가이드는 미리 설치 되어 있지만 설정을 통해 사용 하도록 설정 해야 합니다.

**Windows Admin Center 개발자 가이드를 사용 하도록 설정 합니다.**

* 오픈 Windows Admin Center (1902 이상 버전)
* 클릭 합니다 **설정을** 창의 오른쪽 위 모서리의 아이콘
* 선택 된 **고급** 탭
* 아래 *실험 키*, 클릭 **추가**
* 새 값을 입력 ```msft.sme.shell.devguide``` 에 이전 단계에서 만든 빈 필드에
* 클릭 **저장 하 고 다시 로드**

**Windows Admin Center 개발자 가이드를 엽니다.**

* 오픈 Windows Admin Center (1902 이상 버전)
* 모든 솔루션 형식을 표시 하려면 왼쪽 위에 있는 드롭다운 메뉴를 클릭 합니다.
* 선택 된 **개발자 가이드** 솔루션 
    * 나열 된 솔루션을 보이지 않으면 개발자 가이드를 사용할 수 있는 있는지 확인 (위의 섹션 참조) Windows Admin Center 다시 로드 했습니다.
* 개발자 가이드의 내용을 탭 중 하나를 선택 하 여 찾아보기
    * **방문:** 에 대 한 코드 샘플이 포함 되어 있습니다 *으로 관리* 하 고 *알림* 시나리오
    * **컨트롤:** SDK에서 사용할 수 있는 각 컨트롤의 예제를 포함합니다.
    * **파이프 합니다.** 사용할 수 있는 변환기 및 포맷터 함수 예가 포함 되어 있습니다.
    * **스타일:** SDK에서 사용할 수 있는 CSS 스타일의 예제가 포함 되어 있습니다.
    * **MsftSme:** 고급 시나리오에 대 한 지침 및 예제를 포함합니다. 

### <a name="browse-the-source-code-of-dev-guide-on-github"></a>GitHub의 개발자 가이드의 소스 코드 찾아보기

찾아볼 수 있습니다는 [소스 코드](https://github.com/Microsoft/windows-admin-center-sdk/) 예제 HTML, CSS 및 TypeScript 코드 샘플을 찾으려면 GitHub에서 개발 가이드입니다.

## <a name="2-prepare-your-development-environment-for-the-latest-sdk"></a>2. 최신 SDK에 대 한 개발 환경 준비

설치 또는 node.js 버전을 업데이트 [10.15.1 LTS 이상](https://nodejs.org/en/)합니다.

최신 버전으로 Windows Admin Center CLI를 업데이트 합니다.

[//]: # "npm uninstall -g windows-admin-center-cli@next"

``` cmd
npm uninstall -g windows-admin-center-cli
npm install -g windows-admin-center-cli
```

이러한 버전에 전역 종속성을 업데이트 합니다.

``` cmd
npm install npm@6.4.1 -g
npm install @angular/cli@7.1.2 -g
npm install gulp -g
npm install typescript@3.1.6 -g
npm install tslint@5.11.0 -g
```

## <a name="3-create-a-new-project-with-the-latest-sdk"></a>3. 최신 SDK를 사용 하 여 새 프로젝트 만들기

Windows Admin Center CLI를 사용 하 여 새 프로젝트 대상으로 하는 만들려는 ```next``` 버전 (SDK 1.0):

[//]: # "wac create--회사 ' Contoso Inc'-' 관리 Foo 작동 '-실험적 버전 도구"

``` cmd
wac create --company "Contoso Inc" --tool "Manage Foo Works" --version next
```

다음으로 디렉터리를 방금 만든 폴더로 변경 합니다. 그런 다음 실행 하 여 필요한 로컬 종속성 설치 ```npm install ```합니다.

## <a name="4-modify-an-existing-project-to-use-the-latest-sdk"></a>4. 최신 SDK를 사용 하려면 기존 프로젝트를 수정 합니다.

중요: 계속 하기 전에 프로젝트의 백업을 만듭니다.

다음 줄을 수정 ```package.json``` 대상에는 ```next``` 버전 (SDK 1.0):

[//]: # "'@microsoft/windows-admin-center-sdk': '실험'"

``` json
"@microsoft/windows-admin-center-sdk": "next",
```

그런 다음 ```npm install``` 프로젝트 전체에서 참조를 업데이트 합니다.

## <a name="5-use-the-sdk-cli-to-fix-common-migration-issues"></a>5. SDK CLI를 사용 하 여 일반적인 마이그레이션 문제 해결

중요: 계속 하기 전에 프로젝트의 백업을 만듭니다.

프로젝트의 루트 폴더에서 프로젝트를 자동으로 일반적인 마이그레이션 문제를 해결 하려면 다음 CLI 명령을 실행 합니다.

``` cmd
wac updateSeven --update
```

이 CLI 명령은 다음과 같은 문제를 자동으로 해결합니다.

* 다시 생성 ```package-lock.json```
* Angular 컴파일 환경에서 파일을 업데이트 합니다.
    - ```.gitignore```
    - ```tslint.json```
    - ```tsconfig.json```
    - ```tsconfig.inline.json```
    - ```ng-package.json```
    - ```angular.json```
    - ```src\tsconfig.app.json```
    - ```src\tsconfig.lib.json```
    - ```src\tsconfig.spec.json```

## <a name="6-use-the-sdk-cli-to-understand-common-migration-issues"></a>6. SDK CLI를 사용 하 여 일반적인 마이그레이션 문제 이해

프로젝트의 루트 폴더에서 수동으로 문제를 해결 해야 하는 일반적인 마이그레이션 문제를 찾고 프로젝트를 감사 하려면 다음 CLI 명령을 실행 합니다.

``` cmd
wac updateSeven --audit
```

프로젝트에서 다음과 같은 문제가 인스턴스 나타납니다.

### <a name="replace-usage-of-the-following-css-classes-with-these-sme-classes"></a>이러한 sme 클래스를 사용 하 여 다음 CSS 클래스의 사용을 바꿉니다.

| 이전 CSS 클래스 | 새 CSS 클래스 |
| -- | -- |
| .auto-flex-size |  .sme-position-flex-auto |
| .border 모두 |  테두리 inset sm.sme 및.sme-테두리-색-기본-90 |
| .border 아래쪽 |  테두리 아래쪽 sm.sme AND.sme-border-bottom-color-base-90 |
| .border-horizontal |  테두리 가로 sm.sme AND.sme-border-horizontal-color-base-90 |
| .border-left |  테두리 왼쪽 sm.sme AND.sme-border-left-color-base-90 |
| .border-right |  테두리 오른쪽 sm.sme AND.sme-border-right-color-base-90 |
| .border-top |  테두리 위쪽 sm.sme AND.sme-border-top-color-base-90 |
| .border-vertical |  테두리 세로 sm.sme AND.sme-border-vertical-color-base-90 |
| .break-word |  .sme-arrange-ws-wrap |
| .btn |  .sme 단추 OR 단추 |
| .btn 주 |  .sme button.sme-단추 주 OR.button.sme-단추-기본 |
| .color-dark |  .sme-color-alt |
| .color-light |  .sme-color-base |
| .color-light-gray |  .sme-color-base-90 |
| .fixed-flex-size |  .sme-position-flex-none |
| .flex-layout |  .sme-정렬-스택-h 또는.sme-정렬-스택-v |
| .font-bold |  .sme-font-emphasis1 |
| .highlight |  .sme-background-color-yellow |
| .horizontal |  .sme-arrange-stack-h |
| 변수에 스크롤 |  .sme-position-flex-auto |
| .nowrap |  .sme-정렬-스택-h 또는.sme-정렬-스택-v |
| .relative |  .sme-layout-relative |
| .relative-center |  .sme-layout-absolute .sme-position-center |
| .reverse |  .sme-arrange-stack-reversed |
| .stretch-absolute |  .sme-layout-absolute .sme-position-inset-none |
| .stretch-fixed |  .sme-layout-fixed .sme-position-inset-none |
| .stretch-vertical |  .sme-position-stretch-v |
| .stretch-width |  .sme-position-stretch-h |
| .vertical |  .sme-arrange-stack-v |
| .vertical-scroll-only |  .sme-정렬-숨기기-방향의 sme-정렬-자동-방향 |
| .wrap |  .sme-정렬-wrapstack-h 또는.sme-정렬-wrapstack-v |

### <a name="replace-usage-of-the-following-components-with-these-sme-components"></a>이러한 sme 구성 요소를 사용 하 여 다음 구성 요소 사용을 바꿉니다.

| 이전 구성 요소 | 새 구성 요소 |
| -- | -- |
| .alert |  sme-경고 |
| .alert-danger |  sme-경고 |
| .breadCrumb |  sme-경고 |
| .checkbox |  sme-form-field[type="checkbox"] |
| .combobox |  sme-form-field[type="select"] |
| .dashboard |  sme-레이아웃-콘텐츠-영역-패딩 sme-정렬-스택-h |
| .details-panel |  sme-property-grid |
| .details-panel-container |  sme-property-grid |
| .details-tab |  sme 속성 표 또는 sme 피벗 |
| .details-wrapper |  sme-property-grid |
| .disabled |  sme-disabled |
| 양식 단추 | sme 양식 필드 |
| 양식 컨트롤 | sme 양식 필드 |
| 양식 컨트롤 | sme 양식 필드 |
| .form-group | sme 양식 필드 |
| .form-group-label | sme 양식 필드 |
| .form-input | sme 양식 필드 |
| .form-stretch | sme 양식 필드 |
| .input-file | sme 양식 필드 |
| .nav-tabs |  sme-pivot |
| .radio |  sme-form-field[type="radio"] |
| .required-clue | sme 양식 필드 |
| .searchbox |  sme-form-field[type="search"] |
| .toggle-switch |  sme-form-field[type="toggle-switch"] |
| .tool-container |  sme 레이아웃-콘텐츠 영역 또는 sme 레이아웃-콘텐츠-영역-채워짐 |

### <a name="these-css-classes-are-deprecated-and-are-no-longer-supported"></a>이러한 CSS 클래스는 사용 되지 않으며 더 이상 지원 합니다.

| 이전 클래스 | 사용되지 않음 |
| -- | -- |
| .acceptable | (사용 되지 않음) |
| .color-error | (사용 되지 않음) |
| .color-info | (사용 되지 않음) |
| .color-success | (사용 되지 않음) |
| .color-경고 | (사용 되지 않음) |
| .delete-button | (사용 되지 않음) |
| .details-content | (사용 되지 않음) |
| .error-cover | (사용 되지 않음) |
| .error-message | (사용 되지 않음) |
| .guided 창 단추 | (사용 되지 않음) |
| .header-container | (사용 되지 않음) |
| .icon 우선 | (사용 되지 않음) |
| .indent | (사용 되지 않음) |
| .invalid | (사용 되지 않음) |
| .item-list | (사용 되지 않음) |
| .modal-scrollable | (사용 되지 않음) |
| .multi-section | (사용 되지 않음) |
| 화면 작업 표시줄 | (사용 되지 않음) |
| .overflow-margins | (사용 되지 않음) |
| .overflow-tool | (사용 되지 않음) |
| .progress-cover | (사용 되지 않음) |
| 로요 패널 | (사용 되지 않음) |
| .rollup | (사용 되지 않음) |
| .rollup-status | (사용 되지 않음) |
| .rollup-title | (사용 되지 않음) |
| .rollup-value | (사용 되지 않음) |
| .searchbox-action-bar | (사용 되지 않음) |
| .size-h-1 | (사용 되지 않음) |
| .size-h-2 | (사용 되지 않음) |
| .size-h-3 | (사용 되지 않음) |
| .size-h-4 | (사용 되지 않음) |
| .size-h-full | (사용 되지 않음) |
| .size-h-half | (사용 되지 않음) |
| .size-v-1 | (사용 되지 않음) |
| .size-v-2 | (사용 되지 않음) |
| .size-v-3 | (사용 되지 않음) |
| .size-v-4 | (사용 되지 않음) |
| .status-icon | (사용 되지 않음) |
| .svg-16px | (사용 되지 않음) |
| .table-indent | (사용 되지 않음) |
| .table-sm | (사용 되지 않음) |
| .thin | (사용 되지 않음) |
| .tile | (사용 되지 않음) |
| .tile-body | (사용 되지 않음) |
| .tile-content | (사용 되지 않음) |
| .tile-footer | (사용 되지 않음) |
| .tile-header | (사용 되지 않음) |
| .tile-layout | (사용 되지 않음) |
| .tile-table | (사용 되지 않음) |
| .toolbar | (사용 되지 않음) |
| .tool 표시줄 | (사용 되지 않음) |
| .tool-header | (사용 되지 않음) |
| .tool-header-box | (사용 되지 않음) |
| .tool 창 | (사용 되지 않음) |
| .usage-bar | (사용 되지 않음) |
| .usage-bar-area | (사용 되지 않음) |
| .usage-bar-background | (사용 되지 않음) |
| .usage-bar-title | (사용 되지 않음) |
| .usage-bar-value | (사용 되지 않음) |
| .usage-chart | (사용 되지 않음) |
| .usage-message | (사용 되지 않음) |
| .usage-message-area | (사용 되지 않음) |
| .usage-message-title | (사용 되지 않음) |
| .warning | (사용 되지 않음) |
| .white 공백 | (사용 되지 않음) |

## <a name="7-understand-and-resolve-issues-with-observable-objects"></a>7. 이해 및 관찰 가능한 개체를 사용 하 여 문제를 해결 합니다.

### <a name="update--rxjs-function-use-for-observable-objects"></a>업데이트 ```rxjs``` 관찰 가능한 개체에 대 한 사용 하 여 함수

다음은 변경 된 몇 가지 일반적인 함수 이름, 있을 수 있습니다 다른 프로젝트에서.

* 업데이트 ```Observable.empty()``` 를 ```empty()```
* 업데이트 ```Observable.of()``` 를 ```of()```
* 업데이트 ```.switchMap()``` 를 ```.pipe(switchMap())```
* 업데이트 ```.map()``` 를 ```.pipe(map())```
* 업데이트 ```flatMap()``` 를 ```mergeMap()```


### <a name="resolve-runtime-issues-with-map-and-filter-functions-on-observable-objects"></a>런타임 문제를 해결 ```.map()``` 고 ```.filter()``` 관찰 가능한 개체 함수

컴파일러가 올바르게 식별할 수 없는 경우는 ```observable``` 개체의 형식 ```.map()``` 및 ```.filter()``` 에서 함수는 ```array``` 런타임 시 오류가 발생 하는 사용자 개체에 개체를 대신 매핑할 수 있습니다.  함수 반환 하는 ```observable``` 이 문제를 방지 하려면 명시적 데이터 형식을 지정 하는 개체입니다.

```any``` 및 반환 형식이 없는이 문제를 일으키는, 이러한 패턴을 사용 하 여 코드를 검색할 수 있습니다.

``` ts
public getMyObservable(): any { //any return type can cause issues
 ...
}

public getMyObservable() { //no return type can cause issues
...
}
```

## <a name="8-resolve-other-common-issues"></a>8. 다른 일반적인 문제 해결

이러한 기술은 다른 일반적인 문제를 해결 하는 데 도움이 됩니다.

* 실행 ```ng lint --fix``` 일반적인 lint 문제를 해결 하려면
* 실행할 ```gulp build``` 반복적으로 증분 방식으로 해결 하는 문제의 ```gulp build``` 자동으로 해결할 수

## <a name="9-build-and-serve-your-project"></a>9. 작성 하 고 프로젝트를 제공 합니다.

작성 하 고 최신 버전 (SDK 1.0)을 사용 하 여 프로젝트를 제공 하려면 다음 명령을 실행 합니다.

``` cmd
gulp build
gulp serve --port 4201
```

## <a name="10-turn-on-dark-theme-in-windows-admin-center"></a>10. Windows Admin Center 어두운 테마 켜기

1902 이상에 Windows Admin Center 버전의에서 어두운 테마를 켜려면 다음과이 같이 하십시오.

* 오픈 Windows Admin Center (1902 이상 버전)
* 클릭 합니다 **설정을** 창의 오른쪽 위 모서리의 아이콘
* 선택 된 **고급** 탭
* 아래 *실험 키*, 클릭 **추가**
* 새 값을 입력 ```msft.sme.shell.personalization``` 에 이전 단계에서 만든 빈 필드에
* 클릭 **저장 하 고 다시 로드**
* 설정이 새 탭에 이제 **개인 설정**합니다.  이 탭을 선택 합니다.
* 변경 **색** 에 **어두운 모드 (미리 보기)**
