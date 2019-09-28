---
title: 도구 확장에 모듈 추가
description: 도구 확장 개발 Windows 관리 센터 SDK (Project Honolulu)-도구 확장에 모듈 추가
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 9d30980ca404187ff1481242c1c0ef0a3d571416
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357103"
---
# <a name="add-a-module-to-a-tool-extension"></a>도구 확장에 모듈 추가

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

이 문서에서는 Windows 관리 센터 CLI를 사용 하 여 만든 도구 확장에 빈 모듈을 추가 합니다.

## <a name="prepare-your-environment"></a>사용자 환경 준비

아직 하지 않은 경우 [도구](../develop-tool.md) (또는 [솔루션](../develop-solution.md)) 확장 개발의 지시에 따라 환경을 준비 하 고 비어 있는 새 도구 확장을 만듭니다.

## <a name="use-the-angular-cli-to-create-a-module-and-component"></a>각도 CLI를 사용 하 여 모듈 (및 구성 요소) 만들기

Angular를 처음 사용하는 경우 Angular.Io 웹 사이트의 설명서를 참조하여 Angular 및 NgModule에 대해 자세한 내용을 알아보는 것이 좋습니다. NgModule에 대한 자세한 내용은 https://angular.io/guide/ngmodule 로 이동합니다.

* Angular CLI에서 새 모듈을 생성하는 방법에 대한 자세한 내용: https://github.com/angular/angular-cli/wiki/generate-module
* Angular CLI에서 새 구성 요소를 생성하는 방법에 대한 자세한 내용: https://github.com/angular/angular-cli/wiki/generate-component


명령 프롬프트를 열고 프로젝트에서 \src\app로 디렉터리를 변경한 후 다음 명령을 실행 합니다. ```{!ModuleName}```을 모듈 이름 (공백 제거)으로 바꿉니다.

```
cd \src\app
ng generate module {!ModuleName}
ng generate component {!ModuleName}
```

| 값 | 설명 | 예제 |
| ----- | ----------- | ------- |
| ```{!ModuleName}``` | 모듈 이름(공백 제거) | ```ManageFooWorksPortal``` |

사용 예제:
```
cd \src\app
ng generate module ManageFooWorksPortal
ng generate component ManageFooWorksPortal
```


## <a name="add-routing-information"></a>라우팅 정보 추가

Angular를 처음 사용하는 경우 Angular 라우팅 및 탐색에 대해 알아보는 것이 좋습니다. 아래 섹션에서는 사용자 활동에 대한 응답으로 Windows Admin Center가 확장으로 이동하고 확장의 보기 간에 이동하도록 만드는 필수 라우팅 요소를 정의합니다. 자세한 내용은 https://angular.io/guide/router 로 이동합니다.

위의 단계에서 사용한 것과 동일한 모듈 이름을 사용 합니다.

### <a name="add-content-to-new-routing-file"></a>새 라우팅 파일에 콘텐츠 추가

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

    | 값 | 설명 | 예제 |
    | ----- | ----------- | ------- |
    | ```{!ModuleName}``` | 모듈 이름(공백 제거) | ```ManageFooWorksPortal``` |
    | ```{!module-name}``` | 모듈 이름(소문자, 공백을 파선으로 대체) | ```manage-foo-works-portal``` |

### <a name="add-content-to-new-module-file"></a>새 모듈 파일에 콘텐츠 추가

다음 명명 규칙을 따라 찾은 파일 ```{!module-name}.module.ts```를 엽니다.

| 값 | 설명 | 예제 파일 이름 |
| ----- | ----------- | ------- |
| ```{!module-name}``` | 모듈 이름(소문자, 공백을 파선으로 대체) | ```manage-foo-works-portal.module.ts``` |

* 파일에 콘텐츠를 추가합니다.

    ``` ts
    import { Routing } from './{!module-name}.routing';
    ```

* 방금 추가한 콘텐츠의 값을 원하는 값으로 바꿉니다.

    | 값 | 설명 | 예제 |
    | ----- | ----------- | ------- |
    | ```{!module-name}``` | 모듈 이름(소문자, 공백을 파선으로 대체) | ```manage-foo-works-portal``` |

* 라우팅을 가져올 가져오기 명령문을 수정합니다.

    | 원래 값 | 새로운 값 |
    | -------------- | --------- |
    | ```imports: [ CommonModule ]``` | ```imports: [ CommonModule, Routing ]``` |

* ```import``` 명령문이 원본에 의해 사전순으로 정렬되었는지 확인합니다.

### <a name="add-content-to-new-component-typescript-file"></a>새 구성 요소 typescript 파일에 콘텐츠 추가

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
### <a name="update-app-routingmodulets"></a>App-v를 업데이트 합니다.

파일 ```app-routing.module.ts```을 열고, 기본 경로를 수정 하 여 방금 만든 새 모듈을 로드 합니다.  @No__t-0에 대 한 항목을 찾고 ```loadChildren```을 업데이트 하 여 기본 모듈 대신 모듈을 로드 합니다.

| 값 | 설명 | 예제 |
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


## <a name="build-and-side-load-your-extension"></a>확장을 빌드하고 로드 합니다.

이제 확장에 모듈을 추가 했습니다.  다음으로 Windows 관리 센터에서 확장을 [빌드하고 로드](../develop-tool.md#build-and-side-load-your-extension) 하 여 결과를 볼 수 있습니다.
