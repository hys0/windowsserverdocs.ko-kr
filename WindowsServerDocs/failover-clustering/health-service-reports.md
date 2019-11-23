---
title: 상태 관리 서비스 보고서
ms.prod: windows-server
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: ''
author: cosmosdarwin
ms.date: 10/05/2017
ms.openlocfilehash: e65db8834bd0b059dc7bbebbcaf9288fb46da225
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369683"
---
# <a name="health-service-reports"></a>상태 관리 서비스 보고서
> 적용 대상: Windows Server 2019, Windows Server 2016

## <a name="what-are-reports"></a>보고서 란?  

상태 관리 서비스은 스토리지 공간 다이렉트 클러스터에서 라이브 성능 및 용량 정보를 가져오는 데 필요한 작업을 줄입니다. 새 cmdlet 중 하나는 클러스터 멤버 자격을 검색 하는 기본 제공 논리를 사용 하 여 노드 간에 효율적이 고 동적으로 수집 되는 필수 메트릭의 큐 레이트 목록을 제공 합니다. 모든 값은 실시간 및 지정 시간 값으로만 제공됩니다.  

## <a name="usage-in-powershell"></a>PowerShell에서 사용

이 cmdlet을 사용 하 여 전체 스토리지 공간 다이렉트 클러스터에 대 한 메트릭을 가져올 수 있습니다.

```PowerShell
Get-StorageSubSystem Cluster* | Get-StorageHealthReport
```

선택적 **Count** 매개 변수는 1 초 간격으로 반환할 값 집합 수를 나타냅니다.  

```PowerShell
Get-StorageSubSystem Cluster* | Get-StorageHealthReport -Count <Count>  
```

특정 볼륨 또는 서버에 대 한 메트릭을 가져올 수도 있습니다.  

```PowerShell
Get-Volume -FileSystemLabel <Label> | Get-StorageHealthReport -Count <Count>  

Get-StorageNode -Name <Name> | Get-StorageHealthReport -Count <Count>
```

## <a name="usage-in-net-and-c"></a>.NET 및에서 사용C#

### <a name="connect"></a>연결

상태 관리 서비스를 쿼리하려면 클러스터로 **CimSession** 를 설정 해야 합니다. 이렇게 하려면 전체 .NET 에서만 사용할 수 있는 몇 가지 항목이 필요 합니다. 즉, 웹 또는 모바일 앱에서 바로이 작업을 수행할 수 없습니다. 이러한 코드 샘플은이 데이터 액세스 계층에 가장 간단한 선택 인 C\#를 사용 합니다.

``` 
...
using System.Security;
using Microsoft.Management.Infrastructure;

public CimSession Connect(string Domain = "...", string Computer = "...", string Username = "...", string Password = "...")
{
    SecureString PasswordSecureString = new SecureString();
    foreach (char c in Password)
    {
        PasswordSecureString.AppendChar(c);
    }

    CimCredential Credentials = new CimCredential(
        PasswordAuthenticationMechanism.Default, Domain, Username, PasswordSecureString);
    WSManSessionOptions SessionOptions = new WSManSessionOptions();
    SessionOptions.AddDestinationCredentials(Credentials);
    Session = CimSession.Create(Computer, SessionOptions);
    return Session;
}
```

제공 된 사용자 이름은 대상 컴퓨터의 로컬 관리자 여야 합니다.

사용자 입력에서 암호 **SecureString** 을 실시간으로 직접 생성 하는 것이 좋습니다. 따라서 암호는 일반 텍스트로 메모리에 저장 되지 않습니다. 이렇게 하면 다양 한 보안 문제를 완화할 수 있습니다. 그러나 실제로는 프로토타입 생성을 위해 위와 같이 생성 하는 것이 일반적입니다.

### <a name="discover-objects"></a>개체 검색

**CimSession** 가 설정 되 면 클러스터에서 WMI(WINDOWS MANAGEMENT INSTRUMENTATION) (WMI)를 쿼리할 수 있습니다.

오류나 메트릭을 얻기 전에 여러 관련 개체의 인스턴스를 가져와야 합니다. 먼저, **MSFT\_StorageSubSystem** 은 클러스터의 스토리지 공간 다이렉트를 나타냅니다. 이를 사용 하 여 클러스터의 모든 **msft\_StorageNode** 및 모든 **msft\_볼륨**, 데이터 볼륨을 가져올 수 있습니다. 마지막으로, 상태 관리 서비스 자체인 **MSFT\_StorageHealth**가 필요 합니다.

```
CimInstance Cluster;
List<CimInstance> Nodes;
List<CimInstance> Volumes;
CimInstance HealthService;

public void DiscoverObjects(CimSession Session)
{
    // Get MSFT_StorageSubSystem for Storage Spaces Direct
    Cluster = Session.QueryInstances(@"root\microsoft\windows\storage", "WQL", "SELECT * FROM MSFT_StorageSubSystem")
        .First(Instance => (Instance.CimInstanceProperties["FriendlyName"].Value.ToString()).Contains("Cluster"));

    // Get MSFT_StorageNode for each cluster node
    Nodes = Session.EnumerateAssociatedInstances(Cluster.CimSystemProperties.Namespace,
        Cluster, "MSFT_StorageSubSystemToStorageNode", null, "StorageSubSystem", "StorageNode").ToList();

    // Get MSFT_Volumes for each data volume
    Volumes = Session.EnumerateAssociatedInstances(Cluster.CimSystemProperties.Namespace,
        Cluster, "MSFT_StorageSubSystemToVolume", null, "StorageSubSystem", "Volume").ToList();

    // Get MSFT_StorageHealth itself
    HealthService = Session.EnumerateAssociatedInstances(Cluster.CimSystemProperties.Namespace,
        Cluster, "MSFT_StorageSubSystemToStorageHealth", null, "StorageSubSystem", "StorageHealth").First();
}
```

이러한 개체는 **Get StorageSubSystem**, **StorageNode**및 **get 볼륨**과 같은 cmdlet을 사용 하 여 PowerShell에서 가져옵니다.

[저장소 관리 API 클래스](https://msdn.microsoft.com/library/windows/desktop/hh830612(v=vs.85).aspx)에서 설명 하는 모든 동일한 속성에 액세스할 수 있습니다.

```
...
using System.Diagnostics;

foreach (CimInstance Node in Nodes)
{
    // For illustration, write each node's Name to the console. You could also write State (up/down), or anything else!
    Debug.WriteLine("Discovered Node " + Node.CimInstanceProperties["Name"].Value.ToString());
}
```

**Getreport** 를 호출 하 여 클러스터 멤버 자격을 검색 하는 기본 제공 논리를 사용 하 여 효율적으로 수집 되 고 노드 전체에서 동적으로 집계 되는 필수 메트릭의 큐 레이트 샘플의 스트리밍을 시작 합니다. 그 후에 샘플은 초 마다 도착할 것입니다. 모든 값은 실시간 및 지정 시간 값으로만 제공됩니다.

세 가지 범위 (클러스터, 모든 노드 또는 모든 볼륨)에 대해 메트릭을 스트리밍할 수 있습니다.

Windows Server 2016의 각 범위에서 사용할 수 있는 메트릭의 전체 목록은 아래에 설명 되어 있습니다.

### <a name="iobserveronnext"></a>IObserver. OnNext ()

이 샘플 코드에서는 [관찰자 디자인 패턴](https://msdn.microsoft.com/library/ee850490(v=vs.110).aspx) 을 사용 하 여 새 메트릭 샘플이 도착할 때마다 **onnext ()** 메서드가 호출 되는 관찰자를 구현 합니다. 스트리밍이 종료 되 면 해당 **Oncompleted ()** 메서드가 호출 됩니다. 예를 들어 스트리밍을 다시 시작 하는 데 사용할 수 있으므로 무기한 계속 됩니다.

```
class MetricsObserver<T> : IObserver<T>
{
    public void OnNext(T Result)
    {
        // Cast
        CimMethodStreamedResult StreamedResult = Result as CimMethodStreamedResult;

        if (StreamedResult != null)
        {
            // For illustration, you could store the metrics in this dictionary
            Dictionary<string, string> Metrics = new Dictionary<string, string>();

            // Unpack
            CimInstance Report = (CimInstance)StreamedResult.ItemValue;
            IEnumerable<CimInstance> Records = (IEnumerable<CimInstance>)Report.CimInstanceProperties["Records"].Value;
            foreach (CimInstance Record in Records)
            {
                /// Each Record has "Name", "Value", and "Units"
                Metrics.Add(
                    Record.CimInstanceProperties["Name"].Value.ToString(),
                    Record.CimInstanceProperties["Value"].Value.ToString()
                    );
            }

            // TODO: Whatever you want!
        }
    }
    public void OnError(Exception e)
    {
        // Handle Exceptions
    }
    public void OnCompleted()
    {
        // Reinvoke BeginStreamingMetrics(), defined in the next section
    }
}
```

### <a name="begin-streaming"></a>스트리밍 시작

관찰자가 정의 되 면 스트리밍을 시작할 수 있습니다.

메트릭에 범위가 지정 하려는 대상 **ciminstance 개체로** 를 지정 합니다. 클러스터, 모든 노드 또는 볼륨이 될 수 있습니다.

Count 매개 변수는 스트리밍이 끝나기 전의 샘플 수입니다.

```
CimInstance Target = Cluster; // From among the objects discovered in DiscoverObjects()

public void BeginStreamingMetrics(CimSession Session, CimInstance HealthService, CimInstance Target)
{
    // Set Parameters
    CimMethodParametersCollection MetricsParams = new CimMethodParametersCollection();
    MetricsParams.Add(CimMethodParameter.Create("TargetObject", Target, CimType.Instance, CimFlags.In));
    MetricsParams.Add(CimMethodParameter.Create("Count", 999, CimType.UInt32, CimFlags.In));
    // Enable WMI Streaming
    CimOperationOptions Options = new CimOperationOptions();
    Options.EnableMethodResultStreaming = true;
    // Invoke API
    CimAsyncMultipleResults<CimMethodResultBase> InvokeHandler;
    InvokeHandler = Session.InvokeMethodAsync(
        HealthService.CimSystemProperties.Namespace, HealthService, "GetReport", MetricsParams, Options
        );
    // Subscribe the Observer
    MetricsObserver<CimMethodResultBase> Observer = new MetricsObserver<CimMethodResultBase>(this);
    IDisposable Disposeable = InvokeHandler.Subscribe(Observer);
}
```

이러한 메트릭은 이러한 메트릭을 시각화 하거나 데이터베이스에 저장 하거나 적합 한 방식으로 사용할 수 있습니다.

### <a name="properties-of-reports"></a>보고서 속성

메트릭의 모든 샘플은 개별 메트릭에 해당 하는 많은 "레코드"를 포함 하는 하나의 "보고서"입니다.

전체 스키마의 경우 *Storagewmi*에서 **msft\_** 및 **msft\_HealthRecord** 클래스를 검사 합니다.

각 메트릭에는이 테이블 당 세 가지 속성만 있습니다.

| **속성** | **예제**       |
| -------------|-------------------|
| 이름         | IOLatencyAverage  |
| 값        | 0.00021           |
| 단위        | 3                 |

단위 = {0, 1, 2, 3, 4}, 여기서 0 = "Bytes", 1 = "BytesPerSecond", 2 = "CountPerSecond", 3 = "Seconds" 또는 4 = "백분율".

## <a name="coverage"></a>적용 범위

Windows Server 2016의 각 범위에 사용할 수 있는 메트릭은 다음과 같습니다.

### <a name="msft_storagesubsystem"></a>MSFT_StorageSubSystem

| **이름**                        | **단위** |
|---------------------------------|-----------|
| CPUUsage                        | 추가를 클릭합니다.         |
| CapacityPhysicalPooledAvailable | 0         |
| CapacityPhysicalPooledTotal     | 0         |
| CapacityPhysicalTotal           | 0         |
| CapacityPhysicalUnpooled        | 0         |
| CapacityVolumesAvailable        | 0         |
| CapacityVolumesTotal            | 0         |
| IOLatencyAverage                | 3         |
| IOLatencyRead                   | 3         |
| IOLatencyWrite                  | 3         |
| IOPSRead                        | 2         |
| IOPSTotal                       | 2         |
| IOPSWrite                       | 2         |
| IOThroughputRead                | 1         |
| IOThroughputTotal               | 1         |
| IOThroughputWrite               | 1         |
| MemoryAvailable                 | 0         |
| MemoryTotal                     | 0         |


### <a name="msft_storagenode"></a>MSFT_StorageNode

| **이름**            | **단위** |
|---------------------|-----------|
| CPUUsage            | 추가를 클릭합니다.         |
| IOLatencyAverage    | 3         |
| IOLatencyRead       | 3         |
| IOLatencyWrite      | 3         |
| IOPSRead            | 2         |
| IOPSTotal           | 2         |
| IOPSWrite           | 2         |
| IOThroughputRead    | 1         |
| IOThroughputTotal   | 1         |
| IOThroughputWrite   | 1         |
| MemoryAvailable     | 0         |
| MemoryTotal         | 0         |

### <a name="msft_volume"></a>MSFT_Volume

| **이름**            | **단위** |
|---------------------|-----------|
| CapacityAvailable   | 0         |
| CapacityTotal       | 0         |
| IOLatencyAverage    | 3         |
| IOLatencyRead       | 3         |
| IOLatencyWrite      | 3         |
| IOPSRead            | 2         |
| IOPSTotal           | 2         |
| IOPSWrite           | 2         |
| IOThroughputRead    | 1         |
| IOThroughputTotal   | 1         |
| IOThroughputWrite   | 1         |

## <a name="see-also"></a>참고 항목

- [Windows Server 2016의 상태 관리 서비스](health-service-overview.md)
