---
title: 솔루션에서 도구의 표시 유형 제어
description: 솔루션의 도구 표시 여부 제어 Windows 관리 센터 SDK (Project Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 440ba3d11da671beedc2c2fb90caa3e176f83877
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385324"
---
# <a name="control-your-tools-visibility-in-a-solution"></a>솔루션에서 도구의 표시 유형 제어 #

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

사용 가능한 도구 목록에서 확장 또는 도구를 제외 하거나 숨기는 경우가 있을 수 있습니다. 예를 들어 도구에서 Windows Server 2016 (이전 버전 아님)만 대상으로 하는 경우 Windows Server 2012 R2 서버에 연결 하는 사용자가 도구를 전혀 표시 하지 않을 수 있습니다. (사용자 환경을 클릭 합니다. 즉, 도구를 클릭 하 여 도구가 로드 될 때까지 대기 하 고 해당 기능을 연결에 사용할 수 없다는 메시지만 표시 합니다.) 도구의 매니페스트 json 파일에서 기능을 표시 하거나 숨기는 시기를 정의할 수 있습니다.

## <a name="options-for-deciding-when-to-show-a-tool"></a>도구 표시 시기를 결정 하는 옵션 ##

특정 서버 또는 클러스터 연결에 대해 도구를 표시 하 고 사용할 수 있는지 여부를 결정 하는 데 사용할 수 있는 세 가지 옵션이 있습니다.

* localhost
* 인벤토리 (속성 배열)
* 스크립트(script)

### <a name="localhost"></a>호스트 ###

조건 개체의 localHost 속성에는 연결 노드가 localHost (Windows 관리 센터가 설치 된 컴퓨터) 인지 여부를 유추 하기 위해 평가할 수 있는 부울 값이 포함 되어 있습니다. 속성에 값을 전달 하 여 도구를 표시할 시기 (조건)를 지정 합니다. 예를 들어 사용자가 로컬 호스트에 실제로 연결 되어 있는 경우에만 도구를 표시 하려면 다음과 같이 설정 합니다.

``` json
"conditions": [
{
    "localhost": true
}]
```

또는 연결 노드가 localhost *가 아닌* 경우에만 도구를 표시 하려면 다음을 수행 합니다.

``` json
"conditions": [
{
    "localhost": false
}]
```

연결 노드가 localhost가 아닌 경우에만 도구를 표시 하는 구성 설정은 다음과 같습니다.

``` json
"entryPoints": [
{
    "entryPointType": "tool",
    "name": "main",
    "urlName": "processes",
    "displayName": "resources:strings:displayName",
    "description": "resources:strings:description",
    "icon": "sme-icon:icon-win-serverProcesses",
    "path": "",
    "requirements": [
    {
        "solutionIds": [
        "msft.sme.server-manager!windowsClients"
        ],
        "connectionTypes": [
        "msft.sme.connection-type.windows-client"
        ],
        "conditions": [
        {
            "localhost": true
        }
        ]
    }
    ]
}
```

### <a name="inventory-properties"></a>인벤토리 속성 ###

SDK에는 도구를 사용할 수 있는 시기를 결정 하는 조건을 작성 하는 데 사용할 수 있는 미리 큐 레이트 인벤토리 속성 집합이 포함 되어 있습니다. ' Inventory ' 배열에는 9 개의 다른 속성이 있습니다.

| 속성 이름 | 필요한 값 형식 |
| ------------- | ------------------- |
| 컴퓨터 제조업체 | string |
| operatingSystemSKU | number |
| operatingSystemVersion | version_string (예: "10.1. *") |
| productType | number |
| clusterFqdn | string |
| isHyperVRoleInstalled | boolean |
| isHyperVPowershellInstalled | boolean |
| isManagementToolsAvailable | boolean |
| isWmfInstalled | boolean |

인벤토리 배열의 모든 개체는 다음 json 구조를 준수 해야 합니다.

``` json
"<property name>": {
    "type": "<expected type>",
    "operator": "<defined operator to use>",
    "value": "<expected value to evaluate using the operator>"
}
```

#### <a name="operator-values"></a>연산자 값 ####

| 연산자 | 설명 |
| -------- | ----------- |
| nspi | 보다 큼 |
| ge | 크거나 같음 |
| Lt | 보다 작음 |
| 모바일 | 작거나 같음 |
| 이퀄라이저 | 같음 |
| ne | 같지 않음 |
| is | 값이 true 인지 확인 |
| not | 값이 false 인지 확인 |
| 에서는 | 항목이 문자열에 있습니다. |
| notContains | 항목이 문자열에 없습니다. |

#### <a name="data-types"></a>데이터 형식 ####

' Type ' 속성에 사용할 수 있는 옵션은 다음과 같습니다.

| 형식 | 설명 |
| ---- | ----------- |
| version | 버전 번호 (예: 10.1. *) |
| number | 숫자 값 |
| string | 문자열 값 |
| boolean | true 또는 false |

#### <a name="value-types"></a>값 형식 ####

' Value ' 속성은 다음 형식을 허용 합니다.

* string
* number
* boolean

올바른 형식의 인벤토리 상태 집합은 다음과 같습니다.

``` json
"entryPoints": [
{
    "entryPointType": "tool",
    "name": "main",
    "urlName": "processes",
    "displayName": "resources:strings:displayName",
    "description": "resources:strings:description",
    "icon": "sme-icon:icon-win-serverProcesses",
    "path": "",
    "requirements": [
    {
        "solutionIds": [
        "msft.sme.server-manager!servers"
        ],
        "connectionTypes": [
        "msft.sme.connection-type.server"
        ],
        "conditions": [
        {
            "inventory": {
            "operatingSystemVersion": {
                "type": "version",
                "operator": "gt",
                "value": "6.3"
            },
            "operatingSystemSKU": {
                "type": "number",
                "operator": "eq",
                "value": "8"
            }
            }
        }
        ]
    }
    ]
}
```

### <a name="script"></a>스크립트 ###

마지막으로 사용자 지정 PowerShell 스크립트를 실행 하 여 노드의 가용성 및 상태를 식별할 수 있습니다. 모든 스크립트는 다음과 같은 구조를 가진 개체를 반환 해야 합니다.

``` ps
@{
    State = 'Available' | 'NotSupported' | 'NotConfigured';
    Message = '<Message to explain the reason of state such as not supported and not configured.>';
    Properties =
        @{ Name = 'Prop1'; Value = 'prop1 data'; Type = 'string' },
        @{Name='Prop2'; Value = 12345678; Type='number'; };
}
```
상태 속성은 도구 목록에서 확장을 표시 하거나 숨기는 결정을 제어 하는 중요 한 값입니다.  허용 되는 값은 다음과 같습니다.

| 값 | 설명 |
| ---- | ----------- |
| 사용 가능 | 확장 프로그램은 도구 목록에 표시 되어야 합니다. |
| NotSupported | 확장은 도구 목록에 표시 되지 않아야 합니다. |
| NotConfigured | 이는 도구를 사용할 수 있도록 설정 하기 전에 사용자에 게 추가 구성을 요청 하는 후속 작업의 자리 표시자 값입니다.  현재이 값은 도구가 표시 되 고 ' 사용 가능 '과 동일 하 게 작동 합니다. |

예를 들어 원격 서버에 BitLocker가 설치 된 경우에만 도구를 로드 하려는 경우 스크립트는 다음과 같습니다.

``` ps
$response = @{
    State = 'NotSupported';
    Message = 'Not executed';
    Properties = @{ Name = 'Prop1'; Value = 'prop1 data'; Type = 'string' },
        @{Name='Prop2'; Value = 12345678; Type='number'; };
}

if (Get-Module -ListAvailable -Name servermanager) {
    Import-module servermanager; 
    $isInstalled = (Get-WindowsFeature -name bitlocker).Installed;
    $isGood = $isInstalled;
}

if($isGood) {
    $response.State = 'Available';
    $response.Message = 'Everything should work.';
}

$response
```

스크립트 옵션을 사용 하는 진입점 구성은 다음과 같습니다.

``` json
"entryPoints": [
{
    "entryPointType": "tool",
    "name": "main",
    "urlName": "processes",
    "displayName": "resources:strings:displayName",
    "description": "resources:strings:description",
    "icon": "sme-icon:icon-win-serverProcesses",
    "path": "",
    "requirements": [
    {
        "solutionIds": [
        "msft.sme.server-manager!windowsClients"
        ],
        "connectionTypes": [
        "msft.sme.connection-type.windows-client"
        ],
        "conditions": [
        {
            "localhost": true,
            "inventory": {
            "operatingSystemVersion": {
                "type": "version",
                "operator": "eq",
                "value": "10.0.*"
            },
            "operatingSystemSKU": {
                "type": "number",
                "operator": "eq",
                "value": "4"
            }
            },
            "script": "$response = @{ State = 'NotSupported'; Message = 'Not executed'; Properties = @{ Name = 'Prop1'; Value = 'prop1 data'; Type = 'string' }, @{Name='Prop2'; Value = 12345678; Type='number'; }; }; if (Get-Module -ListAvailable -Name servermanager) { Import-module servermanager; $isInstalled = (Get-WindowsFeature -name bitlocker).Installed; $isGood = $isInstalled; }; if($isGood) { $response.State = 'Available'; $response.Message = 'Everything should work.'; }; $response"
        }
        ]
    }
    ]
}
```

## <a name="supporting-multiple-requirement-sets"></a>여러 요구 사항 집합 지원 ##

여러 가지 요구 사항 집합을 사용 하 여 여러 "요구 사항" 블록을 정의 하 여 도구를 표시할 시기를 결정할 수 있습니다.

예를 들어 "시나리오 A" 또는 "시나리오 B"가 true 인 경우 도구를 표시 하려면 두 가지 요구 사항 블록을 정의 합니다. 둘 중 하나가 true 인 경우 (즉, 요구 사항 블록 내의 모든 조건이 충족 되는 경우) 도구가 표시 됩니다.

``` json
"entryPoints": [
{
    "requirements": [
    {
        "solutionIds": [
            …"scenario A"…
        ],
        "connectionTypes": [
            …"scenario A"…
        ],
        "conditions": [
            …"scenario A"…
        ]
    },
    {
        "solutionIds": [
            …"scenario B"…
        ],
        "connectionTypes": [
            …"scenario B"…
        ],
        "conditions": [
            …"scenario B"…
        ]
    }
    ]
}

```

## <a name="supporting-condition-ranges"></a>지원 조건 범위 ##

서로 다른 연산자를 사용 하 여 동일한 속성을 사용 하 여 여러 개의 "조건" 블록을 정의 하 여 조건의 범위를 정의할 수도 있습니다.

동일한 속성이 서로 다른 연산자를 사용 하 여 정의 된 경우이 도구는 두 조건 사이에 있는 경우에만 표시 됩니다.

예를 들어이 도구는 운영 체제가 6.3.0 및 10.0.0 사이의 버전인 경우에만 표시 됩니다.

``` json
"entryPoints": [
{
    "entryPointType": "tool",
    "name": "main",
    "urlName": "processes",
    "displayName": "resources:strings:displayName",
    "description": "resources:strings:description",
    "icon": "sme-icon:icon-win-serverProcesses",
    "path": "",
    "requirements": [
    {
        "solutionIds": [
             "msft.sme.server-manager!servers"
        ],
        "connectionTypes": [
             "msft.sme.connection-type.server"
        ],
        "conditions": [
        {
            "inventory": {
                "operatingSystemVersion": {
                    "type": "version",
                    "operator": "gt",
                    "value": "6.3.0"
                },
            }
        },
        {
            "inventory": {
                "operatingSystemVersion": {
                    "type": "version",
                    "operator": "lt",
                    "value": "10.0.0"
                }
            }
        }
        ]
    }
    ]
}

```
