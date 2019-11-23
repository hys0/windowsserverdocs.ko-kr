---
title: 도구 확장 개발
description: 도구 확장 Windows 관리 센터 SDK 개발 (Project Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: c5c87be882a32958946198eb6ff1b9d7000577e7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385294"
---
# <a name="install-extension-payload-on-a-managed-node"></a>관리 노드에 확장 페이로드 설치

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

## <a name="setup"></a>설정
> [!NOTE]
> 이 가이드를 따르려면 빌드 1.2.1904.02001 이상이 필요 합니다. 빌드 번호를 확인 하려면 Windows 관리 센터를 열고 오른쪽 위에 있는 물음표를 클릭 합니다.

Windows 관리 센터에 대 한 [도구 확장](../develop-tool.md) 을 아직 만들지 않은 경우 만듭니다. 이 작업을 완료 한 후에는 확장을 만들 때 사용 된 값을 기록해 둡니다.

| 값 | 설명 | 예 |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | 회사 이름 (공백 포함) | ```Contoso``` |
| ```{!Tool Name}``` | 도구 이름 (공백 포함) | ```InstallOnNode``` |

도구 확장 폴더 내에 ```Node``` 폴더 (```{!Tool Name}\Node```)를 만듭니다. 이 API를 사용 하는 경우이 폴더에 배치 된 모든 항목이 관리 노드에 복사 됩니다. 사용 사례에 필요한 파일을 추가 합니다. 

또한 ```{!Tool Name}\Node\installNode.ps1``` 스크립트를 만듭니다. 모든 파일이 ```{!Tool Name}\Node``` 폴더에서 관리 노드로 복사 되 면 관리 되는 노드에서이 스크립트를 실행 합니다. 사용 사례에 대 한 추가 논리를 추가 합니다. 예제 ```{!Tool Name}\Node\installNode.ps1``` 파일은 다음과 같습니다.

``` ps1
# Add logic for installing payload on managed node
echo 'Success'
```

> [!NOTE]
> ```{!Tool Name}\Node\installNode.ps1```에는 API가 찾는 특정 이름이 있습니다. 이 파일의 이름을 변경 하면 오류가 발생 합니다.


## <a name="integration-with-ui"></a>UI와 통합

다음으로 ```\src\app\default.component.ts```를 업데이트 합니다.

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
확장을 만들 때 사용 된 값으로 자리 표시자를 업데이트 합니다.
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

또한 ```\src\app\default.component.html```를 업데이트 합니다.
``` html
<button (click)="installOnNode()">Click to install</button>
<sme-loading-wheel *ngIf="loading" size="large"></sme-loading-wheel>
<p *ngIf="response">{{response}}</p>
```
그리고 마지막으로 ```\src\app\default.module.ts```합니다.
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

## <a name="creating-and-installing-a-nuget-package"></a>NuGet 패키지 만들기 및 설치

마지막 단계는 추가한 파일을 사용 하 여 NuGet 패키지를 빌드한 다음 Windows 관리 센터에서 해당 패키지를 설치 하는 것입니다.

이전에 확장 패키지를 만들지 않은 경우 [게시 확장](../publish-extensions.md) 가이드를 따르세요. 
> [!IMPORTANT]
> 이 확장에 대 한 nuspec 파일에서 ```<id>``` 값이 프로젝트 ```manifest.json```의 이름과 일치 하 고 ```<version>``` ```\src\app\default.component.ts```에 추가 된 항목과 일치 하는 것이 중요 합니다. 또한 ```<files>```아래에 항목을 추가 합니다. 
> 
> ```<file src="Node\**\*.*" target="Node" />```을 참조하십시오.

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

이 패키지를 만든 후에는 해당 피드에 경로를 추가 합니다. Windows 관리 센터에서 설정 > 확장 > 피드로 이동 하 여 패키지가 있는 위치에 경로를 추가 합니다. 확장이 설치 되 면 ```install``` 단추를 클릭 하 여 API가 호출 됩니다.  