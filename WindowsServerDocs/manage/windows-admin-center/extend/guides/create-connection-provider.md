---
title: 솔루션 확장에 대 한 연결 공급자 만들기
description: 솔루션 확장 Windows Admin Center SDK (프로젝트 브라 티) 개발-연결 공급자 만들기
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 883fba96fcb71cb1c6e8162c1564d66924c4e24d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885654"
---
# <a name="create-a-connection-provider-for-a-solution-extension"></a>솔루션 확장에 대 한 연결 공급자 만들기

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

연결 공급자 Windows Admin Center 정의 하 고 연결 가능 개체를 하나 이상의 대상을 사용 하 여 통신 하는 방법에서 중요 한 역할을 수행 합니다. 기본적으로, 연결 공급자 중에 연결, 온라인 상태이 고, 사용 가능한 대상은 또한 연결 하는 사용자를 대상에 액세스 권한이 있는지를 확인 등 작업을 수행 합니다.

기본적으로 Windows Admin Center 다음 연결 공급자를 사용 하 여 제공 됩니다.

* 서버
* Windows 클라이언트
* 장애 조치(failover) 클러스터
* HCI 클러스터

사용자 고유의 사용자 지정 연결 공급자를 만들려면 다음이 단계를 수행 합니다.

* 연결 공급자 세부 정보를 추가 합니다. ```manifest.json```
* 연결 상태 공급자를 정의 합니다.
* 응용 프로그램 계층에서 연결 공급자를 구현 합니다.

## <a name="add-connection-provider-details-to-manifestjson"></a>manifest.json에 연결 공급자 세부 정보 추가

이제 프로젝트의 연결 공급자를 정의 하려면 알아야 할 내용을 살펴보겠습니다 ```manifest.json``` 파일입니다.

### <a name="create-entry-in-manifestjson"></a>manifest.json에 항목 만들기

```manifest.json``` \src 폴더에 있는 파일과 무엇 보다도, 프로젝트에 진입점의 정의가 포함 되어 있습니다. 진입점 유형의 도구, 솔루션 및 연결 공급자를 포함 합니다. 연결 공급자를 정의 했습니다.

연결 공급자 항목은 manifest.json에 샘플은 다음과 같습니다.

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

진입점 "connnectionProvider" 형식의 구성 항목 유효성을 검사할 연결 상태를 솔루션에서 사용할 공급자는 Windows Admin Center 셸에 나타냅니다. 연결 공급자 진입점에는 다양 한 중요 한 속성을 아래에 정의 된 포함 됩니다.

| 속성 | 설명 |
| -------- | ----------- |
| entryPointType | 이것은 필수 속성입니다. 세 가지 유효한 값: "도구", "솔루션" 및 "connectionProvider"입니다. | 
| NAME | 솔루션의 범위 내에서 연결 공급자를 식별합니다. 이 값은 전체 Windows Admin Center 인스턴스 (뿐 아니라 솔루션) 내에서 고유 해야 합니다. |
| path | 솔루션에서 구성 하는 경우 연결에 대해"추가" UI URL 경로를 나타냅니다. 이 값은 앱 routing.module.ts 파일에서 구성 하는 경로 매핑해야 합니다. 솔루션 진입점 연결 rootNavigationBehavior를 사용 하도록 구성 됩니다, 경우에이 경로 추가 연결 UI를 표시 하는 셸에서 사용 되는 모듈을 로드 됩니다. 자세한 정보가 단원의 rootNavigationBehavior에서. |
| displayName | 여기에 입력 한 값은 검은색 Windows Admin Center 표시줄 사용자 로드 솔루션의 연결 페이지 아래쪽의 셸의 오른쪽에 표시 됩니다. |
| 아이콘 | 솔루션을 나타내는 데 솔루션에 대 한 드롭다운 메뉴에서에서 아이콘을 나타냅니다. |
| description | 진입점에 대 한 간단한 설명을 입력 합니다. |
| connectionType | 공급자가 로드 되는 연결 유형을 나타냅니다. 여기에 입력 한 값도 사용할 솔루션 진입점에서 솔루션 이러한 연결을 로드할 수 있는지를 지정 합니다. 여기에 입력 한 값도 사용할 도구 항목 요소에서이 형식을 사용 하 여 호환 가능한 도구 임을 합니다. 여기에 입력이 값도 RPC에 제출 된 연결 개체에 사용할 "추가 창에서" 응용 프로그램 계층 구현 단계에서 호출 합니다. |
| connectionTypeName | 연결 테이블에서 연결 공급자를 사용 하는 연결을 나타내는 데 사용 합니다. 이 복수형 이름 형식의 해야 합니다. |
| connectionTypeUrlName | 인스턴스에 Windows Admin Center 연결 된 후 로드 된 솔루션을 나타내는 URL을 만드는 데. 이 항목이 대상 전과 후 연결에 사용 됩니다. 이 예제에서 "connectionexample" URL에서이 값의 위치는: http://localhost:6516/solutionexample/connections/connectionexample/con-fake1.corp.contoso.com |
| connectionTypeDefaultSolution | 연결 공급자가 로드 해야 하는 기본 구성 요소를 나타냅니다. 이 값의 조합입니다. [a]; 매니페스트의 맨 위에 있는 정의 된 확장 패키지의 이름 [b] 느낌표 (!). [c] 솔루션 항목 지점 이름입니다.    이 값은 "msft.sme.mySample-확장명"를 사용 하 여 프로젝트 및 솔루션 진입점을 이름 "예"를 사용 하 여 "msft.sme.solutionExample 확장! 예제에서는". |
| connectionTypeDefaultTool | 기본을 연결을 성공적으로 로드 해야 하는 도구를 나타냅니다. 이 속성 값을 connectionTypeDefaultSolution 비슷합니다 두 부분으로 구성 됩니다. 이 값의 조합입니다. [a]; 매니페스트의 맨 위에 있는 정의 된 확장 패키지의 이름 [b] 느낌표 (!). [처음에 로드 해야 하는 도구에 대 한 c]에서 도구 항목 지점 이름입니다. 이 값은 "msft.sme.solutionExample-확장명"를 사용 하 여 프로젝트 및 솔루션 진입점을 이름 "예"를 사용 하 여 "msft.sme.solutionExample 확장! 예제에서는". |
| connectionStatusProvider | "연결 상태 공급자 정의" 섹션을 참조 하세요 |

## <a name="define-connection-status-provider"></a>연결 상태 공급자를 정의 합니다.

연결 상태 공급자도 연결 하는 사용자를 대상에 액세스 권한이 있는지를 확인 하는 온라인으로 사용 가능한 대상 검사할지 메커니즘입니다. 현재 두 가지 유형의 연결 상태 공급자  PowerShell 및 RelativeGatewayUrl 합니다.

*   PowerShell 연결 상태 공급자
    *   온라인 상태이 고 PowerShell 스크립트를 통해 액세스할 수 있는 대상 인지 확인 합니다. 아래에 정의 된 단일 속성 "상태"를 사용 하 여 개체에 결과 반환 합니다.
*   RelativeGatewayUrl 연결 상태 공급자
    *   온라인 상태이 고 rest 호출을 통해 액세스할 수 있는 대상 인지 확인 합니다. 아래에 정의 된 단일 속성 "상태"를 사용 하 여 개체에 결과 반환 합니다.

### <a name="define-status"></a>상태를 정의 합니다.

연결 상태 공급자는 단일 속성을 사용 하 여 개체를 반환 하는 데 필요한 ```status``` 다음 형식을 준수 합니다.

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

* 레이블
    * 상태를 설명 하는 레이블을 반환 형식입니다. Note 런타임에서 레이블에 대 한 값을 매핑할 수 있습니다. 런타임에서 매핑 값에 대 한 아래 항목을 참조 하세요.

* 형식
    * 상태 반환 형식입니다. 형식에는 다음 열거형 값입니다. 임의의 값이 2 이상인 플랫폼 연결 된 개체를 탐색 하지 않습니다 하 고 UI에 오류가 표시 됩니다.

형식:

| 값 | Description |
| ----- | ----------- |
| 0 | 온라인 |
| 1 | 경고 |
| 2 | 권한 없음 |
| 3 | Error |
| 4 | 심각한 |
| 5 | 알 수 없음 |

* 설명
    * 자세한 상태를 설명 하는 형식을 반환 합니다.

### <a name="powershell-connection-status-provider-script"></a>연결 상태 공급자 PowerShell 스크립트

연결 상태 공급자 PowerShell 스크립트를 온라인 상태이 고 PowerShell 스크립트를 통해 액세스할 수 있는 대상 인지 여부를 확인 합니다. 결과 단일 속성 "상태"를 사용 하 여 개체에 반환 되어야 합니다. 예제 스크립트는 다음과 같습니다.

PowerShell 스크립트 예제:

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

### <a name="define-relativegatewayurl-connection-status-provider-method"></a>RelativeGatewayUrl 연결 상태 공급자 메서드를 정의 합니다.

연결 상태 공급자 ```RelativeGatewayUrl``` rest 온라인 상태이 고 액세스할 수 있는 대상 인지 확인 하는 API를 호출 합니다. 결과 단일 속성 "상태"를 사용 하 여 개체에 반환 되어야 합니다. RelativeGatewayUrl의 예에서는 연결 공급자 항목은 manifest.json에는 다음과 같습니다.

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

* "relativeGatewayUrl" 게이트웨이 URL에서 연결 상태를 가져올 수 있는 위치를 지정 합니다. 이 URI는 / a p i를 기준으로 합니다. $ConnectionName URL에는 연결의 이름으로 바뀝니다.
* 게이트웨이 확장 프로그램을 만들어 수행할 수 있는 호스트 게이트웨이에 대 한 모든 relativeGatewayUrl 속성을 실행 해야 합니다.

### <a name="map-values-in-runtime"></a>런타임에 값 매핑

반환 개체에 서식을 지정할 수는 상태에서 레이블 및 세부 정보 값 공급자의 "defaultValueMap" 속성에 키와 값을 포함 하 여 시간을 조정 합니다.

예를 들어, 아래 값을 추가 하는 경우 언제 든 지 해당 "defaultConnection_test" 나타난 레이블 또는 정보에 대 한 값으로 구성 된 리소스 문자열 값을 사용 하 여 Windows Admin Center 키를 자동으로 바꿀 됩니다.

``` json
    "defaultConnection_test": "resources:strings:addServer_status_defaultConnection_label"
```

## <a name="implement-connection-provider-in-application-layer"></a>응용 프로그램 계층에서 연결 공급자를 구현 합니다.

이제 OnInit를 구현 하는 TypeScript 클래스를 만들어 응용 프로그램 계층에서 연결 공급자를 구현 하려고 합니다. 클래스에 다음 기능이 있습니다.

| 함수 | 설명 |
| -------- | ----------- |
| constructor(private appContextService: AppContextService 개인 경로: ActivatedRoute) |  |
| public ngOnInit() |  |
| public onSubmit() | 추가 연결 하려고 하는 경우 셸을 업데이트 하기 위한 논리가 포함 |
| 공용 onCancel() | 추가 연결 시도가 취소 될 때 셸을 업데이트 하기 위한 논리가 포함 |

### <a name="define-onsubmit"></a>OnSubmit 정의

```onSubmit``` 문제는 RPC "추가 연결"의 셸 알림 앱 컨텍스트에 다시 호출 합니다. 기본 호출을 다음과 같이 "updateData"를 사용합니다.

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

결과 다음과 같은 구조를 준수 하는 개체의 배열에는 연결 속성:

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

### <a name="define-oncancel"></a>OnCancel 정의

```onCancel``` 빈 연결 배열을 전달 하 여 "연결 추가" 시도가 취소:

``` ts
this.appContextService.rpc.updateData(EnvironmentModule.nameOfShell, '##', <RpcUpdateData>{ results: { connections: [] } });
```

## <a name="connection-provider-example"></a>연결 공급자 예제

연결 공급자를 구현 하는 것에 대 한 전체 TypeScript 클래스는 다음과 같습니다. "ConnectionType" 문자열을 "connectionType은 manifest.json에 있는 연결 공급자에 정의 된 대로 일치 하는지 참고.

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
