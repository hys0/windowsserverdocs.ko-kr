---
title: 도구 확장 개발
description: 개발 도구 확장 Windows Admin Center SDK (프로젝트 브라 티)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 1a068c0d33887e8e9287ff15c1aa14f3dc84915a
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445936"
---
# <a name="install-extension-payload-on-a-managed-node"></a>관리 되는 노드에서 확장 페이로드를 설치 합니다.

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

## <a name="setup"></a>설치 프로그램
> [!NOTE]
> 이 가이드에 따라 필요한 만들어야 1.2.1904.02001 이상. 빌드를 검사할 수는 Windows Admin Center 열고 오른쪽 위에 있는 물음표를 클릭 합니다.

이미 않았다면 만듭니다는 [확장 도구](../develop-tool.md) Windows Admin Center 대 한 합니다. 이 확인을 마친 후 확장을 만들 때 사용한 값을 기록 합니다.

| 값 | 설명 | 예제 |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | 회사 이름 (공백 포함) | ```Contoso``` |
| ```{!Tool Name}``` | 사용자 도구 이름 (공백 포함) | ```InstallOnNode``` |

사용자 도구 확장 폴더 안에 만듭니다는 ```Node``` 폴더 (```{!Tool Name}\Node```). 이 API를 사용 하는 경우이 폴더에 배치 된 모든 개체를 관리 노드로 복사 됩니다. 사용 사례에 필요한 모든 파일을 추가 합니다. 

만들 수도 ```{!Tool Name}\Node\installNode.ps1``` 스크립트입니다. 모든 파일에서 복사 되 면 관리 되는 노드에서이 스크립트를 실행할 수는 ```{!Tool Name}\Node``` 를 관리 노드로 폴더입니다. 사용 사례에 대 한 추가 논리를 추가 합니다. 예로 ```{!Tool Name}\Node\installNode.ps1``` 파일:

``` ps1
# Add logic for installing payload on managed node
echo 'Success'
```

> [!NOTE]
> ```{!Tool Name}\Node\installNode.ps1``` 에 대 한 API를 검색 하는 특정 이름을 있습니다. 이 파일의 이름을 변경 하면 오류가 발생 합니다.


## <a name="integration-with-ui"></a>UI 사용 하 여 통합

업데이트 ```\src\app\default.component.ts``` 다음과:

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
확장을 만들 때 사용 된 값을 자리 표시자를 업데이트 합니다.
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
마지막으로 ```\src\app\default.module.ts```:
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

## <a name="creating-and-installing-a-nuget-package"></a>만들기 및 NuGet 패키지를 설치 합니다.

마지막 단계 추가 했습니다 파일과 함께 NuGet 패키지를 작성 및 다음 Windows Admin Center 해당 패키지를 설치 합니다.

에 따라 합니다 [게시 확장](../publish-extensions.md) 하기 전에 확장 패키지를 만들지 않은 경우 가이드입니다. 
> [!IMPORTANT]
> 이 확장에 대 한.nuspec 파일에서 중요 한 것입니다를 ```<id>``` 값이 프로젝트의 이름과 일치 ```manifest.json``` 및 ```<version>``` 에 추가 된 기능을 일치 ```\src\app\default.component.ts```합니다. 아래에 있는 항목을 추가할 수도 ```<files>```: 
> 
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

이 패키지를 만든 후 해당 피드 경로 추가 합니다. Windows Admin Center 설정으로 이동 > 확장 > 피드를 패키지에 있는 경로 추가 합니다. 확장 완료 되 면 설치 되 고 클릭 수 있습니다는 ```install``` 단추 및 API 호출 됩니다.  