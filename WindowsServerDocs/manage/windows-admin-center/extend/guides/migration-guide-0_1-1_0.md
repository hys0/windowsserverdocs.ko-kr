---
title: Windows Admin Center SDK 0.1 ~ 1.0에서 마이그레이션
description: 이 가이드는 Windows Admin Center SDK 버전 1.0을 0.1에서에서 마이그레이션할 때 도움이 됩니다.
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 02/26/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: ba0e8cda35c51763b5c10b89c76e2bf07e064dfd
ms.sourcegitcommit: 10d7606a5c2a1ddb234af597f199b6779b0058d4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/27/2019
ms.locfileid: "9116593"
---
# Windows Admin Center SDK 0.1 ~ 1.0에서 마이그레이션

>적용 대상: Windows Admin Center 미리 보기

이 가이드는 Windows Admin Center SDK 버전 1.0을 0.1에서에서 마이그레이션하는 데 도움이 됩니다.  

## 1. 개발자 가이드 확장명을 가진 새 컨트롤에 알아봅니다.

Windows Admin Center 버전 1902 이상 컨트롤 (새로 사용 가능한 컨트롤 포함) 및 확장을 빌드하는 방법을 안내 하는 시나리오의 예를 찾는 데 사용할 수 있는 **개발자 가이드** 확장이 포함 됩니다.  개발자 가이드 SDK의 이전 버전에서 **개발자 도구** 확장을 대체합니다.

### 개발자 가이드를 사용 하 여 Windows 관리 센터에서

개발자 가이드는 Windows Admin Center 버전 1902 솔루션으로 사용할 수 있습니다. 이상.  개발자 가이드는 미리 설치 되어 있지만 설정을 통해 사용 하도록 설정 해야 합니다.

**Windows 관리 센터에서 개발자 가이드를 사용 하도록 설정:**

* Open Windows Admin Center (1902 이상 버전)
* 창의 오른쪽 상단 모서리에서 **설정** 아이콘을 클릭
* **고급** 탭을 선택
* *실험 키* **추가** 클릭 합니다.
* 새 값을 입력 ```msft.sme.shell.devguide``` 에서 이전 단계에서 만든 있는 빈 필드
* **저장 하 고 다시 로드** 를 클릭 합니다.

**Windows 관리 센터에서 개발자 가이드를 엽니다.**

* Open Windows Admin Center (1902 이상 버전)
* 드롭다운 목록에서 모든 솔루션 종류를 표시 하기 왼쪽 위를 클릭 합니다.
* **개발자 가이드** 솔루션 선택 
    * 나열 된 솔루션 보이지 않으면 개발자 가이드 설정 되어 있는지 확인 (위 섹션 참조) 하 고 Windows Admin Center를 다시 로드 했습니다.
* 탭 중 하나를 선택 하 여 개발자 가이드의 내용을 살펴봅니다.
    * **방문:** *다음으로 관리* 및 *알림* 시나리오를 위한 코드 샘플을 포함 되어 있습니다.
    * **컨트롤:** SDK에서 사용할 수 있는 각 컨트롤의 예가 나와 있습니다.
    * **파이프:** 사용 가능한 변환기 함수와 포맷터의 예가 나와 있습니다.
    * **스타일:** SDK에서 사용할 수 있는 CSS 스타일의 예가 나와 있습니다.
    * **MsftSme:** 예제에서는 고급 시나리오에 대 한 지침 

### GitHub의 개발자 가이드의 소스 코드 찾아보기

예제에서는 HTML, CSS 및 TypeScript 코드 샘플을 찾을 수 있는 github 개발자 가이드의 [소스 코드](https://github.com/Microsoft/windows-admin-center-sdk/) 를 찾을 수 있습니다.

## 2. 최신 SDK에 대 한 개발 환경을 준비합니다

설치 또는 업데이트 node.js 버전 [10.15.1 LTS 이상](https://nodejs.org/en/)합니다.

Windows Admin Center CLI 최신 버전으로 업데이트 합니다.

[//]: # "npm-g windows-admin-center-cli@next 제거"

``` cmd
npm uninstall -g windows-admin-center-cli
npm install -g windows-admin-center-cli
```

이러한 버전을 전역 종속성을 업데이트 합니다.

``` cmd
npm install npm@6.4.1 -g
npm install @angular/cli@7.1.2 -g
npm install gulp -g
npm install typescript@3.1.6 -g
npm install tslint@5.11.0 -g
```

## 3. 최신 SDK를 사용 하 여 새 프로젝트 만들기

Windows Admin Center CLI를 사용 하 여 대상으로 새 프로젝트를 만들 수는 ```next``` 버전 (SDK 1.0):

[//]: # "wac 만들기-회사 ' Contoso Inc'-도구 ' 관리 Foo 작동 '-실험적 버전"

``` cmd
wac create --company "Contoso Inc" --tool "Manage Foo Works" --version next
```

다음으로 방금 만든 폴더로 디렉터리를 변경 하 고 실행 하 여 필요한 로컬 종속성 설치 ```npm install ```.

## 4. 최신 SDK를 사용 하 여 기존 프로젝트를 수정 합니다.

중요: 프로젝트의 백업 계속 하기 전에 확인 합니다.

다음 줄을 수정 ```package.json``` 대상에는 ```next``` 버전 (SDK 1.0):

[//]: # "'@microsoft/windows-admin-center-sdk': '실험적'"

``` json
"@microsoft/windows-admin-center-sdk": "next",
```

그러고 나 서 ```npm install``` 에서 프로젝트 참조를 업데이트 합니다.

## 5. 일반적인 마이그레이션 문제를 해결 하는 SDK CLI를 사용 합니다.

중요: 프로젝트의 백업 계속 하기 전에 확인 합니다.

프로젝트의 루트 폴더에서 다음 명령을 실행 합니다 CLI를 자동으로 일반적인 마이그레이션 문제를 해결 하려면 프로젝트에서:

``` cmd
wac updateSeven --update
```

이 CLI 명령은 자동으로 다음과 같은 문제를 해결합니다.

* 다시 생성 ```package-lock.json```
* Angular 컴파일 환경에서 업데이트 파일:
    - ```.gitignore```
    - ```tslint.json```
    - ```tsconfig.json```
    - ```tsconfig.inline.json```
    - ```ng-package.json```
    - ```angular.json```
    - ```src\tsconfig.app.json```
    - ```src\tsconfig.lib.json```
    - ```src\tsconfig.spec.json```

## 6. 일반적인 마이그레이션 문제를 이해 하는 SDK CLI를 사용 합니다.

프로젝트의 루트 폴더에서 다음 명령을 실행 합니다 CLI 수동으로 처리 해야 하는 일반적인 마이그레이션 문제를 살펴보고 프로젝트 감사 하려면:

``` cmd
wac updateSeven --audit
```

다음 문제는의 인스턴스를 찾을이 프로젝트에서.

### 이러한 sme 클래스를 사용 하 여 다음 CSS 클래스의 사용을 바꿉니다.

| 기존 CSS 클래스 | 새 CSS 클래스 |
| -- | -- |
| .auto 가변 크기 |  위치 가변 자동.sme |
| .border 모두 |  테두리 표시등이 sm.sme 및.sme-테두리-색-자료-90 |
| .border 아래쪽 |  테두리 아래쪽 sm.sme 및.sme-border-bottom-color-base-90 |
| .border 가로 |  테두리 가로 sm.sme 및.sme-border-horizontal-color-base-90 |
| .border 왼쪽 |  테두리 왼쪽 sm.sme 및.sme-border-left-color-base-90 |
| .border 오른쪽 |  테두리 오른쪽 sm.sme 및.sme-border-right-color-base-90 |
| .border 위쪽 |  테두리 위쪽 sm.sme 및.sme-border-top-color-base-90 |
| .border 바꾸기 |  테두리 세로 sm.sme 및.sme-border-vertical-color-base-90 |
| .break 단어 |  .sme 정렬-ws-잘림 |
| .btn |  .sme 단추 OR 단추 |
| .btn 기본 |  button.sme 단추 기본.sme OR.button.sme-단추-기본 |
| .color 어둡게 |  alt-.sme-색 |
| .color 조명 |  .sme 색 자료 |
| .color 연한 회색 |  색 기본 90.sme |
| .fixed 가변 크기 |  .sme-위치-가변-없음 |
| .flex 레이아웃 |  .sme-정렬-스택-h 또는.sme-정렬-스택-v |
| .font 굵게 |  강조-글꼴-.sme 1 |
| .highlight |  배경 색상 노란색.sme |
| .horizontal |  .sme-정렬-스택-h |
| 화면 스크롤 |  위치 가변 자동.sme |
| .nowrap |  .sme-정렬-스택-h 또는.sme-정렬-스택-v |
| .relative |  .sme 레이아웃 상대 |
| .relative 센터 |  .sme 레이아웃 절대.sme 위치 센터 |
| .reverse |  .sme-정렬-스택-취소 |
| .stretch 절대 |  .sme 레이아웃-절대.sme-위치-표시등이-없음 |
| .stretch 고정 |  고정 된 레이아웃.sme.sme-위치-표시등이-없음 |
| .stretch 바꾸기 |  위치 stretch v.sme |
| .stretch 너비 |  .sme 위치-stretch h |
| .vertical |  .sme-정렬-스택-v |
| .vertical 스크롤 전용 |  .sme-정렬-오버플로-숨기기-sme 정렬-오버플로-자동-xy |
| .wrap |  .sme-정렬-wrapstack-h 또는.sme-정렬-wrapstack-v |

### 이러한 sme 구성 요소를 사용 하 여 다음 구성 요소 사용을 바꿉니다.

| 오래 된 구성 요소 | 새 구성 요소 |
| -- | -- |
| .alert |  sme 경고 |
| .alert 위험 |  sme 경고 |
| .breadCrumb |  sme 경고 |
| .checkbox |  sme 양식 필드 [유형 = "확인란"] |
| .combobox |  sme 양식 필드 [유형 = "선택"] |
| .dashboard |  sme 레이아웃-콘텐츠-영역-채워짐 sme-정렬-스택-h |
| .details 패널 |  sme 속성 그리드 |
| .details 패널 컨테이너 |  sme 속성 그리드 |
| .details 탭 |  sme 속성 그리드 OR sme 피벗 |
| .details 래퍼 |  sme 속성 그리드 |
| .disabled |  sme 사용 안 함 |
| 양식 단추 | sme 양식 필드 |
| 양식 컨트롤 | sme 양식 필드 |
| 양식 컨트롤 | sme 양식 필드 |
| 양식 그룹 | sme 양식 필드 |
| 양식 그룹 레이블 | sme 양식 필드 |
| 양식 입력 | sme 양식 필드 |
| 양식 stretch | sme 양식 필드 |
| .input 파일 | sme 양식 필드 |
| .nav 탭 |  sme 피벗 |
| .radio |  sme 양식 필드 [유형 = "라디오"] |
| .required 신호 | sme 양식 필드 |
| .searchbox |  sme 양식 필드 [유형 = "검색"] |
| .toggle 스위치 |  sme 양식 필드 [유형 = "토글 스위치"] |
| .tool 컨테이너 |  sme 레이아웃-콘텐츠 영역 또는 sme 레이아웃-콘텐츠-영역-채워짐 |

### 이러한 CSS 클래스 사용 되지 않으며, 더 이상 지원 됩니다.

| 기존 클래스 | 사용 중단 |
| -- | -- |
| .acceptable | (사용 되지 않음) |
| .color 오류 | (사용 되지 않음) |
| .color 정보 | (사용 되지 않음) |
| .color 성공 | (사용 되지 않음) |
| .color 경고 | (사용 되지 않음) |
| .delete 단추 | (사용 되지 않음) |
| .details 콘텐츠 | (사용 되지 않음) |
| .error 커버 | (사용 되지 않음) |
| .error 메시지 | (사용 되지 않음) |
| .guided 창 단추 | (사용 되지 않음) |
| .header 컨테이너 | (사용 되지 않음) |
| win.icon | (사용 되지 않음) |
| .indent | (사용 되지 않음) |
| .invalid | (사용 되지 않음) |
| .item 목록 | (사용 되지 않음) |
| 스크롤 가능한.modal | (사용 되지 않음) |
| . 다중 섹션 | (사용 되지 않음) |
| 화면 작업 표시줄 | (사용 되지 않음) |
| .overflow 여백 | (사용 되지 않음) |
| .overflow 도구 | (사용 되지 않음) |
| .progress 커버 | (사용 되지 않음) |
| .right 패널 | (사용 되지 않음) |
| .rollup | (사용 되지 않음) |
| .rollup 상태 | (사용 되지 않음) |
| .rollup 제목 | (사용 되지 않음) |
| .rollup 값 | (사용 되지 않음) |
| .searchbox 작업 표시줄 | (사용 되지 않음) |
| .size-h-1 | (사용 되지 않음) |
| .size-h-2 | (사용 되지 않음) |
| .size-h-3 | (사용 되지 않음) |
| .size-h-4 | (사용 되지 않음) |
| .size-h-전체 | (사용 되지 않음) |
| .size-h-절반 | (사용 되지 않음) |
| .size-v-1 | (사용 되지 않음) |
| .size-v-2 | (사용 되지 않음) |
| .size-v-3 | (사용 되지 않음) |
| .size-v-4 | (사용 되지 않음) |
| .status 아이콘 | (사용 되지 않음) |
| .svg 16px | (사용 되지 않음) |
| .table 들여쓰기 | (사용 되지 않음) |
| .table sm | (사용 되지 않음) |
| .thin | (사용 되지 않음) |
| .tile | (사용 되지 않음) |
| .tile 본문 | (사용 되지 않음) |
| .tile 콘텐츠 | (사용 되지 않음) |
| .tile 폴더 | (사용 되지 않음) |
| .tile 헤더 | (사용 되지 않음) |
| .tile 레이아웃 | (사용 되지 않음) |
| .tile 테이블 | (사용 되지 않음) |
| .toolbar | (사용 되지 않음) |
| .tool 표시줄 | (사용 되지 않음) |
| .tool 헤더 | (사용 되지 않음) |
| .tool 헤더 기본 | (사용 되지 않음) |
| .tool 창 | (사용 되지 않음) |
| .usage 표시줄 | (사용 되지 않음) |
| .usage 표시줄 영역 | (사용 되지 않음) |
| .usage 바 배경 | (사용 되지 않음) |
| 제목 표시줄-.usage- | (사용 되지 않음) |
| .usage 표시줄 값 | (사용 되지 않음) |
| .usage 차트 | (사용 되지 않음) |
| .usage 메시지 | (사용 되지 않음) |
| .usage 메시지 영역 | (사용 되지 않음) |
| .usage 메시지 제목 | (사용 되지 않음) |
| .warning | (사용 되지 않음) |
| .white 공간 | (사용 되지 않음) |

## 7. 이해 하 고 개체를 사용 하 여 문제 해결

### 업데이트 ```rxjs``` 관찰 가능한 개체에 대 한 사용 하 여 작동 합니다.

이 변경 된 몇 가지 일반적인 함수 이름, 있을 다른 프로젝트에서.

* 업데이트 ```Observable.empty()``` 를 ```empty()```
* 업데이트 ```Observable.of()``` 를 ```of()```
* 업데이트 ```.switchMap()``` 를 ```.pipe(switchMap())```
* 업데이트 ```.map()``` 를 ```.pipe(map())```
* 업데이트 ```flatMap()``` 를 ```mergeMap()```


### 런타임 문제를 해결 ```.map()``` 및 ```.filter()``` 개체에는 함수

컴파일러가 제대로 식별할 수 없는 경우는 ```observable``` 개체의 형식 ```.map()``` 및 ```.filter()``` 에서 함수는 ```array``` 런타임 시 오류를 일으키는 개체에 개체 대신 매핑할 수 있습니다.  함수를 반환 하는 ```observable``` 이 문제를 방지 하기 위한 명시적 데이터 형식을 지정 하는 개체입니다.

```any``` 및 반환 형식이 없으므로이 문제가 발생할 수는 이러한 패턴을 사용 하 여 코드를 찾습니다.

``` ts
public getMyObservable(): any { //any return type can cause issues
 ...
}

public getMyObservable() { //no return type can cause issues
...
}
```

## 8. 다른 일반적인 문제를 해결 합니다.

이러한 기술을 다른 일반적인 문제를 해결 하는 데 도움이 됩니다.

* 실행 ```ng lint --fix``` 일반적인 보풀 문제를 해결 하려면
* 실행 ```gulp build``` 반복적으로 점차적으로 해결 실행 하는 ```gulp build``` 자동으로 해결할 수 있습니다

## 9. 빌드 및 제공 프로젝트

작성 하 고 최신 버전 (SDK 1.0)를 사용 하 여 프로젝트에 다음 명령을 실행 합니다.

``` cmd
gulp build
gulp serve --port 4201
```

## 10. Windows 관리 센터에서 어두운 테마 켜기

1902 이상 어두운 테마에서 Windows Admin Center 버전을 설정 하려면 다음이 단계를 따르세요.

* Open Windows Admin Center (1902 이상 버전)
* 창의 오른쪽 상단 모서리에서 **설정** 아이콘을 클릭
* **고급** 탭을 선택
* *실험 키* **추가** 클릭 합니다.
* 새 값을 입력 ```msft.sme.shell.personalization``` 에서 이전 단계에서 만든 있는 빈 필드
* **저장 하 고 다시 로드** 를 클릭 합니다.
* 지금 설정 **개인 설정**, 새 탭을 갖게 됩니다.  이 탭을 선택 합니다.
* **어둠 모드 (미리 보기)를** **색** 변경
