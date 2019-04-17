---
title: "건강 서비스 보고서"
ms.prod: windows-server-threshold
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: 
author: cosmosdarwin
ms.date: 10/05/2017
ms.openlocfilehash: bc21b9fdec5700fec23dc6af7ca15873ded34bea
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="health-service-reports"></a>건강 서비스 보고서
> Windows Server 2016 적용 됩니다.

## <a name="what-are-reports"></a>보고서 이란 무엇 인가요?  

건강 서비스 Storage Spaces Direct 클러스터에서 라이브 성능 및 용량 정보를 다운로드 하는 데 필요한 작업을 줄일 수 있습니다. 새로운 cmdlet 효율적으로 수집 되 고 노드에서 클러스터 구성원을 감지 하는 기본 제공 논리가으로 동적으로 집계 필수 메트릭, 엄선 된 목록이 제공 합니다. 모든 값 실시간 및 시점에만 됩니다.  

## <a name="usage-in-powershell"></a>PowerShell의 사용

이 cmdlet 전체 Storage Spaces Direct 클러스터에 대 한 메트릭을 사용 합니다.

```PowerShell
Get-StorageSubSystem Cluster* | Get-StorageHealthReport
```

선택적 **개수** 매개 한 초 간격을 반환 하 값을 개수 설정 나타냅니다.  

```PowerShell
Get-StorageSubSystem Cluster* | Get-StorageHealthReport -Count <Count>  
```

또한 특정 볼륨 이상 서버에 대 한 메트릭을 이동할 수 있습니다.  

```PowerShell
Get-Volume -FileSystemLabel <Label> | Get-StorageHealthReport -Count <Count>  

Get-StorageNode -Name <Name> | Get-StorageHealthReport -Count <Count>
```

## <a name="usage-in-net-and-c"></a>.NET 및 C# 사용

### <a name="connect"></a>연결

하려면 상태 서비스, 쿼리를 설정 해야 합니다는 **CimSession** 클러스터와 합니다. 이렇게만 전체.NET에서 사용할 수 있는 몇 가지 해야, 알 수 쉽게 이렇게 할 수 없는 웹 또는 모바일 앱에서 직접 합니다. 이러한 코드 샘플 C\ #,이 데이터 액세스 계층을 선택 하는 가장 간단한 사용 합니다.

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

제공 된 사용자 이름 대상 컴퓨터의 로컬 관리자 해야 합니다.

암호를 생성 하는 것이 좋습니다 **SecureString** 직접에서 사용자가 입력 실시간, 따라서 암호 하지 메모리에 저장 되어 암호화 되지 않은 텍스트에 있습니다. 이렇게 하면 다양 한 보안 문제를 완화 수 있습니다. 하지만 실제로 위의 생성 프로토타입 목적을 위해 일반적인 합니다.

### <a name="discover-objects"></a>개체 검색

와 **CimSession** 설정 쿼리 WMI(Windows Management Instrumentation) (WMI) 클러스터의 합니다.

오류 또는 메트릭을 받을 수 있는 전에 인스턴스 관련 된 몇 가지 개체를 다운로드 해야 합니다. 먼저는 **MSFT\_StorageSubSystem** 클러스터에 Storage Spaces Direct 나타내는 합니다. 얻을 수를 사용 하 여, 모든 **MSFT\_StorageNode** 클러스터에서 및 모든 **MSFT\_Volume**, 데이터 볼륨 합니다. 마지막으로 해야 합니다는 **MSFT\_StorageHealth**, 상태 서비스도 있습니다.

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

로그인 할 PowerShell cmdlet 처럼 사용 하 여 동일한 개체 **Get StorageSubSystem**, **Get StorageNode**, 및 **Get 볼륨**합니다.

속성을 설명에 모두 같은 액세스할 수 [저장소 관리 API 클래스](https://msdn.microsoft.com/en-us/library/windows/desktop/hh830612(v=vs.85).aspx)합니다.

```
...
using System.Diagnostics;

foreach (CimInstance Node in Nodes)
{
    // For illustration, write each node's Name to the console. You could also write State (up/down), or anything else!
    Debug.WriteLine("Discovered Node " + Node.CimInstanceProperties["Name"].Value.ToString());
}
```

호출 **GetReport** 효율적으로 수집 되 고 노드에서 클러스터 구성원을 감지 하는 기본 제공 논리가으로 동적으로 집계 된 필수 메트릭 전문가 구성 된 목록의 샘플 스트리밍 시작 합니다. 샘플 매초 그 후에 도착 됩니다. 모든 값 실시간 및 시점에만 됩니다.

세 가지 범위에 대 한 메트릭 스트리밍할 수 있습니다: 클러스터, 모든 노드 또는 볼륨 합니다.

Windows Server 2016에는 각 범위에 사용 가능한 메트릭의 전체 목록은 아래에 설명 되어 있습니다.

### <a name="iobserveronnext"></a>IObserver.OnNext()

이 샘플 코드를 사용 하 여는 [관찰자 디자인 패턴](https://msdn.microsoft.com/en-us/library/ee850490(v=vs.110).aspx) 관찰자 구현 하 해당 **OnNext()** 메트릭 각 새로운 샘플 도착 하면 메서드를 호출 됩니다. 그 **OnCompleted()** 됩니다 때 메서드를 호출 하는 경우/종료 스트리밍 합니다. 예를 들어, 사용할 수 있습니다 것 스트리밍, 다시 시작 하 하므로 동안 계속 됩니다.

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

정의 관찰자 스트리밍을 시작할 수 있습니다.

대상 지정 **CimInstance** 범위 메트릭 대상 합니다. 클러스터, 모든 노드 또는 볼륨 수 있습니다.

Count 매개 변수 스트리밍 종료 하기 전에 샘플 수는 있습니다.

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

물론는 데이터베이스에 저장 또는 안이나 어떤 방식으로 사용 되는 이러한 메트릭 시각화 될 수 있습니다.

### <a name="properties-of-reports"></a>보고서는 속성

모든 샘플 메트릭 하나 "보고서가" 레코드가 많은 "" 개별 메트릭 하는 합니다.

전체 스키마 검사는 **MSFT\_StorageHealthReport** 및 **MSFT\_HealthRecord** 의 클래스 *storagewmi.mof*합니다.

각 메트릭이 표 당 3만 속성 했습니다.

| **속성** | **예제**       |
| -------------|-------------------|
| 이름         | IOLatencyAverage  |
| 값        | 0.00021           |
| 장치        | 3                 |

단위 {0, 1, 2, 3, 4} = 0 = ""를 바이트 1, 2 "BytesPerSecond" = 3 "CountPerSecond" = = "초 동안" 또는 4 = "백분율" 합니다.

## <a name="coverage"></a>검사

다음은 Windows Server 2016에는 각 범위에 사용할 수 있는 메트릭입니다.

### <a name="msftstoragesubsystem"></a>MSFT_StorageSubSystem

| **이름**                        | **장치** |
|---------------------------------|-----------|
| CPUUsage                        | 4         |
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


### <a name="msftstoragenode"></a>MSFT_StorageNode

| **이름**            | **장치** |
|---------------------|-----------|
| CPUUsage            | 4         |
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

### <a name="msftvolume"></a>MSFT_Volume

| **이름**            | **장치** |
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

## <a name="see-also"></a>참조 하십시오

- [Windows Server 2016에에서 상태 서비스](health-service-overview.md)
