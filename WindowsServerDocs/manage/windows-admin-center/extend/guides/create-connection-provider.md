---
title: 솔루션 확장에 대 한 연결 공급자 만들기
description: Windows Admin Center SDK (Project Honolulu) 솔루션 확장 개발-연결 공급자 만들기
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 883fba96fcb71cb1c6e8162c1564d66924c4e24d
ms.sourcegitcommit: be0144eb59daf3269bebea93cb1c467d67e2d2f1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/20/2018
ms.locfileid: "4081140"
---
# 솔루션 확장에 대 한 연결 공급자 만들기

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

연결 공급자에서 Windows Admin Center 정의 하 고 연결 가능한 개체 또는 대상와 통신 하는 방법을 중요 한 역할을 재생 합니다. 주로 연결 공급자 연결 이루어지고, 같은 대상 온라인 상태이 고, 사용 가능한 지 확인 하 고 또한 연결 하는 사용자는 대상에 액세스 권한이 있는지 확인 하는 동안 작업을 수행 합니다.

기본적으로 Windows Admin Center는 다음 연결 공급자와 함께 배송 된:

* 서버
* Windows 클라이언트
* 장애 조치(failover) 클러스터
* HCI 클러스터

사용자 지정 연결 공급자를 만들려면 다음이 단계를 따르세요.

* 연결 공급자 세부 정보를 추가 ```manifest.json```
* 연결 상태 공급자를 정의 합니다.
* 응용 프로그램 계층의 연결 공급자를 구현 합니다.

## Manifest.json를 연결 공급자 정보를 추가 합니다.

이제 프로젝트에 연결 공급자를 정의 하기 위해 알아야 할 사항 살펴봅니다 ```manifest.json``` 파일.

### Manifest.json에 항목 만들기

```manifest.json``` 파일은 \src 폴더에 있으며 특히, 프로젝트에 진입점의 정의 포함 합니다. 진입점 유형의 도구, 솔루션 및 연결 공급자를 포함 합니다. 연결 공급자를 정의 하겠습니다 것입니다.

Manifest.json에 연결 공급자 항목의 예제는 다음과 같습니다.

``` json
    {
      "entryPointType": "connectionProvider",
      "name": "addServer",
      "path": "/add",
      "displayName": "resources:strings:addServer_displayName",
      "icon": "sme-icon:icon-win-server",
      "description": "resources:strings:description",
      "connectionType": "msft.sme.connection-type.server",
      "connectionTypeName": "resources:strings:addServer_connectionTypeName",
      "connectionTypeUrlName": "server",
      "connectionTypeDefaultSolution": "msft.sme.server-manager!servers",
      "connectionTypeDefaultTool": "msft.sme.server-manager!overview",
      "connectionStatusProvider": {
        "powerShell": {
          "script": "## Get-My-Status ##\nfunction Get-Status()\n{\n# A function like this would be where logic would exist to identify if a node is connectable.\n$status = @{label = $null; type = 0; details = $null; }\n$caption = \"MyConstCaption\"\n$productType = \"MyProductType\"\n# A result object needs to conform to the following object structure to be interpreted properly by the Windows Admin Center shell.\n$result = @{ status = $status; caption = $caption; productType = $productType; version = $version }\n# DO FANCY LOGIC #\n# Once the logic is complete, the following fields need to be populated:\n$status.label = \"Display Thing\"\n$status.type = 0 # This value needs to conform to the LiveConnectionStatusType enum. >= 3 represents a failure.\n$status.details = \"success stuff\"\nreturn $result}\nGet-Status"
        },
        "displayValueMap": {
          "wmfMissing-label": "resources:strings:addServer_status_wmfMissing_label",
          "wmfMissing-details": "resources:strings:addServer_status_wmfMissing_details",
          "unsupported-label": "resources:strings:addServer_status_unsupported_label",
          "unsupported-details": "resources:strings:addServer_status_unsupported_details"
        }
      }
    },
```

"ConnnectionProvider" 형식의 진입점 구성 중인 항목 연결 상태를 확인 하는 솔루션에서 사용 될 수 있는 공급자는 Windows Admin Center 셸을 나타냅니다. 연결 공급자 진입점 다양 한 아래에 정의 된 중요 한 속성을 포함 합니다.

| 속성 | 설명 |
| -------- | ----------- |
| entryPointType | 필수 속성입니다. 세 가지 유효한 값: "도구", "솔루션" 및 "connectionProvider". | 
| name | 솔루션의 범위 내에서 연결 공급자를 식별합니다. 이 값은 전체 Windows Admin Center 인스턴스 (솔루션 뿐만 아니라) 내에서 고유 해야 합니다. |
| path | 솔루션에서 구성 하는 경우 연결을 위한"추가" UI, URL 경로를 나타냅니다. 이 값은 앱 routing.module.ts 파일에 구성 된 경로에 매핑해야 합니다. 솔루션 진입점 연결 rootNavigationBehavior를 사용 하 여 구성 되 면이 경로 연결 추가 UI를 표시 하 여 셸에서 사용 되는 모듈을 로드 합니다. 자세한 내용은 사용할 수 있는 섹션에서 rootNavigationBehavior 합니다. |
| displayName | 여기에 입력 한 값은 셸 사용자 솔루션의 연결 페이지를 로드할 때 검은색 Windows Admin Center 표시줄 아래 오른쪽에 표시 됩니다. |
| icon | 솔루션을 나타내는 데 솔루션 드롭다운 메뉴에서에서 아이콘을 나타냅니다. |
| description | 진입점에 대 한 간단한 설명을 입력 합니다. |
| connectionType | 공급자가 로드 하는 연결 형식을 나타냅니다. 여기에 입력 한 값 솔루션 이러한 연결을 로드할 수를 지정 하려면 솔루션 진입점에도 사용 됩니다. 여기에 입력 한 값이이 형식과 호환 도구를 표시 하려면 도구 항목 요소에도 사용 됩니다. 여기에 입력이 값도 RPC 제출 되는 연결 개체에서 사용할 "추가 창에서" 응용 프로그램 계층 구현 단계에서 호출 합니다. |
| connectionTypeName | 연결 테이블에서 연결 공급자를 사용 하는 연결을 나타내는 데 사용 합니다. 이 유형의 복수 이름이 될 예정입니다. |
| connectionTypeUrlName | Windows Admin Center가 인스턴스에 연결한 후 로드 된 솔루션을 나타내는 URL을 만드는 데. 이 항목은 대상 전과 후 연결을 사용 합니다. 이 예제에서는 "connectionexample" URL에이 값이 표시 됩니다.http://localhost:6516/solutionexample/connections/connectionexample/con-fake1.corp.contoso.com |
| connectionTypeDefaultSolution | 연결 공급자를 통해 로드 해야 하는 기본 구성 요소를 나타냅니다. 이 값은 조합을: [는] 매니페스트의; 위쪽에 정의 된 확장 패키지의 이름 [b] 느낌표 (!); [c] 솔루션 진입점 이름을 합니다.    확장명이"msft.sme.mySample-" 프로젝트 및 솔루션 진입점을 이름 "example"을 사용 하 여이 값은 "msft.sme.solutionExample 확장! 예제". |
| connectionTypeDefaultTool | 기본을 연결이 성공적으로에서 로드 되어야 하는 도구를 나타냅니다. 이 속성 값은 connectionTypeDefaultSolution 유사한 두 부분으로 이루어져 있습니다. 이 값은 조합을: [는] 매니페스트의; 위쪽에 정의 된 확장 패키지의 이름 [b] 느낌표 (!); [c] 도구 진입점 이름을 처음 로드 되어야 하는 도구에 대 한 합니다. 확장명이"msft.sme.solutionExample-" 프로젝트 및 솔루션 진입점을 이름 "example"을 사용 하 여이 값은 "msft.sme.solutionExample 확장! 예제". |
| connectionStatusProvider | "연결 상태 공급자 정의" 섹션을 참조 하세요 |

## 연결 상태 공급자를 정의 합니다.

연결 상태 공급자는 온라인 상태로 사용할 수 있으며, 되도록 유효성이 검사 됩니다을 대상으로 하는 메커니즘도 연결 하는 사용자는 대상에 액세스 권한이 있는지 확인 합니다. 두 가지 유형의 연결 상태 공급자는 현재: PowerShell 및 RelativeGatewayUrl 합니다.

*   PowerShell 연결 상태 공급자
    *   즉, PowerShell 스크립트를 사용 하 여 액세스할 수 있는 대상 인지 확인 합니다. 아래에 정의 된 "상태" 단일 속성을 사용 하 여 개체에서 결과 반환 합니다.
*   RelativeGatewayUrl 연결 상태 공급자
    *   온라인 및 rest 호출 하 여 액세스할 수 있는 대상 인지 확인 합니다. 아래에 정의 된 "상태" 단일 속성을 사용 하 여 개체에서 결과 반환 합니다.

### 상태를 정의 합니다.

연결 상태 공급자는 단일 속성을 사용 하 여 개체를 반환 하는 데 필요한 ```status``` 다음 형식에 맞는:

``` json
{
    status: {
        label: string;
        type: int;
        details: string;
    }
}
```

상태 속성:

* Label
    * 상태를 설명 하는 레이블 반환 형식입니다. Note 런타임에서 레이블에 대 한 값을 매핑할 수 있습니다. 런타임에서 매핑 값에 대 한 아래 항목을 참조 하세요.

* 유형
    * 상태 반환 형식입니다. 형식에는 다음 열거형 값에 있습니다. 모든 값 2 또는 위에 플랫폼 연결 된 개체를 탐색 하지 않습니다 및 UI에 오류가 표시 됩니다.

유형:

| 값 | 설명 |
| ----- | ----------- |
| 0 | 온라인 |
| 1 | Warning |
| 2 | 권한 없음 |
| 3 | 오류 |
| 4 | 심각한 |
| 5 | 알 수 없음 |

* 세부 정보
    * 상태를 설명 하는 추가 세부 정보가 반환 형식입니다.

### 연결 상태 공급자 PowerShell 스크립트

연결 상태 공급자 PowerShell 스크립트는 대상 온라인 및 PowerShell 스크립트를 사용 하 여 액세스할 수 있는 인지 여부를 확인 합니다. 단일 속성 "status"를 사용 하 여 개체에서 결과 반환 합니다. 예제 스크립트는 다음과 같습니다.

PowerShell 스크립트 예:

``` ts
## Get-My-Status ##

function Get-Status()
{
    # A function like this would be where logic would exist to identify if a node is connectable.
    $status = @{label = $null; type = 0; details = $null; }
    $caption = "MyConstCaption"
    $productType = "MyProductType"

    # A result object needs to conform to the following object structure to be interperated properly by the Windows Admin Center shell.
    $result = @{ status = $status; caption = $caption; productType = $productType; version = $version }

    # DO FANCY LOGIC #

    # Once the logic is complete, the following fields need to be populated:
    $status.label = "Display Thing"
    $status.type = 0 # This value needs to conform to the LiveConnectionStatusType enum. >= 3 represents a failure.
    $status.details = "success stuff"

    return $result
}

Get-Status
```

### RelativeGatewayUrl 연결 상태 공급자 메서드 정의

연결 상태 공급자 ```RelativeGatewayUrl``` 메서드를 호출 하는 rest API를 대상을 온라인 및 액세스할 수 있는지 확인 합니다. 단일 속성 "status"를 사용 하 여 개체에서 결과 반환 합니다. RelativeGatewayUrl의 manifest.json 연결 공급자 항목 예는 다음과 같습니다.

``` json
    {
      "entryPointType": "connectionProvider",
      "name": "addServer",
      "path": "/add/server",
      "displayName": "resources:strings:addServer_displayName",
      "icon": "sme-icon:icon-win-server",
      "description": "resources:strings:description",
      "connectionType": "msft.sme.connection-type.server",
      "connectionTypeName": "resources:strings:addServer_connectionTypeName",
      "connectionTypeUrlName": "server",
      "connectionTypeDefaultSolution": "msft.sme.server-manager!servers",
      "connectionTypeDefaultTool": "msft.sme.server-manager!overview",
      "connectionStatusProvider": {
        "relativeGatewayUrl": "<URL here post /api>",
        "displayValueMap": {
          "wmfMissing-label": "resources:strings:addServer_status_wmfMissing_label",
          "wmfMissing-details": "resources:strings:addServer_status_wmfMissing_details",
          "unsupported-label": "resources:strings:addServer_status_unsupported_label",
          "unsupported-details": "resources:strings:addServer_status_unsupported_details"
        }
      }
    },
```

RelativeGatewayUrl 사용에 대 한 참고 사항:

* "relativeGatewayUrl" 게이트웨이 URL에서 연결 상태를 확인할 수 있는 위치를 지정 합니다. 이 URI /api에서 상대적입니다. $ConnectionName URL에서 발견 되 면 연결의 이름으로 대체 됩니다.
* 모든 relativeGatewayUrl 속성에 대해 게이트웨이 확장을 작성 하 여 수행할 수 있는 호스트 게이트웨이 실행 해야

### 지도 런타임 값

상태 반환 개체에서 사용할 수의 레이블 및 세부 정보 값 "defaultValueMap" 속성 공급자의 키와 값을 포함 하 여 시간을 조정 합니다.

예를 들어 아래의 값을 추가 하는 경우 언제 든 지 "defaultConnection_test" 나타난 레이블 또는 세부 정보에 대 한 값으로 구성 된 리소스 문자열 값으로 Windows Admin Center 키를 자동으로 바꿀 것입니다.

``` json
    "defaultConnection_test": "resources:strings:addServer_status_defaultConnection_label"
```

## 응용 프로그램 계층의 연결 공급자를 구현 합니다.

이제 다음 OnInit를 구현 하는 TypeScript 클래스를 만들어 응용 프로그램 계층의 연결 공급자를 구현 하는 것이 하겠습니다. 클래스에 다음 기능이 있습니다.

| 함수 | 설명 |
| -------- | ----------- |
| 생성자 (개인 appContextService: AppContextService, 개인 경로: ActivatedRoute) |  |
| 공용 ngOnInit() |  |
| 공용 onSubmit() | 추가 연결 시도가 있을 때 셸을 업데이트 하는 논리가 포함 되어 있습니다. |
| 공용 onCancel() | 추가 연결 시도 취소할 때 셸을 업데이트 하는 논리가 포함 되어 있습니다. |

### OnSubmit 정의

```onSubmit``` 문제 RPC "추가 연결" 셸 알리기 위해 앱 컨텍스트를 다시 호출 합니다. 기본 호출 같이 "updateData"를 사용합니다.

``` ts
this.appContextService.rpc.updateData(
    EnvironmentModule.nameOfShell,
    '##',
    <RpcUpdateData>{
        results: {
            connections: connections,
            credentials: this.useCredentials ? this.creds : null
        }
    }
);
```

그 결과로 연결 속성은 다음 구조를 준수 하는 개체의 배열입니다.

``` ts

/**
 * The connection attributes class.
 */
export interface ConnectionAttribute {

    /**
     * The id string of this attribute
     */
    id: string;

    /**
     * The value of the attribute. used for attributes that can have variable values such as Operating System
     */
    value?: string | number;
}

/**
 * The connection class.
 */
export interface Connection {

    /**
     * The id of the connection, this is unique per connection
     */
    id: string;

    /**
     * The type of connection
     */
    type: string;

    /**
     * The name of the connection, this is unique per connection type
     */
    name: string;

    /**
     * The property bag of the connection
     */
    properties?: ConnectionProperties;

    /**
     * The ids of attributes identified for this connection
     */
    attributes?: ConnectionAttribute[];

    /**
     * The tags the user(s) have assigned to this connection
     */
    tags?: string[];
}

/**
 * Defines connection type strings known by core
 * Be careful that these strings match what is defined by the manifest of @msft-sme/server-manager
 */
export const connectionTypeConstants = {
    server: 'msft.sme.connection-type.server',
    cluster: 'msft.sme.connection-type.cluster',
    hyperConvergedCluster: 'msft.sme.connection-type.hyper-converged-cluster',
    windowsClient: 'msft.sme.connection-type.windows-client',
    clusterNodesProperty: 'nodes'
};
```

### OnCancel 정의

```onCancel``` 빈 연결 배열을 전달 하 여 "연결 추가" 시도 취소 합니다.

``` ts
this.appContextService.rpc.updateData(EnvironmentModule.nameOfShell, '##', <RpcUpdateData>{ results: { connections: [] } });
```

## 연결 공급자 예제

아래 연결 공급자를 구현 하기 위한 전체 TypeScript 클래스가입니다. 참고 "connectionType" 문자열은 "connectionType manifest.json에서 연결 공급자에 정의 된 대로 일치.

``` ts
import { Component, OnInit } from '@angular/core';
import { ActivatedRoute } from '@angular/router';
import { AppContextService } from '@msft-sme/shell/angular';
import { Connection, ConnectionUtility } from '@msft-sme/shell/core';
import { EnvironmentModule } from '@msft-sme/shell/dist/core/manifest/environment-modules';
import { RpcUpdateData } from '@msft-sme/shell/dist/core/rpc/rpc-base';
import { Strings } from '../../generated/strings';

@Component({
  selector: 'add-example',
  templateUrl: './add-example.component.html',
  styleUrls: ['./add-example.component.css']
})
export class AddExampleComponent implements OnInit {
  public newConnectionName: string;
  public strings = MsftSme.resourcesStrings<Strings>().SolutionExample;
  private connectionType = 'msft.sme.connection-type.example'; // This needs to match the connectionTypes value used in the manifest.json.
  
  constructor(private appContextService: AppContextService, private route: ActivatedRoute) {
    // TODO:
  }

  public ngOnInit() {
    // TODO
  }

  public onSubmit() {
    let connections: Connection[] = [];

    let connection = <Connection> {
      id: ConnectionUtility.createConnectionId(this.connectionType, this.newConnectionName),
      type: this.connectionType,
      name: this.newConnectionName
    };

    connections.push(connection);

    this.appContextService.rpc.updateData(
      EnvironmentModule.nameOfShell,
      '##',
      <RpcUpdateData> {
        results: {
          connections: connections,
          credentials: null
        }
      }
    );
  }

  public onCancel() {
    this.appContextService.rpc.updateData(
      EnvironmentModule.nameOfShell, '##', <RpcUpdateData>{ results: { connections: [] } });
  }
}

```
