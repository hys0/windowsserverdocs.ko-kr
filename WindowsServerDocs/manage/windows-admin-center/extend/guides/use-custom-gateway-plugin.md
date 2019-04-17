---
title: 도구 확장에 있는 사용자 지정 게이트웨이 플러그 인 사용
description: Windows Admin Center SDK (Project Honolulu) 도구 확장 개발-도구 확장에 사용자 지정 게이트웨이 플러그 인 사용
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 4652616478b7b05bde97db48bf84648984b5a325
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296765"
---
# 도구 확장에 있는 사용자 지정 게이트웨이 플러그 인 사용

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

이 문서에서는 Windows Admin Center CLI를 사용 하 여 만든 새, 빈 도구 확장에 사용자 지정 게이트웨이 플러그 인을 사용 합니다.

## 사용자 환경 준비 ##

않은 경우 새, 빈 도구 확장을 만들고 환경을 준비 [도구 확장 개발](..\develop-tool.md) 에 지시를 따릅니다.

## 프로젝트에 모듈 추가 ##

않은 경우 다음 단계에서 사용 하는 프로젝트에 새 [빈 모듈](add-module.md) 을 추가 합니다.  

## 사용자 지정 게이트웨이 플러그 인에 통합 추가 ##

이제 방금 만든 새, 빈 모듈에서 사용자 지정 게이트웨이 플러그 인을 사용 됩니다.

### Plugin.service.ts 만들기

위에서 만든 새 도구 모듈의 디렉터리를 변경 (```\src\app\{!Module-Name}```), 새 파일을 만듭니다 ```plugin.service.ts```.

방금 만든 파일에 다음 코드를 추가 합니다.
``` ts
import { Injectable } from '@angular/core';
import { AppContextService, HttpService } from '@microsoft/windows-admin-center-sdk/angular';
import { Cim, Http, PowerShell, PowerShellSession } from '@microsoft/windows-admin-center-sdk/core';
import { AjaxResponse, Observable } from 'rxjs';

@Injectable()
export class PluginService {
    constructor(private appContextService: AppContextService, private http: Http) {
    }
    
    public getGatewayRestResponse(): Observable<any> {
        let callUrl = this.appContextService.activeConnection.nodeName;

        return this.appContextService.node.get(callUrl, 'features/Sample%20Uno').map(
            (response: any) => {
                return response;
            }
        )
    }
}
```

변경에 대 한 참조가 ```Sample Uno``` 및 ```Sample%20Uno``` 를 적절 하 게 기능 이름으로 합니다.

[!WARNING]
> 기본 제공 하는 권장 ```this.appContextService.node``` 에 사용자 지정 게이트웨이 플러그 인에 정의 된 모든 API를 호출 하는 데 사용 됩니다. 이렇게 하면 하는 자격 증명 하는 것은 올바르게 처리 하 여 게이트웨이 플러그 인 내에서 필요한 경우.

### Module.ts 수정

Open 합니다 ```module.ts``` 앞에서 만든 새 모듈의 파일 (예: ```{!Module-Name}.module.ts```):

다음 가져오기 문을 추가 합니다.

``` ts
import { HttpService } from '@microsoft/windows-admin-center-sdk/angular';
import { Http } from '@microsoft/windows-admin-center-sdk/core';
import { PluginService } from './plugin.service';
```

(선언) 후 다음 공급자를 추가 합니다.

``` ts
  ,
  providers: [
    HttpService,
    PluginService,
    Http
  ]
```

### Component.ts 수정

Open 합니다 ```component.ts``` 앞에서 만든 새 모듈의 파일 (예: ```{!Module-Name}.component.ts```):

다음 가져오기 문을 추가 합니다.

``` ts
import { ActivatedRouteSnapshot } from '@angular/router';
import { AppContextService } from '@microsoft/windows-admin-center-sdk/angular';
import { Subscription } from 'rxjs';
import { Strings } from '../../generated/strings';
import { PluginService } from './plugin.service';
```

다음 변수를 추가 합니다.

``` ts
  private serviceSubscription: Subscription;
  private responseResult: string;
```

생성자를 수정 하 고 다음 함수를 수정/추가 합니다.

``` ts
  constructor(private appContextService: AppContextService, private plugin: PluginService) {
    //
  }

  public ngOnInit() {
    this.responseResult = 'click go to do something';
  }

  public onClick() {
    this.serviceSubscription = this.plugin.getGatewayRestResponse().subscribe(
      (response: any) => {
        this.responseResult = 'response: ' + response.message;
      },
      (error) => {
        console.log(error);
      }
    );
  }
```

### Component.html 수정 ###

Open 합니다 ```component.html``` 앞에서 만든 새 모듈의 파일 (예: ```{!Module-Name}.component.html```):

Html 파일에 다음 콘텐츠를 추가 합니다.
``` html
<button (click)="onClick()" >go</button>
{{ responseResult }}
```

## 빌드 및 사이드 로드 확장

마쳤으면 이제 준비 [빌드 및 사이드 로드](..\develop-tool.md#build-and-side-load-your-extension) 에 Windows Admin Center 확장 합니다.
