---
title: 솔루션에 도구의 표시 여부를 제어
description: Windows Admin Center SDK (Project Honolulu) 솔루션에 도구의 표시 여부를 제어
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: f3f34b4c86854bfc55cf4b1b57a0fd3c2baf2ffc
ms.sourcegitcommit: be0144eb59daf3269bebea93cb1c467d67e2d2f1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/20/2018
ms.locfileid: "4080970"
---
# 솔루션에 도구의 표시 여부를 제어 #

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

제외 (또는 숨기기) 확장 또는 도구 사용 가능한 도구 목록에서 원하는 시간 있을 수 있습니다. 예를 들어 도구에만 Windows Server 2016 (하지 이전 버전)를 대상으로 하는 경우 하지 않을 도구를 전혀 확인 하려면 Windows Server 2012 R2 서버에 연결 하는 사용자. (사용자 환경-상상할 클릭, 도구 기능 연결에 사용할 수 없는 하는 메시지에, 로드 될 때까지 기다리는 것입니다.) 도구의 manifest.json 파일에서 기능을 표시 (또는 숨기기) 하는 시기를 정의할 수 있습니다.

## 도구를 표시 하는 시기를 결정 하기 위한 옵션 ##

세 가지 다른 옵션을 표시 하 고 특정 서버 또는 클러스터 연결에 사용할 수 있는 도구 수 있는지 여부를 결정 하는 데 사용할 수 있습니다.

* localhost
* 인벤토리 (속성 배열)
* 스크립트

### LocalHost ###

LocalHost 속성 조건 개체의 또는 연결 노드가 localHost (Windows Admin Center에 설치 되어 있는 동일한 컴퓨터) 이면 유추할 계산 될 수 있는 부울 값을 포함 합니다. 속성 값을 전달 하 여 하도록 지정 하는 경우 (조건) 도구를 표시 합니다. 예를 들어 도구를 사용자가 실제로 로컬 호스트에 연결 하는 경우 표시 하려는 경우, 설정 같이:

``` json
"conditions": [
{
    "localhost": true
}]
```

또는 도구에 표시 될 때 싶다면 연결 노드 *없는* localhost:

``` json
"conditions": [
{
    "localhost": false
}]
```

구성 설정을 모습을 표시 하도록 도구 연결 노드가 localhost 때 다음과 같습니다.

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

### 인벤토리 속성 ###

SDK 미리 큐 레이트 때 도구에 사용할 수 있어야 여부를 확인 하는 조건문을 빌드하는 데 사용할 수 있는 인벤토리 속성 집합을 포함 합니다. '인벤토리' 배열에 9 개의 서로 다른 속성을 가지 있습니다.

| 속성 이름 | 예상 값 형식 |
| ------------- | ------------------- |
| computerManufacturer | string |
| operatingSystemSKU | 숫자 |
| operatingSystemVersion | version_string (예: "10.1. *") |
| productType | 숫자 |
| clusterFqdn | string |
| isHyperVRoleInstalled | 부울 |
| isHyperVPowershellInstalled | 부울 |
| isManagementToolsAvailable | 부울 |
| isWmfInstalled | 부울 |

인벤토리 배열에 있는 모든 개체는 다음과 같은 json 구조를 따라야 합니다.

``` json
"<property name>": {
    "type": "<expected type>",
    "operator": "<defined operator to use>",
    "value": "<expected value to evaluate using the operator>"
}
```

#### 연산자 값 ####

| 연산자 | 설명 |
| -------- | ----------- |
| gt | 보다 큼 |
| ge | 보다 크거나 |
| lt | 미만 |
| le | 보다 작거나 같아야 |
| eq | 같음 |
| ne | 같지 않음 |
| 이  | 값이 true 인지 확인 합니다. |
| 없음 | 값이 false 인지 확인 합니다. |
| 포함 | 문자열에 있는 항목 |
| notContains | 문자열에 항목이 없습니다. |

#### 데이터 형식 ####

'형식의' 속성에 사용할 수 있는 옵션:

| 유형 | 설명 |
| ---- | ----------- |
| 버전 | 버전 번호 (예: 10.1. *) |
| 숫자 | 숫자 값 |
| string | 문자열 값 |
| 부울 | true 또는 false |

#### 값 형식 ####

'' 값은 이러한 형식을 사용할 수 있습니다.

* string
* 숫자
* 부울

제대로 구성 인벤토리 조건 세트는 다음과 같습니다.

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

### 스크립트 ###

마지막으로, 가용성과 노드의 상태를 식별 하는 사용자 지정 PowerShell 스크립트를 실행할 수 있습니다. 모든 스크립트는 다음 구조를 사용 하 여 개체를 반환 해야 합니다.

``` ps
@{
    State = 'Available' | 'NotSupported' | 'NotConfigured';
    Message = '<Message to explain the reason of state such as not supported and not configured.>';
    Properties =
        @{ Name = 'Prop1'; Value = 'prop1 data'; Type = 'string' },
        @{Name='Prop2'; Value = 12345678; Type='number'; };
}
```
상태 속성에는 확장 도구 목록에 표시할지 결정을 제어 하는 중요 한 값입니다.  허용 되는 값은 다음과 같습니다.
| 값 | 설명 |
| ---- | ----------- |
| 사용 가능 | 확장 도구 목록에 표시 되어야 합니다. |
| NotSupported | 확장 도구 목록에 표시 되지 해야 합니다. |
| NotConfigured | 이 도구는 사용할 수 있게 되기 전에 사용자에 게 추가 구성이 묻습니다 이후 작업에 대 한 자리 표시자 값입니다.  현재이 값이 표시 되는 도구에서 발생 하 고 기능 해당 하는 '가능'. |

예를 들어 원격 서버에 BitLocker를 설치 하는 경우에 로드 하는 도구, 원하는 경우 스크립트 다음과 같습니다.

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

## 여러 요구 사항 집합 지원 ##

여러 "요구 사항" 블록을 정의 하 여 도구를 표시 하는 시기를 결정할 요구 사항 집합이 여러 개를 사용할 수 있습니다.

예를 들어, 도구를 표시 하려면 "시나리오 A" 또는 "시나리오 B" true 이면 두 요구 사항 블록; 정의 중 하나에 해당 하는 경우 (즉, 요구 사항 블록 내에서 모든 조건이 충족 되) 도구에 표시 됩니다.

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

## 조건 범위를 지원합니다. ##

또한 동일한 속성을 사용 하지만 다른 연산자를 사용 하 여 여러 "조건" 블록을 정의 하 여 다양 한 조건을 정의할 수 있습니다.

동일한 속성은 다른 연산자를 사용 하 여 정의 되 면 도구는 값은 두 조건으로 표시 됩니다.

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
