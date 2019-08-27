---
title: Vm 및 컨테이너에 대 한 HCN (호스트 계산 네트워크) 서비스 API
description: HCN (호스트 계산 네트워크) 서비스 API는 가상 네트워크, 가상 네트워크 끝점 및 관련 정책을 관리 하는 플랫폼 수준 액세스를 제공 하는 공용 Win32 API입니다. 여기에는 Windows 호스트에서 실행 되는 Vm (가상 컴퓨터) 및 컨테이너에 대 한 연결 및 보안이 제공 됩니다.
ms.author: jmesser
author: jmesser81
ms.date: 11/05/2018
ms.openlocfilehash: e30a778d661fa7c6d2e248234218eb25fba007a1
ms.sourcegitcommit: 213989f29cc0c30a39a78573bd4396128a59e729
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/26/2019
ms.locfileid: "70031549"
---
# <a name="host-compute-network-hcn-service-api-for-vms-and-containers"></a>Vm 및 컨테이너에 대 한 HCN (호스트 계산 네트워크) 서비스 API

>적용 대상: Windows Server (반기 채널), Windows Server 2019

HCN (호스트 계산 네트워크) 서비스 API는 가상 네트워크, 가상 네트워크 끝점 및 관련 정책을 관리 하는 플랫폼 수준 액세스를 제공 하는 공용 Win32 API입니다. 여기에는 Windows 호스트에서 실행 되는 Vm (가상 컴퓨터) 및 컨테이너에 대 한 연결 및 보안이 제공 됩니다. 

개발자는 HCN 서비스 API를 사용 하 여 응용 프로그램 워크플로에서 Vm 및 컨테이너에 대 한 네트워킹을 관리 합니다. HCN API는 개발자에 게 최상의 환경을 제공 하도록 설계 되었습니다. 최종 사용자는 이러한 Api와 직접 상호 작용 하지 않습니다.  

## <a name="features-of-the-hcn-service-api"></a>HCN 서비스 API의 기능
-   OnCore/VM의 HNS (호스트 네트워크 서비스)에서 호스트 되는 C API로 구현 됩니다.

-   네트워크, 끝점, 네임 스페이스, 정책 등의 HCN 개체를 만들고, 수정 하 고, 삭제 하 고, 열거 하는 기능을 제공 합니다. 작업은 개체 (예: 네트워크 핸들)에 대 한 핸들에 대해 수행 되 고 내부적으로 이러한 핸들은 RPC 컨텍스트 핸들을 사용 하 여 구현 됩니다.

-   스키마 기반. API의 대부분 함수는 입력 및 출력 매개 변수를 JSON 문서로 함수 호출의 인수를 포함 하는 문자열로 정의 합니다. JSON 문서는 강력한 형식의 스키마를 기반으로 하며, 이러한 스키마는 공용 설명서의 일부입니다. 

-   클라이언트에서 네트워크 만들기 및 삭제와 같은 서비스 차원의 이벤트에 대 한 알림을 등록할 수 있도록 구독/콜백 API가 제공 됩니다.

-   HCN API는 데스크톱 브리지 ( Centennial) 시스템 서비스에서 실행 되는 앱입니다. API는 호출자에서 사용자 토큰을 검색 하 여 ACL을 확인 합니다.

>[!TIP]
>HCN 서비스 API는 백그라운드 작업 및 비 포그라운드 창에서 지원 됩니다. 

## <a name="terminology-host-vs-compute"></a>용어: 호스트 및 컴퓨팅
호스트 계산 서비스를 사용 하면 호출자가 단일 물리적 컴퓨터에서 가상 컴퓨터와 컨테이너를 모두 만들고 관리할 수 있습니다. 산업 용어를 따르도록 이름이 지정 됩니다. 

- **호스트** 는 가상화 된 리소스를 제공 하는 운영 체제를 참조 하는 가상화 업계에서 널리 사용 되 고 있습니다.

- **Compute** 는 가상 머신 보다 더 넓은 가상화 방법을 참조 하는 데 사용 됩니다. 호스트 계산 네트워크 서비스를 사용 하면 호출자가 단일 물리적 컴퓨터의 가상 머신과 컨테이너 모두에 대해 네트워킹을 만들고 관리할 수 있습니다.

## <a name="schema-based-configuration-documents"></a>스키마 기반 구성 문서
잘 정의 된 스키마를 기반으로 하는 구성 문서는 가상화 공간에 설정 된 산업 표준입니다. Docker 및 Kubernetes와 같은 대부분의 가상화 솔루션은 구성 문서를 기반으로 Api를 제공 합니다. Microsoft의 참여와 관련 된 몇 가지 업계 이니셔티브는 [Openapi](https://www.openapis.org/)와 같은 이러한 스키마를 정의 하 고 유효성을 검사 하는 에코 시스템을 구동 합니다.  이러한 이니셔티브는 또한 [OCI (Open Container 이니셔티브)](https://www.opencontainers.org/)와 같은 컨테이너에 사용 되는 스키마에 대 한 특정 스키마 정의의 표준화를 추진 합니다.

구성 문서를 작성 하는 데 사용 되는 언어는와 함께 사용 하는 [JSON](https://tools.ietf.org/html/rfc8259)입니다.
-   문서에 대 한 개체 모델을 정의 하는 스키마 정의
-   JSON 문서가 스키마에 맞는지 여부에 대 한 유효성 검사
-   Api 호출자가 사용 하는 프로그래밍 언어에서 이러한 스키마의 네이티브 표현과 JSON 문서를 자동으로 변환 

자주 사용 되는 스키마 정의는 문서에서 속성에 대 한 자세한 정의를 지정할 수 있는 [Openapi](https://www.openapis.org/) 및 [JSON 스키마](http://json-schema.org/)입니다. 예를 들면 다음과 같습니다.
-   속성에 대 한 유효한 값 집합 (예: 백분율을 나타내는 속성의 경우 0-100)입니다.
-   속성에 유효한 문자열 집합으로 표현 되는 열거형의 정의입니다.
-   예상 되는 문자열 형식에 대 한 정규식입니다. 

HCN Api를 문서화 하는 과정에서, JSON 문서의 스키마를 OpenAPI 사양으로 게시할 계획입니다. 이 사양에 따라 스키마의 언어별 표현은 클라이언트에서 사용 하는 프로그래밍 언어로 형식이 안전한 스키마 개체를 사용할 수 있습니다. 

### <a name="example"></a>예제 

다음은 VM의 구성 문서에서 SCSI 컨트롤러를 나타내는 개체에 대 한이 워크플로의 예입니다. 

Windows 소스 코드에서 mars 파일을 사용 하 여 스키마를 정의 합니다. onecore/vm/dv/net/hns/schema/mars/Schema/HCN.

```
enum IpamType
{
    [NewIn("2.0")] Static,
    [NewIn("2.0")] Dhcp,
};

class Ipam
{
    // Type : dhcp
    [NewIn("2.0"),OmitEmpty] IpamType   Type;
    [NewIn("2.0"),OmitEmpty] Subnet     Subnets[];
};

class Subnet : HCN.Schema.Common.Base
{
    [NewIn("2.0"),OmitEmpty] string         IpAddressPrefix;
    [NewIn("2.0"),OmitEmpty] SubnetPolicy   Policies[];
    [NewIn("2.0"),OmitEmpty] Route          Routes[];
};


enum SubnetPolicyType
{
    [NewIn("2.0")] VLAN
};

class SubnetPolicy
{
    [NewIn("2.0"),OmitEmpty] SubnetPolicyType                 Type;
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Common.PolicySettings Data;
};

class PolicySettings
{
    [NewIn("2.0"),OmitEmpty]  string      Name;
};

class VlanPolicy : HCN.Schema.Common.PolicySettings 
{
    [NewIn("2.0")] uint32 IsolationId;
};

class Route 
{
    [NewIn("2.0"),OmitEmpty] string NextHop;
    [NewIn("2.0"),OmitEmpty] string DestinationPrefix;
    [NewIn("2.0"),OmitEmpty] uint16 Metric;
};

```

>[!TIP]
>[NewIn ("2.0") 주석은 스키마 정의에 대 한 버전 관리 지원의 일부입니다.

이 내부 정의에서 스키마에 대 한 OpenAPI 사양을 생성 합니다.

```
{ 
    "swagger" : "2.0", 
    "info" : { 
       "version" : "2.1", 
       "title" : "HCN API" 
    },
    "definitions": {        
        "Ipam": {
            "type": "object",
            "properties": {
                "Type": {
                    "type": "string",
                    "enum": [
                        "Static",
                        "Dhcp"
                    ],
                    "description": " Type : dhcp"
                },
                "Subnets": {
                    "type": "array",
                    "items": {
                        "$ref": "#/definitions/Subnet"
                    }
                }
            }
        },
        "Subnet": {
            "type": "object",
            "properties": {
                "ID": {
                    "type": "string",
                    "pattern": "^[0-9A-Fa-f]{8}-([0-9A-Fa-f]{4}-){3}[0-9A-Fa-f]{12}$"
                },                
                "IpAddressPrefix": {
                    "type": "string"
                },
                "Policies": {
                    "type": "array",
                    "items": {
                        "$ref": "#/definitions/SubnetPolicy"
                    }
                },
                "Routes": {
                    "type": "array",
                    "items": {
                        "$ref": "#/definitions/Route"
                    }
                }
            }
        },
        "SubnetPolicy": {
            "type": "object",
            "properties": {
                "Type": {
                    "type": "string",
                    "enum": [
                        "VLAN",
                        "VSID"
                    ]
                },
                "Data": {
                    "$ref": "#/definitions/PolicySettings"
                }
            }
        },
        "PolicySettings": {
            "type": "object",
            "properties": {
                "Name": {
                    "type": "string"
                }
            }
        },                      
        "VlanPolicy": {
            "type": "object",
            "properties": {
                "Name": {
                    "type": "string"
                },
                "IsolationId": {
                    "type": "integer",
                    "format": "uint32"
                }
            }
        },
        "Route": {
            "type": "object",
            "properties": {
                "NextHop": {
                    "type": "string"
                },
                "DestinationPrefix": {
                    "type": "string"
                },
                "Metric": {
                    "type": "integer",
                    "format": "uint16"
                }
            }
        }        
    }
} 
```

[Swagger](https://swagger.io/)와 같은 도구를 사용 하 여 클라이언트에서 사용 하는 스키마 프로그래밍 언어의 언어별 표현을 생성할 수 있습니다. Swagger는 C#, Go, Javascript 및 Python과 같은 다양 한 언어를 지원 합니다.

- 최상위 IPAM & 서브넷 개체에 대해 [생성 된 C# 코드의 예](example-c-sharp.md) 입니다.

- 최상위 IPAM & 서브넷 개체에 대해 [생성 된 Go 코드의 예](example-go.md) 입니다. Go는 호스트 계산 네트워크 서비스 Api의 두 소비자 인 Docker 및 Kubernetes에서 사용 됩니다. Go는 JSON 문서에 대 한 Go 형식 마샬링을 위한 기본 제공 지원입니다.

코드 생성 및 유효성 검사 외에도 도구를 사용 하 여 JSON 문서 작업을 간소화할 수 있습니다. 즉, [Visual Studio Code](https://code.visualstudio.com/Docs/languages/json).

### <a name="top-level-objects-defined-in-the-hcnschemasmars-file"></a>HCN에 정의 된 최상위 개체입니다. 스키마 mars 파일
위에서 언급 한 것 처럼: onecore/vm/dv/net/hns/schema/mars/Schema 아래의 mars 파일 집합에서 HCN Api에 사용 되는 문서에 대 한 문서 스키마를 찾을 수 있습니다.

최상위 개체는 다음과 같습니다.
- [HostComputeNetwork](hcn-scenarios.md#scenario-hcn)
- [HostComputeEndpoint](hcn-scenarios.md#scenario-hcn-endpoint)
- [HostComputeNamespace](hcn-scenarios.md#scenario-hcn-namespace)
- [HostComputeLoadBalancer](hcn-scenarios.md#scenario-hcn-load-balancer)

```
class HostComputeNetwork : HCN.Schema.Common.Base
{
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.NetworkMode          Type;
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.NetworkPolicy        Policies[];
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.MacPool              MacPool;
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.DNS                  Dns;
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.Ipam                 Ipams[];
};

class HostComputeEndpoint : HCN.Schema.Common.Base
{
    [NewIn("2.0"),OmitEmpty] string                                     HostComputeNetwork;
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.Endpoint.EndpointPolicy Policies[];
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.Endpoint.IpConfig       IpConfigurations[];
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.DNS                     Dns;
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.Route                   Routes[];
    [NewIn("2.0"),OmitEmpty] string                                     MacAddress;
};

class HostComputeNamespace : HCN.Schema.Common.Base
{
    [NewIn("2.0"),OmitEmpty] uint32                                    NamespaceId;
    [NewIn("2.0"),OmitEmpty] Guid                                      NamespaceGuid;
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Namespace.NamespaceType        Type;
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Namespace.NamespaceResource    Resources[];
};

class HostComputeLoadBalancer : HCN.Schema.Common.Base
{
    [NewIn("2.0"), OmitEmpty] string                                               HostComputeEndpoints[]; 
    [NewIn("2.0"), OmitEmpty] string                                               VirtualIPs[]; 
    [NewIn("2.0"), OmitEmpty] HCN.Schema.Network.Endpoint.Policy.PortMappingPolicy PortMappings[]; 
    [NewIn("2.0"), OmitEmpty] HCN.Schema.LoadBalancer.LoadBalancerPolicy           Policies[];
};
```

## <a name="next-steps"></a>다음 단계

- [일반적인 HCN 시나리오](hcn-scenarios.md)에 대해 자세히 알아보세요.

- [HCN의 RPC 컨텍스트 핸들](hcn-declaration-handles.md)에 대해 자세히 알아보세요.

- [Hcn JSON 문서 스키마](hcn-json-document-schemas.md)에 대해 자세히 알아보세요.