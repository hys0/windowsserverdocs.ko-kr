---
title: 상태 서비스 오류
ms.prod: windows-server-threshold
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: ''
author: cosmosdarwin
ms.date: 10/05/2017
ms.openlocfilehash: 72b1593503db75aa275b9eb45c8342cee6724001
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280394"
---
# <a name="health-service-faults"></a>상태 서비스 오류
> 적용 대상: Windows Server 2019, Windows Server 2016

## <a name="what-are-faults"></a>오류는 무엇 인가요

상태 관리 서비스 문제를 감지 하 고 "오류"를 생성 하려면 저장소 공간 다이렉트 클러스터를 지속적으로 모니터링 합니다. 하나의 새 cmdlet을 쉽게 모든 엔터티를 조회 하지 않고 배포의 상태를 확인 하거나 기능 현재의 모든 오류가 표시 됩니다. 오류는 정확하고, 이해하기 쉽고, 조치 가능하도록 설계되었습니다.  

각 오류에는 5 개의 중요 한 필드가 포함 됩니다.  

-   Severity
-   문제에 대한 설명
-   문제 해결을 위한 권장 다음 단계
-   오류가 있는 엔터티에 대한 식별 정보
-   물리적 위치(해당되는 경우)

예를 들어 다음은 일반적인 오류입니다.  

```
Severity: MINOR                                         
Reason: Connectivity has been lost to the physical disk.                           
Recommendation: Check that the physical disk is working and properly connected.    
Part: Manufacturer Contoso, Model XYZ9000, Serial 123456789                        
Location: Seattle DC, Rack B07, Node 4, Slot 11
```

 >[!NOTE]
 > 물리적 위치는 장애 도메인 구성에서 파생됩니다. 장애 도메인에 대 한 자세한 내용은 참조 하세요. [Windows Server 2016의 장애 도메인](fault-domains.md)합니다. 이 정보를 제공하지 않으면 위치 필드가 유용하지 않습니다. 예를 들어 슬롯 번호만 표시될 수 있습니다.  

## <a name="root-cause-analysis"></a>근본 원인 분석

상태 관리 서비스 오류를 식별 하 여 오류 동일한 기본 문제의 결과 결합 하는 엔터티 간의 잠재적 인과 관계를 평가할 수 있습니다. 효과 체인을 인식하면 보고 내용이 깔끔해집니다. 예를 들어 서버가 다운 경우 서버 내에서 모든 드라이브를 연결 없이 보다 예상 됩니다. 따라서 하나의 오류만 근본 원인-이 경우 서버에 대해 발생 합니다.  

## <a name="usage-in-powershell"></a>PowerShell에서 사용

PowerShell에서 현재 오류를 보려면이 cmdlet을 실행 합니다.

```PowerShell
Get-StorageSubSystem Cluster* | Debug-StorageSubSystem  
```

이 전체 저장소 공간 다이렉트 클러스터에 영향을 주는 모든 오류를 반환 합니다. 대부분의 경우 이러한 오류 하드웨어 또는 구성과 관련이 있습니다. 오류가 없는 경우이 cmdlet은 아무 것도 반환 합니다.  

>[!NOTE]
> 비-프로덕션 환경에서 및 모든 위험은 사용자 오류를 트리거하여-예를 들어 하나의 실제 디스크를 제거 하거나 하나의 노드를 종료 하 여이 기능을 사용 하 여 실험할 수 있습니다. 오류를 표시 한 후 다시 삽입 실제 디스크를 다시 시작 노드 및 오류가 다시 사라집니다.

또한 특정 볼륨이 나 다음 cmdlet 사용 하 여 파일 공유에만 영향을 주는 오류를 볼 수 있습니다.  

```PowerShell
Get-Volume -FileSystemLabel <Label> | Debug-Volume  

Get-FileShare -Name <Name> | Debug-FileShare  
```

이 특정 볼륨이 나 파일 공유만 영향을 주는 모든 오류를 반환 합니다. 대부분의 경우 이러한 오류 용량 계획, 데이터 복원 력 또는 저장소 서비스 품질 또는 저장소 복제본과 같은 기능 관련이 있습니다. 

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

### <a name="query-faults"></a>쿼리 오류

호출 **진단** 대상 범위는 현재 오류를 가져오려면 **CimInstance**, 클러스터 또는 모든 볼륨 수입니다.

Windows Server 2016의 각 범위에 사용할 수 있는 오류 목록은 아래 설명 되어 있습니다.

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

### <a name="optional-myfault-class"></a>선택 사항: MyFault 클래스

생성 하 고 고유한 표현을 오류의 유지 적합할 수 있습니다. 이 예를 들어 **MyFault** 클래스는 오류를 비롯 한 여러 가지 주요 속성을 저장 합니다 **FaultId**, 업데이트 연결 또는 알림을 제거 하거나 중복 제거를 나중에 사용할 수 있는 이벤트에 동일한 오류는 어떤 이유로 든 여러 번 검색 됩니다.

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

각 오류에 대 한 속성의 전체 목록은 (**DiagnoseResult**) 아래 설명 되어 있습니다.

### <a name="fault-events"></a>오류 이벤트

오류 생성, 제거 또는 업데이트를 하는 경우 상태 관리 서비스는 WMI 이벤트를 생성 합니다. 이러한 폴링이 자주 수행 하지 않고 동기화 응용 프로그램 상태를 유지 하는 데 필수적 이며 예를 들어 전자 메일 경고를 보낼 시기를 결정 하는 등 도움이 될 수 있습니다. 이러한 이벤트를 구독 하려면이 샘플 코드는 관찰자 디자인 패턴을 다시 사용 합니다.

첫째, 구독할 **MSFT\_StorageFaultEvent** 이벤트입니다.

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

다음으로, 관찰자 구현입니다 **OnNext()** 메서드는 새 이벤트가 생성 될 때마다 호출 됩니다.

각 이벤트에 포함 **ChangeType** 여부 오류를 만들고 있는 중 이며, 제거 또는 업데이트와 관련 나타내는 **FaultId**합니다.

또한 오류 자체의 모든 속성을 포함 합니다.

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

### <a name="understand-fault-lifecycle"></a>오류 수명 주기 이해

"표시" 또는 사용자가 해결 된 표시할 오류를 사용 하는 것이 없습니다. Health Service가 문제를 준수 하 고 자동으로 제거 하는 경우 및 상태 관리 서비스 문제를 더 이상 확인할 수 없습니다 하는 경우에 생성 됩니다. 일반적으로 문제가 해결 되었습니다를 반영 합니다.

그러나 일부 경우에 오류 수 다시 검색할 Health Service에서 (예: 장애 조치 후 또는 간헐적 연결 등으로 인해). 따라서 쉽게 중복 제거할 수 있도록 고유한 표현을 오류를 유지 하는 것이 있도록 수 있습니다. 이 전자 메일 알림을 보내거나 해당 하는 경우에 특히 유용 합니다.

### <a name="properties-of-faults"></a>오류의 속성

이 표에서 오류 개체의 여러 가지 주요 속성을 표시합니다. 전체 스키마에 대해 검사 합니다 **MSFT\_StorageDiagnoseResult** 클래스 *storagewmi.mof*합니다.

| **속성**              | **예제**                                                     |
|---------------------------|-----------------------------------------------------------------|
| FaultId                   | {12345-12345-12345-12345-12345}                                 |
| FaultType                 | Microsoft.Health.FaultType.Volume.Capacity                      |
| Reason                    | "볼륨은 사용 가능한 공간이 부족 합니다."                 |
| PerceivedSeverity         | 5                                                               |
| FaultingObjectDescription | Contoso XYZ9000 S.N. 123456789                                  |
| FaultingObjectLocation    | 슬롯 11 A06, RU 25 랙                                        |
| RecommendedActions        | {"확장 볼륨", "다른 볼륨에 워크 로드를 마이그레이션합니다."}   |

**FaultId** 한 클러스터의 범위 내에서 고유 합니다.

**PerceivedSeverity** PerceivedSeverity = {4, 5, 6} = {"Informational", "Warning" 및 "오류"} 또는 파랑, 노랑, 빨강 등 해당 색입니다.

**FaultingObjectDescription** 부 소프트웨어 개체에 대 한 일반적으로 빈 하드웨어에 대 한 정보입니다.

**FaultingObjectLocation** 하드웨어에 대 한 위치 정보는 일반적으로 소프트웨어 개체에 대 한 비어 있습니다.

**RecommendedActions** 특정 순서 없이 독립적인 권장 되는 작업의 목록입니다. 현재이 목록 길이가 1 인 경우가 있습니다.

## <a name="properties-of-fault-events"></a>오류 이벤트의 속성

이 표에서 오류 이벤트의 여러 가지 주요 속성을 표시합니다. 전체 스키마에 대해 검사 합니다 **MSFT\_StorageFaultEvent** 클래스 *storagewmi.mof*합니다.

참고 합니다 **ChangeType**는 만들어지는지 여부를 나타냅니다 오류 되 고, 제거 또는 업데이트와 **FaultId**합니다. 또한 이벤트 오류의 영향을 받는 모든 속성을 포함 합니다.

| **속성**              | **예제**                                                     |
|---------------------------|-----------------------------------------------------------------|
| ChangeType                | 0                                                               |
| FaultId                   | {12345-12345-12345-12345-12345}                                 |
| FaultType                 | Microsoft.Health.FaultType.Volume.Capacity                      |
| Reason                    | "볼륨은 사용 가능한 공간이 부족 합니다."                 |
| PerceivedSeverity         | 5                                                               |
| FaultingObjectDescription | Contoso XYZ9000 S.N. 123456789                                  |
| FaultingObjectLocation    | 슬롯 11 A06, RU 25 랙                                        |
| RecommendedActions        | {"확장 볼륨", "다른 볼륨에 워크 로드를 마이그레이션합니다."}   |

**ChangeType** ChangeType = {0, 1, 2} = {"만들기", "제거", "업데이트"}.

## <a name="coverage"></a>적용 범위

Windows Server 2016에서 상태 관리 서비스는 다음 오류 검사를 제공합니다.  

### <a name="physicaldisk-8"></a>**PhysicalDisk (8)**

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskfailedmedia"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.FailedMedia
* 심각도: 경고
* 이유: *"실제 디스크 실패 했습니다."*
* RecommendedAction: *"실제 디스크를 교체 합니다."*

#### <a name="faulttype-microsofthealthfaulttypephysicaldisklostcommunication"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.LostCommunication
* 심각도: 경고
* 이유: *"연결 손실 된 실제 디스크에 있습니다."*
* RecommendedAction: *"실제 디스크 작동 하 고 올바르게 연결 인지 확인 합니다."*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunresponsive"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.Unresponsive
* 심각도: 경고
* 이유: *"실제 디스크 되풀이 무응답 현상이 있습니다."*
* RecommendedAction: *"실제 디스크를 교체 합니다."*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskpredictivefailure"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.PredictiveFailure
* 심각도: 경고
* 이유: *"실제 디스크의 오류는 곧 되려면 예측 됩니다."*
* RecommendedAction: *"실제 디스크를 교체 합니다."*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunsupportedhardware"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.UnsupportedHardware
* 심각도: 경고
* 이유: *"실제 디스크는 격리 솔루션 공급 업체에서 지원 되지 않으므로."*
* RecommendedAction: *"지원 되는 하드웨어를 사용 하 여 실제 디스크를 대체 합니다."*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunsupportedfirmware"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.UnsupportedFirmware
* 심각도: 경고
* 이유: *"실제 디스크 이므로 격리에 해당 펌웨어 버전이 솔루션 공급 업체에서 지원 되지 않습니다."*
* RecommendedAction: *"대상 버전에 실제 디스크에서 펌웨어를 업데이트 합니다."*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunrecognizedmetadata"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.UnrecognizedMetadata
* 심각도: 경고
* 이유: *"실제 디스크에 메타 데이터를 인식할 수 없습니다."*
* RecommendedAction: *"이이 디스크는 알 수 없는 저장소 풀에서 데이터를 포함할 수 있습니다. 먼저이 디스크에 유용한 데이터가 없는지 확인 한 다음 디스크를 다시 설정 합니다. "*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskfailedfirmwareupdate"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.FailedFirmwareUpdate
* 심각도: 경고
* 이유: *"실제 디스크에서 펌웨어를 업데이트 하려면 실패 한 시도입니다."*
* RecommendedAction: *"이진 다른 펌웨어를 사용해 보세요."*

### <a name="virtual-disk-2"></a>**가상 디스크 (2)**

#### <a name="faulttype-microsofthealthfaulttypevirtualdisksneedsrepair"></a>FaultType: Microsoft.Health.FaultType.VirtualDisks.NeedsRepair
* 심각도: 정보
* 이유: *"이이 볼륨의 일부 데이터가 완전히 복원 되지 않습니다. 합니다. 상태로 액세스할 수 있습니다. "*
* RecommendedAction: *"데이터의 복원 력을 복원합니다."*

#### <a name="faulttype-microsofthealthfaulttypevirtualdisksdetached"></a>FaultType: Microsoft.Health.FaultType.VirtualDisks.Detached
* 심각도: 심각
* 이유: *"는 볼륨에 액세스할 수 없습니다. 일부 데이터가 손실 될 수 있습니다. "*
* RecommendedAction: *"실제 확인 및/또는 네트워크의 모든 저장소 장치의 연결 합니다. 해야 백업에서 복원 해야 합니다. "*

### <a name="pool-capacity-1"></a>**풀 용량 (1)**

#### <a name="faulttype-microsofthealthfaulttypestoragepoolinsufficientreservecapacityfault"></a>FaultType: Microsoft.Health.FaultType.StoragePool.InsufficientReserveCapacityFault
* 심각도: 경고
* 이유: *"저장소 풀의 경우 최소 권장 되는 예약 용량 이 제한 될 수 있습니다 드라이브-오류 발생 시 데이터 복원 력을 복원 하는 기능입니다. "*
* RecommendedAction: *"저장소 풀에 추가 용량을 추가 하거나 용량을 확보 합니다. 최소 권장 예약, 배포에서 달라 지지만 용량의 약 2 드라이브의 분량은. "*

### <a name="volume-capacity-2sup1sup"></a>**(2) 볼륨 용량은**<sup>1</sup>

#### <a name="faulttype-microsofthealthfaulttypevolumecapacity"></a>FaultType: Microsoft.Health.FaultType.Volume.Capacity
* 심각도: 경고
* 이유: *"볼륨은 사용 가능한 공간이 부족 합니다."*
* RecommendedAction: *"볼륨을 확장 하거나 다른 볼륨에 워크 로드를 마이그레이션합니다."*

#### <a name="faulttype-microsofthealthfaulttypevolumecapacity"></a>FaultType: Microsoft.Health.FaultType.Volume.Capacity
* 심각도: 심각
* 이유: *"볼륨은 사용 가능한 공간이 부족 합니다."*
* RecommendedAction: *"볼륨을 확장 하거나 다른 볼륨에 워크 로드를 마이그레이션합니다."*

### <a name="server-3"></a>**서버 (3)**

#### <a name="faulttype-microsofthealthfaulttypeserverdown"></a>FaultType: Microsoft.Health.FaultType.Server.Down
* 심각도: 심각
* 이유: *"서버를 연결할 수 없습니다."*
* RecommendedAction: *"시작 하거나 서버를 교체 합니다."*

#### <a name="faulttype-microsofthealthfaulttypeserverisolated"></a>FaultType: Microsoft.Health.FaultType.Server.Isolated
* 심각도: 심각
* 이유: *"서버는 연결 문제로 인해 클러스터에서 격리 됩니다."*
* RecommendedAction: *"격리 지속 되 면 네트워크를 확인 하거나 다른 노드로 워크 로드를 마이그레이션합니다."*

#### <a name="faulttype-microsofthealthfaulttypeserverquarantined"></a>FaultType: Microsoft.Health.FaultType.Server.Quarantined
* 심각도: 심각
* 이유: *"서버 되풀이 오류로 인해 클러스터에서 격리 됩니다."*
* RecommendedAction: *"는 서버를 교체 하거나 네트워크를 수정 합니다."*

### <a name="cluster-1"></a>**클러스터 (1)**

#### <a name="faulttype-microsofthealthfaulttypeclusterquorumwitnesserror"></a>FaultType: Microsoft.Health.FaultType.ClusterQuorumWitness.Error
* 심각도: 심각
* 이유: *"클러스터가 다운에서 한 서버 오류."*
* RecommendedAction: *"미러링 모니터 서버 리소스를 확인 하 고 필요에 따라 다시 시작 합니다. 시작 하거나 실패 한 서버를 대체 합니다. "*

### <a name="network-adapterinterface-4"></a>**네트워크 어댑터/인터페이스 (4)**

#### <a name="faulttype-microsofthealthfaulttypenetworkadapterdisconnected"></a>FaultType: Microsoft.Health.FaultType.NetworkAdapter.Disconnected
* 심각도: 경고
* 이유: *"네트워크 인터페이스가 연결 되어 있지."*
* RecommendedAction: *"네트워크 케이블 다시 연결 합니다."*

#### <a name="faulttype-microsofthealthfaulttypenetworkinterfacemissing"></a>FaultType: Microsoft.Health.FaultType.NetworkInterface.Missing
* 심각도: 경고
* 이유: *"{Server} 누락 된 네트워크 어댑터 {0} 클러스터 네트워크가} 클러스터 네트워크에 연결 합니다."*
* RecommendedAction: *"누락 된 클러스터 네트워크에 서버를 연결 합니다."*

#### <a name="faulttype-microsofthealthfaulttypenetworkadapterhardware"></a>FaultType: Microsoft.Health.FaultType.NetworkAdapter.Hardware
* 심각도: 경고
* 이유: *"네트워크 인터페이스는 하드웨어 오류가 발생을 했습니다."*
* RecommendedAction: *"네트워크 인터페이스 어댑터를 대체 합니다."*

#### <a name="faulttype-microsofthealthfaulttypenetworkadapterdisabled"></a>FaultType: Microsoft.Health.FaultType.NetworkAdapter.Disabled
* 심각도: 경고
* 이유: *"네트워크 인터페이스 {0} 네트워크 인터페이스 (를) 사용할 수 없습니다 및 사용 되지 않습니다."*
* RecommendedAction: *"네트워크 인터페이스를 사용 합니다."*

### <a name="enclosure-6"></a>**인클로저 (6)**

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurelostcommunication"></a>FaultType: Microsoft.Health.FaultType.StorageEnclosure.LostCommunication
* 심각도: 경고
* 이유: *"통신 손실 된 저장소 엔클로저를."*
* RecommendedAction: *"시작 하거나 저장소 엔클로저를 바꿉니다."*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurefanerror"></a>FaultType: Microsoft.Health.FaultType.StorageEnclosure.FanError
* 심각도: 경고
* 이유: *"저장소 엔클로저의의 {0} 위치} 위치의 팬 실패 했습니다."*
* RecommendedAction: *"저장소 엔클로저에서 팬을 대체 합니다."*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurecurrentsensorerror"></a>FaultType: Microsoft.Health.FaultType.StorageEnclosure.CurrentSensorError
* 심각도: 경고
* 이유: *"위치의 {위치} 저장소 엔클로저 전류 센서 실패 했습니다."*
* RecommendedAction: *"저장소 엔클로저에서 전류 센서를 대체 합니다."*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurevoltagesensorerror"></a>FaultType: Microsoft.Health.FaultType.StorageEnclosure.VoltageSensorError
* 심각도: 경고
* 이유: *"저장소 엔클로저의의 {0} 위치} 위치의 전압 센서 실패 했습니다."*
* RecommendedAction: *"저장소 엔클로저의 전압 센서를 대체 합니다."*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosureiocontrollererror"></a>FaultType: Microsoft.Health.FaultType.StorageEnclosure.IoControllerError
* 심각도: 경고
* 이유: *"저장소 엔클로저의의 {0} 위치} 위치의 IO 컨트롤러 실패 했습니다."*
* RecommendedAction: *"저장소 엔클로저의 IO 컨트롤러 교체 합니다."*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosuretemperaturesensorerror"></a>FaultType: Microsoft.Health.FaultType.StorageEnclosure.TemperatureSensorError
* 심각도: 경고
* 이유: *"저장소 엔클로저의의 {0} 위치} 위치의 온도 센서 실패 했습니다."*
* RecommendedAction: *"저장소 엔클로저의의 온도 센서를 대체 합니다."*

### <a name="firmware-rollout-3"></a>**펌웨어 롤아웃을 (3)**

#### <a name="faulttype-microsofthealthfaulttypefaultdomainfailedmaintenancemode"></a>FaultType: Microsoft.Health.FaultType.FaultDomain.FailedMaintenanceMode
* 심각도: 경고
* 이유: *"현재 못했습니다 펌웨어 출시를 수행 하는 동안 진행률을 확인 합니다."*
* RecommendedAction: *"모든 저장소 공간 정상이 고 장애 도메인이 없습니다. 현재 유지 관리 모드 인지 확인 합니다."*

#### <a name="faulttype-microsofthealthfaulttypefaultdomainfirmwareverifyversionfaile"></a>FaultType: Microsoft.Health.FaultType.FaultDomain.FirmwareVerifyVersionFaile
* 심각도: 경고
* 이유: *"펌웨어 롤아웃은 펌웨어 업데이트를 적용 한 후 읽을 수 없거나 예기치 않은 펌웨어 버전 정보로 인해 취소 되었습니다."*
* RecommendedAction: *"다시 시작 펌웨어 롤아웃 면 펌웨어 문제가 해결 되었습니다."*

#### <a name="faulttype-microsofthealthfaulttypefaultdomaintoomanyfailedupdates"></a>FaultType: Microsoft.Health.FaultType.FaultDomain.TooManyFailedUpdates
* 심각도: 경고
* 이유: *"펌웨어 롤아웃은 펌웨어 업데이트 시도 실패 한 실제 디스크가 너무 많으면 인해 취소 되었습니다."*
* RecommendedAction: *"다시 시작 펌웨어 롤아웃 면 펌웨어 문제가 해결 되었습니다."*

### <a name="storage-qos-3sup2sup"></a>**저장소 QoS (3)** <sup>2</sup>

#### <a name="faulttype-microsofthealthfaulttypestorqosinsufficientthroughput"></a>FaultType: Microsoft.Health.FaultType.StorQos.InsufficientThroughput
* 심각도: 경고
* 이유: *"저장소 처리량 예약을 충족 하기 위해 충분 하지 않습니다."*
* RecommendedAction: *"저장소 QoS 정책을 다시 구성 합니다."*

#### <a name="faulttype-microsofthealthfaulttypestorqoslostcommunication"></a>FaultType: Microsoft.Health.FaultType.StorQos.LostCommunication
* 심각도: 경고
* 이유: *"저장소 QoS 정책 관리자는 볼륨을 사용 하 여 통신 손실 되었습니다."*
* RecommendedAction: *"{노드} 노드를 다시 부팅 하세요"*

#### <a name="faulttype-microsofthealthfaulttypestorqosmisconfiguredflow"></a>FaultType: Microsoft.Health.FaultType.StorQos.MisconfiguredFlow
* 심각도: 경고
* 이유: *"하나 이상의 저장소 소비자 (일반적으로 가상 머신) 사용 하는 존재 하지 않는 정책 id가 {id}를 사용 하 여."*
* RecommendedAction: *"누락 된 모든 저장소 QoS 정책을 다시 만드십시오."*

<sup>1</sup> 나타냅니다 80% (경미한 심각도) 또는 90% (중대 한 심각도) 볼륨에 도달 했습니다.  
<sup>2</sup> 볼륨에서 일부 경미 최소 IOPS를 충족 되지 않았음을 나타냅니다에 대해 10% (보조), 30% (중대) 또는 50% (심각) 24 시간 창입니다.  

>[!NOTE]
> 팬, 전원 공급 장치 및 센서와 같은 저장소 엔클로저 구성 요소의 상태는 SCSI(SCSI Enclosure Services)에서 파생됩니다. 공급업체에서 이 정보를 제공하지 않은 경우 상태 관리 서비스에서 정보를 표시할 수 없습니다.  

## <a name="see-also"></a>참조

- [Windows Server 2016의에서 상태 관리 서비스](health-service-overview.md)
