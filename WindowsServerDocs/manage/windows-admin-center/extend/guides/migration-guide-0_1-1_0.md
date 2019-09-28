---
title: Windows 관리 센터 SDK 0.1에서 1.0로 마이그레이션
description: 이 가이드는 Windows 관리 센터 SDK 버전 0.1에서 1.0로 마이그레이션하는 데 도움이 됩니다.
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 02/26/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: c52870178e7caff0abc8ddcccc62966d637dd3c9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357062"
---
# <a name="migrate-from-windows-admin-center-sdk-01-to-10"></a>Windows 관리 센터 SDK 0.1에서 1.0로 마이그레이션

>적용 대상: Windows Admin Center 미리 보기

이 가이드는 Windows 관리 센터 SDK 버전 0.1에서 1.0로 마이그레이션하는 데 도움이 됩니다.  

## <a name="1-learn-about-new-controls-with-the-dev-guide-extension"></a>1. 개발자 가이드 확장을 사용 하 여 새 컨트롤에 대 한 자세한 정보

Windows 관리 센터 버전 1902 이상에는 사용자 고유의 확장을 빌드하는 데 도움이 되는 컨트롤의 예 (새로 사용 가능한 컨트롤 포함) 및 시나리오를 찾는 데 사용할 수 있는 **개발자 가이드** 확장이 포함 되어 있습니다.  개발자 가이드는 이전 버전의 SDK에서 **개발자 도구** 확장을 대체 합니다.

### <a name="use-the-dev-guide-in-windows-admin-center"></a>Windows 관리 센터에서 개발자 가이드 사용

개발자 가이드는 Windows 관리 센터 버전 1902 이상에서 솔루션으로 사용할 수 있습니다.  개발자 가이드는 미리 설치 되어 있지만 설정을 통해 사용 하도록 설정 해야 합니다.

**Windows 관리 센터에서 개발자 가이드를 사용 하도록 설정 합니다.**

* Windows 관리 센터 (버전 1902 이상) 열기
* 창의 오른쪽 위 모퉁이에 있는 **설정** 아이콘을 클릭 합니다.
* **고급** 탭을 선택 합니다.
* *실험 키*에서 **추가** 를 클릭 합니다.
* 이전 단계에서 만든 빈 필드에 새 값 ```msft.sme.shell.devguide```을 입력 합니다.
* **저장 후 다시 로드를** 클릭 합니다.

**Windows 관리 센터에서 개발자 가이드를 엽니다.**

* Windows 관리 센터 (버전 1902 이상) 열기
* 모든 솔루션 유형을 표시 하려면 왼쪽 상단에 있는 드롭다운을 클릭 합니다.
* **개발자 가이드** 솔루션 선택 
    * 솔루션이 나열 되지 않으면 개발자 가이드 (위 섹션 참조)를 사용 하도록 설정 하 고 Windows 관리 센터를 다시 로드 했는지 확인 합니다.
* 탭 중 하나를 선택 하 여 개발자 가이드의 내용 찾아보기
    * **방문** *관리* 및 *알림* 시나리오에 대 한 코드 샘플이 포함 되어 있습니다.
    * **제어가** SDK에서 사용 가능한 각 컨트롤의 예제를 포함 합니다.
    * **파이프** 사용 가능한 변환기 및 포맷터 함수의 예를 포함 합니다.
    * **유형이** SDK에서 사용할 수 있는 CSS 스타일의 예가 포함 되어 있습니다.
    * **MsftSme:** 고급 시나리오에 대 한 예제 및 지침이 포함 되어 있습니다. 

### <a name="browse-the-source-code-of-dev-guide-on-github"></a>GitHub에서 개발자 가이드의 소스 코드 찾아보기

GitHub에서 개발자 가이드의 [소스 코드](https://github.com/Microsoft/windows-admin-center-sdk/) 를 검색 하 여 HTML, CSS 및 TypeScript 코드 샘플을 찾을 수 있습니다.

## <a name="2-prepare-your-development-environment-for-the-latest-sdk"></a>2. 최신 SDK를 위한 개발 환경 준비

Node.js 버전 [10.15.1 LTS](https://nodejs.org/en/)이상을 설치 하거나 업데이트 합니다.

Windows 관리 센터 CLI를 최신 버전으로 업데이트 합니다.

[//]: # "npm 제거-g windows-admin-center-cli@next"

``` cmd
npm uninstall -g windows-admin-center-cli
npm install -g windows-admin-center-cli
```

이러한 버전에 대 한 전역 종속성을 업데이트 합니다.

``` cmd
npm install npm@6.4.1 -g
npm install @angular/cli@7.1.2 -g
npm install gulp -g
npm install typescript@3.1.6 -g
npm install tslint@5.11.0 -g
```

## <a name="3-create-a-new-project-with-the-latest-sdk"></a>3. 최신 SDK를 사용 하 여 새 프로젝트 만들기

Windows 관리 센터 CLI를 사용 하 여 ```next``` 버전 (SDK 1.0)을 대상으로 하는 새 프로젝트를 만듭니다.

[//]: # "wac create--company ' Contoso Inc. '--tool ' Foo Works 관리 '--버전 실험적"

``` cmd
wac create --company "Contoso Inc" --tool "Manage Foo Works" --version next
```

그런 다음, 디렉터리를 앞에서 만든 폴더로 변경한 다음 ```npm install ```을 실행 하 여 필요한 로컬 종속성을 설치 합니다.

## <a name="4-modify-an-existing-project-to-use-the-latest-sdk"></a>4. 최신 SDK를 사용 하도록 기존 프로젝트 수정

중요: 계속 하기 전에 프로젝트의 백업을 만드십시오.

@No__t-0에서 다음 줄을 수정 하 여 ```next``` 버전 (SDK 1.0)을 대상으로 합니다.

[//]: # "' @microsoft/windows-admin-center-sdk ': ' 실험적 '"

``` json
"@microsoft/windows-admin-center-sdk": "next",
```

그런 다음 ```npm install```을 실행 하 여 프로젝트 전체에서 참조를 업데이트 합니다.

## <a name="5-use-the-sdk-cli-to-fix-common-migration-issues"></a>5. SDK CLI를 사용 하 여 일반적인 마이그레이션 문제 해결

중요: 계속 하기 전에 프로젝트의 백업을 만드십시오.

프로젝트의 루트 폴더에서 프로젝트에 대해 다음 CLI 명령을 실행 하 여 일반적인 마이그레이션 문제를 자동으로 해결 합니다.

``` cmd
wac updateSeven --update
```

이 CLI 명령은 다음 문제를 자동으로 해결 합니다.

* @No__t 다시 생성-0
* 각도 컴파일 환경에서 파일을 업데이트 합니다.
    - ```.gitignore```
    - ```tslint.json```
    - ```tsconfig.json```
    - ```tsconfig.inline.json```
    - ```ng-package.json```
    - ```angular.json```
    - ```src\tsconfig.app.json```
    - ```src\tsconfig.lib.json```
    - ```src\tsconfig.spec.json```

## <a name="6-use-the-sdk-cli-to-understand-common-migration-issues"></a>6. SDK CLI를 사용 하 여 일반적인 마이그레이션 문제를 이해 합니다.

프로젝트의 루트 폴더에서 다음 CLI 명령을 실행 하 여 프로젝트를 감사 하 고 수동으로 해결 해야 하는 일반적인 마이그레이션 문제를 찾습니다.

``` cmd
wac updateSeven --audit
```

이렇게 하면 프로젝트에서 다음 문제의 인스턴스가 검색 됩니다.

### <a name="replace-usage-of-the-following-css-classes-with-these-sme-classes"></a>다음 CSS 클래스의 사용을 다음 sme 클래스로 바꿉니다.

| 이전 CSS 클래스 | 새 CSS 클래스 |
| -- | -- |
| . 자동 플렉스 크기 |  . sme-자동 |
| . 테두리-모두 |  . sme-sme-----90 |
| . 테두리-아래쪽 |  . sme-sme-----밑-90 |
| . 테두리-가로 |  . sme-sme-------90 |
| . 왼쪽 테두리 |  . sme-sme------------90 |
| . 테두리-오른쪽 |  . sme-sme-------90 |
| . 테두리-위쪽 |  . sme-sme------------90 |
| . 테두리-세로 |  . sme-sme-------90 |
| . break 단어 |  . sme-ws-wrap |
| .btn |  . sme-단추 또는 단추 |
| . btn-기본 |  . sme-sme-button 또는. sme-기본 |
| . 색-어둡게 |  sme |
| . 색-밝게 |  sme |
| . 색-연한 회색 |  sme-90 |
| . 고정-플렉스 크기 |  . sme-없음 |
| . flex-레이아웃 |  . sme 또는. sme--stack-v |
| . font-size-굵게 |  sme-emphasis1 |
| . 강조 표시 |  sme-노랑-배경색 |
| . 가로 |  . sme-------------h |
| . 없음-스크롤 |  . sme-자동 |
| . nowrap |  . sme 또는. sme--stack-v |
| . 상대 |  . sme-상대 |
| . 상대-가운데 |  . sme-sme-위치-가운데 |
| . 역방향 |  . sme-스택-반전 |
| . 스트레치-절대 |  sme-sme-오목-없음 |
| . 스트레치-고정 |  sme-sme-오목-없음 |
| . 스트레치-세로 |  . sme-스트레치-v |
| . 스트레치-너비 |  . sme--스트레치-h |
| . 세로 |  . sme-stack-v |
| . 세로 스크롤 전용 |  . sme-sme-hide-x-auto-y |
| . wrap |  . sme-wrapstack-h 또는. sme-wrapstack-v |

### <a name="replace-usage-of-the-following-components-with-these-sme-components"></a>다음 구성 요소의 사용을 다음 sme 구성 요소로 바꿉니다.

| 이전 구성 요소 | 새 구성 요소 |
| -- | -- |
| . 경고 |  sme-경고 |
| . 경고-위험 |  sme-경고 |
| . 이동 경로 |  sme-경고 |
| . checkbox |  sme [type = "checkbox"] |
| . combobox |  sme [type = "select"] |
| . 대시보드 |  sme-sme-패딩-h-h |
| . 세부 정보-패널 |  sme-속성-그리드 |
| . 세부 정보-패널-컨테이너 |  sme-속성-그리드 |
| . details-tab |  sme 또는 sme |
| . 세부 정보-래퍼 |  sme-속성-그리드 |
| . 사용 안 함 |  sme-사용 안 함 |
| . 양식-단추 | sme-필드 |
| . form-컨트롤 | sme-필드 |
| . form-controls | sme-필드 |
| . 양식-그룹 | sme-필드 |
| . 양식-그룹-레이블 | sme-필드 |
| . form-input | sme-필드 |
| . 양식-스트레치 | sme-필드 |
| . 입력 파일 | sme-필드 |
| . 탐색 탭 |  sme |
| . radio |  sme [type = "radio"] |
| . 필수-단서 | sme-필드 |
| . searchbox |  sme [type = "search"] |
| . toggle 스위치 |  sme [type = "toggle 스위치"] |
| . 도구-컨테이너 |  sme 또는 sme-채워짐-zone-채워짐 |

### <a name="these-css-classes-are-deprecated-and-are-no-longer-supported"></a>이러한 CSS 클래스는 더 이상 사용 되지 않으며 더 이상 지원 되지 않습니다.

| 이전 클래스 | 사용되지 않음 |
| -- | -- |
| . 허용 가능 | mapi |
| . color-error | mapi |
| . 색-정보 | mapi |
| . 색-성공 | mapi |
| . color-warning | mapi |
| . 삭제-단추 | mapi |
| . 세부 정보-콘텐츠 | mapi |
| . 오류-커버 | mapi |
| . 오류-메시지 | mapi |
| . 단계별 창 단추 | mapi |
| . 헤더-컨테이너 | mapi |
| . 아이콘-win | mapi |
| . 들여쓰기 | mapi |
| . 잘못 됨 | mapi |
| . 항목 목록 | mapi |
| . 모달-스크롤 가능 | mapi |
| . 다중 섹션 | mapi |
| . 작업--작업 표시줄 | mapi |
| . 넘침 여백 | mapi |
| . 오버플로 도구 | mapi |
| . 진행률-커버 | mapi |
| . 오른쪽 패널 | mapi |
| . rollup | mapi |
| . rollup-상태 | mapi |
| . rollup-제목 | mapi |
| . rollup-값 | mapi |
| . searchbox-작업 표시줄 | mapi |
| . 크기-h-1 | mapi |
| . 크기-h-2 | mapi |
| . 크기-h-3 | mapi |
| . 크기-h-4 | mapi |
| . 크기-h-전체 | mapi |
| . 크기-h-절반 | mapi |
| . 크기-v-1 | mapi |
| . 크기-v-2 | mapi |
| . 크기-v-3 | mapi |
| . 크기-v-4 | mapi |
| . 상태-아이콘 | mapi |
| node.js-16px | mapi |
| . 테이블-들여쓰기 | mapi |
| . 테이블-sm | mapi |
| . 씬 | mapi |
| . 타일 | mapi |
| . 타일-본문 | mapi |
| . 타일-콘텐츠 | mapi |
| . 타일-바닥글 | mapi |
| . 타일-헤더 | mapi |
| . 타일-레이아웃 | mapi |
| . 타일-테이블 | mapi |
| . 도구 모음 | mapi |
| . 도구 모음 | mapi |
| . 도구-헤더 | mapi |
| . 도구-헤더-상자 | mapi |
| . 도구 창 | mapi |
| . 사용-가로 막대형 | mapi |
| . 사용-가로 막대형-영역 | mapi |
| . 사용-가로 막대형-배경 | mapi |
| . 사용-가로 막대형-제목 | mapi |
| . 사용-가로-값 | mapi |
| . 사용-차트 | mapi |
| . 사용-메시지 | mapi |
| . 사용법-메시지 영역 | mapi |
| . 사용법-메시지 제목 | mapi |
| . 경고 | mapi |
| . 공백 | mapi |

## <a name="7-understand-and-resolve-issues-with-observable-objects"></a>7. 관찰 가능한 개체와 관련 된 문제 이해 및 해결

### <a name="update--rxjs-function-use-for-observable-objects"></a>관찰 가능 개체에 대 한 업데이트 ```rxjs``` 함수 사용

이러한 이름 중 일부는 변경 된 것 이며 프로젝트에 다른 다른 함수가 있을 수 있습니다.

* @No__t-0을 ```empty()```로 업데이트 합니다.
* @No__t-0을 ```of()```로 업데이트 합니다.
* @No__t-0을 ```.pipe(switchMap())```로 업데이트 합니다.
* @No__t-0을 ```.pipe(map())```로 업데이트 합니다.
* @No__t-0을 ```mergeMap()```로 업데이트 합니다.


### <a name="resolve-runtime-issues-with-map-and-filter-functions-on-observable-objects"></a>관찰 가능한 개체에서 ```.map()``` 및 ```.filter()``` 함수를 사용 하 여 런타임 문제 해결

컴파일러가 ```observable``` 개체의 형식을 올바르게 식별할 수 없는 경우에는 ```array``` 개체의 ```.map()``` 및 ```.filter()``` 함수가 개체에 대신 매핑될 수 있으므로 런타임에 오류가 발생 합니다.  함수에서이 문제를 방지 하기 위해 명시적 데이터 형식을 지정 하는 ```observable``` 개체를 반환 하는지 확인 합니다.

```any``` 및 반환 형식 없이이 문제가 발생할 수 있습니다. 이러한 패턴을 사용 하 여 코드를 찾습니다.

``` ts
public getMyObservable(): any { //any return type can cause issues
 ...
}

public getMyObservable() { //no return type can cause issues
...
}
```

## <a name="8-resolve-other-common-issues"></a>8. 기타 일반적인 문제 해결

이러한 기술은 다른 일반적인 문제를 해결 하는 데 도움이 됩니다.

* @No__t-0을 실행 하 여 일반적인 보풀이 문제를 해결 합니다.
* @No__t-0을 반복적으로 실행 하 ```gulp build```이 자동으로 해결 될 수 있는 문제를 점진적으로 해결 합니다.

## <a name="9-build-and-serve-your-project"></a>9. 프로젝트 빌드 및 제공

다음 명령을 실행 하 여 최신 버전 (SDK 1.0)을 사용 하 여 프로젝트를 빌드하고 제공 합니다.

``` cmd
gulp build
gulp serve --port 4201
```

## <a name="10-turn-on-dark-theme-in-windows-admin-center"></a>10. Windows 관리 센터에서 짙은 테마 켜기

Windows 관리 센터 버전 1902 이상에서 어두운 테마를 켜려면 다음 단계를 수행 합니다.

* Windows 관리 센터 (버전 1902 이상) 열기
* 창의 오른쪽 위 모퉁이에 있는 **설정** 아이콘을 클릭 합니다.
* **고급** 탭을 선택 합니다.
* *실험 키*에서 **추가** 를 클릭 합니다.
* 이전 단계에서 만든 빈 필드에 새 값 ```msft.sme.shell.personalization```을 입력 합니다.
* **저장 후 다시 로드를** 클릭 합니다.
* 이제 설정에 새 탭, **개인 설정**이 있습니다.  이 탭을 선택 합니다.
* **색** 을 **어둡게 모드로 변경 (미리 보기)**
