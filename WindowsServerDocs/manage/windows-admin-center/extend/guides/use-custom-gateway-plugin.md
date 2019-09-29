---
title: 도구 확장에 있는 사용자 지정 게이트웨이 플러그 인 사용
description: 도구 확장 개발 Windows 관리 센터 SDK (Project Honolulu)-도구 확장에서 사용자 지정 게이트웨이 플러그 인 사용
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 829cbf6df8cc2738bf4066b36210b860595774ed
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385233"
---
# <a name="use-a-custom-gateway-plugin-in-your-tool-extension"></a>도구 확장에 있는 사용자 지정 게이트웨이 플러그 인 사용

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

이 문서에서는 Windows 관리 센터 CLI를 사용 하 여 만든 새로운 빈 도구 확장에서 사용자 지정 게이트웨이 플러그 인을 사용 합니다.

## <a name="prepare-your-environment"></a>사용자 환경 준비 ##

아직 하지 않은 경우 [도구 확장 개발](../develop-tool.md) 의 지시에 따라 환경을 준비 하 고 비어 있는 새 도구 확장을 만듭니다.

## <a name="add-a-module-to-your-project"></a>프로젝트에 모듈 추가 ##

새 모듈을 아직 추가 하지 않은 경우 프로젝트에 추가 합니다 .이 [모듈](add-module.md) 은 다음 단계에서 사용할 수 있습니다.  

## <a name="add-integration-to-custom-gateway-plugin"></a>사용자 지정 게이트웨이 플러그 인에 통합 추가 ##

이제 방금 만든 비어 있는 새 모듈에서 사용자 지정 게이트웨이 플러그 인을 사용 합니다.

### <a name="create-pluginservicets"></a>플러그 인을 만듭니다. 서비스.

위에서 만든 새 도구 모듈의 디렉터리 (```\src\app\{!Module-Name}```)로 변경 하 고-1 @no__t 새 파일을 만듭니다.

앞에서 만든 파일에 다음 코드를 추가 합니다.
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

@No__t-0 및 ```Sample%20Uno```에 대 한 참조를 해당 기능 이름으로 변경 합니다.

[!WARNING]
> 기본 제공 ```this.appContextService.node```은 사용자 지정 게이트웨이 플러그 인에 정의 된 API를 호출 하는 데 사용 하는 것이 좋습니다. 이렇게 하면 게이트웨이 플러그 인 내에 자격 증명이 필요한 경우 적절 하 게 처리 됩니다.

### <a name="modify-modulets"></a>모듈을 수정 합니다.

이전에 만든 새 모듈의 ```module.ts``` 파일을 엽니다 (예: ```{!Module-Name}.module.ts```).

다음 import 문을 추가 합니다.

``` ts
import { HttpService } from '@microsoft/windows-admin-center-sdk/angular';
import { Http } from '@microsoft/windows-admin-center-sdk/core';
import { PluginService } from './plugin.service';
```

다음 공급자를 추가 합니다 (선언 후).

``` ts
  ,
  providers: [
    HttpService,
    PluginService,
    Http
  ]
```

### <a name="modify-componentts"></a>구성 요소를 수정 합니다.

이전에 만든 새 모듈의 ```component.ts``` 파일을 엽니다 (예: ```{!Module-Name}.component.ts```).

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

### <a name="modify-componenthtml"></a>구성 요소 html 수정 ###

이전에 만든 새 모듈의 ```component.html``` 파일을 엽니다 (예: ```{!Module-Name}.component.html```).

Html 파일에 다음 콘텐츠를 추가 합니다.
``` html
<button (click)="onClick()" >go</button>
{{ responseResult }}
```

## <a name="build-and-side-load-your-extension"></a>확장을 빌드하고 로드 합니다.

이제 Windows 관리 센터에서 확장을 [빌드하고 로드할](../develop-tool.md#build-and-side-load-your-extension) 준비가 되었습니다.
