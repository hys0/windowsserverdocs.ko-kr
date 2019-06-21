---
title: Health Service가 보고
ms.prod: windows-server-threshold
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: ''
author: cosmosdarwin
ms.date: 10/05/2017
ms.openlocfilehash: e018c0270a0bf410dada9c05d2c25e51fdfac1d8
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280160"
---
# <a name="health-service-reports"></a>Health Service가 보고
> 적용 대상: Windows Server 2019, Windows Server 2016

## <a name="what-are-reports"></a>보고서 란  

상태 관리 서비스 저장소 공간 다이렉트 클러스터에서 실시간 성능 및 용량 정보를 가져오는 데 필요한 작업을 줄입니다. 하나의 새 cmdlet에는 효율적으로 수집 되 고 클러스터 멤버 자격을 검색 하기 위한 기본 제공 논리가 구성 된 노드에서 동적으로 집계 하는 기본 메트릭 목록을 제공 합니다. 모든 값은 실시간 및 지정 시간 값으로만 제공됩니다.  

## <a name="usage-in-powershell"></a>PowerShell에서 사용

이 cmdlet를 사용 하 여 전체 저장소 공간 다이렉트 클러스터에 대 한 메트릭을 가져옵니다.

```PowerShell
Get-StorageSubSystem Cluster* | Get-StorageHealthReport
```

선택적 **개수** 반환할 1 초 간격 값의 수 설정 매개 변수를 나타냅니다.  

```PowerShell
Get-StorageSubSystem Cluster* | Get-StorageHealthReport -Count <Count>  
```

또한 하나의 특정 볼륨이 나 서버에 대 한 메트릭을 가져올 수 있습니다.  

```PowerShell
Get-Volume -FileSystemLabel <Label> | Get-StorageHealthReport -Count <Count>  

Get-StorageNode -Name <Name> | Get-StorageHealthReport -Count <Count>
```

## <a name="usage-in-net-and-c"></a>.NET에서 사용 하 고C#

### <a name="connect"></a>연결

상태 관리 서비스를 쿼리 하기 위해 설정 해야 합니다는 **CimSession** 클러스터를 사용 하 여 합니다. 하므로 전체.NET에만 사용할 수 있는 몇 가지 해야 할 것을 의미 하므로 수행할 수 없습니다 쉽게 웹 또는 모바일 앱에서 직접. 다음 코드 샘플은 C를 사용 하 여\#는 가장 간단한이 데이터 액세스 계층을 선택 합니다.

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

제공 된 사용자 이름 대상 컴퓨터의 로컬 관리자 여야 합니다.

암호를 생성 하는 것이 좋습니다 **SecureString** 직접에 사용자 입력에서 실시간으로 따라서 암호가 없습니다 메모리에 저장 됩니다 텍스트로 합니다. 이렇게 하면 다양 한 보안 문제를 완화 합니다. 이지만 실제로 위와 생성 프로토타입 용도로 일반적입니다.

### <a name="discover-objects"></a>개체 검색

사용 하 여 합니다 **CimSession** 설정를 쿼리할 수 있습니다 Windows Management Instrumentation (WMI) 클러스터입니다.

오류 또는 메트릭을 가져올 수 있습니다, 전에 여러 관련 개체의 인스턴스를 가져오는 해야 합니다. 먼저 합니다 **MSFT\_StorageSubSystem** 클러스터에서 저장소 공간 다이렉트를 나타내는입니다. 가져올 수 있는 사용 마다 **MSFT\_전달 하면 StorageNode** 클러스터의 매 **MSFT\_볼륨**, 데이터 볼륨. 마지막으로 해야 합니다 **MSFT\_StorageHealth**, Health Service가 자체를 너무 합니다.

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

이 동일한 개체와 같은 cmdlet을 사용 하 여 PowerShell에서 얻게 **Get-storagesubsystem**, **Get-storagenode**, 및 **Get-volume**합니다.

에 설명 된 속성 모두 동일한 액세스할 수 있습니다 [저장소 관리 API 클래스](https://msdn.microsoft.com/library/windows/desktop/hh830612(v=vs.85).aspx)합니다.

```
...
using System.Diagnostics;

foreach (CimInstance Node in Nodes)
{
    // For illustration, write each node's Name to the console. You could also write State (up/down), or anything else!
    Debug.WriteLine("Discovered Node " + Node.CimInstanceProperties["Name"].Value.ToString());
}
```

호출할 **GetReport** 효율적으로 수집 되 고 클러스터 멤버 자격을 검색 하기 위한 기본 제공 논리가 구성 된 노드에서 동적으로 집계 하는 필수 메트릭의 전문가 큐 레이트 목록의 샘플 스트리밍을 시작 하려면. 샘플 이후 1 초 마다 도착 합니다. 모든 값은 실시간 및 지정 시간 값으로만 제공됩니다.

세 가지 범위에 대 한 메트릭을 스트리밍할 수 있습니다: 클러스터, 모든 노드 또는 모든 볼륨입니다.

Windows Server 2016의 각 범위에 사용할 수 있는 메트릭 전체 목록은 아래 설명 되어 있습니다.

### <a name="iobserveronnext"></a>IObserver.OnNext()

이 샘플 코드를 사용 하는 [관찰자 디자인 패턴](https://msdn.microsoft.com/library/ee850490(v=vs.110).aspx) 관찰자 구현에입니다 **OnNext()** 메트릭의 각 새 샘플 도착할 때 메서드가 호출 됩니다. 해당 **OnCompleted()** 메서드가 호출 됩니다/종료를 스트리밍하는 경우. 예를 들어 사용할 수 있습니다이 스트리밍의 경우, 다시 시작 하려면 무기한 계속 됩니다.

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

정의 된 관찰자를 사용 하 여 스트리밍을 시작할 수 있습니다.

대상 지정 **CimInstance** 범위 메트릭을 추가할 합니다. 클러스터, 모든 노드 또는 모든 볼륨 수 있습니다.

Count 매개 변수 끝을 스트리밍하기 전에 샘플의 수를입니다.

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

물론 데이터베이스에 저장 하거나 필요에 원하는 방식으로 사용 되는 이러한 메트릭을 시각화할 수 있습니다.

### <a name="properties-of-reports"></a>보고서의 속성

모든 샘플 메트릭 하나 "보고서" 여러 "레코드"에 해당 개별 메트릭 하를 포함 하는 경우

전체 스키마에 대해 검사 합니다 **MSFT\_StorageHealthReport** 하 고 **MSFT\_HealthRecord** 의 클래스 *storagewmi.mof*합니다.

각 메트릭에 아래이 표에 따라 3 개의 속성입니다.

| **속성** | **예제**       |
| -------------|-------------------|
| 이름         | IOLatencyAverage  |
| 값        | 0.00021           |
| 단위        | 3                 |

단위 = {0, 1, 2, 3, 4}, 여기서 0 = 1 "Bytes", "BytesPerSecond", 2 = "CountPerSecond", 3 = = "Seconds", 또는 4 = "Percentage"입니다.

## <a name="coverage"></a>적용 범위

다음은 Windows Server 2016에서 각 범위에 사용할 수 있는 메트릭입니다.

### <a name="msftstoragesubsystem"></a>MSFT_StorageSubSystem

| **이름**                        | **단위** |
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

| **이름**            | **단위** |
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

## <a name="see-also"></a>참조

- [Windows Server 2016의에서 상태 관리 서비스](health-service-overview.md)
