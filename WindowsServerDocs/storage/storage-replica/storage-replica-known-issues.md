---
title: "저장소 복제본의 알려진 문제"
ms.prod: windows-server-threshold
manager: siroy
ms.author: nedpyle
ms.technology: storage-replica
ms.topic: get-started-article
author: nedpyle
ms.date: 10/13/2016
ms.assetid: ceddb0fa-e800-42b6-b4c6-c06eb1d4bc55
ms.openlocfilehash: 6f02ece1f327cf53667df09e6d13ace001259885
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="known-issues-with-storage-replica"></a>저장소 복제본의 알려진 문제

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 섹션에서는 Windows Server 2016의 저장소 복제본에 대한 알려진 문제를 설명합니다.  

## <a name="after-removing-replication-disks-are-offline-and-you-cannot-configure-replication-again"></a>복제를 제거한 후 디스크가 오프라인 상태가 되어 복제를 다시 구성할 수 없음  
Windows Server 2016에서 이전에 복제한 볼륨에서 복제를 프로비전할 수 없거나, 탑재할 수 없는 볼륨을 찾을 수 없습니다. 이는 일부 오류 조건이 복제 제거를 방지하는 경우 또는 이전에 데이터를 복제한 컴퓨터에 운영 체제를 다시 설치한 경우에 발생할 수 있습니다.  

이 문제를 해결하려면 `Clear-SRMetadata` cmdlet을 사용하여 디스크에서 숨겨진 저장소 복제본 파티션을 지우고 쓰기 가능한 상태로 되돌려야 합니다.  

-   분리된 모든 저장소 복제본 파티션 데이터베이스 슬롯을 제거하고 모든 파티션을 다시 탑재하려면 다음과 같이 `-AllPartitions` 매개 변수를 사용합니다.  

    ```  
    Clear-SRMetadata -AllPartitions  
    ```  

-   분리된 모든 저장소 복제본 로그 데이터를 제거하려면 다음과 같이 `-AllLogs` 매개 변수를 사용합니다.  

    ```  
    Clear-SRMetadata -AllLogs  
    ```  

-   분리된 모든 장애 조치(failover) 클러스터 구성 데이터를 제거하려면 다음과 같이 `-AllConfiguration` 매개 변수를 사용합니다.  

    ```  
    Clear-SRMetadata -AllConfiguration  
    ```  

-   개별 복제 그룹 메타데이터를 제거하려면 다음과 같이 `-Name` 매개 변수를 사용하고 복제 그룹을 지정합니다.  

    ```  
    Clear-SRMetadata -Name RG01 -Logs -Partition  
    ```  

파티션 데이터베이스를 지운 후 서버를 다시 시작해야 할 수 있습니다. `-NoRestart`를 사용하여 이를 일시적으로 억제할 수 있지만 cmdlet에서 요청한 경우 서버 다시 시작을 건너뛰어서는 안 됩니다. 이 cmdlet은 데이터 볼륨과 해당 볼륨에 포함된 데이터를 제거하지 않습니다.  

## <a name="during-initial-sync-see-event-log-4004-warnings"></a>초기 동기화 중에 이벤트 로그 4004 경고가 표시됨  
Windows Server 2016에서 복제를 구성할 때 원본 및 대상 서버 모두에서 초기 동기화 중에 "API를 완료하기 위한 시스템 리소스가 부족합니다." 상태의 여러 **StorageReplica\Admin** 이벤트 로그 4004 경고가 표시될 수 있습니다. 5014 오류도 표시될 수 있습니다. 이는 서버에 사용 가능한 메모리(RAM)가 부족하여 초기 동기화 및 워크로드를 실행할 수 없음을 나타냅니다. RAM을 추가하거나, 저장소 복제본 이외의 기능 및 응용 프로그램에서 사용되는 RAM을 줄입니다.  

## <a name="when-using-guest-clusters-with-shared-vhdx-and-a-host-without-a-csv-virtual-machines-stop-responding-after-configuring-replication"></a>공유 VHDX가 있는 게스트 클러스터와 CSV가 없는 호스트를 사용하는 경우 복제를 구성한 후 가상 컴퓨터의 응답이 중지됨  
Windows Server 2016에서 저장소 복제본 테스트 또는 데모용으로 Hyper-V 게스트 클러스터를 사용하고 공유 VHDX를 게스트 클러스터 저장소로 사용하는 경우 복제를 구성한 후 가상 컴퓨터의 응답이 중지됩니다. Hyper-V 호스트를 다시 시작하면 가상 컴퓨터가 응답하기 시작하지만 복제 구성이 완료되지 않고 복제가 발생하지 않습니다.  

이 동작은 CSV를 실행하는 Hyper-V 호스트에 대한 요구 사항을 무시하기 위해 **fltmc.exe attach svhdxflt**를 사용할 때 발생합니다. 이 명령의 사용은 지원되지 않으며 테스트 및 데모용으로만 제공됩니다.  

속도 저하의 원인은 Windows Server 2016의 저장소 QoS 기능과 수동으로 연결된 공유 VHDX 필터 간의 설계에 따른 상호 운용성 문제입니다. 이 문제를 해결하려면 저장소 QoS 필터 드라이버를 사용하지 않도록 설정하고 Hyper-V 호스트를 다시 시작합니다.  

```  
SC config storqosflt start= disabled  
```  

## <a name="cannot-configure-replication-when-using-new-volume-and-differing-storage"></a>New-Volume 및 서로 다른 저장소를 사용하는 경우 복제를 구성할 수 없음  
원본 및 대상 서버에서 서로 다른 저장소 집합(예: 두 개의 SAN 또는 디스크가 서로 다른 두 개의 JBOD)과 함께 `New-Volume` cmdlet을 사용하는 경우 이후에 `New-SRPartnership`을 사용하여 복제를 구성할 수 없습니다. 다음과 같은 오류가 표시될 수 있습니다.  

    Data partition sizes are different in those two groups  

대신 `New-Partition**` cmdlet을 사용하여 볼륨을 만들고 서식을 지정합니다. 전자의 `New-Volume` cmdlet은 서로 다른 저장소 배열에서 볼륨 크기를 반올림할 수 있기 때문입니다. NTFS 볼륨을 이미 만든 경우 `Resize-Partition`을 사용하여 볼륨 중 하나를 다른 볼륨과 일치하도록 확장하거나 축소할 수 있습니다(ReFS 볼륨에서는 불가능). **Diskmgmt** 또는 **서버 관리자**를 사용하는 경우에는 반올림이 발생하지 않습니다.  

## <a name="running-test-srtopology-fails-with-name-related-errors"></a>이름 관련 오류와 함께 Test-SRTopology 실행 실패

`Test-SRTopology`를 사용하고 할 때 다음 오류 중 하나가 나타납니다.  

**오류 예 1:**

    WARNING: Invalid value entered for target computer name: sr-srv03. Test-SrTopology cmdlet does not accept IP address as  
    input for target computer name parameter. NetBIOS names and fully qualified domain names are acceptable inputs  
    WARNING: System.Exception  
    WARNING:    at Microsoft.FileServices.SR.Powershell.TestSRTopologyCommand.BeginProcessing()  
    Test-SRTopology : Invalid value entered for target computer name: sr-srv03. Test-SrTopology cmdlet does not accept IP  
    address as input for target computer name parameter. NetBIOS names and fully qualified domain names are acceptable  
    inputs  
    At line:1 char:1  
    + Test-SRTopology -SourceComputerName sr-srv01 -SourceVolumeName d: -So ...  
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~  
        + CategoryInfo          : InvalidArgument: (:) [Test-SRTopology], Exception  
        + FullyQualifiedErrorId : TestSRTopologyFailure,Microsoft.FileServices.SR.Powershell.TestSRTopologyCommand  

**오류 예 2:**

    WARNING: Invalid value entered for source computer name

**오류 예 3:**

    The specified volume cannot be found G: cannot be found on computer SRCLUSTERNODE1

이 cmdlet은 Windows Server 2016에서 제한적인 오류 보고 기능을 포함하며, 많은 일반적인 문제에 대해 동일한 출력을 반환합니다. 이 오류는 다음과 같은 이유로 나타날 수 있습니다.  

* 도메인 사용자가 아니라 로컬 사용자로 원본 컴퓨터에 로그온했습니다.  
* 대상 컴퓨터가 실행 중이지 않거나 네트워크를 통해 액세스할 수 없습니다.  
* 대상 컴퓨터의 이름을 잘못 지정했습니다.  
* 대상 서버의 IP 주소를 지정했습니다.  
* 대상 컴퓨터 방화벽이 PowerShell 및/또는 CIM 호출에 대한 액세스를 차단하고 있습니다.  
* 대상 컴퓨터에서 WMI 서비스를 실행하고 있지 않습니다.   
* 관리 컴퓨터에서 원격으로 `Test-SRTopology` cmdlet을 실행할 때 CREDSSP를 사용하지 않았습니다.
* 지정된 원본 또는 대상 볼륨은 클러스터된 디스크가 아니라 클러스터 노드에서 로컬 디스크입니다.  

## <a name="configuring-new-storage-replica-partnership-returns-an-error---failed-to-provision-partition"></a>새 저장소 복제본 파트너 관계를 구성할 때 “파티션을 프로비전하지 못했습니다.” 오류가 반환됨
`New-SRPartnership`을 사용하여 새 복제 파트너 관계를 만들려고 할 때 다음과 같은 오류가 발생합니다.

    New-SRPartnership : Unable to create replication group test01, detailed reason: Failed to provision partition ed0dc93f-107c-4ab4-a785-afd687d3e734.
    At line: 1 char: 1
    + New-SRPartnership -SourceComputerName srv1 -SourceRGName test01
    + Categorylnfo : ObjectNotFound: (MSFT_WvrAdminTasks : root/ Microsoft/. . s) CNew-SRPartnership], CimException
    + FullyQua1ifiedErrorId : Windows System Error 1168 ,New-SRPartnership

이는 시스템 드라이브와 동일한 파티션(즉, 해당 Windows 폴더가 있는 **C:** 드라이브)에 있는 데이터 볼륨을 선택했기 때문입니다. 예를 들어 동일한 파티션에서 생성된 **C:** 및 **D:** 볼륨을 둘 다 포함하는 드라이브가 여기에 해당합니다. 이는 저장소 복제본에서 지원되지 않습니다. 복제할 다른 볼륨을 선택해야 합니다.

## <a name="attempting-to-grow-a-replicated-volume-fails-due-to-missing-update"></a>업데이트 누락으로 인해 복제된 볼륨을 확장할 수 없음
복제된 볼륨을 늘리거나 확장하려고 하면 다음 오류가 발생합니다.

    PS C:\> Resize-Partition -DriveLetter d -Size 44GB
    Resize-Partition : The operation failed with return code 8
    At line:1 char:1
    + Resize-Partition -DriveLetter d -Size 44GB
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (StorageWMI:ROOT/Microsoft/.../MSFT_Partition
    [Resize-Partition], CimException
    + FullyQualifiedErrorId : StorageWMI 8,Resize-Partition

디스크 관리 MMC 스냅인을 사용하는 경우 다음 오류가 발생합니다. 

    Element not found

`Set-SRGroup -Name rg01 -AllowVolumeResize $TRUE`를 사용하여 원본 서버에서 볼륨 크기 조정을 제대로 설정해도 이 오류가 발생합니다. 

이 문제는 Windows 10 Version 1607 및 Windows Server 2016의 누적 업데이트에서 해결되었습니다(2016년 12월 9일(KB3201845)). 

## <a name="attempting-to-grow-a-replicated-volume-fails-due-to-missing-step"></a>단계 누락으로 인해 복제된 볼륨을 확장할 수 없음
먼저 `-AllowResizeVolume $TRUE`를 설정하지 않고 원본 서버에서 복제된 볼륨의 크기를 조정하려는 경우 다음과 같은 오류가 표시됩니다.

    PS C:\> Resize-Partition -DriveLetter I -Size 8GB
    Resize-Partition : Failed
    Activity ID: {87aebbd6-4f47-4621-8aa4-5328dfa6c3be}
    At line:1 char:1
    + Resize-Partition -DriveLetter I -Size 8GB
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (StorageWMI:ROOT/Microsoft/.../MSFT_Partition) [Resize-Partition], CimException
        + FullyQualifiedErrorId : StorageWMI 4,Resize-Partition

저장소 복제 이벤트 로그 오류 10307:

    Attempted to resize a partition that is protected by Storage Replica .

    DeviceName: \Device\Harddisk1\DR1
    PartitionNumber: 7
    PartitionId: {b71a79ca-0efe-4f9a-a2b9-3ed4084a1822}

    Guidance: To grow a source data partition, set the policy on the replication group containing the data partition.

    Set-SRGroup -ComputerName [ComputerName] -Name [ReplicationGroupName] -AllowVolumeResize $true

    Before you grow the source data partition, ensure that the destination data partition has enough space to grow to an equal size. Shrinking of data partition protected by Storage Replica is blocked.

디스크 관리 스냅인 오류: 

    An unexpected error has occurred 

볼륨의 크기를 조정한 후 `Set-SRGroup -Name rg01 -AllowVolumeResize $FALSE`를 통해 크기 조정을 비활성화해야 합니다. 이 매개 변수는 대상 볼륨에 충분한 공간이 있는지 확인하기 전에 관리자가 볼륨의 크기를 조정하지 못하게 방지합니다. 일반적으로 저장소 복제본의 존재를 인식하지 못했기 때문입니다. 

## <a name="attempting-to-move-a-pdr-resource-between-sites-on-an-asynchronous-stretch-cluster-fails"></a>비동기 확장 클러스터에서 사이트 간에 PDR 리소스를 이동하려고 하면 실패합니다.
비동기 확장 클러스터에서 연결된 저장소를 이동하기 위해 일반 용도의 파일 서버와 같은 실제 디스크 리소스 연결 역할을 이동하려고 하면 오류가 발생합니다.

장애 조치 클러스터 관리자 스냅인을 사용하는 경우:

    Error
    The operation has failed.
    The action 'Move' did not complete.
    Error Code: 0x80071398
    The operation failed because either the specified cluster node is not the owner of the group, or the node is not a possible owner of the group
    
클러스터 powershell cmdlet을 사용하는 경우:

    PS C:\> Move-ClusterGroup -Name sr-fs-006 -Node sr-srv07
    Move-ClusterGroup : An error occurred while moving the clustered role 'sr-fs-006'.
    The operation failed because either the specified cluster node is not the owner of the group, or the node is not a
    possible owner of the group
    At line:1 char:1
    + Move-ClusterGroup -Name sr-fs-006 -Node sr-srv07
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (:) [Move-ClusterGroup], ClusterCmdletException
    + FullyQualifiedErrorId : Move-ClusterGroup,Microsoft.FailoverClusters.PowerShell.MoveClusterGroupCommand

이는 Windows Server 2016의 기본 동작으로 인해 발생합니다. `Set-SRPartnership`을 사용하여 비동기 확장 클러스터에서 이러한 PDR 디스크를 이동합니다.  

## <a name="attempting-to-add-disks-to-a-two-node-asymmetric-cluster-returns-no-disks-suitable-for-cluster-disks-found"></a>2-노드 비대칭 클러스터에 디스크를 추가하려고 하면 "클러스터 디스크에 적합한 디스크가 없음" 오류가 반환됩니다. 
저장소 복제본을 확장 복제를 추가하기 전에 노드가 2개만 있는 클러스터를 프로비전하려고 할 경우 두 번째 사이트에 있는 디스크를 사용 가능한 디스크에 추가하려고 합니다. 이 경우 다음과 같은 오류가 발생합니다.

    "No disks suitable for cluster disks found. For diagnostic information about disks available to the cluster, use the Validate a Configuration Wizard to run Storage tests." 

클러스터에 노드가 3개 이상 있는 경우 이러한 문제는 발생하지 않습니다. 이 문제는 Windows Server 2016에서 기본적으로 비대칭 저장소 클러스터링 동작이 변경되었기 때문에 발생합니다. 

저장소를 추가하려면 두 번째 사이트의 노드에서 다음 명령을 실행하면 됩니다.

`Get-ClusterAvailableDisk -All | Add-ClusterDisk`

노드 로컬 저장소에서는 이 명령이 작동하지 않습니다. 저장소 복제본을 사용하여 총 두 개의 노드 간에 확장 클러스터를 복제할 수 있습니다. **노드마다 고유의 공유 저장소 집합이 있습니다.** 

## <a name="the-smb-bandwidth-limiter-fails-to-throttle-storage-replica-bandwidth"></a>SMB 대역폭 제한이 저장소 복제본 대역폭 조절에 실패
저장소 복제본의 대역폭 제한을 지정할 때 제한이 무시되고 전체 대역폭이 사용됩니다. 예:

`Set-SmbBandwidthLimit  -Category StorageReplication -BytesPerSecond 32MB`

이 문제는 저장소 복제본과 SMB 간의 상호 운용성 문제 때문에 발생합니다. 이 문제는 2017년 7월 Windows Server 2016 누적 업데이트와 Windows Server, 버전 1709에서 처음 해결되었습니다.

## <a name="event-1241-warning-repeated-during-initial-sync"></a>초기 동기화 중에 이벤트 1241 경고가 반복됨
복제 파트너 관계를 비동기로 지정할 때 원본 컴퓨터가 저장소 복제본 관리자 채널에서 경고 이벤트 1241을 반복적으로 기록합니다. 예:

    Log Name:      Microsoft-Windows-StorageReplica/Admin
    Source:        Microsoft-Windows-StorageReplica
    Date:          3/21/2017 3:10:41 PM
    Event ID:      1241
    Task Category: (1)
    Level:         Warning
    Keywords:      (1)
    User:          SYSTEM
    Computer:      sr-srv05.corp.contoso.com
    Description:
    The Recovery Point Objective (RPO) of the asynchronous destination is unavailable.

    LocalReplicationGroupName: rg01
    LocalReplicationGroupId: {e20b6c68-1758-4ce4-bd3b-84a5b5ef2a87}
    LocalReplicaName: f:\
    LocalPartitionId: {27484a49-0f62-4515-8588-3755a292657f}
    ReplicaSetId: {1f6446b5-d5fd-4776-b29b-f235d97d8c63}
    RemoteReplicationGroupName: rg02
    RemoteReplicationGroupId: {7f18e5ea-53ca-4b50-989c-9ac6afb3cc81}
    TargetRPO: 30

    Guidance: This is typically due to one of the following reasons: 

현재 비동기 대상의 연결이 끊어졌습니다. 연결이 복원되면 RPO를 다시 사용할 수 있습니다.

    The asynchronous destination is unable to keep pace with the source such that the most recent destination log record is no longer present in the source log. The destination will start block copying. The RPO should become available after block copying completes.

이는 초기 동기화에서 예상된 동작이며 무시해도 됩니다. 이 동작은 이후 릴리스에서 변경될 수 있습니다. 비동기 복제가 진행되는 동안 이 동작이 발견되면 파트너 관계를 조사하여 구성된 RPO(기본적으로 30초)보다 더 오랫동안 복제가 지연되는 이유를 확인하세요.

## <a name="event-4004-warning-repeated-after-rebooting-a-replicated-node"></a>복제된 노드를 다시 부팅한 후 이벤트 4004 경고가 반복됨
파트너 관계에 있는 서버를 다시 부팅하면 복제가 실패하고 다시 부팅된 노드가 액세스 거부 오류와 함께 경고 이벤트 4004를 기록하는 현상이 매우 드물게 발생하기도 하며 대부분은 이 현상을 재현할 수도 없습니다.

    Log Name:      Microsoft-Windows-StorageReplica/Admin
    Source:        Microsoft-Windows-StorageReplica
    Date:          3/21/2017 11:43:25 AM
    Event ID:      4004
    Task Category: (7)
    Level:         Warning
    Keywords:      (256)
    User:          SYSTEM
    Computer:      server.contoso.com
    Description:
    Failed to establish a connection to a remote computer.

    RemoteComputerName: server
    LocalReplicationGroupName: rg01
    LocalReplicationGroupId: {a386f747-bcae-40ac-9f4b-1942eb4498a0}
    RemoteReplicationGroupName: rg02
    RemoteReplicationGroupId: {a386f747-bcae-40ac-9f4b-1942eb4498a0}
    ReplicaSetId: {00000000-0000-0000-0000-000000000000}
    RemoteShareName:{a386f747-bcae-40ac-9f4b-1942eb4498a0}.{00000000-0000-0000-0000-000000000000}
    Status: {Access Denied}
    A process has requested access to an object, but has not been granted those access rights.

    Guidance: Possible causes include network failures, share creation failures for the remote replication group, or firewall settings. Make sure SMB traffic is allowed and there are no connectivity issues between the local computer and the remote computer. You should expect this event when suspending replication or removing a replication partnership.

`Status: "{Access Denied}"` 및 `A process has requested access to an object, but has not been granted those access rights.` 메시지.
이는 저장소 복제본 내에서 알려진 문제이고, 2017년 9월 12일 품질 업데이트 - KB4038782(OS 빌드 14393.1715) https://support.microsoft.com/en-us/help/4038782/windows-10-update-kb4038782에서 해결되었습니다. 

## <a name="error-failed-to-bring-the-resource-cluster-disk-x-online-with-a-stretch-cluster"></a>확장 클러스터에서 "'클러스터 디스크 x' 리소스를 온라인 상태로 전환하지 못했습니다." 오류 발생
장애 조치(failover) 후 클러스터 디스크를 온라인으로 전환하고 원래 소스 사이트를 다시 기본 사이트로 만들려고 시도하면 장애 조치(failover) 클러스터 관리자에서 오류가 발생합니다. 예:

    Error
    The operation has failed.
    Failed to bring the resource 'Cluster Disk 2' online.
    
    Error Code: 0x80071397
    The operation failed because either the specified cluster node is not the owner of the resource, or the node is not a possible owner of the resource.
    
디스크나 CSV를 수동으로 이동하려고 하면 추가 오류가 발생합니다. 예:

    Error
    The operation has failed.
    The action 'Move' did not complete.
    
    Error Code: 0x8007138d
    A cluster node is not available for this operation

이 문제는 하나 이상의 초기화되지 않은 디스크가 하나 이상의 클러스터 노드에 연결된 경우에 발생합니다. 이 문제를 해결하려면 DiskMgmt.msc, DISKPART.EXE 또는 Initialize-Disk PowerShell cmdlet을 사용하여 모든 연결된 저장소를 초기화해야 합니다.

이 문제를 영구적으로 해결하는 업데이트를 제공하기 위해 현재 작업 중입니다. Microsoft 프리미어 지원 계약을 맺은 분들 중에서 문제 해결을 도와주실 생각이 있는 분들은 저희와 함께 협력하여 백포트 요청을 제출할 수 있도록 SRFEED@microsoft.com으로 이메일을 보내주세요.

## <a name="gpt-error-when-attempting-to-create-a-new-sr-partnership"></a>새 SR 파트너 관계를 만들려고 시도하면 GPT 오류 발생

New-SRPartnership을 실행하면 다음 오류와 함께 작업이 실패합니다. 

    Disk layout type for volume \\?\Volume{GUID}\ is not a valid GPT style layout.
    New-SRPartnership : Unable to create replication group SRG01, detailed reason: Disk layout type for volume
    \\?\Volume{GUID}\ is not a valid GPT style layout.
    At line:1 char:1
    + New-SRPartnership -SourceComputerName nodesrc01 -SourceRGName SRG01 ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (MSFT_WvrAdminTasks:root/Microsoft/...T_WvrAdminTasks) [New-SRPartnership]
    , CimException
    + FullyQualifiedErrorId : Windows System Error 5078,New-SRPartnership

장애 조치(failover) 클러스터 관리자 GUI에는 디스크에 복제를 설정하는 옵션이 없습니다.

Test-SRTopology를 실행하면 다음 오류와 함께 작업이 실패합니다. 

    WARNING: Object reference not set to an instance of an object.
    WARNING: System.NullReferenceException
    WARNING:    at Microsoft.FileServices.SR.Powershell.MSFTPartition.GetPartitionInStorageNodeByAccessPath(String AccessPath, String ComputerName, MIObject StorageNode)
       at Microsoft.FileServices.SR.Powershell.Volume.GetVolume(String Path, String ComputerName)
       at Microsoft.FileServices.SR.Powershell.TestSRTopologyCommand.BeginProcessing()
    Test-SRTopology : Object reference not set to an instance of an object.
    At line:1 char:1
    + Test-SRTopology -SourceComputerName nodesrc01 -SourceVolumeName U: - ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidArgument: (:) [Test-SRTopology], NullReferenceException
    + FullyQualifiedErrorId : TestSRTopologyFailure,Microsoft.FileServices.SR.Powershell.TestSRTopologyCommand 

클러스터 기능 수준이 여전히 Windows Server 2012 R2(예: FL 8)로 설정되어 있기 때문에 발생하는 문제입니다. 저장소 복제본은 여기서 특정 오류 반환을 지원하지만 그 대신 잘못된 오류 매핑을 반환합니다.

각 노드에서 Get-Cluster | fl *를 실행합니다.

ClusterFunctionalLevel이 9이면 이 노드에 저장소 복제본을 구현하는 데 필요한 것은 Windows 2016 ClusterFunctionalLevel 버전입니다.
ClusterFunctionalLevel이 9가 아닌 경우 이 노드에 저장소 복제본을 구현하려면 ClusterFunctionalLevel을 업데이트해야 합니다.

이 문제를 해결하려면 PowerShell cmdlet Update-ClusterFunctionalLevel https://technet.microsoft.com/itpro/powershell/windows/failoverclusters/update-clusterfunctionallevel을 실행하여 클러스터 기능 수준을 높이세요.

## <a name="small-unknown-partition-listed-in-diskmgmt-for-each-replicated-volume"></a>복제된 각 볼륨마다 알 수 없는 작은 파티션이 DISKMGMT에 나열됨

디스크 관리 스냅인(DISKMGMT.MSC)을 실행하면 레이블이나 드라이브 문자가 없는 1MB 크기의 볼륨이 하나 이상 나열됩니다. 이 알 수 없는 볼륨을 삭제할 수 있는 경우도 있으나, 삭제되지 않고 다음과 같은 메시지가 나타나는 경우가 있습니다.

    "An Unexpected Error has Occurred"  

이 동작은 의도된 것입니다. 이것은 볼륨이 아니라 파티션입니다. 저장소 복제는 복제 작업을 위한 데이터베이스 슬롯으로 사용하기 위해 512KB 파티션을 하나 만듭니다(레거시 DiskMgmt.msc 도구는 근사치 MB로 반올림). 복제된 각 볼륨에 대해 이와 같은 파티션을 두는 것은 정상적이며 바람직합니다. 더 이상 사용되지 않는 경우에는 이 512KB 파티션을 삭제할 수 있으나 사용 중인 경우에는 삭제할 수 없습니다. 이 파티션은 절대 커지거나 줄어들지 않습니다. 사용되지 않는 파티션은 저장소 복제가 관리할 것이므로 복제를 재생성하는 경우 해당 파티션은 그대로 두는 것이 좋습니다.

세부 정보를 보려면 DISKPART 도구 또는 Get-Partition cmdlet을 사용합니다. 이러한 파티션은 GPT 유형의 `558d43c5-a1ac-43c0-aac8-d1472b2923d1`(을)를 갖습니다. 

## <a name="see-also"></a>참고 항목  
- [저장소 복제본](storage-replica-overview.md)  
- [공유 저장소를 사용하여 확장 클러스터 복제](stretch-cluster-replication-using-shared-storage.md)  
- [서버 간 저장소 복제](server-to-server-storage-replication.md)  
- [클러스터 간 저장소 복제](cluster-to-cluster-storage-replication.md)  
- [저장소 복제본: 질문과 대답](storage-replica-frequently-asked-questions.md)  
- [직접 액세스 저장소 공간](../storage-spaces/storage-spaces-direct-overview.md)  
