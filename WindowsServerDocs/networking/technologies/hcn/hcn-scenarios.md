---
title: 호스트 네트워크 계산 (HCN) 시나리오
description: ''
ms.author: jmesser
author: jmesser81
ms.date: 11/05/2018
ms.openlocfilehash: 2a81b09c41c3b665d6a026da4b63a6119fbe202d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816304"
---
# <a name="common-scenarios"></a>일반적인 시나리오

>적용 대상: Windows Server (반기 채널), Windows Server 2016

## <a name="scenario-hcn"></a>시나리오: HCN 


### <a name="create-an-hcn"></a>HCN 만들기

이 샘플에는 네트워크를 만드는 호스트 계산 가상 머신 또는 컨테이너에 가상 NIC를 연결할 수 있는 호스트의 호스트 계산 네트워크 서비스 API를 사용 하는 방법을 보여 줍니다.

```C++
using unique_hcn_network = wil::unique_any< 
    HCN_NETWORK, 
    decltype(&HcnCloseNetwork), 
    HcnCloseNetwork>; 


/// Creates a simple HCN Network, waiting synchronously to finish the task
void CreateHcnNetwork() 
{

    unique_hcn_network hcnnetwork;
    wil::unique_cotaskmem_string result;
    std::wstring settings = LR"( 
    { 
        "SchemaVersion": { 
            "Major": 2, 
            "Minor": 0 
        }, 
        "Owner" : "WDAGNetwork", 
        "Flags" : 0,
        "Type"  : 0,
        "Ipams" : [
            {
                "Type" : 0,
                "Subnets" : [
                    {
                        "IpAddressPrefix" : "192.168.1.0/24",
                        "Policies" : [
                            {
                                "Type" : "VLAN",
                                "IsolationId" : 100,
                            }
                        ],
                        "Routes" : [
                            {
                                "NextHop" : "192.168.1.1",
                                "DestinationPrefix" : "0.0.0.0/0",
                            }
                        ]

                    }
                ],
            },
        ],
        "MacPool":  {
            "Ranges" : [
                {
                    "EndMacAddress":  "00-15-5D-52-CF-FF",
                    "StartMacAddress":  "00-15-5D-52-C0-00"
                }
            ],
        },
        "Dns" : {
            "Suffix" : "net.home",
            "ServerList" : ["10.0.0.10"],
        }
    }
    })";    
    
    GUID networkGuid;  
    HRESULT result = CoCreateGuid(&networkGuid);

    result = HcnCreateNetwork(
        networkGuid,              // Unique ID 
        settings.c_str(),      // Compute system settings document 
        &hcnnetwork,
        &result 
        );
    if (FAILED(result)) 
    { 
                    // UnMarshal  the result Json
     // ErrorSchema
        //   {
        //  "ErrorCode" : <uint32>,
        //  "Error" : <string>,
        //  "Success" : <bool>,
       //   }

        // Failed to create network
        THROW_HR(result); 
    }  

    // Close the Handle
    result = HcnCloseNetwork(hcnnetwork.get());

    if (FAILED(result)) 
    {
        // UnMarshal  the result Json
        THROW_HR(result);
    }
        
}
```

### <a name="delete-an-hcn"></a>HCN 삭제

이 샘플에서는 호스트 계산 네트워크 서비스 API를 사용 하 여 열 및 계산 호스트 네트워크를 삭제 하는 방법을 보여 줍니다. 

```C++
    wil::unique_cotaskmem_string errorRecord;
    GUID networkGuid; // Initialize it to appropriate network guid value 
    HRESULT hr = HcnDeleteNetwork(networkGuid, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal the result Json
        THROW_HR(hr);
    }
```


### <a name="enumerate-all-networks"></a>모든 네트워크 열거

이 샘플에는 호스트 계산 네트워크 서비스 API를 사용 하 여 모든 호스트 계산 네트워크를 열거 하는 방법을 보여 줍니다.

```C++
     wil::unique_cotaskmem_string resultNetworks;
     wil::unique_cotaskmem_string errorRecord;

     // Filter to select Networks based on properties
     std::wstring filter [] = LR"(
     { 
         "Name"  : "WDAG",
     })";
     HRESULT result = HcnEnumerateNetworks(filter.c_str(), &resultNetworks, &errorRecord);
     if (FAILED(result))
     {
         // UnMarshal  the result Json

         THROW_HR(result);
     }
```


### <a name="query-network-properties"></a>쿼리 네트워크 속성

이 샘플에는 속성을 쿼리하지 네트워크 호스트 계산 네트워크 서비스 API를 사용 하는 방법을 보여 줍니다.

```C++
    unique_hcn_network hcnnetwork;
    wil::unique_cotaskmem_string errorRecord;
    wil::unique_cotaskmem_string properties;
    std:wstring query = LR"(
    { 
        // Future
    })";
    GUID networkGuid; // Initialize it to appropriate network guid value
    HRESULT hr = HcnOpenNetwork(networkGuid, &hcnnetwork, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }


    hr = HcnQueryNetworkProperties(hcnnetwork.get(), query.c_str(), &properties, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
```


## <a name="scenario-hcn-endpoint"></a>시나리오: HCN 끝점

### <a name="create-an-hcn-endpoint"></a>HCN 끝점 만들기

이 샘플에는 호스트 계산 네트워크 서비스 API를 사용 하 여 호스트 계산 네트워크 끝점을 만들고 가상 머신 또는 컨테이너 핫 추가 하는 방법을 보여 줍니다.

```C++
using unique_hcn_endpoint = wil::unique_any< 
    HCN_ENDPOINT, 
    decltype(&HcnCloseEndpoint), 
    HcnCloseEndpoint>; 

void CreateAndHotAddEndpoint() 
{
    unique_hcn_endpoint hcnendpoint;
    unique_hcn_network hcnnetwork;

    wil::unique_cotaskmem_string errorRecord;


    std::wstring settings[] = LR"( 
    { 
        "SchemaVersion": { 
            "Major": 2, 
            "Minor": 0 
        }, 
        "Owner" : "Sample", 
                   "Flags" : 0,
        "HostComputeNetwork" : "87fdcf16-d210-426e-959d-2a1d4f41d6d3",
        "DNS" : {
            "Suffix" : "net.home",
            "ServerList" : "10.0.0.10",
        }
    })”;
    GUID endpointGuid;  
    HRESULT result = CoCreateGuid(&endpointGuid);

    result = HcnOpenNetwork(
        networkGuid,              // Unique ID 
        &hcnnetwork,
        &errorRecord
        );
    if (FAILED(result)) 
    { 
        // Failed to find network
        THROW_HR(result); 
    }                

    result = HcnCreateEndpoint(
        hcnnetwork.get(),
        endpointGuid,              // Unique ID 
        settings.c_str(),      // Compute system settings document 
        &hcnendpoint,
        &errorRecord
        );

    if (FAILED(result)) 
    { 
        // Failed to create endpoint
        THROW_HR(result); 
    }

    // Can use the sample from HCS API Spec on how to attach this endpoint 
    // to the VM using AddNetworkAdapterToVm   

    result = HcnCloseEndpoint(hcnendpoint.get());

    if (FAILED(result))
    {
        // UnMarshal  the result Json
        THROW_HR(result);
    }
             
}
```


### <a name="delete-an-endpoint"></a>끝점 삭제

이 샘플에는 호스트 계산 네트워크 끝점을 삭제 하려면 호스트 계산 네트워크 서비스 API를 사용 하는 방법을 보여 줍니다.

```C++
    wil::unique_cotaskmem_string errorRecord;
    GUID endpointGuid; // Initialize it to appropriate endpoint guid value
    HRESULT hr = HcnDeleteEndpoint(endpointGuid, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
```


### <a name="modify-and-endpoint"></a>수정 및 끝점

이 샘플에는 호스트 계산 네트워크 서비스 API를 사용 하 여 호스트 계산 네트워크 끝점을 수정 하는 방법을 보여 줍니다.

```C++
    unique_hcn_endpoint hcnendpoint;
    GUID endpointGuid; // Initialize it to appropriate endpoint guid value
    
    HRESULT hr = HcnOpenEndpoint(endpointGuid, &hcnendpoint, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }


    std::wstring  ModifySettingAddPortJson = LR"(
    {
        "ResourceType" : 0,
        "RequestType" : 0,
        "Settings" : {
            "PortName" : "acbd341a-ec08-44c0-9d5e-61af0ee86902"
            "VirtualNicName" : "641313e1-7ae8-4ddb-94e5-3215f3a0b218--87fdcf16-d210-426e-959d-2a1d4f41d6d1"
            "VirtualMachineId" : "641313e1-7ae8-4ddb-94e5-3215f3a0b218"
        }
    }
    )";


    hr = HcnModifyEndpoint(hcnendpoint.get(), ModifySettingAddPortJson.c_str(), &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
```


### <a name="enumerate-all-enpoints"></a>모든 enpoints 열거

이 샘플에는 호스트 계산 네트워크 서비스 API를 사용 하 여 모든 호스트의 계산 네트워크 끝점을 열거 하는 방법을 보여 줍니다.

```C++
    wil::unique_cotaskmem_string errorRecord;

    wil::unique_cotaskmem_string resultEndpoints;
    wil::unique_cotaskmem_string errorRecord;

    // Filter to select Endpoint based on properties
    std::wstring filter [] = LR"(
    { 
        "Name"  : "sampleNetwork",
    })";
    result = HcnEnumerateEndpoints(filter.c_str(), &resultEndpoints, &errorRecord);
    if (FAILED(result))
    {
        THROW_HR(result);
    }
```


### <a name="query-endpoint-properties"></a>쿼리 끝점 속성

이 샘플에서는 호스트 계산 네트워크 서비스 API를 사용 하 여 호스트 계산 네트워크 끝점의 모든 속성을 쿼리 하는 방법을 보여 줍니다.

```C++
    unique_hcn_endpoint hcnendpoint;
    wil::unique_cotaskmem_string errorRecord;
    GUID endpointGuid; // Initialize it to appropriate endpoint guid value

    HRESULT hr = HcnOpenEndpoint(endpointGuid, &hcnendpoint, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }



    wil::unique_cotaskmem_string properties;
    std:wstring query = LR"(
    { 
        // Future
    })";

    hr = HcnQueryEndpointProperties(hcnendpoint.get(), query.c_str(), &properties, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the errorRecord Json
        THROW_HR(hr);
    }
```


## <a name="scenario-hcn-namespace"></a>시나리오: HCN 네임 스페이스

### <a name="create-an-hcn-namespace"></a>HCN 네임 스페이스 만들기

이 샘플에는 끝점 및 컨테이너 연결을 사용할 수 있는 호스트의 호스트 계산 네트워크 Namespace를 만들려면 호스트 계산 네트워크 서비스 API를 사용 하는 방법을 보여 줍니다.

```C++
using unique_hcn_namespace = wil::unique_any< 
    HCN_NAMESPACE, 
    decltype(&HcnCloseNamespace), 
    HcnCloseNamespace>; 

/// Creates a simple HCN Network, waiting synchronously to finish the task
void CreateHcnNamespace() 
{

    unique_hcn_namespace handle;
    wil::unique_cotaskmem_string errorRecord;
    std::wstring settings = LR"( 
    { 
        "SchemaVersion": { 
            "Major": 2, 
            "Minor": 0 
        }, 
        "Owner" : "Sample", 
        "Flags" : 0,
        "Type" : 0,
    })";    
   
    GUID namespaceGuid;  
    HRESULT result = CoCreateGuid(&namespaceGuid);

    result = HcnCreateNamespace(
        namespaceGuid,              // Unique ID 
        settings.c_str(),      // Compute system settings document 
        &handle,
        &errorRecord
        );
    if (FAILED(result)) 
    { 
                    // UnMarshal  the result Json
     // ErrorSchema
        //   {
        //  "ErrorCode" : <uint32>,
        //  "Error" : <string>,
        //  "Success" : <bool>,
       //   }

        // Failed to create network
        THROW_HR(result); 
    } 

    result = HcnCloseNamespace(handle.get());

    if (FAILED(result))
    {
        // UnMarshal  the result Json
        THROW_HR(result);
    }
         
}
```


### <a name="delete-an-hcn-namespace"></a>HCN 네임 스페이스 삭제

이 샘플에는 호스트 네트워크 서비스 API가 계산 호스트 계산 네트워크 Namespace 삭제를 사용 하는 방법을 보여 줍니다.

```C++
    wil::unique_cotaskmem_string errorRecord;
    GUID namespaceGuid; // Initialize it to appropriate namespace guid value
    HRESULT hr = HcnDeleteNamespace(namespaceGuid, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal the result Json
        THROW_HR(hr);
    }

```


### <a name="modify-an-hcn-namespace"></a>HCN 네임 스페이스를 수정

이 샘플에는 호스트 계산 네트워크 서비스 API를 사용 하 여 호스트 계산 네트워크 Namespace를 수정 하는 방법을 보여 줍니다.

```C++
    unique_hcn_namespace handle;
    GUID namespaceGuid; // Initialize it to appropriate namespace guid value
    HRESULT hr = HcnOpenNamespace(namespaceGuid, &handle, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }

    wil::unique_cotaskmem_string errorRecord;
    static std::wstring  ModifySettingAddEndpointJson = LR"(
    {
        "ResourceType" : 1,
        "ResourceType" : 0,
        "Settings" : {
            "EndpointId" : "87fdcf16-d210-426e-959d-2a1d4f41d6d1"
        }
    }
    )";

    
    hr = HcnModifyNamespace(handle.get(), ModifySettingAddEndpointJson.c_str(), &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal the result Json
        THROW_HR(hr);
    }
    hr = HcnCloseNamespace(handle.get());

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
    
```


### <a name="enumerate-all-namespaces"></a>모든 네임 스페이스 열거

이 샘플에는 호스트 계산 네트워크 서비스 API를 사용 하 여 모든 호스트 계산 네트워크 네임 스페이스를 열거 하는 방법을 보여 줍니다.

```C++
    wil::unique_cotaskmem_string resultNamespaces;
    wil::unique_cotaskmem_string errorRecord;

    std::wstring filter [] = LR"(
    { 
            // Future       
    })";
    HRESULT hr = HcnEnumerateNamespace(filter.c_str(), &resultNamespaces, &errorRecord);
    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }

```


### <a name="query-namespace-properties"></a>쿼리 네임 스페이스 속성

이 샘플에서는 쿼리 네트워크 Namespace을 계산 하는 호스트 속성에 호스트 계산 네트워크 서비스 API를 사용 하는 방법을 보여 줍니다.

```C++
    unique_hcn_namespace handle;
    GUID namespaceGuid; // Initialize it to appropriate namespace guid value
    HRESULT hr = HcnOpenNamespace(namespaceGuid, &handle, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }


    wil::unique_cotaskmem_string errorRecord;
    wil::unique_cotaskmem_string properties;
    std:wstring query = LR"(
    { 
        // Future
    })";

    HRESULT hr = HcnQueryNamespaceProperties(handle.get(), query.c_str(), &properties, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }

```


## <a name="scenario-hcn-load-balancer"></a>시나리오: HCN 부하 분산 장치

### <a name="create-an-hcn-load-balancer"></a>HCN 부하 분산 장치 만들기

이 샘플에는 부하 분산 끝점에서 계산을 위해 사용할 수 있는 호스트의 호스트 계산 네트워크 부하 분산 장치를 만들려면 호스트 계산 네트워크 서비스 API를 사용 하는 방법을 보여 줍니다.

```C++
using unique_hcn_loadbalancer = wil::unique_any< 
    HCN_LOADBALANCER, 
    decltype(&HcnCloseLoadBalancer), 
    HcnCloseLoadBalancer>; 

/// Creates a simple HCN LoadBalancer, waiting synchronously to finish the task
void CreateHcnLoadBalancer() 
{

    unique_hcn_loadbalancer handle;
    wil::unique_cotaskmem_string errorRecord;
    std::wstring settings = LR"( 
     { 
        "SchemaVersion": { 
            "Major": 2, 
            "Minor": 0 
        }, 
        "Owner" : "Sample", 
        "HostComputeEndpoints" : [
            "87fdcf16-d210-426e-959d-2a1d4f41d6d1"
        ],
        "VirtualIPs" : [ "10.0.0.10" ],
        "PortMappings" : [
            {
                "Protocol" : 0,
                "InternalPort" : 8080,
                "ExternalPort" : 80,
            }
        ],
        "EnableDirectServerReturn" : true,
        "InternalLoadBalancer" : false,
    }
     )";    
   
    GUID lbGuid;  
    HRESULT result = CoCreateGuid(&lbGuid);


    HRESULT hr = HcnCreateLoadBalancer(
        lbGuid,              // Unique ID 
        settings.c_str(),      // LoadBalancer settings document 
        &handle,
        &errorRecord
        );
    if (FAILED(hr)) 
    { 
                    // UnMarshal  the result Json
     // ErrorSchema
        //   {
        //  "ErrorCode" : <uint32>,
        //  "Error" : <string>,
        //  "Success" : <bool>,
       //   }

        // Failed to create network
        THROW_HR(hr); 
    }

    hr = HcnCloseLoadBalancer(handle.get());

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
          
}
```


### <a name="delete-an-hcn-load-balancer"></a>HCN 부하 분산 장치를 삭제 합니다.

이 샘플에는 호스트 계산 네트워크 부하 분산 장치를 삭제 하려면 호스트 계산 네트워크 서비스 API를 사용 하는 방법을 보여 줍니다.

```C++
    wil::unique_cotaskmem_string errorRecord;
    GUID lbGuid; // Initialize it to appropriate loadbalancer guid value
    HRESULT hr = HcnDeleteLoadBalancer(lbGuid , &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal the result Json
        THROW_HR(hr);
    }
```


### <a name="modify-an-hcn-load-balancer"></a>HCN 부하 분산 장치를 수정 합니다.

이 샘플에는 호스트 계산 네트워크 서비스 API를 사용 하 여 호스트 계산 네트워크 Namespace를 수정 하는 방법을 보여 줍니다.

```C++
    unique_hcn_loadbalancer handle;
    GUID lbGuid; // Initialize it to appropriate loadbalancer guid value

    HRESULT hr = HcnOpenLoadBalancer(lbGuid, &handle, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }

    wil::unique_cotaskmem_string errorRecord;
    static std::wstring  ModifySettingAddEndpointJson = LR"(
    {
        "ResourceType" : 1,
        "ResourceType" : 0,
        "Settings" : {
            "EndpointId" : "87fdcf16-d210-426e-959d-2a1d4f41d6d1"
        }
    }
    )";

    
    hr = HcnModifyLoadBalancer(handle.get(), ModifySettingAddEndpointJson.c_str(), &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal the result Json
        THROW_HR(hr);
    }
    hr = HcnCloseLoadBalancer(handle.get());

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
```


### <a name="enumerate-all-load-balancers"></a>모든 부하 분산 장치를 열거 합니다.

이 샘플에는 호스트 계산 네트워크 서비스 API를 사용 하 여 모든 호스트 계산 네트워크 부하 분산 장치를 열거 하는 방법을 보여 줍니다.

```C++
    wil::unique_cotaskmem_string resultLoadBalancers;
    wil::unique_cotaskmem_string errorRecord;

    std::wstring filter [] = LR"(
    { 
         // Future

    })";
    HRESULT result = HcnEnumerateLoadBalancers(filter.c_str(), & resultLoadbalancers, &errorRecord);
    if (FAILED(result))
    {
            // UnMarshal  the result Json

            THROW_HR(result);
    }
```


### <a name="query-load-balancer-properties"></a>쿼리 부하 분산 장치 속성

이 샘플에는 속성을 쿼리하지 호스트 계산 네트워크 부하 분산 장치 호스트 계산 네트워크 서비스 API를 사용 하는 방법을 보여 줍니다.

```C++
    unique_hcn_loadbalancer handle;
    GUID lbGuid; // Initialize it to appropriate loadbalancer guid value

    HRESULT hr = HcnOpenLoadBalancer(lbGuid, &handle, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }


    wil::unique_cotaskmem_string errorRecord;
    wil::unique_cotaskmem_string properties;
    std:wstring query = LR"(
    { 
        "ID"  : "",
        "Type" : 0,
    })";

    hr = HcnQueryNProperties(handle.get(), query.c_str(), &properties, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
```


## <a name="scenario-hcn-notifications"></a>시나리오: HCN 알림

### <a name="register-and-unregister-service-wide-notifications"></a>등록 및 서비스 전반에 걸친 알림을 등록 취소

이 샘플에는 호스트 계산 네트워크 서비스 API를 사용 하 여 등록 및 서비스 전반에 걸친 알림에 등록 하는 방법을 보여 줍니다. 이렇게 하면 호출자 (등록 중에 지정 하는 콜백 함수)를 통해 알림을 받을 수 있습니다. 새 네트워크 만들기 이벤트와 같은 서비스 전반에 걸친 작업을 때마다 발생 합니다.

```C++
using unique_hcn_callback = wil::unique_any< 
    HCN_CALLBACK, 
    decltype(&HcnUnregisterServiceCallback), 
    HcnUnregisterServiceCallback>; 

// Callback handle returned by registration api. Kept at 
// global or module scope as it will automatically be
// unregistered when it goes out of scope.
unique_hcn_callback g_Callback;

// Event notification callback function.
void
CALLBACK
ServiceCallback(
    DWORD   NotificationType,
    void*   Context,
    HRESULT NotificationStatus,
    PCWSTR  NotificationData)
{
    // Optional client context
    UNREFERENCED_PARAMETER(context);
    // Reserved for future use
    UNREFERENCED_PARAMETER(NotificationStatus);

    switch (NotificationType)
    {
        case HcnNotificationNetworkCreate:
            // TODO: UnMarshal the NotificationData
            //
            // // Notification
            // {
            //     "ID" : Guid,
            //     "Flags" : <uint32>,
            // };
            break;

        case HcnNotificationNetworkDelete:
            // TODO: UnMarshal the NotificationData
            break;

        Default:
            // TODO: handle other events.
            break;
    }
}

/// Register for service-wide notifications
void RegisterForServiceNotifications() 
{
    THROW_IF_FAILED(HcnRegisterServiceCallback(
        ServiceCallback,
        nullptr,
        &g_Callback));        
}

/// Unregister from service-wide notifications
void UnregisterForServiceNotifications()
{
    // As this is a unique_hcn_callback, this will cause HcnUnregisterServiceCallback to be invoked
    g_Callback.reset();

}
```

## <a name="next-steps"></a>다음 단계

- 에 대 한 자세한 정보는 [RPC 컨텍스트 HCN에 대 한 처리](hcn-declaration-handles.md)합니다.

- 에 대 한 자세한 정보는 [HCN JSON 문서 스키마](hcn-json-document-schemas.md)합니다.