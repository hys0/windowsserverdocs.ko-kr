---
title: "건강 서비스 오류"
ms.prod: windows-server-threshold
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: 
author: cosmosdarwin
ms.date: 10/05/2017
ms.openlocfilehash: c9e1fb4568ee93739c49ccc1a13106b09161c5f3
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="health-service-faults"></a>건강 서비스 오류
> Windows Server 2016 적용 됩니다.

## <a name="what-are-faults"></a>오류 이란 무엇 인가요?

건강 서비스는 문제를 발견 하 고 "오류"를 생성 하 여 Storage Spaces Direct 클러스터 지속적으로 모니터링 합니다. 새로운 cmdlet을 쉽게 없이 모든 엔터티 보고 배포의 상태를 확인 하거나 결과적 기능 있는 현재 오류를 표시 합니다. 오류는 정확 하 게 하 고를 이해 하기 쉽게 고 하도록 설계 되었습니다.  

각 오류 5 중요 한 필드를 포함 되어 있습니다.  

-   심각도
-   문제에 대 한
-   권장 되는 문제를 해결 하려면 다음 단계
-   오류 엔터티의 신원 파악이 가능한 정보가
-   실제 위치 (가능한 경우)

예를 들어 다음은 일반적인 오류가입니다.  

```
Severity: MINOR                                         
Reason: Connectivity has been lost to the physical disk.                           
Recommendation: Check that the physical disk is working and properly connected.    
Part: Manufacturer Contoso, Model XYZ9000, Serial 123456789                        
Location: Seattle DC, Rack B07, Node 4, Slot 11
```

 >[!NOTE]
 > 실제 위치 오류 도메인 구성에서 파생 되었습니다. 오류 도메인에 대 한 자세한 내용은 참조 [Windows Server 2016에 오류 도메인](fault-domains.md)합니다. 이 정보를 제공 하지 않는 경우 위치 필드 덜 도움이 됩니다.-예를 들어, 슬롯 번호를 표시만 수 있습니다.  

## <a name="root-cause-analysis"></a>근본 원인 분석

건강 서비스를 식별 하 고 결합 하는 동일한 기본 문제의 결과 오류 기관과 부재 중 잠재적인 인과 관계를 평가할 수 있습니다. 체인 효과 인식 하 여 덜 추세 보고 따라서 합니다. 예를 들어, 서버 중단 되는 경우 예상 보다 연결할 수 없는 서버 내 드라이브가 수도 있습니다. 따라서 근본 원인을-이 경우에 서버에 대 한 하나만 오류가 발생 합니다.  

## <a name="usage-in-powershell"></a>PowerShell의 사용

PowerShell의 현재 있는 오류를 표시 하려면이 cmdlet을 실행 합니다.

```PowerShell
Get-StorageSubSystem Cluster* | Debug-StorageSubSystem  
```

전체 Storage Spaces Direct 클러스터에 영향을 주는 모든 오류를 반환 합니다. 대부분의 경우 이러한 오류 관련 하드웨어 또는 구성 되어 있습니다. 오류 인 경우 아무 작업도이 cmdlet 반환 됩니다.  

>[!NOTE]
> 등에 환경 및 책임이 자신에 시험해 볼 수이 기능은 직접 오류를 트리거하-예를 들어, 제거 하 여 실제 디스크를 한 또는 노드를 종료 합니다. 오류가 표시 되 면 다시 삽입 하 여 실제 디스크 또는 노드와 오류 사라집니다 다시 다시 시작 합니다.

또한 특정 볼륨 또는 다음 cmdlet와 파일 공유 영향을 받는 오류를 볼 수 있습니다.  

```PowerShell
Get-Volume -FileSystemLabel <Label> | Debug-Volume  

Get-FileShare -Name <Name> | Debug-FileShare  
```

특정 파일 또는 볼륨 공유만 영향을 주는 모든 오류를 반환 합니다. 대부분의 경우 이러한 오류 용량 계획, 데이터 복구 또는 저장소 서비스 품질 또는 복제 저장소와 같은 기능 관련이 있습니다. 

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

### <a name="query-faults"></a>쿼리 오류

호출 **진단** 대상에 범위는 현재 오류를 **CimInstance**, 클러스터 또는 볼륨 수는 있습니다.

Windows Server 2016에는 각 범위에 사용 가능한 오류의 전체 목록은 아래에 설명 되어 있습니다.

```       
public void GetFaults(CimSession Session, CimInstance Target)
{
    // Set Parameters (None)
    CimMethodParametersCollection FaultsParams = new CimMethodParametersCollection();
    // Invoke API
    CimMethodResult Result = Session.InvokeMethod(Target, "Diagnose", FaultsParams);
    IEnumerable<CimInstance> DiagnoseResults = (IEnumerable<CimInstance>)Result.OutParameters["DiagnoseResults"].Value;
    // Unpack
    if (DiagnoseResults != null)
    {
        foreach (CimInstance DiagnoseResult in DiagnoseResults)
        {
            // TODO: Whatever you want!
        }
    }
}
```

### <a name="optional-myfault-class"></a>옵션: MyFault 클래스

에 대해 생성 하 고 직접 표현 오류를 유지 해야 합니다. 예를 들어이 **MyFault** 클래스 저장 오류를 포함 한 몇 가지 주요 속성의 **FaultId**, 업데이트 연결 또는 알림을, 제거 또는 deduplicate 동일한 오류는는 나중에 사용할 수 있는 어떤 이유에서는 여러 번을 발견 했습니다.

```       
public class MyFault {
    public String FaultId { get; set; }
    public String Reason { get; set; }
    public String Severity { get; set; }
    public String Description { get; set; }
    public String Location { get; set; }

    // Constructor
    public MyFault(CimInstance DiagnoseResult)
    {
        CimKeyedCollection<CimProperty> Properties = DiagnoseResult.CimInstanceProperties;
        FaultId     = Properties["FaultId"                  ].Value.ToString();
        Reason      = Properties["Reason"                   ].Value.ToString();
        Severity    = Properties["PerceivedSeverity"        ].Value.ToString();
        Description = Properties["FaultingObjectDescription"].Value.ToString();
        Location    = Properties["FaultingObjectLocation"   ].Value.ToString();
    }
}
```

```
List<MyFault> Faults = new List<MyFault>;

foreach (CimInstance DiagnoseResult in DiagnoseResults)
{
    Faults.Add(new Fault(DiagnoseResult));
}
```

각 오류가 속성의 전체 목록은 (**DiagnoseResult**) 아래에 설명 되어 있습니다.

### <a name="fault-events"></a>오류 이벤트

오류 생성 된, 제거 또는 업데이트 상태 서비스 WMI 이벤트 생성 합니다. 이러한 필요 자주 폴링을 않고도 동기화 응용 프로그램 상태를 유지 하 고 예를 들어 메일 알림을 보냅니다 하는 시기를 결정 하는 등의 작업에 도움이 될 수 있습니다. 이러한 이벤트 구독할이 샘플 코드 관찰자 디자인 패턴을 다시 사용 합니다.

먼저 구독할 **MSFT\_StorageFaultEvent** 이벤트 합니다.

```      
public void ListenForFaultEvents()
{
    IObservable<CimSubscriptionResult> Events = Session.SubscribeAsync(
        @"root\microsoft\windows\storage", "WQL", "SELECT * FROM MSFT_StorageFaultEvent");
    // Subscribe the Observer
    FaultsObserver<CimSubscriptionResult> Observer = new FaultsObserver<CimSubscriptionResult>(this);
    IDisposable Disposeable = Events.Subscribe(Observer);
}   
```

다음으로 관찰자 구현 해당 **OnNext()** 새 이벤트 생성 때마다 메서드를 호출 됩니다.

각 이벤트 포함 **ChangeType** 여부는 오류 만들고 제거 또는 업데이트와 관련 나타내는 **FaultId**합니다.

또한 오류 자체의 모든 속성 포함 됩니다.

```
class FaultsObserver : IObserver
{
    public void OnNext(T Event)
    {
        // Cast
        CimSubscriptionResult SubscriptionResult = Event as CimSubscriptionResult;

        if (SubscriptionResult != null)
        {
            // Unpack            
            CimKeyedCollection<CimProperty> Properties = SubscriptionResult.Instance.CimInstanceProperties;
            String ChangeType = Properties["ChangeType"].Value.ToString();
            String FaultId = Properties["FaultId"].Value.ToString();

            // Create
            if (ChangeType == "0")
            {
                Fault MyNewFault = new MyFault(SubscriptionResult.Instance);
                // TODO: Whatever you want!
            }
            // Remove
            if (ChangeType == "1")
            {
                // TODO: Use FaultId to find and delete whatever representation you have...
            }
            // Update
            if (ChangeType == "2")
            {
                // TODO: Use FaultId to find and modify whatever representation you have...
            }
        }
    }
    public void OnError(Exception e)
    {
        // Handle Exceptions
    }
    public void OnCompleted()
    {
        // Nothing
    }
}
```

### <a name="understand-fault-lifecycle"></a>이해 오류 수명 주기

오류 "확인" 또는 사용자가 확인 표시는 없습니다. 상태 서비스 관찰 문제를 자동 제거 되 고 상태 서비스 문제를 더 이상 확인할 수 있을 때만 만들어집니다. 일반적으로이 반영 문제가 해결 되었습니다.

그러나 경우에 따라 오류 수 다시 검색할 Health 서비스에 의해 (장애 조치를 후 예를 들어 또는 일시적인 연결 등 때문입니다.). 이러한 이유로 것이 좋습니다 deduplicate 쉽게 수 있으므로 직접 표현 오류를 유지할 수 될 수 있습니다. 이 보내는 메일 알림 또는 해당 하는 경우 특히 중요 합니다.

### <a name="properties-of-faults"></a>오류의 속성

이 표에서 오류 개체의 몇 가지 주요 속성을 보여 줍니다. 전체 스키마 검사는 **MSFT\_StorageDiagnoseResult** 클래스 *storagewmi.mof*합니다.

| **속성**              | **예제**                                                     |
|---------------------------|-----------------------------------------------------------------|
| FaultId                   | {12345-12345-12345-12345-12345}                                 |
| FaultType                 | Microsoft.Health.FaultType.Volume.Capacity                      |
| 이유                    | "볼륨 사용 가능한 공간이 부족 합니다."                 |
| PerceivedSeverity         | 5                                                               |
| FaultingObjectDescription | Contoso XYZ9000 S.N. 123456789                                  |
| FaultingObjectLocation    | 랙 A06, 25 한국, 11 슬롯                                        |
| RecommendedActions        | {"확장 볼륨.", "다른 볼륨 작업 마이그레이션을."}   |

**FaultId** 한 클러스터의 범위 내 고유 합니다.

**PerceivedSeverity** PerceivedSeverity = {4, 5, 6} {"알림", "경고" 및 "오류"} = 또는 파란색, 노란색 및 빨간색 같이 해당 색 합니다.

**FaultingObjectDescription** 부 개체 소프트웨어에 대해 일반적으로 새 하드웨어에 대 한 정보입니다.

**FaultingObjectLocation** 하드웨어에 대 한 위치 정보는 일반적으로 개체 소프트웨어에 대 한 비어 있습니다.

**RecommendedActions** 독립적인 권장 작업을 하 고이 목록입니다. 오늘날,이 목록은 자주 길이 1입니다.

## <a name="properties-of-fault-events"></a>오류 이벤트 속성

이 표 오류 이벤트의 몇 가지 주요 속성을 표시합니다. 전체 스키마 검사는 **MSFT\_StorageFaultEvent** 클래스 *storagewmi.mof*합니다.

노트는 **ChangeType**, 여부는 오류 만들고, 제거 되거나 업데이트를 나타냅니다 및 **FaultId**합니다. 이벤트에는 영향을 받는 오류의 모든 속성 포함 되어 있습니다.

| **속성**              | **예제**                                                     |
|---------------------------|-----------------------------------------------------------------|
| ChangeType                | 0                                                               |
| FaultId                   | {12345-12345-12345-12345-12345}                                 |
| FaultType                 | Microsoft.Health.FaultType.Volume.Capacity                      |
| 이유                    | "볼륨 사용 가능한 공간이 부족 합니다."                 |
| PerceivedSeverity         | 5                                                               |
| FaultingObjectDescription | Contoso XYZ9000 S.N. 123456789                                  |
| FaultingObjectLocation    | 랙 A06, 25 한국, 11 슬롯                                        |
| RecommendedActions        | {"확장 볼륨.", "다른 볼륨 작업 마이그레이션을."}   |

**ChangeType** ChangeType = {0, 1, 2} {"을 만들", "제거", "업데이트"} = 합니다.

## <a name="coverage"></a>검사

Windows Server 2016 건강 서비스 제공 다음과 같은 오류 검사를 합니다.  

### **<a name="physicaldisk-8"></a>(8) 실제 디스크**

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskfailedmedia"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.FailedMedia
* 심각도: 경고
* 이유: *"실제 디스크 하지 못했습니다."*
* RecommendedAction: *"실제 디스크를 대체 합니다."*

#### <a name="faulttype-microsofthealthfaulttypephysicaldisklostcommunication"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.LostCommunication
* 심각도: 경고
* 이유: *"연결이 끊긴 실제 디스크에 있습니다."*
* RecommendedAction: *"실제 디스크를 작동 및 제대로 연결 되어 있는지 확인 합니다."*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunresponsive"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.Unresponsive
* 심각도: 경고
* 이유: *"실제 디스크 반복 응답 현상이 있습니다."*
* RecommendedAction: *"실제 디스크를 대체 합니다."*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskpredictivefailure"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.PredictiveFailure
* 심각도: 경고
* 이유: *"실제 디스크 오류 잠시 후에 예측."*
* RecommendedAction: *"실제 디스크를 대체 합니다."*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunsupportedhardware"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.UnsupportedHardware
* 심각도: 경고
* 이유: *"실제 디스크는 격리 솔루션 공급 업체에서 지원 되지 않으므로."*
* RecommendedAction: *"지원 되는 하드웨어와 실제 디스크를 대체 합니다."*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunsupportedfirmware"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.UnsupportedFirmware
* 심각도: 경고
* 이유: *"실제 디스크 차단에서 하기 때문입니다의 펌웨어 버전 솔루션 공급 업체에서 지원 되지 않습니다."*
* RecommendedAction: *"대상 버전으로 실제 디스크에서 펌웨어를 업데이트 합니다."*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunrecognizedmetadata"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.UnrecognizedMetadata
* 심각도: 경고
* 이유: *"실제 디스크 메타 데이터를 테이블 했습니다."*
* RecommendedAction: *"이이 디스크 알 수 없는 저장소 풀 데이터가 포함 될 수 있습니다. 먼저이 디스크에 유용 데이터가 있는지 확인 한 다음 재설정 디스크. "*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskfailedfirmwareupdate"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.FailedFirmwareUpdate
* 심각도: 경고
* 이유: *"실제 디스크에 대 한 펌웨어 업데이트 실패 시도 합니다."*
* RecommendedAction: *"이진 다른 펌웨어를 사용해 봅니다."*

### **<a name="virtual-disk-2"></a>가상 디스크 (2)**

#### <a name="faulttype-microsofthealthfaulttypevirtualdisksneedsrepair"></a>FaultType: Microsoft.Health.FaultType.VirtualDisks.NeedsRepair
* 심각도: 정보
* 이유: *"이이 볼륨의 일부 데이터는 완벽 하 게 복원 합니다. 그에 계속 액세스할 수 있습니다. "*
* RecommendedAction: *"복원 복구 하는 데이터의."*

#### <a name="faulttype-microsofthealthfaulttypevirtualdisksdetached"></a>FaultType: Microsoft.Health.FaultType.VirtualDisks.Detached
* 심각도: 중요 한
* 이유: *"볼륨 액세스할 수 없는 경우 일부 데이터가 손실 될 수 있습니다. "*
* RecommendedAction: *"물리적 확인 하거나 네트워크의 모든 저장 장치에 연결 합니다. 해야 백업에서 복원 해야 합니다. "*

### **<a name="pool-capacity-1"></a>풀 용량 (1)**

#### <a name="faulttype-microsofthealthfaulttypestoragepoolinsufficientreservecapacityfault"></a>FaultType: Microsoft.Health.FaultType.StoragePool.InsufficientReserveCapacityFault
* 심각도: 경고
* 이유: *"저장소 풀에 없는 최소 권장된 예약 용량 합니다. 이 수 제한 복원 드라이브 오류 발생 하는 경우 데이터 복구 가능성. "*
* RecommendedAction: *"저장소 풀에 추가 용량을 추가 하거나 용량을 확보 합니다. 최소 좋지만 예약 배포 국가별로 용량은 약 2 개의 드라이브의 동안의입니다. "*

### <a name="volume-capacity-2sup1sup"></a>**볼륨 용량 (2)**<sup>1</sup>

#### <a name="faulttype-microsofthealthfaulttypevolumecapacity"></a>FaultType: Microsoft.Health.FaultType.Volume.Capacity
* 심각도: 경고
* 이유: *"볼륨 사용 가능한 공간이 부족 합니다."*
* RecommendedAction: *"볼륨 확장 하거나 다른 볼륨 작업 마이그레이션을."*

#### <a name="faulttype-microsofthealthfaulttypevolumecapacity"></a>FaultType: Microsoft.Health.FaultType.Volume.Capacity
* 심각도: 중요 한
* 이유: *"볼륨 사용 가능한 공간이 부족 합니다."*
* RecommendedAction: *"볼륨 확장 하거나 다른 볼륨 작업 마이그레이션을."*

### **<a name="server-3"></a>서버 (3)**

#### <a name="faulttype-microsofthealthfaulttypeserverdown"></a>FaultType: Microsoft.Health.FaultType.Server.Down
* 심각도: 중요 한
* 이유: *"서버에 연결할 수 없습니다."*
* RecommendedAction: *"시작 하거나 교체 서버."*

#### <a name="faulttype-microsofthealthfaulttypeserverisolated"></a>FaultType: Microsoft.Health.FaultType.Server.Isolated
* 심각도: 중요 한
* 이유: *"서버 인해 연결 문제가 클러스터 분리 됩니다."*
* RecommendedAction: *"격리 계속 되 면 네트워크를 확인 하거나 통하지 작업 마이그레이션을."*

#### <a name="faulttype-microsofthealthfaulttypeserverquarantined"></a>FaultType: Microsoft.Health.FaultType.Server.Quarantined
* 심각도: 중요 한
* 이유: *"서버 반복 문제로 인해 클러스터에서 격리."*
* RecommendedAction: *"서버 바꾸거나 네트워크 문제를 해결 합니다."*

### **<a name="cluster-1"></a>클러스터 (1)**

#### <a name="faulttype-microsofthealthfaulttypeclusterquorumwitnesserror"></a>FaultType: Microsoft.Health.FaultType.ClusterQuorumWitness.Error
* 심각도: 중요 한
* 이유: *"클러스터 이동 하 여 멀리 개의 서버 오류입니다."*
* RecommendedAction: *"감시 리소스를 확인 하 고 필요에 따라 다시 시작 합니다. 시작 또는 실패 서버 교체 합니다. "*

### **<a name="network-adapterinterface-4"></a>네트워크 어댑터/인터페이스 (4)**

#### <a name="faulttype-microsofthealthfaulttypenetworkadapterdisconnected"></a>FaultType: Microsoft.Health.FaultType.NetworkAdapter.Disconnected
* 심각도: 경고
* 이유: *"네트워크 인터페이스 연결 되어 있지."*
* RecommendedAction: *"네트워크 케이블을 연결 합니다."*

#### <a name="faulttype-microsofthealthfaulttypenetworkinterfacemissing"></a>FaultType: Microsoft.Health.FaultType.NetworkInterface.Missing
* 심각도: 경고
* 이유: *"{서버} 서버에 누락 된 네트워크 어댑터가 클러스터 {클러스터} 네트워크에 연결 되어 있습니다."*
* RecommendedAction: *"서버 누락 클러스터 네트워크에 연결 합니다."*

#### <a name="faulttype-microsofthealthfaulttypenetworkadapterhardware"></a>FaultType: Microsoft.Health.FaultType.NetworkAdapter.Hardware
* 심각도: 경고
* 이유: *"네트워크 인터페이스는 하드웨어 오류를 초래 했습니다."*
* RecommendedAction: *"네트워크 인터페이스 어댑터를 교체 합니다."*

#### <a name="faulttype-microsofthealthfaulttypenetworkadapterdisabled"></a>FaultType: Microsoft.Health.FaultType.NetworkAdapter.Disabled
* 심각도: 경고
* 이유: *""네트워크 인터페이스 {네트워크 인터페이스} 사용할 수 없습니다 및 사용 되지는 않습니다.*
* RecommendedAction: *"를 사용 하도록 설정에서 네트워크 인터페이스."*

### **<a name="enclosure-6"></a>엔클로저 (6)**

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurelostcommunication"></a>FaultType: Microsoft.Health.FaultType.StorageEnclosure.LostCommunication
* 심각도: 경고
* 이유: *"통신 되었습니다 스토리지 엔클로저 손실 됩니다."*
* RecommendedAction: *""시작 또는 스토리지 엔클로저 교체 합니다.*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurefanerror"></a>FaultType: Microsoft.Health.FaultType.StorageEnclosure.FanError
* 심각도: 경고
* 이유: *"{위치} 스토리지 엔클로저의 위치에서 팬 하지 못했습니다."*
* RecommendedAction: *"스토리지 엔클로저의 팬 바꿉니다."*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurecurrentsensorerror"></a>FaultType: Microsoft.Health.FaultType.StorageEnclosure.CurrentSensorError
* 심각도: 경고
* 이유: *"{위치} 스토리지 엔클로저의 위치에서 현재 센서 하지 못했습니다."*
* RecommendedAction: *"스토리지 엔클로저에서 현재 센서 교체 합니다."*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurevoltagesensorerror"></a>FaultType: Microsoft.Health.FaultType.StorageEnclosure.VoltageSensorError
* 심각도: 경고
* 이유: *"{위치} 스토리지 엔클로저의 위치에서 전압 센서 하지 못했습니다."*
* RecommendedAction: *"저장소 모양에 전압 센서 교체 합니다."*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosureiocontrollererror"></a>FaultType: Microsoft.Health.FaultType.StorageEnclosure.IoControllerError
* 심각도: 경고
* 이유: *"{위치} 스토리지 엔클로저의 위치에서 IO 컨트롤러 하지 못했습니다."*
* RecommendedAction: *"저장소 모양에 IO 컨트롤러 교체 합니다."*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosuretemperaturesensorerror"></a>FaultType: Microsoft.Health.FaultType.StorageEnclosure.TemperatureSensorError
* 심각도: 경고
* 이유: *"{위치} 스토리지 엔클로저의 위치에 온도 센서 하지 못했습니다."*
* RecommendedAction: *"저장소 모양에 온도 센서 교체 합니다."*

### **<a name="firmware-rollout-3"></a>펌웨어 롤아웃 (3)**

#### <a name="faulttype-microsofthealthfaulttypefaultdomainfailedmaintenancemode"></a>FaultType: Microsoft.Health.FaultType.FaultDomain.FailedMaintenanceMode
* 심각도: 경고
* 이유: *"현재 할 수 없는 펌웨어 롤아웃 수행 하는 동안 진행 상태를 확인 합니다."*
* RecommendedAction: *"저장소 공간에는 모든, 건강 한 되며 오류 도메인이 현재 유지 관리 모드에 있는지 확인 합니다."*

#### <a name="faulttype-microsofthealthfaulttypefaultdomainfirmwareverifyversionfaile"></a>FaultType: Microsoft.Health.FaultType.FaultDomain.FirmwareVerifyVersionFaile
* 심각도: 경고
* 이유: *"펌웨어 롤아웃 펌웨어 업데이트를 적용 한 후 읽을 수 없거나 예기치 않은 펌웨어 버전 정보로 인해 취소 되었습니다."*
* RecommendedAction: *"다시 시작 펌웨어 출시 후 펌웨어 문제가 해결 되었습니다."*

#### <a name="faulttype-microsofthealthfaulttypefaultdomaintoomanyfailedupdates"></a>FaultType: Microsoft.Health.FaultType.FaultDomain.TooManyFailedUpdates
* 심각도: 경고
* 이유: *"펌웨어 롤아웃 펌웨어 업데이트 시도가 실패 너무 많은 실제 디스크 인해 취소 되었습니다."*
* RecommendedAction: *"다시 시작 펌웨어 출시 후 펌웨어 문제가 해결 되었습니다."*

### <a name="storage-qos-3sup2sup"></a>**저장소 QoS (3)**<sup>2</sup>

#### <a name="faulttype-microsofthealthfaulttypestorqosinsufficientthroughput"></a>FaultType: Microsoft.Health.FaultType.StorQos.InsufficientThroughput
* 심각도: 경고
* 이유: *"저장소 처리량 예약을 충족 하는 데 충분 하지 않습니다."*
* RecommendedAction: *"저장소 QoS 정책을 재구성."*

#### <a name="faulttype-microsofthealthfaulttypestorqoslostcommunication"></a>FaultType: Microsoft.Health.FaultType.StorQos.LostCommunication
* 심각도: 경고
* 이유: *"저장소 QoS 정책 관리자 볼륨와 통신 잃어버린."*
* RecommendedAction: *"노드 {노드} 재부팅 주세요"*

#### <a name="faulttype-microsofthealthfaulttypestorqosmisconfiguredflow"></a>FaultType: Microsoft.Health.FaultType.StorQos.MisconfiguredFlow
* 심각도: 경고
* 이유: *"하나 이상의 저장소 소비자 (일반적으로 가상 컴퓨터) 사용 하 고 없는 정책을 id {id}로."*
* RecommendedAction: *"누락 된 저장소 QoS 정책 다시."*

<sup>1</sup> 나타냅니다 볼륨 80% 전체 (부 심각도) 또는 90% 전체 (주 심각도)에 도달 했습니다.  
<sup>2</sup> 볼륨의 몇 가지.vhd(s)에 대 한 자신의 최소 IOPS 만족 하지 나타냅니다 끝남 10% (부), 30% (주) 또는 50%는 24 시간 창 롤링 (중요 한).  

>[!NOTE]
> 팬, 전원 공급 장치, 센서 등 엔클로저 구성 요소 저장소 건강 SCSI 엔클로저 서비스 (SES)에서 파생 되었습니다. 공급 업체는이 정보를 제공 하지 상태 서비스 표시할 수 없습니다.  

## <a name="see-also"></a>참조 하십시오

- [Windows Server 2016에에서 상태 서비스](health-service-overview.md)
