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
ms.openlocfilehash: 2269a2ac2cabda6f8fdd829994f36e89d581bd23
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297010"
---
# 관리 되는 노드에 확장 페이로드 설치

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

## Setup
> [!NOTE]
> 이 가이드에는 필요한 빌드할 1.2.1904.02001 이상. 빌드를 확인 하려면 번호는 Windows Admin Center 열고 오른쪽 위에 있는 물음표를 클릭 합니다.

않은 경우 Windows Admin Center에 대 한 [도구 확장](../develop-tool.md) 을 만듭니다. 이 완료 한 후 확장을 만들 때 사용 되는 값의 참고:
| 값 | 설명 | 예 |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | 회사 이름 (공백 포함) | ```Contoso``` |
| ```{!Tool Name}``` | 사용자 도구 이름 (공백 포함) | ```InstallOnNode``` |

도구 확장 폴더 안에 만들기는 ```Node``` 폴더 (```{!Tool Name}\Node```). 이 API를 사용 하는 경우이 폴더에 배치 된 모든 요소는 관리 되는 노드에 복사 됩니다. 사용 사례에 필요한 모든 파일을 추가 합니다. 

또한 만들기는 ```{!Tool Name}\Node\installNode.ps1``` 스크립트입니다. 이 스크립트에서 모든 파일이 복사 되 면 관리 되는 노드에서 실행 됩니다는 ```{!Tool Name}\Node``` 관리 되는 노드에 폴더. 사용 사례에 대 한 추가 논리를 추가 합니다. 예 ```{!Tool Name}\Node\installNode.ps1``` 파일:

``` ps1
# Add logic for installing payload on managed node
echo 'Success'
```

> [!NOTE]
> ```{!Tool Name}\Node\installNode.ps1``` 이름이 특정 API를 찾습니다. 이 파일의 이름을 변경 하면 오류가 발생 합니다.


## UI와 통합

업데이트 ```\src\app\default.component.ts``` 다음:

``` ts
import { Component } from '@angular/core';
import { AppContextService } from '@microsoft/windows-admin-center-sdk/angular';
import { Observable } from 'rxjs';

@Component({
  selector: 'default-component',
  templateUrl: './default.component.html',
  styleUrls: ['./default.component.css']
})

export class DefaultComponent {
  constructor(private appContextService: AppContextService) { }

  public response: any;
  public loading = false;

  public installOnNode() {
    this.loading = true;
    this.post('{!Company Name}.{!Tool Name}', '1.0.0',
      this.appContextService.activeConnection.nodeName).subscribe(
        (response: any) => {
          console.log(response);
          this.response = response;
          this.loading = false;
        },
        (error) => {
          console.log(error);
          this.response = error;
          this.loading = false;
        }
      );
  }

  public post(id: string, version: string, targetNode: string): Observable<any> {
    return this.appContextService.node.post(targetNode,
      `features/extensions/${id}/versions/${version}/install`);
  }

}
```
자리 표시자를 확장을 만들 때 사용 된 값을 업데이트 합니다.
``` ts
this.post('contoso.install-on-node', '1.0.0',
      this.appContextService.activeConnection.nodeName).subscribe(
        (response: any) => {
          console.log(response);
          this.response = response;
          this.loading = false;
        },
        (error) => {
          console.log(error);
          this.response = error;
          this.loading = false;
        }
      );
```

또한 업데이트 ```\src\app\default.component.html``` 하려면:
``` html
<button (click)="installOnNode()">Click to install</button>
<sme-loading-wheel *ngIf="loading" size="large"></sme-loading-wheel>
<p *ngIf="response">{{response}}</p>
```
마지막으로 하 고 ```\src\app\default.module.ts```:
``` ts
import { CommonModule } from '@angular/common';
import { NgModule } from '@angular/core';

import { LoadingWheelModule } from '@microsoft/windows-admin-center-sdk/angular';
import { DefaultComponent } from './default.component';
import { Routing } from './default.routing';

@NgModule({
  imports: [
    CommonModule,
    LoadingWheelModule,
    Routing
  ],
  declarations: [DefaultComponent]
})
export class DefaultModule { }

```

## 만들고 NuGet 패키지 설치

마지막 단계 NuGet 패키지를 추가한 파일을 사용 하 여 작성 및 다음 Windows 관리 센터에서 해당 패키지를 설치 합니다.

하기 전에 확장 패키지를 만들지 않은 경우 [확장 게시](../publish-extensions.md) 가이드를 따릅니다. 
> [!IMPORTANT]
> 이 확장에 대 한.nuspec 파일에서 것이 중요 하는 ```<id>``` 값에서 프로젝트의 이름과 일치 ```manifest.json``` 및 ```<version>``` 추가 된 항목 일치 ```\src\app\default.component.ts```. 또한 아래 항목을 추가 ```<files>```: 

> ```<file src="Node\**\*.*" target="Node" />```.

``` xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2011/08/nuspec.xsd">
  <metadata>
    <id>contoso.install-on-node</id>
    <version>1.0.0</version>
    <authors>Contoso</authors>
    <owners>Contoso</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <projectUrl>https://msft-sme.myget.org/feed/windows-admin-center-feed/package/nuget/contoso.sme.install-on-node-extension</projectUrl>
    <licenseUrl>http://YourLicenseLink</licenseUrl>
    <iconUrl>http://YourLogoLink</iconUrl>
    <description>Install on node extension by Contoso</description>
    <copyright>(c) Contoso. All rights reserved.</copyright> 
  </metadata>
    <files>
    <file src="bundle\**\*.*" target="ux" />
    <file src="package\**\*.*" target="gateway" />
    <file src="Node\**\*.*" target="Node" />
  </files>
</package>
```

이 패키지를 만든 후 해당 피드를 경로 추가 합니다. Windows Admin Center에서 설정 gt_ 확장 gt_ 피드 이동한 다음 해당 패키지가에 경로 추가 합니다. 확장 완료 되 면 설치 되 고 있어야 클릭 하는 ```install``` 단추와 API가 호출 됩니다.  