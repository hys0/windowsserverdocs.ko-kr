---
title: 솔루션 확장에 대 한 연결 공급자 만들기
description: 솔루션 확장 개발 Windows 관리 센터 SDK (Project Honolulu)-연결 공급자 만들기
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 06/06/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: c1f3a7f7004b573fece71cdaf2f43661c13ad496
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70869626"
---
# <a name="create-a-connection-provider-for-a-solution-extension"></a>솔루션 확장에 대 한 연결 공급자 만들기

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

연결 공급자는 Windows 관리 센터에서 연결 가능한 개체 또는 대상을 정의 하 고 통신 하는 방법에 중요 한 역할을 합니다. 기본적으로 연결 공급자는 대상이 온라인 상태이 고 사용 가능한 지 확인 하 고 연결 하는 사용자에 게 대상에 대 한 액세스 권한이 있는지 확인 하는 등의 작업을 수행 하는 동안 작업을 수행 합니다.

기본적으로 Windows 관리 센터에는 다음 연결 공급자가 제공 됩니다.

* 서버
* Windows 클라이언트
* 장애 조치(failover) 클러스터
* HCI 클러스터

사용자 고유의 사용자 지정 연결 공급자를 만들려면 다음 단계를 수행 합니다.

* 연결 공급자 세부 정보 추가```manifest.json```
* 연결 상태 공급자 정의
* 응용 프로그램 계층에서 연결 공급자 구현

## <a name="add-connection-provider-details-to-manifestjson"></a>매니페스트에 연결 공급자 세부 정보를 추가 합니다. json

이제 프로젝트의 ```manifest.json``` 파일에 연결 공급자를 정의 하기 위해 알아야 하는 내용을 살펴보겠습니다.

### <a name="create-entry-in-manifestjson"></a>매니페스트에서 항목 만들기. json

이 ```manifest.json``` 파일은 \src 폴더에 있으며, 프로젝트에 대 한 진입점의 정의를 포함 합니다. 진입점 유형에는 도구, 솔루션 및 연결 공급자가 있습니다. 연결 공급자를 정의 합니다.

다음은 매니페스트에서 연결 공급자 항목의 샘플입니다. json은 다음과 같습니다.

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

"ConnnectionProvider" 형식의 진입점은 구성 중인 항목이 솔루션에서 연결 상태를 확인 하는 데 사용 되는 공급자 임을 Windows 관리 센터 셸에 나타냅니다. 연결 공급자 진입점에는 아래 정의 된 여러 가지 중요 한 속성이 포함 되어 있습니다.

| 속성 | 설명 |
| -------- | ----------- |
| Entrypointtype 않으면 | 이것은 필수 속성입니다. "Tool", "solution" 및 "connectionProvider"의 세 가지 유효한 값이 있습니다. | 
| name | 솔루션의 범위 내에서 연결 공급자를 식별 합니다. 이 값은 솔루션 뿐만 아니라 전체 Windows 관리 센터 인스턴스 내에서 고유 해야 합니다. |
| path | 솔루션에 의해 구성 되는 경우 "연결 추가" UI에 대 한 URL 경로를 나타냅니다. 이 값은 app.config 파일에 구성 된 경로에 매핑되어야 합니다. 솔루션 진입점이 연결 rootNavigationBehavior를 사용 하도록 구성 된 경우이 경로는 셸에서 추가 연결 UI를 표시 하는 데 사용 되는 모듈을 로드 합니다. RootNavigationBehavior 섹션에서 사용할 수 있는 자세한 내용입니다. |
| displayName | 여기에 입력 한 값은 사용자가 솔루션의 연결 페이지를 로드 하는 경우 검은색 Windows 관리 센터 표시줄 아래에 있는 셸의 오른쪽에 표시 됩니다. |
| 아이콘 | 솔루션을 나타내기 위해 솔루션 드롭다운 메뉴에 사용 되는 아이콘을 나타냅니다. |
| description | 진입점에 대 한 간단한 설명을 입력 합니다. |
| connectionType | 공급자가 로드할 연결 형식을 나타냅니다. 여기에 입력 한 값은 솔루션 진입점에서 솔루션을 사용 하 여 해당 연결을 로드할 수 있도록 지정 하는 데도 사용 됩니다. 여기에 입력 된 값은 도구가이 유형과 호환 됨을 나타내기 위해 도구 진입점에도 사용 됩니다. 여기에 입력 한이 값은 응용 프로그램 계층 구현 단계의 "창 추가"에서 RPC 호출에 전송 된 연결 개체에도 사용 됩니다. |
| connectionTypeName | 연결 테이블에서 연결 공급자를 사용 하는 연결을 나타내는 데 사용 됩니다. 이는 형식의 복수 이름이 될 것으로 예상 됩니다. |
| connectionTypeUrlName | Windows 관리 센터에서 인스턴스에 연결한 후 로드 된 솔루션을 나타내는 URL을 만드는 데 사용 됩니다. 이 항목은 연결 후, 대상 앞에 사용 됩니다. 이 예제에서 "connectionexample"은 URL에이 값이 표시 되는 위치입니다.`http://localhost:6516/solutionexample/connections/connectionexample/con-fake1.corp.contoso.com` |
| connectionTypeDefaultSolution | 연결 공급자에서 로드 해야 하는 기본 구성 요소를 나타냅니다. 이 값은 다음과 같은 조합입니다. <br>[a] 매니페스트 맨 위에 정의 된 확장 패키지의 이름입니다. <br>[b] 느낌표 (!); <br>[c] 솔루션 진입점 이름입니다.    <br>이름이 "sme"이 고 이름이 "example" 인 솔루션 진입점을 포함 하는 프로젝트의 경우이 값은 "msft. sme (예: 확장! example")입니다. |
| connectionTypeDefaultTool | 성공적으로 연결 되 면 로드 되어야 하는 기본 도구를 나타냅니다. 이 속성 값은 connectionTypeDefaultSolution 비슷한 두 부분으로 구성 됩니다. 이 값은 다음과 같은 조합입니다. <br>[a] 매니페스트 맨 위에 정의 된 확장 패키지의 이름입니다. <br>[b] 느낌표 (!); <br>[c] 초기에 로드 해야 하는 도구의 진입점 이름입니다. <br>이름이 "sme"이 고 이름이 "example" 인 솔루션 진입점을 포함 하는 프로젝트의 경우이 값은 "msft. sme 예제-확장! example"이 됩니다. |
| connectionStatusProvider | "연결 상태 공급자 정의" 섹션을 참조 하세요. |

## <a name="define-connection-status-provider"></a>연결 상태 공급자 정의

연결 상태 공급자는 대상이 온라인 상태이 고 사용 가능한 상태 인지 확인 하 여 연결 하는 사용자에 게 대상에 대 한 액세스 권한이 있는지 확인 하는 메커니즘입니다. 현재 연결 상태 공급자에는 다음과 같은 두 가지 유형이 있습니다.  PowerShell 및 RelativeGatewayUrl.

*   <strong>Powershell 연결 상태 공급자</strong> -대상이 온라인 상태이 고 PowerShell 스크립트를 사용 하 여 액세스할 수 있는지 여부를 확인 합니다. 결과는 아래에 정의 된 단일 속성 "status"가 있는 개체에서 반환 되어야 합니다.
*   <strong>RelativeGatewayUrl 연결 상태 제공자</strong> -대상이 온라인 상태이 고 rest 호출로 액세스할 수 있는지 여부를 확인 합니다. 결과는 아래에 정의 된 단일 속성 "status"가 있는 개체에서 반환 되어야 합니다.

### <a name="define-status"></a>상태 정의

연결 상태 공급자는 다음 형식을 따르는 단일 속성 ```status``` 을 가진 개체를 반환 해야 합니다.

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

* <strong>레이블</strong> -상태 반환 형식을 설명 하는 레이블입니다. 레이블에 대 한 값은 런타임에 매핑될 수 있습니다. 런타임에 값 매핑에 대해서는 아래 항목을 참조 하세요.

* <strong>유형</strong> -상태 반환 유형입니다. 형식에는 다음과 같은 열거형 값이 있습니다. 값 2 이상에서 플랫폼은 연결 된 개체를 탐색 하지 않으며 UI에 오류가 표시 됩니다.

   종류

  | 값 | 설명 |
  | ----- | ----------- |
  | 0 | 온라인 |
  | 1 | 경고 |
  | 2 | 권한 없음 |
  | 3 | 오류 |
  | 4 | 심각한 |
  | 5 | 알 수 없음 |

* <strong>Details</strong> -상태 반환 형식에 대 한 추가 세부 정보입니다.

### <a name="powershell-connection-status-provider-script"></a>PowerShell 연결 상태 공급자 스크립트

연결 상태 제공자 PowerShell 스크립트는 대상이 온라인 상태이 고 PowerShell 스크립트를 사용 하 여 액세스할 수 있는지 여부를 확인 합니다. 단일 속성 "status"를 사용 하는 개체에서 결과를 반환 해야 합니다. 예제 스크립트는 다음과 같습니다.

PowerShell 스크립트 예:

```PowerShell
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

### <a name="define-relativegatewayurl-connection-status-provider-method"></a>RelativeGatewayUrl 연결 상태 공급자 메서드 정의

연결 상태 공급자 ```RelativeGatewayUrl``` 메서드는 rest API를 호출 하 여 대상이 온라인 상태이 고 액세스 가능한 지 확인 합니다. 단일 속성 "status"를 사용 하는 개체에서 결과를 반환 해야 합니다. RelativeGatewayUrl의 예제 연결 공급자 항목은 다음과 같습니다.

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

* "relativeGatewayUrl"은 게이트웨이 URL에서 연결 상태를 가져올 위치를 지정 합니다. 이 URI는/api. 상대 경로입니다. URL에 $connectionName 있는 경우 연결의 이름으로 대체 됩니다.
* 모든 relativeGatewayUrl 속성은 게이트웨이 확장을 만들어 수행할 수 있는 호스트 게이트웨이에 대해 실행 해야 합니다.

### <a name="map-values-in-runtime"></a>런타임에 값 매핑

상태 반환 개체의 레이블 및 세부 정보 값은 튜닝할 때 공급자의 "defaultValueMap" 속성에 키 및 값을 포함 하 여 형식을 지정할 수 있습니다.

예를 들어 아래 값을 추가 하는 경우 "defaultConnection_test"가 레이블 또는 세부 정보에 대 한 값으로 표시 되 면 Windows 관리 센터는 키를 구성 된 리소스 문자열 값으로 자동으로 바꿉니다.

``` json
    "defaultConnection_test": "resources:strings:addServer_status_defaultConnection_label"
```

## <a name="implement-connection-provider-in-application-layer"></a>응용 프로그램 계층에서 연결 공급자 구현

이제 OnInit을 구현 하는 TypeScript 클래스를 만들어 응용 프로그램 계층에서 연결 공급자를 구현할 예정입니다. 클래스에는 다음과 같은 함수가 있습니다.

| 함수 | 설명 |
| -------- | ----------- |
| 생성자 (개인 appContextService: AppContextService, 개인 경로: ActivatedRoute) |  |
| public ngOnInit () |  |
| public onSubmit () | 연결 추가 시도가 수행 될 때 셸을 업데이트 하는 논리를 포함 합니다. |
| public onCancel () | 연결 추가 시도가 취소 될 때 셸을 업데이트 하는 논리를 포함 합니다. |

### <a name="define-onsubmit"></a>OnSubmit 정의

```onSubmit```앱 컨텍스트에 대 한 RPC 호출을 실행 하 여 "연결 추가"를 셸에 알립니다. 기본 호출은 다음과 같이 "updateData"를 사용 합니다.

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

결과는 다음 구조를 준수 하는 개체의 배열인 연결 속성입니다.

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

```onCancel```빈 연결 배열을 전달 하 여 "연결 추가" 시도를 취소 합니다.

``` ts
this.appContextService.rpc.updateData(EnvironmentModule.nameOfShell, '##', <RpcUpdateData>{ results: { connections: [] } });
```

## <a name="connection-provider-example"></a>연결 공급자 예

연결 공급자를 구현 하기 위한 전체 TypeScript 클래스는 아래와 같습니다. "ConnectionType" 문자열은 매니페스트에서 연결 공급자에 정의 된 대로 "connectionType과 일치 합니다.

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
