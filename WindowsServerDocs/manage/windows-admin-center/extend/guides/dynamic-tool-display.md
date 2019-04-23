---
title: 솔루션에서 도구의 표시 유형을 제어합니다
description: 솔루션 (프로젝트 브라 티) Windows Admin Center SDK에서에서 도구의 표시 유형을 제어합니다
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: f3f34b4c86854bfc55cf4b1b57a0fd3c2baf2ffc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839254"
---
# <a name="control-your-tools-visibility-in-a-solution"></a>솔루션에서 도구의 표시 유형을 제어합니다 #

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

제외 (또는 숨깁니다)에 확장 프로그램이 나 도구를 사용할 수 있는 도구 목록에서 하는 상황이 있을 수 있습니다. 예를 들어, 도구만 Windows Server 2016 (없습니다 이전 버전)을 대상으로 하는 경우에 Windows Server 2012 R2 서버에 연결 하는 도구를 전혀 볼 사용자를 좋습니다 하지. (사용자 환경-imagine 로드에 메시지가 해당 기능을 해당 연결에 사용할 수 없습니다를 도구용 대기를 클릭 하 고 해당.) 표시 하거나 숨깁니다. 도구의 manifest.json 파일의 기능 하는 시기를 정의할 수 있습니다.

## <a name="options-for-deciding-when-to-show-a-tool"></a>도구를 표시 하는 시기를 결정 하기 위한 옵션 ##

세 가지 다른 옵션을 표시 하 고 특정 서버 또는 클러스터 연결에 사용할 수 있는 도구를 해야 하는지 여부를 결정 하는 데 사용할 수 있습니다.

* localhost
* 인벤토리 (속성의 배열)
* 스크립트(script)

### <a name="localhost"></a>LocalHost ###

여부 연결 노드는 localHost (Windows Admin Center 설치 되어 있는 동일한 컴퓨터) 하는 경우 유추를 평가할 수 있는 부울 값을 포함 하는 조건 개체의 localHost 속성입니다. 하 여 속성에 값을 전달, 표시 될 때 (조건) 도구가 표시 합니다. 예를 들어 사용자가 실제로 로컬 호스트에 연결 하는 경우를 표시 하려면 도구만 하려는 경우, 다음과 같이 설정 합니다.

``` json
"conditions": [
{
    "localhost": true
}]
```

또는 시기를 표시 하기 위한 도구만 하려는 경우 연결 노드 *아닙니다* localhost:

``` json
"conditions": [
{
    "localhost": false
}]
```

구성 설정의 모양을 표시할 도구 연결 노드 localhost 없는 경우 다음과 같습니다.

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

SDK는 미리 큐 레이 팅 된 경우 도구 사용할지 여부를 결정 하는 조건을 작성 하는 데 사용할 수 있는 인벤토리 속성 집합이 포함 되어 있습니다. [인벤토리] 배열에 9 개의 서로 다른 속성을 가지 있습니다.

| 속성 이름 | 예상 값 형식 |
| ------------- | ------------------- |
| computerManufacturer | string |
| operatingSystemSKU | number |
| operatingSystemVersion | version_string (예: "10.1.*") |
| productType | number |
| clusterFqdn | string |
| isHyperVRoleInstalled | boolean |
| isHyperVPowershellInstalled | boolean |
| isManagementToolsAvailable | boolean |
| isWmfInstalled | boolean |

인벤토리 배열에 있는 모든 개체는 다음 json 구조를 따라야 합니다.

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
| gt | 보다 큼 |
| ge | 보다 크거나 같음 |
| lt | 미만 |
| le | 보다 작거나 같음 |
| eq | 같음 |
| ne | 같지 않음 |
| 이 | 값이 true 인지 확인 |
| not | 값 false 인지 확인 |
| 포함 | 문자열에 있는 항목 |
| notContains | 문자열에 항목이 없습니다. |

#### <a name="data-types"></a>데이터 형식 ####

'Type' 속성에 대 한 사용 가능한 옵션:

| 형식 | 설명 |
| ---- | ----------- |
| version | 버전 번호 (예: 10.1.*) |
| number | 숫자 값 |
| string | 문자열 값 |
| boolean | true 또는 false |

#### <a name="value-types"></a>값 형식 ####

'Value' 속성에는 이러한 형식을 허용:

* string
* number
* boolean

제대로 된 형식의 인벤토리 조건 집합은 다음과 같습니다.

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

마지막으로, 가용성 및 노드의 상태를 식별 하는 사용자 지정 PowerShell 스크립트를 실행할 수 있습니다. 모든 스크립트는 다음과 같은 구조를 사용 하 여 개체를 반환 해야 합니다.

``` ps
@{
    State = 'Available' | 'NotSupported' | 'NotConfigured';
    Message = '<Message to explain the reason of state such as not supported and not configured.>';
    Properties =
        @{ Name = 'Prop1'; Value = 'prop1 data'; Type = 'string' },
        @{Name='Prop2'; Value = 12345678; Type='number'; };
}
```
State 속성에는 제어 도구 목록에서 확장을 표시할지를 결정 하는 중요 한 값입니다.  허용 되는 값은:
| 값 | 설명 |
| ---- | ----------- |
| 사용 가능 | 확장 도구 목록에 표시 합니다. |
| NotSupported | 확장 도구 목록에 표시 되지 해야 합니다. |
| NotConfigured | 이 도구를 사용할 수 있는 되기 전에 추가 구성에 대 한 사용자를 묻습니다 향후 작업에 대 한 자리 표시자 값입니다.  현재이 값 하면 표시 되는 도구 이며 '사용 가능'으로 동일 합니다. |

예를 들어 원격 서버에서 BitLocker를 설치 하는 경우에 로드 하는 도구를 원하는 경우 스크립트는 다음과 같습니다.

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

스크립트 옵션을 사용 하는 항목 지점 구성은 다음과 같습니다.

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

"요구 사항" 블록을 여러 개 정의 하 여 도구를 표시할 시기를 확인 하려면 요구 사항 집합이 둘 이상 사용할 수 있습니다.

예를 들어, 경우에 도구를 표시 하려면 "시나리오 A" 또는 "시나리오 B"가 true 이면 두 요구 사항을 블록; 정의 중 하나에 해당 하는 경우 (즉, 요구 사항 블록 내에서 모든 조건이 충족 되) 도구가 표시 됩니다.

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

## <a name="supporting-condition-ranges"></a>조건 범위를 지원합니다. ##

또한 동일한 속성을 사용 하지만 다른 연산자를 사용 하 여 "조건" 블록을 여러 개 정의 하 여 다양 한 조건 정의할 수 있습니다.

동일한 속성에 다양 한 연산자를 사용 하 여 정의 되 면 도구는 값은 두 가지 조건으로 표시 됩니다.

예를 들어,이 도구는 운영 체제가 6.3.0 사이의 10.0.0 버전으로 표시 됩니다.

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
