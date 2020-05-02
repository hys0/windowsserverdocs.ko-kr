---
title: 상태 관리 서비스 오류
ms.prod: windows-server
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
author: cosmosdarwin
ms.date: 10/05/2017
ms.openlocfilehash: 5fe2f98c89d97325c1f59dc6ba292831e0ffa5ff
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720559"
---
# <a name="health-service-faults"></a>상태 관리 서비스 오류

> 적용 대상: Windows Server 2019, Windows Server 2016

## <a name="what-are-faults"></a>오류 란?

상태 관리 서비스은 스토리지 공간 다이렉트 클러스터를 지속적으로 모니터링 하 여 문제를 감지 하 고 "오류"를 생성 합니다. 새 cmdlet 중 하나는 모든 현재 오류를 표시 하므로 모든 엔터티 또는 기능을 차례로 확인 하지 않고도 배포 상태를 쉽게 확인할 수 있습니다. 오류는 정확하고, 이해하기 쉽고, 조치 가능하도록 설계되었습니다.  

각 오류에는 5 개의 중요 한 필드가 포함 됩니다.  

-   심각도
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
 > 물리적 위치는 장애 도메인 구성에서 파생됩니다. 장애 도메인에 대 한 자세한 내용은 [Windows Server 2016의 장애 도메인](fault-domains.md)을 참조 하세요. 이 정보를 제공하지 않으면 위치 필드가 유용하지 않습니다. 예를 들어 슬롯 번호만 표시될 수 있습니다.  

## <a name="root-cause-analysis"></a>근본 원인 분석

상태 관리 서비스는 오류가 발생 한 엔터티 간의 잠재적 인과 관계을 평가 하 여 동일한 기본 문제로 인해 발생 하는 오류를 식별 하 고 결합할 수 있습니다. 효과 체인을 인식하면 보고 내용이 깔끔해집니다. 예를 들어 서버가 다운 된 경우 서버 내의 드라이브가 연결 되지 않은 상태 여야 합니다. 따라서 근본 원인 (이 경우에는 서버)에 대해 하나의 오류가 발생 합니다.  

## <a name="usage-in-powershell"></a>PowerShell에서 사용

PowerShell에서 현재 오류를 확인 하려면 다음 cmdlet을 실행 합니다.

```PowerShell
Get-StorageSubSystem Cluster* | Debug-StorageSubSystem  
```

그러면 전체 스토리지 공간 다이렉트 클러스터에 영향을 주는 오류가 반환 됩니다. 대체로 이러한 오류는 하드웨어 또는 구성과 관련이 있습니다. 오류가 없는 경우이 cmdlet은 아무 것도 반환 하지 않습니다.  

>[!NOTE]
> 프로덕션 환경이 아닌 환경에서 사용자의 책임에 따라 오류를 직접 트리거할 수 있습니다. 예를 들어 하나의 실제 디스크를 제거 하거나 한 노드를 종료 하 여이 기능을 시험해 볼 수 있습니다. 오류가 표시 되 면 실제 디스크를 다시 삽입 하거나 노드를 다시 시작 하면 오류가 다시 사라집니다.

다음 cmdlet을 사용 하 여 특정 볼륨 또는 파일 공유에만 영향을 주는 오류를 볼 수도 있습니다.  

```PowerShell
Get-Volume -FileSystemLabel <Label> | Debug-Volume  

Get-FileShare -Name <Name> | Debug-FileShare  
```

이렇게 하면 특정 볼륨 또는 파일 공유에만 영향을 주는 오류가 반환 됩니다. 대부분의 경우 이러한 오류는 용량 계획, 데이터 복원 력 또는 Storage 서비스 품질 또는 저장소 복제본과 같은 기능과 관련이 있습니다. 

## <a name="usage-in-net-and-c"></a>.NET 및 C에서 사용 #

### <a name="connect"></a>연결

상태 관리 서비스를 쿼리하려면 클러스터로 **CimSession** 를 설정 해야 합니다. 이렇게 하려면 전체 .NET 에서만 사용할 수 있는 몇 가지 항목이 필요 합니다. 즉, 웹 또는 모바일 앱에서 바로이 작업을 수행할 수 없습니다. 이러한 코드 샘플은이 데이터\#액세스 계층에 가장 간단한 선택 인 C를 사용 합니다.

```
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

오류나 메트릭을 얻기 전에 여러 관련 개체의 인스턴스를 가져와야 합니다. 먼저 클러스터에서 스토리지 공간 다이렉트를 나타내는 **MSFT\_storagesubsystem** 입니다. 이를 사용 하 여 클러스터의 **모든\_msft StorageNode** 및 모든 **msft\_볼륨**, 데이터 볼륨을 가져올 수 있습니다. 마지막으로, 상태 관리 서비스 **\_MSFT storagehealth**가 필요 합니다.

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
using System.Diagnostics;

foreach (CimInstance Node in Nodes)
{
    // For illustration, write each node's Name to the console. You could also write State (up/down), or anything else!
    Debug.WriteLine("Discovered Node " + Node.CimInstanceProperties["Name"].Value.ToString());
}
```

### <a name="query-faults"></a>쿼리 오류

**진단** 을 호출 하 여 대상 **ciminstance 개체로**범위가 지정 된 클러스터 또는 임의 볼륨으로 현재 오류를 가져옵니다.

Windows Server 2016의 각 범위에서 사용할 수 있는 오류의 전체 목록은 아래에 설명 되어 있습니다.

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

고유한 오류 표현을 생성 하 고 유지 하는 것이 적합할 수 있습니다. 예를 들어이 **Myfault** 클래스는 나중에 업데이트 또는 제거 알림을 연결 하는 데 사용할 수 있는 **FaultId**를 비롯 하 여 오류에 대 한 몇 가지 주요 속성을 저장 하거나, 어떤 이유로 든 동일한 오류가 여러 번 감지 되는 경우 중복을 제거 합니다.

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

각 오류의 전체 속성 목록 (**DiagnoseResult**)은 아래에 설명 되어 있습니다.

### <a name="fault-events"></a>오류 이벤트

오류가 생성, 제거 또는 업데이트 되 면 상태 관리 서비스에서 WMI 이벤트를 생성 합니다. 이는 자주 폴링하는 대신 응용 프로그램 상태를 동기화 상태로 유지 하는 데 필수적 이며, 예를 들어 전자 메일 경고를 보낼 시기를 결정 하는 등의 작업에 도움이 될 수 있습니다. 이러한 이벤트를 구독 하기 위해이 샘플 코드는 관찰자 디자인 패턴을 다시 사용 합니다.

먼저 **MSFT\_storagefaultevent** 이벤트를 구독 합니다.

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

다음으로, 새 이벤트가 생성 될 때마다 **Onnext ()** 메서드가 호출 되는 관찰자를 구현 합니다.

각 이벤트에는 오류를 생성, 제거 또는 업데이트 하 고 있는지 여부와 관련 **FaultId**을 나타내는 잘못 된 **내용이 포함 되어** 있습니다.

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

오류는 "확인 됨"으로 표시 되거나 사용자가 해결할 수 없습니다. 상태 관리 서비스는 문제를 관찰할 때 생성 되며, 상태 관리 서비스에서 문제를 더 이상 관찰할 수 없을 때만 자동으로 제거 됩니다. 일반적으로이 문제는 문제가 해결 되었음을 나타냅니다.

그러나 일부 경우에 상태 관리 서비스는 오류 (예: 장애 조치 (failover) 후 또는 일시적인 연결 등) 시 수 있습니다. 따라서 고유한 오류 표현을 유지 하는 것이 좋을 수 있으므로 쉽게 복제할 수 있습니다. 전자 메일 경고 또는 이와 동등한 것을 보내는 경우에 특히 중요 합니다.

### <a name="properties-of-faults"></a>오류의 속성

이 표에서는 오류 개체의 몇 가지 주요 속성을 보여 줍니다. 전체 스키마의 경우 *storagewmi .mof*에서 **\_MSFT StorageDiagnoseResult** 클래스를 검사 합니다.

| **속성**              | **예제**                                                     |
|---------------------------|-----------------------------------------------------------------|
| FaultId                   | {12345-12345-12345-12345-12345}                                 |
| FaultType                 | Microsoft Health..                      |
| 이유                    | "볼륨에 사용 가능한 공간이 부족 합니다."                 |
| PerceivedSeverity         | 5                                                               |
| FaultingObjectDescription | Contoso XYZ9000 S.N. 123456789                                  |
| FaultingObjectLocation    | 랙 A06, 매우 25, 슬롯 11                                        |
| RecommendedActions        | {"볼륨을 확장 합니다.", "다른 볼륨으로 워크 로드 마이그레이션"}   |

**FaultId** 한 클러스터의 범위 내에서 고유 합니다.

**PerceivedSeverity** PerceivedSeverity = {4, 5, 6} = {"정보", "경고" 및 "오류"} 또는 파랑, 노랑, 빨강 등의 동일한 색입니다.

**FaultingObjectDescription** 하드웨어에 대 한 파트 정보 이며 일반적으로 소프트웨어 개체의 경우 비어 있습니다.

**FaultingObjectLocation** 하드웨어에 대 한 위치 정보 이며 일반적으로 소프트웨어 개체의 경우 비어 있습니다.

**RecommendedActions** 특정 순서에 관계 없이 독립적인 권장 작업 목록입니다. 현재이 목록은 보통 길이가 1입니다.

## <a name="properties-of-fault-events"></a>오류 이벤트의 속성

이 표에서는 오류 이벤트의 몇 가지 주요 속성을 보여 줍니다. 전체 스키마의 경우 *storagewmi .mof*에서 **\_MSFT storagefaultevent** 클래스를 검사 합니다.

오류를 생성, 제거 또는 업데이트 하 고 있는지 여부를 나타내는 **FaultId** **를 확인**합니다. 이벤트에는 영향을 받는 오류의 모든 속성도 포함 됩니다.

| **속성**              | **예제**                                                     |
|---------------------------|-----------------------------------------------------------------|
| ChangeType                | 0                                                               |
| FaultId                   | {12345-12345-12345-12345-12345}                                 |
| FaultType                 | Microsoft Health..                      |
| 이유                    | "볼륨에 사용 가능한 공간이 부족 합니다."                 |
| PerceivedSeverity         | 5                                                               |
| FaultingObjectDescription | Contoso XYZ9000 S.N. 123456789                                  |
| FaultingObjectLocation    | 랙 A06, 매우 25, 슬롯 11                                        |
| RecommendedActions        | {"볼륨을 확장 합니다.", "다른 볼륨으로 워크 로드 마이그레이션"}   |

**ChangeType** 고가 고가 = {0, 1, 2} = {"Create", "Remove", "Update"}.

## <a name="coverage"></a>적용 범위

Windows Server 2016에서 상태 관리 서비스는 다음과 같은 오류 검사를 제공 합니다.  

### <a name="physicaldisk-8"></a>**PhysicalDisk (8)**

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskfailedmedia"></a>FaultType: PhysicalDisk 미디어입니다.
* 심각도: 경고
* 이유: *"실제 디스크에 오류가 발생 했습니다."*
* RecommendedAction: *"실제 디스크를 바꿉니다."*

#### <a name="faulttype-microsofthealthfaulttypephysicaldisklostcommunication"></a>FaultType: PhysicalDisk. LostCommunication
* 심각도: 경고
* 이유: *"실제 디스크에 대 한 연결이 끊겼습니다."*
* RecommendedAction: *"실제 디스크가 작동 하 고 올바르게 연결 되었는지 확인 합니다."*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunresponsive"></a>FaultType: PhysicalDisk. 응답 없음
* 심각도: 경고
* 이유: *"실제 디스크에 되풀이 응답 하지 않습니다."*
* RecommendedAction: *"실제 디스크를 바꿉니다."*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskpredictivefailure"></a>FaultType: PhysicalDisk. PredictiveFailure
* 심각도: 경고
* 이유: *"실제 디스크의 실패가 곧 발생 합니다."*
* RecommendedAction: *"실제 디스크를 바꿉니다."*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunsupportedhardware"></a>FaultType: PhysicalDisk. UnsupportedHardware
* 심각도: 경고
* 이유: *"실제 디스크가 솔루션 공급 업체에서 지원 되지 않기 때문에 격리 되어 있습니다."*
* RecommendedAction: *"실제 디스크를 지원 되는 하드웨어로 바꿉니다."*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunsupportedfirmware"></a>FaultType: PhysicalDisk. UnsupportedFirmware
* 심각도: 경고
* 이유: *"실제 디스크가 격리 되어 있습니다. 해당 펌웨어 버전이 솔루션 공급 업체에서 지원 되지 않기 때문입니다."*
* RecommendedAction: *"실제 디스크의 펌웨어를 대상 버전으로 업데이트 합니다."*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunrecognizedmetadata"></a>FaultType: PhysicalDisk. UnrecognizedMetadata
* 심각도: 경고
* 이유: *"실제 디스크에 인식할 수 없습니다 메타 데이터가 있습니다."*
* RecommendedAction: *"이 디스크에는 알 수 없는 저장소 풀의 데이터가 포함 될 수 있습니다. 먼저이 디스크에 유용한 데이터가 없는지 확인 한 다음 디스크를 다시 설정 하십시오. "*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskfailedfirmwareupdate"></a>FaultType: PhysicalDisk. FailedFirmwareUpdate
* 심각도: 경고
* 이유: *"실제 디스크에서 펌웨어를 업데이트 하지 못했습니다."*
* RecommendedAction: *"다른 펌웨어 이진을 사용해 보세요."*

### <a name="virtual-disk-2"></a>**가상 디스크 (2)**

#### <a name="faulttype-microsofthealthfaulttypevirtualdisksneedsrepair"></a>FaultType: NeedsRepair을 입력 합니다.
* 심각도: 알림
* 이유: *"이 볼륨의 일부 데이터가 완전히 복원 되지 않습니다. 계속 해 서 액세스할 수 있습니다. "*
* RecommendedAction: *"데이터 복원 력을 복원 합니다."*

#### <a name="faulttype-microsofthealthfaulttypevirtualdisksdetached"></a>FaultType: Microsoft...
* 심각도: 위험
* 이유: *"볼륨에 액세스할 수 없습니다. 일부 데이터가 손실 될 수 있습니다. "*
* RecommendedAction: *"모든 저장 장치의 물리적 및/또는 네트워크 연결을 확인 합니다. 백업에서 복원 해야 할 수 있습니다. "*

### <a name="pool-capacity-1"></a>**풀 용량 (1)**

#### <a name="faulttype-microsofthealthfaulttypestoragepoolinsufficientreservecapacityfault"></a>FaultType: InsufficientReserveCapacityFault를 입력 합니다.
* 심각도: 경고
* 이유: *"저장소 풀에 권장 되는 최소 예약 용량이 없습니다. 이로 인해 드라이브 오류가 발생할 경우 데이터 복원 력을 복원 하는 기능이 제한 될 수 있습니다. "*
* RecommendedAction: *"저장소 풀에 용량을 더 추가 하거나 용량을 확보 합니다. 권장 되는 최소 예약은 배포에 따라 다르지만 약 2 개 드라이브의 용량입니다. "*

### <a name="volume-capacity-2sup1sup"></a>**볼륨 용량 (2)**<sup>1</sup>

#### <a name="faulttype-microsofthealthfaulttypevolumecapacity"></a>FaultType: Microsoft Health.
* 심각도: 경고
* 이유: *"볼륨에 사용 가능한 공간이 부족 합니다."*
* RecommendedAction: *"볼륨을 확장 하거나 작업을 다른 볼륨으로 마이그레이션"*

#### <a name="faulttype-microsofthealthfaulttypevolumecapacity"></a>FaultType: Microsoft Health.
* 심각도: 위험
* 이유: *"볼륨에 사용 가능한 공간이 부족 합니다."*
* RecommendedAction: *"볼륨을 확장 하거나 작업을 다른 볼륨으로 마이그레이션"*

### <a name="server-3"></a>**서버 (3)**

#### <a name="faulttype-microsofthealthfaulttypeserverdown"></a>FaultType: Microsoft...
* 심각도: 위험
* 이유: *"서버에 연결할 수 없습니다."*
* RecommendedAction: *"서버 시작 또는 바꾸기"*

#### <a name="faulttype-microsofthealthfaulttypeserverisolated"></a>FaultType: Microsoft...
* 심각도: 위험
* 이유: *"연결 문제로 인해 서버가 클러스터에서 격리 되었습니다."*
* RecommendedAction: *"격리가 지속 되 면 네트워크를 확인 하거나 다른 노드로 워크 로드를 마이그레이션합니다."*

#### <a name="faulttype-microsofthealthfaulttypeserverquarantined"></a>FaultType: Microsoft...
* 심각도: 위험
* 이유: *"반복 되는 오류가 발생 하 여 서버가 클러스터에 의해 격리 됩니다."*
* RecommendedAction: *"서버를 교체 하거나 네트워크를 수정 합니다."*

### <a name="cluster-1"></a>**클러스터 (1)**

#### <a name="faulttype-microsofthealthfaulttypeclusterquorumwitnesserror"></a>FaultType: ClusterQuorumWitness. 오류
* 심각도: 위험
* 이유: *"클러스터의 작동이 중단 되지 않습니다."*
* RecommendedAction: *"미러링 모니터 리소스를 확인 하 고 필요에 따라 다시 시작 합니다. 실패 한 서버를 시작 하거나 바꿉니다. "*

### <a name="network-adapterinterface-4"></a>**네트워크 어댑터/인터페이스 (4)**

#### <a name="faulttype-microsofthealthfaulttypenetworkadapterdisconnected"></a>FaultType: 네트워크 어댑터. 연결 끊김
* 심각도: 경고
* 이유: *"네트워크 인터페이스의 연결을 끊었습니다."*
* RecommendedAction: *"네트워크 케이블을 다시 연결 합니다."*

#### <a name="faulttype-microsofthealthfaulttypenetworkinterfacemissing"></a>FaultType: NetworkInterface. 누락
* 심각도: 경고
* 원인: *"서버 {server}에 클러스터 네트워크 {cluster network}에 연결 된 네트워크 어댑터가 없습니다."*
* RecommendedAction: *"누락 된 클러스터 네트워크에 서버를 연결 합니다."*

#### <a name="faulttype-microsofthealthfaulttypenetworkadapterhardware"></a>FaultType: 네트워크 어댑터. 하드웨어
* 심각도: 경고
* 이유: *"네트워크 인터페이스에 하드웨어 오류가 발생 했습니다."*
* RecommendedAction: *"네트워크 인터페이스 어댑터를 바꿉니다."*

#### <a name="faulttype-microsofthealthfaulttypenetworkadapterdisabled"></a>FaultType: 네트워크 어댑터. 사용 안 함
* 심각도: 경고
* 이유: *"네트워크 인터페이스 {network interface}은 (는) 사용 하도록 설정 되어 있지 않으며 사용 중이 아닙니다."*
* RecommendedAction: *"네트워크 인터페이스를 사용 하도록 설정 합니다."*

### <a name="enclosure-6"></a>**인클로저 (6)**

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurelostcommunication"></a>FaultType: LostCommunication을 입력 합니다.
* 심각도: 경고
* 이유: *"저장소 엔클로저에 대 한 통신이 끊어졌습니다."*
* RecommendedAction: *"저장소 엔클로저를 시작 하거나 바꿉니다."*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurefanerror"></a>FaultType: FanError을 입력 합니다.
* 심각도: 경고
* 이유: *"저장소 엔클로저의 {position} 위치에 있는 팬이 실패 했습니다."*
* RecommendedAction: *"저장소 엔클로저의 팬을 교체 합니다."*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurecurrentsensorerror"></a>FaultType: CurrentSensorError을 입력 합니다.
* 심각도: 경고
* 이유: *"저장소 엔클로저의 {position} 위치에서 현재 센서가 실패 했습니다."*
* RecommendedAction: *"저장소 엔클로저의 현재 센서를 바꿉니다."*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurevoltagesensorerror"></a>FaultType: VoltageSensorError을 입력 합니다.
* 심각도: 경고
* 이유: *"저장소 엔클로저의 {position} 위치에 있는 전압 센서가 실패 했습니다."*
* RecommendedAction: *"저장소 엔클로저의 전압 센서를 바꿉니다."*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosureiocontrollererror"></a>FaultType:. StorageEnclosure. IoControllerError
* 심각도: 경고
* 이유: *"저장소 엔클로저의 {position} 위치에 있는 IO 컨트롤러에 오류가 발생 했습니다."*
* RecommendedAction: *"저장소 엔클로저의 IO 컨트롤러를 바꿉니다."*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosuretemperaturesensorerror"></a>FaultType: TemperatureSensorError을 입력 합니다.
* 심각도: 경고
* 이유: *"저장소 엔클로저 {position}의 온도 센서가 실패 했습니다."*
* RecommendedAction: *"저장소 엔클로저의 온도 센서를 바꿉니다."*

### <a name="firmware-rollout-3"></a>**펌웨어 출시 (3)**

#### <a name="faulttype-microsofthealthfaulttypefaultdomainfailedmaintenancemode"></a>FaultType: FailedMaintenanceMode을 입력 합니다.
* 심각도: 경고
* 이유: *"펌웨어 출시를 수행 하는 동안 현재 진행을 수행할 수 없습니다."*
* RecommendedAction: *"모든 저장소 공간이 정상 이며 장애 도메인이 현재 유지 관리 모드에 있지 않은지 확인 합니다."*

#### <a name="faulttype-microsofthealthfaulttypefaultdomainfirmwareverifyversionfaile"></a>FaultType: FirmwareVerifyVersionFaile을 입력 합니다.
* 심각도: 경고
* 이유: *"펌웨어 업데이트를 적용 한 후에는 읽을 수 없거나 예기치 않은 펌웨어 버전 정보로 인해 펌웨어 롤아웃이 취소 되었습니다."*
* RecommendedAction: *"펌웨어 문제가 해결 되 면 펌웨어 출시를 다시 시작 합니다."*

#### <a name="faulttype-microsofthealthfaulttypefaultdomaintoomanyfailedupdates"></a>FaultType: TooManyFailedUpdates을 입력 합니다.
* 심각도: 경고
* 원인: *"펌웨어 업데이트 시도에 실패 한 실제 디스크 수가 너무 많아 펌웨어 롤아웃이 취소 되었습니다."*
* RecommendedAction: *"펌웨어 문제가 해결 되 면 펌웨어 출시를 다시 시작 합니다."*

### <a name="storage-qos-3sup2sup"></a>**저장소 QoS (3)**<sup>2</sup>

#### <a name="faulttype-microsofthealthfaulttypestorqosinsufficientthroughput"></a>FaultType: InsufficientThroughput을 입력 합니다.
* 심각도: 경고
* 이유: *"저장소 처리량이 부족 하 여 예약을 충족할 수 없습니다."*
* RecommendedAction: *"저장소 QoS 정책 다시 구성"*

#### <a name="faulttype-microsofthealthfaulttypestorqoslostcommunication"></a>FaultType: LostCommunication을 입력 합니다.
* 심각도: 경고
* 이유: *"저장소 QoS 정책 관리자에서 볼륨과의 통신이 끊겼습니다."*
* RecommendedAction: *"노드 {nodes}"을 (를) 다시 부팅 하세요* .

#### <a name="faulttype-microsofthealthfaulttypestorqosmisconfiguredflow"></a>FaultType: MisconfiguredFlow을 입력 합니다.
* 심각도: 경고
* 이유: *"하나 이상의 저장소 소비자 (일반적으로 Virtual Machines)에서 id가 {id} 인 존재 하지 않는 정책을 사용 하 고 있습니다."*
* RecommendedAction: *"누락 된 저장소 QoS 정책을 다시 만듭니다."*

<sup>1</sup> 은 볼륨이 80% 전체 (사소한 심각도) 또는 90% full (주요 심각도)에 도달 했음을 나타냅니다.  
<sup>2</sup> 는 일부의 볼륨이 10% (부), 30% (주) 또는 50% (위험), 24 시간 기간의 최소 IOPS를 충족 하지 못했음을 나타냅니다.  

>[!NOTE]
> 팬, 전원 공급 장치 및 센서와 같은 스토리지 엔클로저 구성 요소의 상태는 SCSI(SCSI Enclosure Services)에서 파생됩니다. 공급업체에서 이 정보를 제공하지 않은 경우 상태 관리 서비스에서 정보를 표시할 수 없습니다.  

## <a name="see-also"></a>참고 항목

- [Windows Server 2016의 상태 관리 서비스](health-service-overview.md)
