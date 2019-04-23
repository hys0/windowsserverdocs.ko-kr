---
title: Vm 및 컨테이너에 대 한 계산 네트워크 (HCN) 서비스 API를 호스트 합니다.
description: 호스트 네트워크 계산 (HCN) 서비스 API에는 가상 네트워크, 가상 네트워크 엔드포인트와 연결 된 정책 관리에 대 한 플랫폼 수준 액세스를 제공 하는 공용 Win32 API입니다. 함께 제공 연결 및 보안 virtual machines (Vm) 및 Windows 호스트에서 실행 중인 컨테이너에 대 한 합니다.
ms.author: jmesser
author: jmesser81
ms.date: 11/05/2018
ms.openlocfilehash: 50af0dab69633aa6e07ded68e9246aa0315377f0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844984"
---
# <a name="host-compute-network-hcn-service-api-for-vms-and-containers"></a>Vm 및 컨테이너에 대 한 계산 네트워크 (HCN) 서비스 API를 호스트 합니다.

>적용 대상: Windows Server (반기 채널), Windows Server 2016

호스트 네트워크 계산 (HCN) 서비스 API에는 가상 네트워크, 가상 네트워크 엔드포인트와 연결 된 정책 관리에 대 한 플랫폼 수준 액세스를 제공 하는 공용 Win32 API입니다. 함께 제공 연결 및 보안 virtual machines (Vm) 및 Windows 호스트에서 실행 중인 컨테이너에 대 한 합니다. 

개발자는 HCN 서비스 API를 사용 하 여 Vm에 대 한 네트워킹 및 응용 프로그램 워크플로에서 해당 컨테이너를 관리할 수 있습니다. HCN API는 개발자를 위한 최상의 환경을 제공 하도록 설계 되었습니다. 최종 사용자가 직접 이러한 Api 상호 작용 하지 않습니다.  

## <a name="features-of-the-hcn-service-api"></a>HCN 서비스 API의 기능
-   여는 네트워크 서비스 HNS (호스트) OnCore/VM에서 호스트 되는 C API로 구현 됩니다.

-   만들기, 수정, 삭제 및 네트워크, 끝점, 네임 스페이스 및 정책과 같은 HCN 개체를 열거 하는 기능을 제공 합니다. 개체 (예를 들어 네트워크 핸들)에 대 한 핸들에서 작업을 수행 하 고 내부적으로 이러한 핸들 RPC 컨텍스트 핸들을 사용 하 여 구현 됩니다.

-   스키마를 기반 합니다. API의 대부분의 함수 입력을 정의 하 고 JSON 문서로 함수 호출의 인수를 포함 하는 문자열 매개 변수를 출력 합니다. 강력한 형식화 된 파일과 버전이 스키마를 기반으로 하는 JSON 문서, 이러한 스키마는 공용 설명서의 일부입니다. 

-   구독/콜백은 API는 클라이언트의 네트워크 만들기 및 삭제와 같은 서비스 수준의 이벤트 알림을 등록할 수 있도록 제공 됩니다.

-   HCN API에서 작동 하는 데스크톱 브리지 (즉 시스템 서비스에서 실행 중인 centennial) 앱입니다. API는 호출자의 사용자 토큰을 검색 하 여 ACL을 확인 합니다.

>[!TIP]
>HCN 서비스 API는 백그라운드 작업 및 포그라운드 아닌 windows에서 지원 됩니다. 

## <a name="terminology-host-vs-compute"></a>용어: Vs를 호스트 합니다. 컴퓨팅
호스트 계산 서비스를 만들고 가상 컴퓨터와 컨테이너는 단일 물리적 컴퓨터를 관리 하는 호출자를 허용 합니다. 업계 용어를 따라 지정 됩니다. 

- **호스트** 가상화 된 리소스를 제공 하는 운영 체제를 가리키도록 가상화 업계에서 널리 사용 됩니다.

- **계산** 만 가상 머신 보다 광범위 한 가상화 메서드를 참조 하는 데 사용 됩니다. 네트워크 서비스를 계산 하는 호스트를 만들고 가상 머신 및 컨테이너는 단일 물리적 컴퓨터 모두에 대 한 네트워킹 관리는 호출자를 허용 합니다.

## <a name="schema-based-configuration-documents"></a>구성 스키마 기반 문서
잘 정의 된 스키마를 기반으로 하는 구성 문서는 가상화 공간에 설정 된 업계 표준입니다. Docker 및 Kubernetes와 같은 대부분의 가상화 솔루션 구성 문서를 기반으로 Api를 제공 합니다. Microsoft의 참여를 사용 하 여 여러 업계 이니셔티브 정의 및와 같은 이러한 스키마 유효성 검사에 대 한 에코 시스템 드라이브 [OpenAPI](https://www.openapis.org/)합니다.  이러한 이니셔티브와 같은 컨테이너에 대 한 사용 하는 스키마에 대 한 특정 스키마 정의의 표준화 구동 [Open Container Initiative OCI ()](https://www.opencontainers.org/)합니다.

구성 문서 작성에 사용 되는 언어가 [JSON](https://tools.ietf.org/html/rfc8259)를 함께에서 사용 하는:
-   문서 개체 모델을 정의 하는 스키마 정의
-   JSON 문서 스키마를 준수 하는지 여부의 유효성 검사
-   네이티브 Api의 호출자에 의해 사용 되는 프로그래밍 언어로 이러한 스키마 표현을 JSON 문서의 변환을 자동화 

자주 사용 되는 스키마 정의 [OpenAPI](https://www.openapis.org/) 하 고 [JSON 스키마](http://json-schema.org/), 예를 들어 문서에서 속성의 자세한 정의 지정할 수 있습니다.
-   유효한 집합 0에서 100 사이의 백분율을 나타내는 속성에 대 한 같은 속성에 대 한 값입니다.
-   정의 속성에 대 한 유효한 문자열 집합으로 표현 되는 열거형입니다.
-   정규식 예상 되는 형식에 대 한 문자열입니다. 

HCN Api 문서화의 일부로, OpenAPI 사양으로 JSON 문서 스키마를 게시할 계획 합니다. 이 사양에 따라 클라이언트에서 사용 하 여 프로그래밍 언어의 스키마 개체의 형식이 안전한 사용에 대 한 스키마의 언어별 표현을 사용 수 있습니다. 

### <a name="example"></a>예제 

다음은 VM의 구성 문서에서 SCSI 컨트롤러를 나타내는 개체에 대 한이 워크플로의 예입니다. 

Windows 소스 코드.mars 파일을 사용 하 여 스키마를 정의 합니다: onecore/vm/dv/net/hns/schema/mars/Schema/HCN.Schema.Network.mars

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
>[NewIn("2.0") 주석은 스키마 정의 대 한 버전 관리 지원의 일부입니다.

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

와 같은 도구를 사용할 수 있습니다 [Swagger](https://swagger.io/)를 클라이언트에서 사용 된 프로그래밍 언어 스키마의 언어별 표현을 생성 합니다. Swagger와 같은 다양 한 언어를 지원 합니다 C#, Go, Javascript 및 Python).

- [예제에서는 생성 된 C# 코드](example-c-sharp.md) 상위 수준 IPAM & 서브넷에 대 한 개체입니다.

- [생성 된 Go 코드 예가](example-go.md) 상위 수준 IPAM & 서브넷에 대 한 개체입니다. Go는 Docker 및 Kubernetes의 호스트 네트워크 서비스 계산 Api 소비자의 두 가지는에서 사용 됩니다. Go는 Go 형식에 JSON 문서에서 마샬링 기본 제공 지원 합니다.

코드 생성 및 유효성 검사 하는 것 외에도 JSON 문서를 사용 하 여 작업을 간소화 하기 위해 도구를 사용할 수 있습니다-이므로 [Visual Studio Code](https://code.visualstudio.com/Docs/languages/json)합니다.

### <a name="top-level-objects-defined-in-the-hcnschemasmars-file"></a>HCN에 정의 된 최상위 개체입니다. Schemas.mars 파일
위에서 설명 했 듯이.mars 파일 집합이 HCN Api에서 사용 되는 문서에 대 한 문서 스키마를 찾을 수 있습니다: onecore/vm/dv/net/hns/스키마/mars/스키마

최상위 개체입니다.
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

- 에 대 한 자세한 정보는 [HCN 시나리오로](hcn-scenarios.md)합니다.

- 에 대 한 자세한 정보는 [RPC 컨텍스트 HCN에 대 한 처리](hcn-declaration-handles.md)합니다.

- 에 대 한 자세한 정보는 [HCN JSON 문서 스키마](hcn-json-document-schemas.md)합니다.