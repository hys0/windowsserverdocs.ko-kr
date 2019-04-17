---
title: 도구 확장에 모듈을 추가
description: Windows Admin Center SDK (Project Honolulu) 도구 확장 개발-모듈 도구 확장을 추가
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: e6978ce20a7c6da8addb217de8d30f733b40d261
ms.sourcegitcommit: be0144eb59daf3269bebea93cb1c467d67e2d2f1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/20/2018
ms.locfileid: "4081210"
---
# 도구 확장에 모듈을 추가

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

이 문서는 빈 모듈 Windows Admin Center CLI를 사용 하 여 만든 도구 확장을 추가 합니다.

## 사용자 환경 준비

아직 수행 지시에 새, 빈 도구 확장을 만들고 환경을 준비 [도구](..\develop-tool.md) (또는 [솔루션](..\develop-solution.md)) 확장을 개발 합니다.

## Angular CLI를 사용 하 여 모듈 (및 구성 요소)를 만듭니다

Angular를 처음 사용하는 경우 Angular.Io 웹 사이트의 설명서를 참조하여 Angular 및 NgModule에 대해 자세한 내용을 알아보는 것이 좋습니다. NgModule에 대한 자세한 내용은 https://angular.io/guide/ngmodule로 이동합니다.

* Angular CLI에서 새 모듈을 생성하는 방법에 대한 자세한 내용: https://github.com/angular/angular-cli/wiki/generate-module
* Angular CLI에서 새 구성 요소를 생성하는 방법에 대한 자세한 내용: https://github.com/angular/angular-cli/wiki/generate-component


명령 프롬프트를 열고, 프로젝트에서 \src\app을 디렉터리를 변경한 다음 바꿔 다음 명령을 실행 ```{!ModuleName}``` 모듈 이름 (공백 제거)를 사용 하 여:

```
cd \src\app
ng generate module {!ModuleName}
ng generate component {!ModuleName}
```

| 값 | 설명 | 예 |
| ----- | ----------- | ------- |
| ```{!ModuleName}``` | 모듈 이름(공백 제거) | ```ManageFooWorksPortal``` |

사용 예제:
```
cd \src\app
ng generate module ManageFooWorksPortal
ng generate component ManageFooWorksPortal
```


## 라우팅 정보 추가

Angular를 처음 사용하는 경우 Angular 라우팅 및 탐색에 대해 알아보는 것이 좋습니다. 아래 섹션에서는 사용자 활동에 대한 응답으로 Windows Admin Center가 확장으로 이동하고 확장의 보기 간에 이동하도록 만드는 필수 라우팅 요소를 정의합니다. 자세한 내용은 https://angular.io/guide/router로 이동합니다.

위의 단계에서 사용한 것과 동일한 모듈 이름을 사용 합니다.

### 새 라우팅 파일에 콘텐츠 추가

* 이전 단계에서 ``` ng generate ```로 만들 모듈 폴더로 이동합니다.

* 이 명명 규칙을 따라 새 파일 ```{!module-name}.routing.ts```를 만듭니다.

    | 값 | 설명 | 예제 파일 이름 |
    | ----- | ----------- | ------- |
    | ```{!module-name}``` | 모듈 이름(소문자, 공백을 파선으로 대체) | ```manage-foo-works-portal.routing.ts``` |

* 방금 만든 파일에 이 콘텐츠를 추가합니다.

    ``` ts
    import { NgModule } from '@angular/core';
    import { RouterModule, Routes } from '@angular/router';
    import { {!ModuleName}Component } from './{!module-name}.component';

    const routes: Routes = [
        {
            path: '',
            component: {!ModuleName}Component,
            // if the component has child components that need to be routed to, include them in the children array.
            children: [
                {
                    path: '', 
                    redirectTo: 'base',
                    pathMatch: 'full'
                }
            ]
    }];

    @NgModule({
        imports: [
            RouterModule.forChild(routes)
        ],
        exports: [
            RouterModule
        ]
    })
    export class Routing { }
    ```

* 방금 만든 파일의 값을 원하는 값으로 바꿉니다.

    | 값 | 설명 | 예 |
    | ----- | ----------- | ------- |
    | ```{!ModuleName}``` | 모듈 이름(공백 제거) | ```ManageFooWorksPortal``` |
    | ```{!module-name}``` | 모듈 이름(소문자, 공백을 파선으로 대체) | ```manage-foo-works-portal``` |

### 새 모듈 파일에 콘텐츠 추가

다음 명명 규칙을 따라 찾은 파일 ```{!module-name}.module.ts```를 엽니다.

| 값 | 설명 | 예제 파일 이름 |
| ----- | ----------- | ------- |
| ```{!module-name}``` | 모듈 이름(소문자, 공백을 파선으로 대체) | ```manage-foo-works-portal.module.ts``` |

* 파일에 콘텐츠를 추가합니다.

    ``` ts
    import { Routing } from './{!module-name}.routing';
    ```

* 방금 추가한 콘텐츠의 값을 원하는 값으로 바꿉니다.

    | 값 | 설명 | 예 |
    | ----- | ----------- | ------- |
    | ```{!module-name}``` | 모듈 이름(소문자, 공백을 파선으로 대체) | ```manage-foo-works-portal``` |

* 라우팅을 가져올 가져오기 명령문을 수정합니다.

    | 원래 값 | 새 값 |
    | -------------- | --------- |
    | ```imports: [ CommonModule ]``` | ```imports: [ CommonModule, Routing ]``` |

* ```import``` 명령문이 원본에 의해 사전순으로 정렬되었는지 확인합니다.

### 새 구성 요소 typescript 파일에 콘텐츠 추가

다음 명명 규칙을 따라 찾은 파일 ```{!module-name}.component.ts```를 엽니다.

| 값 | 설명 | 예제 파일 이름 |
| ----- | ----------- | ------- |
| ```{!module-name}``` | 모듈 이름(소문자, 공백을 파선으로 대체) | ```manage-foo-works-portal.component.ts``` |
    
파일의 콘텐츠를 다음으로 수정합니다.

``` ts
constructor() {
    // TODO
}

public ngOnInit() {
    // TODO
}
```
### Routing.module.ts 앱 업데이트

파일 열기 ```app-routing.module.ts```를 방금 만든 새 모듈을 로드 하는 기본 경로 수정 합니다.  에 대 한 항목을 찾을 ```path: ''```를 업데이트 하 고 ```loadChildren``` 기본 모듈 대신 모듈을 로드 하려면:

| 값 | 설명 | 예 |
| ----- | ----------- | ------- |
| ```{!ModuleName}``` | 모듈 이름(공백 제거) | ```ManageFooWorksPortal``` |
| ```{!module-name}``` | 모듈 이름(소문자, 공백을 파선으로 대체) | ```manage-foo-works-portal``` |

``` ts
    {
        path: '', 
        loadChildren: 'app/{!module-name}/{!module-name}.module#{!ModuleName}Module'
    },
```
업데이트 된 기본 경로의 예는 다음과 같습니다.
``` ts
    {
        path: '', 
        loadChildren: 'app/manage-foo-works-portal/manage-foo-works-portal.module#ManageFooWorksPortalModule'
    },
```


## 빌드 및 사이드 로드 확장

이제 모듈에 추가한 확장 합니다.  다음으로 하면 [빌드 및 사이드 로드](..\develop-tool.md#build-and-side-load-your-extension) 결과 확인을 위해 Windows Admin Center 확장 됩니다.
