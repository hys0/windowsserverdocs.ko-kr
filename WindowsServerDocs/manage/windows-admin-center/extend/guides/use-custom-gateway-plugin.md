---
title: 도구 확장에 있는 사용자 지정 게이트웨이 플러그 인 사용
description: Windows Admin Center SDK (프로젝트 브라 티) 도구 확장을 개발-도구 확장에서 사용자 지정 게이트웨이 플러그 인을 사용 하 여
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: c9b2e9201d58472286b42a9c89a36423f40d143d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834514"
---
# <a name="use-a-custom-gateway-plugin-in-your-tool-extension"></a>도구 확장에 있는 사용자 지정 게이트웨이 플러그 인 사용

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

이 문서에서는 Windows Admin Center CLI를 사용 하 여 만든 새로운 빈 도구 확장에서 사용자 지정 게이트웨이 플러그 인을 사용 합니다.

## <a name="prepare-your-environment"></a>사용자 환경 준비 ##

이미 않았다면의 지시를 따릅니다 [개발 도구 확장](..\develop-tool.md) 환경을 준비 하 고 새 빈 도구 확장 합니다.

## <a name="add-a-module-to-your-project"></a>프로젝트에 모듈을 추가 합니다. ##

이미 않았다면 새 추가 [빈 모듈](add-module.md) 다음 단계에서 사용 하는 프로젝트에 있습니다.  

## <a name="add-integration-to-custom-gateway-plugin"></a>통합 사용자 지정 게이트웨이 플러그 인 추가 ##

이제 방금 만든 비어 있는 모듈의 사용자 지정 게이트웨이 플러그 인을 사용 하겠습니다.

### <a name="create-pluginservicets"></a>Plugin.service.ts 만들기

위에서 만든 새 도구 모듈의 디렉터리 (```\src\app\{!Module-Name}```), 새 파일을 만들고 ```plugin.service.ts```합니다.

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

에 대 한 참조를 변경 ```Sample Uno``` 고 ```Sample%20Uno``` 적절 하 게 기능 이름입니다.

### <a name="modify-modulets"></a>Module.ts 수정

엽니다는 ```module.ts``` 앞에서 만든 새 모듈의 파일 (예: ```{!Module-Name}.module.ts```):

다음 import 문을 추가 합니다.

``` ts
import { HttpService } from '@microsoft/windows-admin-center-sdk/angular';
import { Http } from '@microsoft/windows-admin-center-sdk/core';
import { PluginService } from './plugin.service';
```

(선언) 뒤에 다음 공급자를 추가 합니다.

``` ts
  ,
  providers: [
    HttpService,
    PluginService,
    Http
  ]
```

### <a name="modify-componentts"></a>Component.ts 수정

엽니다는 ```component.ts``` 앞에서 만든 새 모듈의 파일 (예: ```{!Module-Name}.component.ts```):

다음 import 문을 추가 합니다.

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

### <a name="modify-componenthtml"></a>Modify component.html ###

엽니다는 ```component.html``` 앞에서 만든 새 모듈의 파일 (예: ```{!Module-Name}.component.html```):

Html 파일에 다음 콘텐츠를 추가 합니다.
``` html
<button (click)="onClick()" >go</button>
{{ responseResult }}
```

## <a name="build-and-side-load-your-extension"></a>빌드 및 쪽에 확장을 로드합니다.

준비가 이제 [빌드 및 부하 쪽](..\develop-tool.md#build-and-side-load-your-extension) Windows Admin Center 확장 합니다.
