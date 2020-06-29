---
title: 스토리지 복제본의 알려진 문제
ms.prod: windows-server
manager: siroy
ms.author: nedpyle
ms.technology: storage-replica
ms.topic: get-started-article
author: nedpyle
ms.date: 06/25/2019
ms.assetid: ceddb0fa-e800-42b6-b4c6-c06eb1d4bc55
ms.openlocfilehash: 1ab4c0946c1081019747420448a0217359282bf1
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85469728"
---
# <a name="known-issues-with-storage-replica"></a>스토리지 복제본의 알려진 문제

>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server(반기 채널)

이 항목에서는 Windows Server에서 저장소 복제본의 알려진 문제에 대해 설명 합니다.

## <a name="after-removing-replication-disks-are-offline-and-you-cannot-configure-replication-again"></a>복제를 제거한 후 디스크가 오프라인 상태가 되어 복제를 다시 구성할 수 없음

Windows Server 2016에서 이전에 복제한 볼륨에서 복제를 프로비전할 수 없거나, 탑재할 수 없는 볼륨을 찾을 수 없습니다. 이는 일부 오류 조건이 복제 제거를 방지하는 경우 또는 이전에 데이터를 복제한 컴퓨터에 운영 체제를 다시 설치한 경우에 발생할 수 있습니다.

이 문제를 해결하려면 `Clear-SRMetadata` cmdlet을 사용하여 디스크에서 숨겨진 스토리지 복제본 파티션을 지우고 쓰기 가능한 상태로 되돌려야 합니다.

-   분리된 모든 스토리지 복제본 파티션 데이터베이스 슬롯을 제거하고 모든 파티션을 다시 탑재하려면 다음과 같이 `-AllPartitions` 매개 변수를 사용합니다.

    ```PowerShell
    Clear-SRMetadata -AllPartitions
    ```

-   분리된 모든 스토리지 복제본 로그 데이터를 제거하려면 다음과 같이 `-AllLogs` 매개 변수를 사용합니다.

    ```PowerShell
    Clear-SRMetadata -AllLogs
    ```

-   분리된 모든 장애 조치(failover) 클러스터 구성 데이터를 제거하려면 다음과 같이 `-AllConfiguration` 매개 변수를 사용합니다.

    ```PowerShell
    Clear-SRMetadata -AllConfiguration
    ```

-   개별 복제 그룹 메타데이터를 제거하려면 다음과 같이 `-Name` 매개 변수를 사용하고 복제 그룹을 지정합니다.

    ```PowerShell
    Clear-SRMetadata -Name RG01 -Logs -Partition
    ```

파티션 데이터베이스를 지운 후 서버를 다시 시작해야 할 수 있습니다. `-NoRestart`를 사용하여 이를 일시적으로 억제할 수 있지만 cmdlet에서 요청한 경우 서버 다시 시작을 건너뛰어서는 안 됩니다. 이 cmdlet은 데이터 볼륨과 해당 볼륨에 포함된 데이터를 제거하지 않습니다.

## <a name="during-initial-sync-see-event-log-4004-warnings"></a>초기 동기화 중에 이벤트 로그 4004 경고가 표시됨

Windows Server 2016에서 복제를 구성할 때 원본 및 대상 서버 모두에서 초기 동기화 중에 "API를 완료하기 위한 시스템 리소스가 부족합니다." 상태의 여러 **StorageReplica\Admin** 이벤트 로그 4004 경고가 표시될 수 있습니다. 5014 오류도 표시될 수 있습니다. 이는 서버에 사용 가능한 메모리(RAM)가 부족하여 초기 동기화 및 워크로드를 실행할 수 없음을 나타냅니다. RAM을 추가하거나, 스토리지 복제본 이외의 기능 및 애플리케이션에서 사용되는 RAM을 줄입니다.

## <a name="when-using-guest-clusters-with-shared-vhdx-and-a-host-without-a-csv-virtual-machines-stop-responding-after-configuring-replication"></a>공유 VHDX가 있는 게스트 클러스터와 CSV가 없는 호스트를 사용하는 경우 복제를 구성한 후 가상 컴퓨터의 응답이 중지됨

Windows Server 2016에서 스토리지 복제본 테스트 또는 데모용으로 Hyper-V 게스트 클러스터를 사용하고 공유 VHDX를 게스트 클러스터 스토리지로 사용하는 경우 복제를 구성한 후 가상 컴퓨터의 응답이 중지됩니다. Hyper-V 호스트를 다시 시작하면 가상 컴퓨터가 응답하기 시작하지만 복제 구성이 완료되지 않고 복제가 발생하지 않습니다.

이 동작은 CSV를 실행하는 Hyper-V 호스트에 대한 요구 사항을 무시하기 위해 **fltmc.exe attach svhdxflt**를 사용할 때 발생합니다. 이 명령의 사용은 지원되지 않으며 테스트 및 데모용으로만 제공됩니다.

속도 저하의 원인은 Windows Server 2016의 스토리지 QoS 기능과 수동으로 연결된 공유 VHDX 필터 간의 설계에 따른 상호 운용성 문제입니다. 이 문제를 해결하려면 스토리지 QoS 필터 드라이버를 사용하지 않도록 설정하고 Hyper-V 호스트를 다시 시작합니다.

```
SC config storqosflt start= disabled
```

## <a name="cannot-configure-replication-when-using-new-volume-and-differing-storage"></a>New-Volume 및 서로 다른 스토리지를 사용하는 경우 복제를 구성할 수 없음

원본 및 대상 서버에서 서로 다른 스토리지 집합(예: 두 개의 SAN 또는 디스크가 서로 다른 두 개의 JBOD)과 함께 `New-Volume` cmdlet을 사용하는 경우 이후에 `New-SRPartnership`을 사용하여 복제를 구성할 수 없습니다. 다음과 같은 오류가 표시될 수 있습니다.

    Data partition sizes are different in those two groups

`New-Volume` 대신 `New-Partition**` cmdlet을 사용하여 볼륨을 만들고 서식을 지정합니다. 전자의 cmdlet은 서로 다른 스토리지 배열에서 볼륨 크기를 반올림할 수 있기 때문입니다. NTFS 볼륨을 이미 만든 경우 `Resize-Partition`을 사용하여 볼륨 중 하나를 다른 볼륨과 일치하도록 확장하거나 축소할 수 있습니다(ReFS 볼륨에서는 불가능). **Diskmgmt** 또는 **서버 관리자**를 사용하는 경우에는 반올림이 발생하지 않습니다.

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

## <a name="configuring-new-storage-replica-partnership-returns-an-error---failed-to-provision-partition"></a>새 스토리지 복제본 파트너 관계를 구성할 때 “파티션을 프로비전하지 못했습니다.” 오류가 반환됨

`New-SRPartnership`을 사용하여 새 복제 파트너 관계를 만들려고 할 때 다음과 같은 오류가 발생합니다.

    New-SRPartnership : Unable to create replication group test01, detailed reason: Failed to provision partition ed0dc93f-107c-4ab4-a785-afd687d3e734.
    At line: 1 char: 1
    + New-SRPartnership -SourceComputerName srv1 -SourceRGName test01
    + Categorylnfo : ObjectNotFound: (MSFT_WvrAdminTasks : root/ Microsoft/. . s) CNew-SRPartnership], CimException
    + FullyQua1ifiedErrorId : Windows System Error 1168 ,New-SRPartnership

이는 시스템 드라이브와 동일한 파티션(즉, 해당 Windows 폴더가 있는 **C:** 드라이브)에 있는 데이터 볼륨을 선택했기 때문입니다. 예를 들어 동일한 파티션에서 생성된 **C:** 및 **D:** 볼륨을 둘 다 포함하는 드라이브가 여기에 해당합니다. 이는 스토리지 복제본에서 지원되지 않습니다. 복제할 다른 볼륨을 선택해야 합니다.

## <a name="attempting-to-grow-a-replicated-volume-fails-due-to-missing-update"></a>업데이트가 누락 되어 복제 된 볼륨을 확장 하는 동안 오류가 발생 함

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

이는를 사용 하 여 원본 서버에서 볼륨 크기 조정을 올바르게 사용 하도록 설정 하는 경우에도 발생 `Set-SRGroup -Name rg01 -AllowVolumeResize $TRUE` 합니다.

이 문제는 Windows 10 버전 1607 (기념일 업데이트) 및 Windows Server 2016:12 월 9 2016 일 (KB3201845)에 대 한 누적 업데이트에서 해결 되었습니다.

## <a name="attempting-to-grow-a-replicated-volume-fails-due-to-missing-step"></a>누락 된 단계 때문에 복제 된 볼륨을 확장 하려는 시도가 실패 함

먼저를 설정 하지 않고 원본 서버에서 복제 된 볼륨의 크기를 조정 하려고 하면 `-AllowResizeVolume $TRUE` 다음과 같은 오류가 표시 됩니다.

    PS C:\> Resize-Partition -DriveLetter I -Size 8GB
    Resize-Partition : Failed

    Activity ID: {87aebbd6-4f47-4621-8aa4-5328dfa6c3be}
    At line:1 char:1
    + Resize-Partition -DriveLetter I -Size 8GB
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (StorageWMI:ROOT/Microsoft/.../MSFT_Partition) [Resize-Partition], CimException
        + FullyQualifiedErrorId : StorageWMI 4,Resize-Partition

    Storage Replica Event log error 10307:

    Attempted to resize a partition that is protected by Storage Replica .

    DeviceName: \Device\Harddisk1\DR1
    PartitionNumber: 7
    PartitionId: {b71a79ca-0efe-4f9a-a2b9-3ed4084a1822}

    Guidance: To grow a source data partition, set the policy on the replication group containing the data partition.

    Set-SRGroup -ComputerName [ComputerName] -Name [ReplicationGroupName] -AllowVolumeResize $true

    Before you grow the source data partition, ensure that the destination data partition has enough space to grow to an equal size. Shrinking of data partition protected by Storage Replica is blocked.

디스크 관리 스냅인 오류:

    An unexpected error has occurred

볼륨의 크기를 조정한 후에는로 크기 조정을 사용 하지 않도록 설정 해야 `Set-SRGroup -Name rg01 -AllowVolumeResize $FALSE` 합니다. 이 매개 변수는 일반적으로 저장소 복제본의 현재 상태를 인식할 수 없기 때문에 관리자가 대상 볼륨에 충분 한 공간을 확보 하기 전에 볼륨의 크기를 조정 하는 것을 방지 합니다.

## <a name="attempting-to-move-a-pdr-resource-between-sites-on-an-asynchronous-stretch-cluster-fails"></a>비동기 확장 클러스터에서 사이트 간에 PDR 리소스를 이동 시 실패

비동기 확장 클러스터에서 연결된 스토리지를 이동하기 위해 일반 용도의 파일 서버와 같은 실제 디스크 리소스 연결 역할을 이동하려고 하면 오류가 발생합니다.

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

이 문제는 Windows Server 2016의 설계상의 동작으로 인해 발생 합니다. `Set-SRPartnership`를 사용 하 여 비동기 확장 클러스터에서 이러한 PDR 디스크를 이동 합니다.

이 동작은 사용자 의견에 따라 비동기 복제를 사용 하 여 수동 및 자동 장애 조치 (failover)를 수행할 수 있도록 Windows Server, 버전 1709에서 변경 되었습니다.

## <a name="attempting-to-add-disks-to-a-two-node-asymmetric-cluster-returns-no-disks-suitable-for-cluster-disks-found"></a>2노드 비대칭 클러스터에 디스크를 추가하려고 하면 "클러스터 디스크에 적합한 디스크가 없음" 오류가 반환됩니다.

스토리지 복제본 확장 복제를 추가하기 전에 노드가 2개만 있는 클러스터를 프로비전하려고 할 경우 두 번째 사이트에 있는 디스크를 사용 가능한 디스크에 추가하려고 합니다. 이 경우 다음과 같은 오류가 발생합니다.

    "No disks suitable for cluster disks found. For diagnostic information about disks available to the cluster, use the Validate a Configuration Wizard to run Storage tests."

클러스터에 노드가 3개 이상 있는 경우 이러한 문제는 발생하지 않습니다. 이 문제는 Windows Server 2016에서 기본적으로 비대칭 스토리지 클러스터링 동작이 변경되었기 때문에 발생합니다.

스토리지를 추가하려면 두 번째 사이트의 노드에서 다음 명령을 실행할 수 있습니다.

`Get-ClusterAvailableDisk -All | Add-ClusterDisk`

이는 노드 로컬 저장소에서 작동 하지 않습니다. 저장소 복제본을 사용 하 여 두 개의 총 노드 간에 확장 클러스터를 복제할 수 있습니다 **. 각 노드는 자체 공유 저장소 집합을 사용 합니다.**

## <a name="the-smb-bandwidth-limiter-fails-to-throttle-storage-replica-bandwidth"></a>SMB 대역폭 제한을 사용 하면에서 저장소 복제본 대역폭을 제한 하지 못함

저장소 복제본에 대 한 대역폭 제한을 지정 하는 경우이 제한은 무시 되 고 전체 대역폭이 사용 됩니다. 예를 들면 다음과 같습니다.

`Set-SmbBandwidthLimit  -Category StorageReplication -BytesPerSecond 32MB`

이 문제는 저장소 복제본과 SMB 간의 상호 운용성 문제로 인해 발생 합니다. 이 문제는 Windows Server 2016 및 Windows Server 버전 1709의 7 월 2017 누적 업데이트에서 처음으로 수정 되었습니다.

## <a name="event-1241-warning-repeated-during-initial-sync"></a>초기 동기화 중에 이벤트 1241 경고가 반복 됨

복제 파트너 관계 지정이 비동기 인 경우 원본 컴퓨터는 저장소 복제본 관리 채널에서 경고 이벤트 1241를 반복 해 서 기록 합니다. 예를 들면 다음과 같습니다.

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

비동기 대상이 현재 연결 되어 있지 않습니다. 연결이 복원 된 후 RPO를 사용할 수 있습니다.

    The asynchronous destination is unable to keep pace with the source such that the most recent destination log record is no longer present in the source log. The destination will start block copying. The RPO should become available after block copying completes.

이는 초기 동기화 중에 예상 되는 동작이 며 안전 하 게 무시할 수 있습니다. 이 동작은 이후 릴리스에서 변경될 수 있습니다. 비동기 복제를 진행 하는 동안이 동작이 표시 되 면 파트너 관계를 조사 하 여 복제가 구성 된 RPO (기본적으로 30 초) 이상 지연 되는 이유를 확인 합니다.

## <a name="event-4004-warning-repeated-after-rebooting-a-replicated-node"></a>복제 된 노드를 다시 부팅 한 후 이벤트 4004 경고가 반복 됨

드물지만 일반적으로 unreproducable 하는 경우에는 파트너 관계에 있는 서버를 다시 부팅 하면 복제가 실패 하 고 다시 부팅 된 노드 로깅 경고 이벤트 4004에 액세스 거부 오류가 발생 합니다.

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

`Status: "{Access Denied}"`및 메시지는 `A process has requested access to an object, but has not been granted those access rights.` 저장소 복제본의 알려진 문제 이며 2017 년 9 월 12 일 (KB4038782) (OS 빌드 14393.1715)에서 수정 되었습니다.https://support.microsoft.com/help/4038782/windows-10-update-kb4038782

## <a name="error-failed-to-bring-the-resource-cluster-disk-x-online-with-a-stretch-cluster"></a>"' 클러스터 디스크 x '를 온라인 상태로 전환 하지 못했습니다." 오류가 발생 합니다. 스트레치 클러스터 사용

장애 조치 (failover) 후 원래 원본 사이트의 기본 사이트를 다시 설정 하려고 시도 하는 경우 클러스터 디스크를 온라인 상태로 전환 하는 경우 장애 조치(Failover) 클러스터 관리자에 오류가 표시 됩니다. 예를 들면 다음과 같습니다.

    Error
    The operation has failed.
    Failed to bring the resource 'Cluster Disk 2' online.

    Error Code: 0x80071397
    The operation failed because either the specified cluster node is not the owner of the resource, or the node is not a possible owner of the resource.

디스크 또는 CSV를 수동으로 이동 하려고 하면 추가 오류가 발생 합니다. 예를 들면 다음과 같습니다.

    Error
    The operation has failed.
    The action 'Move' did not complete.

    Error Code: 0x8007138d
    A cluster node is not available for this operation

하나 이상의 클러스터 노드에 초기화 되지 않은 디스크가 하나 이상 연결 되어 있기 때문에이 문제가 발생 합니다. 이 문제를 해결 하려면 Diskmgmt.msc, DISKPART.EXE 또는 Initialize-Disk PowerShell cmdlet을 사용 하 여 연결 된 모든 저장소를 초기화 합니다.

이 문제를 영구적으로 해결 하는 업데이트를 제공 하기 위해 노력 하 고 있습니다. Microsoft 프리미어 지원 계약을 체결 하는 데 관심이 있는 경우 백 포팅하 요청을 처리 하는 데 사용할 수 있도록 전자 메일을 보내 주시기 바랍니다 SRFEED@microsoft.com .

## <a name="gpt-error-when-attempting-to-create-a-new-sr-partnership"></a>새 SR 파트너 관계를 만드는 동안 GPT 오류가 발생 했습니다.

새 SRPartnership 관계를 실행 하는 경우 오류가 발생 하 고 실패 합니다.

    Disk layout type for volume \\?\Volume{GUID}\ is not a valid GPT style layout.
    New-SRPartnership : Unable to create replication group SRG01, detailed reason: Disk layout type for volume
    \\?\Volume{GUID}\ is not a valid GPT style layout.
    At line:1 char:1
    + New-SRPartnership -SourceComputerName nodesrc01 -SourceRGName SRG01 ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (MSFT_WvrAdminTasks:root/Microsoft/...T_WvrAdminTasks) [New-SRPartnership]
    , CimException
    + FullyQualifiedErrorId : Windows System Error 5078,New-SRPartnership

장애 조치(Failover) 클러스터 관리자 GUI에는 디스크에 대 한 복제를 설정 하는 옵션이 없습니다.

Test-srtopology를 실행 하는 경우 다음을 사용 하 여 실패 합니다.

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

이는 클러스터 기능 수준이 여전히 Windows Server 2012 R2 (즉, FL 8)로 설정 된 경우에 발생 합니다. 저장소 복제본은 여기에 특정 오류를 반환 하지만 대신 잘못 된 오류 매핑을 반환 합니다.

Get Cluster를 실행 합니다. 각 노드의 fl *

ClusterFunctionalLevel = 9 인 경우이 노드에서 저장소 복제본을 구현 하는 데 필요한 Windows 2016 ClusterFunctionalLevel 버전입니다.
ClusterFunctionalLevel가 9가 아니면이 노드에 저장소 복제본을 구현 하기 위해 ClusterFunctionalLevel를 업데이트 해야 합니다.

이 문제를 해결 하려면 [ClusterFunctionalLevel](https://docs.microsoft.com/powershell/module/failoverclusters/update-clusterfunctionallevel) PowerShell cmdlet을 실행 하 여 클러스터 기능 수준을 올립니다.

## <a name="small-unknown-partition-listed-in-diskmgmt-for-each-replicated-volume"></a>복제 된 각 볼륨에 대해 DISKMGMT.MSC에 나열 된 작은 알 수 없는 파티션

디스크 관리 스냅인 (DISKMGMT.MSC)을 실행 하는 경우 MSC)를 사용 하는 경우 레이블이 나 드라이브 문자 및 1MB 크기를 포함 하지 않는 볼륨이 하나 이상 표시 됩니다. 알 수 없는 볼륨을 삭제할 수 있거나 다음을 받을 수 있습니다.

    "An Unexpected Error has Occurred"

이 동작은 의도된 것입니다. 볼륨이 아니라 파티션입니다. 저장소 복제본은 복제 작업에 대 한 데이터베이스 슬롯으로 512KB 파티션을 만듭니다 (레거시 Diskmgmt.msc 도구는 가장 가까운 MB로 반올림). 복제 된 각 볼륨에 대해 이와 같은 파티션이 있으면이는 정상 이며 바람직한 방법입니다. 더 이상 사용 하지 않는 경우이 512KB 파티션을 자유롭게 삭제할 수 있습니다. 사용 중인 항목을 삭제할 수 없습니다. 파티션은 확장 되거나 축소 되지 않습니다. 복제를 다시 만드는 경우 저장소 복제본이 사용 하지 않는 것을 요청 하므로 파티션을 그대로 두는 것이 좋습니다.

세부 정보를 보려면 DISKPART 도구나 파티션 가져오기 cmdlet을 사용 합니다. 이러한 파티션은의 GPT 형식이 됩니다 `558d43c5-a1ac-43c0-aac8-d1472b2923d1` .

## <a name="a-storage-replica-node-hangs-when-creating-snapshots"></a>스냅숏을 만들 때 저장소 복제본 노드가 중단 됨

백업, VSSADMIN 등을 통해 VSS 스냅숏을 만들 때 저장소 복제본 노드가 중단 되며, 강제로 복구 하려면 노드를 강제로 다시 시작 해야 합니다. 오류가 없으며 서버의 하드 중단이 발생 합니다.

이 문제는 로그 볼륨의 VSS 스냅숏을 만들 때 발생 합니다. 기본적인 원인은 저장소 복제본이 아닌 VSS의 레거시 디자인 측면입니다. 저장소 복제본 로그 볼륨을 스냅숏을 만들면 생성 되는 동작은 VSS i/o queing 메커니즘이 서버의 교착 상태를 발생 하는 것입니다.

이 동작을 방지 하려면 저장소 복제본 로그 볼륨을 스냅숏 하지 마십시오. 이러한 로그는 복원할 수 없으므로 저장소 복제본 로그 볼륨을 스냅숏 할 필요는 없습니다. 또한 로그 볼륨은 다른 워크 로드를 포함 하지 않아야 하므로 일반적으로 스냅숏이 필요 하지 않습니다.

## <a name="high-io-latency-increase-when-using-storage-spaces-direct-with-storage-replica"></a>저장소 복제본과 함께 스토리지 공간 다이렉트를 사용 하는 경우 IO 대기 시간이 증가 합니다.

NVME 또는 SSD 캐시를 사용 하 여 스토리지 공간 다이렉트를 사용 하는 경우 스토리지 공간 다이렉트 클러스터 간에 저장소 복제본 복제를 구성 하는 동안 예상 되는 대기 시간이 증가 하는 것을 볼 수 있습니다. 대기 시간의 변화는 성능 + 용량 구성에서 NVME 및 SSD를 사용 하 고 HDD 계층 또는 용량 계층은 사용 하지 않는 것 보다 훨씬 더 높습니다.

이 문제는 느린 미디어와 비교할 때 저장소 복제본의 로그 메커니즘 내에서 NVME의 대기 시간이 매우 짧은 경우의 아키텍처 제한 때문에 발생 합니다. 스토리지 공간 다이렉트 캐시를 사용 하는 경우 모든 최근 읽기/쓰기 응용 프로그램 IO와 함께 저장소 복제본 로그의 모든 i/o가 캐시에서 발생 하 고 성능 또는 용량 계층에는 사용 되지 않습니다. 즉, 모든 저장소 복제본 작업이 동일한 속도 미디어에서 발생 합니다 .이 구성은 지원 되지만 권장 되지 않습니다 ( https://aka.ms/srfaq 로그 권장 사항 참조).

Hdd와 함께 스토리지 공간 다이렉트를 사용 하는 경우 캐시를 사용 하지 않도록 설정 하거나 방지할 수 없습니다. 해결 방법으로, SSD 및 NVME만 사용 하는 경우 성능 및 용량 계층만 구성할 수 있습니다. 해당 구성을 사용 하는 경우 성능 계층에 SR 로그를 서비스를 수행 하는 데이터 볼륨만 용량 계층에 배치 하면 위에서 설명한 대기 시간이 긴 문제를 피할 수 있습니다. 더 빠르고 느린 Ssd와 NVME를 혼합 하 여 동일한 작업을 수행할 수 있습니다.

이 해결 방법은 유용 하지 않으며 일부 고객이 사용 하지 못할 수도 있습니다. 저장소 복제본 팀은 나중에 이러한 인공 병목 현상을 줄이기 위해 최적화 및 업데이트 된 로그 메커니즘에 대해 작업 하 고 있습니다. 이 v2.0 로그는 먼저 Windows Server 2019에서 사용할 수 있게 되었으며, 향상 된 성능은 [서버 저장소 블로그의](https://blogs.technet.microsoft.com/filecab/2018/12/13/chelsio-rdma-and-storage-replica-perf-on-windows-server-2019-are-💯/)에 설명 되어 있습니다.

## <a name="error-could-not-find-file-when-running-test-srtopology-between-two-clusters"></a>두 클러스터 간에 Test-srtopology를 실행 하는 동안 "파일을 찾을 수 없습니다" 오류 발생

두 클러스터와 해당 CSV 경로 간에 Test-srtopology를 실행 하는 경우 오류와 함께 실패 합니다.

    PS C:\Windows\system32> Test-SRTopology -SourceComputerName NedClusterA -SourceVolumeName C:\ClusterStorage\Volume1 -SourceLogVolumeName L: -DestinationComputerName NedClusterB -DestinationVolumeName C:\ClusterStorage\Volume1 -DestinationLogVolumeName L: -DurationInMinutes 1 -ResultPath C:\Temp

    Validating data and log volumes...
    Measuring Storage Replica recovery and initial synchronization performance...
    WARNING: Could not find file '\\NedNode1\C$\CLUSTERSTORAGE\VOLUME1TestSRTopologyRecoveryTest\SRRecoveryTestFile01.txt'.
    WARNING: System.IO.FileNotFoundException
    WARNING:    at System.IO.__Error.WinIOError(Int32 errorCode, String maybeFullPath)
    at System.IO.FileStream.Init(String path, FileMode mode, FileAccess access, Int32 rights, Boolean useRights, FileShare share, Int32 buff
    erSize, FileOptions options, SECURITY_ATTRIBUTES secAttrs, String msgPath, Boolean bFromProxy, Boolean useLongPath, Boolean checkHost)
    at System.IO.FileStream..ctor(String path, FileMode mode, FileAccess access, FileShare share, Int32 bufferSize, FileOptions options)
    at Microsoft.FileServices.SR.Powershell.TestSRTopologyCommand.GenerateWriteIOWorkload(String Path, UInt32 IoSizeInBytes, UInt32 Parallel
    IoCount, UInt32 Duration)
    at Microsoft.FileServices.SR.Powershell.TestSRTopologyCommand.<>c__DisplayClass75_0.<PerformRecoveryTest>b__0()
    at System.Threading.Tasks.Task.Execute()
    Test-SRTopology : Could not find file '\\NedNode1\C$\CLUSTERSTORAGE\VOLUME1TestSRTopologyRecoveryTest\SRRecoveryTestFile01.txt'.
    At line:1 char:1
    + Test-SRTopology -SourceComputerName NedClusterA -SourceVolumeName  ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (:) [Test-SRTopology], FileNotFoundException
    + FullyQualifiedErrorId : TestSRTopologyFailure,Microsoft.FileServices.SR.Powershell.TestSRTopologyCommand

이 문제는 Windows Server 2016의 알려진 코드 오류로 인해 발생 합니다. 이 문제는 Windows Server, 버전 1709 및 연결 된 RSAT 도구에서 처음으로 수정 되었습니다. 하위 수준 확인의 경우 Microsoft 지원에 문의 하 여 백 포트 업데이트를 요청 하세요. 해결 방법이 없습니다.

## <a name="error-specified-volume-could-not-be-found-when-running-test-srtopology-between-two-clusters"></a>두 클러스터 간에 Test-srtopology를 실행 하는 경우 "지정한 볼륨을 찾을 수 없습니다." 오류

두 클러스터와 해당 CSV 경로 간에 Test-srtopology를 실행 하는 경우 오류와 함께 실패 합니다.

    PS C:\> Test-SRTopology -SourceComputerName RRN44-14-09 -SourceVolumeName C:\ClusterStorage\Volume1 -SourceLogVolumeName L: -DestinationComputerName RRN44-14-13 -DestinationVolumeName C:\ClusterStorage\Volume1 -DestinationLogVolumeName L: -DurationInMinutes 30 -ResultPath c:\report

    Test-SRTopology : The specified volume C:\ClusterStorage\Volume1 cannot be found on computer RRN44-14-09. If this is a cluster node, the volume must be part of a role or CSV; volumes in Available Storage are not accessible
    At line:1 char:1
    + Test-SRTopology -SourceComputerName RRN44-14-09 -SourceVolumeName C:\ ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : ObjectNotFound: (:) [Test-SRTopology], Exception
        + FullyQualifiedErrorId : TestSRTopologyFailure,Microsoft.FileServices.SR.Powershell.TestSRTopologyCommand

원본 볼륨으로 원본 노드 CSV를 지정 하는 경우 CSV를 소유 하는 노드를 선택 해야 합니다. CSV를 지정 된 노드로 이동 하거나에서 지정한 노드 이름을 변경할 수 있습니다 `-SourceComputerName` . 이 오류는 Windows Server 2019에서 향상 된 메시지를 받았습니다.

## <a name="unable-to-access-the-data-drive-in-storage-replica-after-unexpected-reboot-when-bitlocker-is-enabled"></a>BitLocker를 사용 하는 경우 예기치 않은 다시 부팅 후 저장소 복제본의 데이터 드라이브에 액세스할 수 없음

두 드라이브 (로그 드라이브 및 데이터 드라이브)에서 BitLocker를 사용 하도록 설정 하 고 두 저장소 복제본 드라이브 모두에서 주 서버를 다시 부팅 하는 경우 BitLocker에서 로그 드라이브의 잠금을 해제 한 후에도 기본 드라이브에 액세스할 수 없습니다.

이는 정상적인 동작입니다. 데이터를 복구 하거나 드라이브에 액세스 하려면 먼저 로그 드라이브의 잠금을 해제 한 다음 Diskmgmt.msc를 열어 데이터 드라이브를 찾아야 합니다. 데이터 드라이브를 오프 라인으로 전환 하 고 다시 온라인으로 전환 합니다. 드라이브의 BitLocker 아이콘을 찾아 드라이브의 잠금을 해제 합니다.

## <a name="issue-unlocking-the-data-drive-on-secondary-server-after-breaking-the-storage-replica-partnership"></a>저장소 복제본 파트너 관계를 중단 한 후 보조 서버에서 데이터 드라이브의 잠금을 해제 하는 문제

SR 파트너 관계를 사용 하지 않도록 설정 하 고 저장소 복제본을 제거한 후에는 해당 암호 또는 키를 사용 하 여 보조 서버의 데이터 드라이브를 잠금 해제할 수 없는 경우 예상 됩니다.

보조 서버의 데이터 드라이브를 잠금 해제 하려면 주 서버 데이터 드라이브의 키 또는 암호를 사용 해야 합니다.

## <a name="test-failover-doesnt-mount-when-using-asynchronous-replication"></a>비동기 복제를 사용 하는 경우 테스트 장애 조치가 탑재 되지 않음

Mount-SRDestination을 실행 하 여 테스트 장애 조치 (Failover) 기능의 일부로 대상 볼륨을 온라인 상태로 전환 하면 오류가 발생 하 여 실패 합니다.

    Mount-SRDestination: Unable to mount SR group <TEST>, detailed reason: The group or resource is not in the correct state to perform the supported operation.
    At line:1 char:1
    + Mount-SRDestination -ComputerName SRV1 -Name TEST -TemporaryP . . .
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (MSFT WvrAdminTasks : root/Microsoft/...(MSFT WvrAdminTasks : root/Microsoft/. T_WvrAdminTasks) (Mount-SRDestination], CimException
        + FullyQua1ifiedErrorId : Windows System Error 5823, Mount-SRDestination.

동기 파트너 관계 유형을 사용 하는 경우 테스트 장애 조치 (failover)가 정상적으로 작동 합니다.

이 문제는 Windows Server 버전 1709의 알려진 코드 오류로 인해 발생 합니다. 이 문제를 해결 하려면 [2018 년 10 월 18 일 업데이트](https://support.microsoft.com/help/4462932/windows-10-update-kb4462932)를 설치 합니다. 이 문제는 Windows Server 2019 및 Windows Server 버전 1809 이상에는 제공 되지 않습니다.

## <a name="additional-references"></a>추가 참조

- [스토리지 복제본](storage-replica-overview.md)
- [공유 저장소를 사용 하 여 확장 클러스터 복제](stretch-cluster-replication-using-shared-storage.md)
- [서버 간 저장소 복제](server-to-server-storage-replication.md)
- [클러스터 간 저장소 복제](cluster-to-cluster-storage-replication.md)
- [스토리지 복제본: 질문과 대답](storage-replica-frequently-asked-questions.md)
- [스토리지 공간 다이렉트](../storage-spaces/storage-spaces-direct-overview.md)
