---
title: 스토리지 공간 다이렉트 문제 해결
description: 스토리지 공간 다이렉트 배포 문제를 해결 하는 방법을 알아봅니다.
keywords: 저장소 공간
ms.prod: windows-server-threshold
ms.author: ''
ms.technology: storage-spaces
ms.topic: article
author: kaushika-msft
ms.date: 10/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7cc5709723b300f46ce108b36501e7ace272cd45
ms.sourcegitcommit: 6f968368c12b9dd699c197afb3a3d13c2211f85b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/26/2019
ms.locfileid: "68544571"
---
# <a name="troubleshoot-storage-spaces-direct"></a>문제 해결 스토리지 공간 다이렉트

> 적용 대상: Windows Server 2019, Windows Server 2016

다음 정보를 사용 하 여 스토리지 공간 다이렉트 배포 문제를 해결할 수 있습니다.

일반적으로 다음 단계를 시작 합니다.

1. Windows Server 카탈로그를 사용 하 여 SSD의 제조업체/모델이 Windows server 2016 및 Windows Server 2019에 대해 인증 되었는지 확인 합니다. 공급 업체에 드라이브가 스토리지 공간 다이렉트 지원 되는지 확인 합니다.
2. 저장소에서 잘못 된 드라이브를 검사 합니다. 저장소 관리 소프트웨어를 사용 하 여 드라이브의 상태를 확인 합니다. 드라이브에 오류가 발생 하는 경우 공급 업체와 함께 작업 합니다. 
3. 필요한 경우 저장소 및 드라이브 펌웨어를 업데이트 합니다.
   모든 노드에 최신 Windows 업데이트가 설치 되어 있는지 확인 합니다. Windows 10 및 windows server [2016 업데이트 기록과](https://aka.ms/update2016) windows [10 및 windows server 2019 업데이트 기록](https://support.microsoft.com/help/4464619)의 windows server 2019에 2016 대 한 최신 업데이트를 다운로드할 수 있습니다.
4. 네트워크 어댑터 드라이버 및 펌웨어를 업데이트 합니다.
5. 클러스터 유효성 검사를 실행 하 고 저장소 공간 다이렉트 섹션을 검토 하 여 캐시에 사용 되는 드라이브가 올바르게 보고 되 고 오류가 없는지 확인 합니다.

여전히 문제가 발생 하는 경우 아래 시나리오를 검토 하세요.

## <a name="virtual-disk-resources-are-in-no-redundancy-state"></a>가상 디스크 리소스가 중복 상태가 아닙니다.
크래시 또는 전원 오류로 인해 스토리지 공간 다이렉트 시스템의 노드가 예기치 않게 다시 시작 됩니다. 그런 다음, 하나 이상의 가상 디스크가 온라인 상태가 아닐 수 있으며 "중복 정보가 충분 하지 않습니다." 라는 설명이 표시 됩니다.

|FriendlyName|ResiliencySettingName| OperationalStatus| HealthStatus| IsManualAttach|Size| PSComputerName|
|------------|---------------------| -----------------| ------------| --------------|-----| --------------|
|Disk4| Mirror| 확인|  정상| True|  10TB|  노드-01. conto ...|
|Disk3         |Mirror                 |확인                          |정상       |True            |10TB | 노드-01. conto ...|
|Disk2         |Mirror                 |중복성 없음               |Unhealthy     |True            |10TB | 노드-01. conto ...|
|Disk1         |Mirror                 |{중복 없음, InService}  |Unhealthy     |True            |10TB | 노드-01. conto ...| 

또한 가상 디스크를 온라인 상태로 전환 하려고 하면 다음 정보가 클러스터 로그 (DiskRecoveryAction)에 기록 됩니다.  

```
[Verbose] 00002904.00001040::YYYY/MM/DD-12:03:44.891 INFO [RES] Physical Disk <DiskName>: OnlineThread: SuGetSpace returned 0.
[Verbose] 00002904.00001040:: YYYY/MM/DD -12:03:44.891 WARN [RES] Physical Disk < DiskName>: Underlying virtual disk is in 'no redundancy' state; its volume(s) may fail to mount.
[Verbose] 00002904.00001040:: YYYY/MM/DD -12:03:44.891 ERR [RES] Physical Disk <DiskName>: Failing online due to virtual disk in 'no redundancy' state. If you would like to attempt to online the disk anyway, first set this resource's private property 'DiskRecoveryAction' to 1. We will try to bring the disk online for recovery, but even if successful, its volume(s) or CSV may be unavailable. 
``` 

디스크가 실패 한 경우 또는 시스템에서 가상 디스크의 데이터에 액세스할 수 없는 경우 **중복성 없음 작업 상태가** 발생할 수 있습니다. 이 문제는 노드에서 유지 관리 하는 동안 노드에서 다시 부팅이 발생 하는 경우에 발생할 수 있습니다.

이 문제를 해결 하려면 다음 단계를 수행 합니다.

1. CSV에서 영향을 받는 가상 디스크를 제거 합니다. 이렇게 하면 클러스터의 "사용 가능한 저장소" 그룹에 포함 되 고 "실제 디스크"의 ResourceType으로 표시 되기 시작 합니다.

   ```powershell
   Remove-ClusterSharedVolume -name "VdiskName"
   ``` 
2. 사용 가능한 저장소 그룹을 소유한 노드에서 중복성이 없는 모든 디스크에 대해 다음 명령을 실행 합니다. "사용 가능한 저장소" 그룹이 있는 노드를 식별 하기 위해 다음 명령을 실행할 수 있습니다.

   ```powershell
   Get-ClusterGroup
   ```
3. 디스크 복구 작업을 설정 하 고 디스크를 시작 합니다.
   ```powershell
   Get-ClusterResource "VdiskName" | Set-ClusterParameter -Name DiskRecoveryAction -Value 1
   Start-ClusterResource -Name "VdiskName"
   ```
4. 복구는 자동으로 시작 됩니다. 복구가 완료 될 때까지 기다립니다. 일시 중단 된 상태로 전환 되 고 다시 시작할 수 있습니다. 진행률을 모니터링 하려면: 
    - **Get StorageJob** 을 실행 하 여 복구 상태를 모니터링 하 고 완료 된 시간을 확인 합니다.
    - **VirtualDisk** 를 실행 하 고 공간이 정상 HealthStatus을 반환 하는지 확인 합니다.
5. 복구가 완료 되 고 가상 디스크가 정상 상태 이면 가상 디스크 매개 변수를 다시 변경 합니다.

   ```powershell
    Get-ClusterResource "VdiskName" | Set-ClusterParameter -Name DiskRecoveryAction -Value 0
   ```
6. 디스크를 오프 라인 상태로 전환한 다음 다시 온라인으로 전환 하 여 DiskRecoveryAction 적용 합니다.

   ```powershell
   Stop-ClusterResource "VdiskName"
   Start-ClusterResource "VdiskName"
   ``` 
7. 영향을 받는 가상 디스크를 CSV에 다시 추가 합니다.

   ```powershell
   Add-ClusterSharedVolume -name "VdiskName"
   ```

**DiskRecoveryAction** 는 검사 없이 읽기/쓰기 모드에서 공간 볼륨을 연결할 수 있도록 하는 재정의 스위치입니다. 속성을 사용 하면 볼륨이 온라인 상태가 되지 않는 이유에 대 한 진단을 수행할 수 있습니다. 유지 관리 모드와 매우 비슷하지만 실패 상태의 리소스에서이를 호출할 수 있습니다. 또한 데이터에 액세스할 수 있으므로 데이터에 액세스할 수 있는 모든 데이터에 대 한 액세스 권한을 얻을 수 있는 "중복성 없음"과 같은 상황에서 유용할 수 있습니다. DiskRecoveryAction 속성은 2 월 22 일 2018, 업데이트, KB 4077525에 추가 되었습니다.


## <a name="detached-status-in-a-cluster"></a>클러스터의 분리 된 상태 

**VirtualDisk** cmdlet을 실행 하면 하나 이상의 스토리지 공간 다이렉트 가상 디스크에 대 한 OperationalStatus가 분리 됩니다. 그러나 **PhysicalDisk** cmdlet에 의해 보고 된 HealthStatus는 모든 실제 디스크가 정상 상태에 있음을 나타냅니다.

다음은 **VirtualDisk** cmdlet의 출력 예입니다.

|FriendlyName|  ResiliencySettingName|  OperationalStatus|   HealthStatus|  IsManualAttach|  Size|   PSComputerName|
|-|-|-|-|-|-|-|
|Disk4|         Mirror|                 확인|                  정상|       True|            10TB|  노드-01. conto ...|
|Disk3|         Mirror|                 확인|                  정상|       True|            10TB|  노드-01. conto ...|
|Disk2|         Mirror|                 Detached|            알 수 없음|       True|            10TB|  노드-01. conto ...|
|Disk1|         Mirror|                 Detached|            알 수 없음|       True|            10TB|  노드-01. conto ...| 


또한 노드에 다음과 같은 이벤트가 기록 될 수 있습니다.

```
Log Name: Microsoft-Windows-StorageSpaces-Driver/Operational
Source: Microsoft-Windows-StorageSpaces-Driver 
Event ID: 311 
Level: Error
User: SYSTEM 
Computer: Node#.contoso.local 
Description: Virtual disk {GUID} requires a data integrity scan.  

Data on the disk is out-of-sync and a data integrity scan is required. 

To start the scan, run the following command:   
Get-ScheduledTask -TaskName "Data Integrity Scan for Crash Recovery" | Start-ScheduledTask                

Once you have resolved the condition listed above, you can online the disk by using the following commands in PowerShell:   

Get-VirtualDisk | ?{ $_.ObjectId -Match "{GUID}" } | Get-Disk | Set-Disk -IsReadOnly $false 
Get-VirtualDisk | ?{ $_.ObjectId -Match "{GUID}" } | Get-Disk | Set-Disk -IsOffline  $false
------------------------------------------------------------

Log Name: System
Source: Microsoft-Windows-ReFS 
Event ID: 134
Level: Error 
User: SYSTEM
Computer: Node#.contoso.local 
Description: The file system was unable to write metadata to the media backing volume <VolumeId>. A write failed with status "A device which does not exist was specified." ReFS will take the volume offline. It may be mounted again automatically.
------------------------------------------------------------
Log Name: Microsoft-Windows-ReFS/Operational
Source: Microsoft-Windows-ReFS 
Event ID: 5 
Level: Error 
User: SYSTEM 
Computer: Node#.contoso.local 
Description: ReFS failed to mount the volume. 
Context: 0xffffbb89f53f4180 
Error: A device which does not exist was specified.
Volume GUID:{00000000-0000-0000-0000-000000000000} 
DeviceName: 
Volume Name:
``` 

손상 된 **작업 상태** 는 비정상 상태 추적 (DRT) 로그가 가득 찬 경우에 발생할 수 있습니다. 저장소 공간에서는 미러된 공간에 대해 DRT (더티 영역 추적)를 사용 하 여 전원 오류가 발생할 때 저장소 공간에서 저장소 공간을 다시 실행 하거나 실행 취소 하 여 저장소 공간을 유연 하 게 가져올 수 있도록 메타 데이터에 대 한 진행 중인 모든 업데이트를 기록 합니다. 전원이 복원 되 고 시스템에 백업이 제공 되는 경우 일관 된 상태입니다. DRT 로그가 가득 찬 경우에는 DRT 메타 데이터를 동기화 하 고 플러시할 때까지 가상 디스크를 온라인 상태로 만들 수 없습니다. 이 프로세스를 완료 하려면 전체 검색을 실행 해야 합니다 .이 작업은 완료 하는 데 몇 시간이 걸릴 수 있습니다.

이 문제를 해결 하려면 다음 단계를 수행 합니다.
1. CSV에서 영향을 받는 가상 디스크를 제거 합니다.

   ```powershell
   Remove-ClusterSharedVolume -name "VdiskName"
   ``` 
2. 온라인 상태가 아닌 모든 디스크에서 다음 명령을 실행 합니다. 

   ```powershell
   Get-ClusterResource -Name "VdiskName" | Set-ClusterParameter DiskRunChkDsk 7
   Start-ClusterResource -Name "VdiskName"
   ``` 
3. 분리 된 볼륨이 온라인 상태인 모든 노드에서 다음 명령을 실행 합니다. 

   ```powershell
   Get-ScheduledTask -TaskName "Data Integrity Scan for Crash Recovery" | Start-ScheduledTask 
   ```
   이 작업은 분리 된 볼륨이 온라인 상태인 모든 노드에서 시작 해야 합니다. 복구는 자동으로 시작 됩니다. 복구가 완료 될 때까지 기다립니다. 일시 중단 된 상태로 전환 되 고 다시 시작할 수 있습니다. 진행률을 모니터링 하려면: 
   - **Get StorageJob** 을 실행 하 여 복구 상태를 모니터링 하 고 완료 된 시간을 확인 합니다.
   - **VirtualDisk** 를 실행 하 고 공간이 정상 HealthStatus을 반환 하는지 확인 합니다.
     - "크래시 복구에 대 한 데이터 무결성 검사"는 저장소 작업으로 표시 되지 않고 진행률 표시기는 없는 작업입니다. 태스크가 실행 중으로 표시 되는 경우 실행 중입니다. 완료 되 면 완료 됨으로 표시 됩니다.

       또한 다음 cmdlet을 사용 하 여 실행 중인 일정 태스크의 상태를 볼 수 있습니다. 
       ```powershell
       Get-ScheduledTask | ? State -eq running
       ``` 
4. "크래시 복구에 대 한 데이터 무결성 검사"가 완료 되 면 복구를 완료 하 고 가상 디스크가 정상 상태가 되 면 가상 디스크 매개 변수를 다시 변경 합니다. 

   ```powershell
   Get-ClusterResource -Name "VdiskName" | Set-ClusterParameter DiskRunChkDsk 0 
   ```

5. 디스크를 오프 라인 상태로 전환한 다음 다시 온라인으로 전환 하 여 DiskRecoveryAction 적용 합니다.

   ```powershell
   Stop-ClusterResource "VdiskName"
   Start-ClusterResource "VdiskName"
   ``` 

6. 영향을 받는 가상 디스크를 CSV에 다시 추가 합니다.    

   ```powershell
   Add-ClusterSharedVolume -name "VdiskName"
   ```  
   **Diskrunchkdsk 값 7** 은 공간 볼륨을 연결 하 고 파티션을 읽기 전용 모드로 전환 하는 데 사용 됩니다. 이렇게 하면 복구를 트리거하여 공간을 자동으로 검색 하 고 자동 치료할 수 있습니다. 복구는 탑재 된 후 자동으로 실행 됩니다. 또한 데이터에 액세스할 수 있으므로 복사할 수 있는 모든 데이터에 대 한 액세스를 얻는 데 도움이 될 수 있습니다. 전체 DRT 로그와 같은 일부 오류 조건의 경우 크래시 복구 예약 된 작업에 대 한 데이터 무결성 검사를 실행 해야 합니다.

**크래시 복구 작업에 대 한 데이터 무결성 검사** 는 전체 비정상 영역 추적 (DRT) 로그를 동기화 하 고 지우는 데 사용 됩니다. 이 작업을 완료 하는 데 몇 시간 정도 걸릴 수 있습니다. "크래시 복구에 대 한 데이터 무결성 검사"는 저장소 작업으로 표시 되지 않고 진행률 표시기는 없는 작업입니다. 태스크가 실행 중으로 표시 되는 경우 실행 중입니다. 완료 되 면 완료로 표시 됩니다. 작업을 취소 하거나이 작업이 실행 되는 동안 노드를 다시 시작 하는 경우 작업을 처음부터 다시 시작 해야 합니다.

자세한 내용은 [상태 및 작동 상태 스토리지 공간 다이렉트 문제 해결](storage-spaces-states.md)을 참조 하세요.

## <a name="event-5120-with-statusiotimeout-c00000b5"></a>STATUS_IO_TIMEOUT c00000b5를 사용 하는 이벤트 5120 

> [!Important]
> **Windows Server 2016:** 픽스를 사용 하 여 업데이트를 적용 하는 동안 이러한 증상이 발생할 가능성을 줄이려면 아래 저장소 유지 관리 모드 절차를 사용 하 여 [10 월 18 일 2018, Windows Server 2016 이상 버전에 대 한 누적 업데이트](https://support.microsoft.com/help/4462928) 를 설치 하는 것이 좋습니다. 현재 노드가 2016 년 5 월 [8 일 2018](https://support.microsoft.com/help/4103723) ~ [10 월 9 2018 일](https://support.microsoft.com/help/KB4462917)에 출시 된 Windows Server 누적 업데이트를 설치 했습니다.

5120 년 5 월 [8 일, 2018 KB 4103723](https://support.microsoft.com/help/4103723) 에서 [10 월 9 2018 일](https://support.microsoft.com/help/4462917) 에 릴리스된 누적 업데이트를 사용 하 여 Windows Server 2016에서 노드를 다시 시작한 후에는 STATUS_IO_TIMEOUT c00000b5를 사용 하 여 이벤트을 받을 수 있습니다.

노드를 다시 시작 하는 경우 이벤트 5120는 시스템 이벤트 로그에 기록 되 고 다음 오류 코드 중 하나를 포함 합니다.

```
Event Source: Microsoft-Windows-FailoverClustering
Event ID: 5120
Description:    Cluster Shared Volume 'CSVName' ('Cluster Virtual Disk (CSVName)') has entered a paused state because of 'STATUS_IO_TIMEOUT(c00000b5)'. All I/O will temporarily be queued until a path to the volume is reestablished. 

Cluster Shared Volume ‘CSVName’ ('Cluster Virtual Disk (CSVName)') has entered a paused state because of 'STATUS_CONNECTION_DISCONNECTED(c000020c)'. All I/O will temporarily be queued until a path to the volume is reestablished.    
```

이벤트 5120이 기록 되 면 추가 증상이 발생 하거나 성능에 영향을 미칠 수 있는 디버깅 정보를 수집 하기 위해 라이브 덤프가 생성 됩니다. 라이브 덤프를 생성 하면 덤프 파일을 쓰기 위해 메모리의 스냅숏을 만들 수 있는 잠깐 일시 중지 됩니다. 많은 메모리가 있고 스트레스 상태에 있는 시스템은 노드가 클러스터 멤버 자격에서 삭제 될 수 있으며 다음 이벤트 1135이 기록 될 수도 있습니다.

```
Event source: Microsoft-Windows-FailoverClustering
Event ID: 1135  
Description: Cluster node 'NODENAME'was removed from the active failover cluster membership. The Cluster service on this node may have stopped. This could also be due to the node having lost communication with other active nodes in the failover cluster. Run the Validate a Configuration wizard to check your network configuration. If the condition persists, check for hardware or software errors related to the network adapters on this node. Also check for failures in any other network components to which the node is connected such as hubs, switches, or bridges.
```

2018, 2016 년 5 월 8 일에 도입 된 변경 내용은 클러스터 내 SMB 네트워크 세션 스토리지 공간 다이렉트에 대 한 SMB 복원 핸들을 추가 하는 누적 업데이트입니다. 일시적인 네트워크 오류에 대 한 복원 력을 개선 하 고 RoCE에서 네트워크 정체를 처리 하는 방법을 개선 하기 위해이 작업이 수행 되었습니다. 이러한 향상 된 기능으로 인해 SMB 연결을 다시 연결 하 고 노드를 다시 시작 하는 동안 시간이 초과 될 때까지 대기 시간이 초과 될 수도 있습니다. 이러한 문제는 스트레스 상태의 시스템에 영향을 줄 수 있습니다. 계획 되지 않은 가동 중지 시간 동안 시스템이 시간 초과 될 때까지 대기 하는 동안에는 최대 60 초의 IO 일시 중지가 관찰 됩니다. 이 문제를 해결 하려면 [10 월 18 일 2018, Windows Server 2016 이상 버전에 대 한 누적 업데이트](https://support.microsoft.com/help/4462928) 를 설치 합니다.

*참고* 이 업데이트는이 문제를 해결 하기 위해 SMB 연결 제한 시간을 사용 하 여 CSV 제한 시간을 조정 합니다. 해결 방법 섹션에 언급 된 라이브 덤프 생성을 사용 하지 않도록 설정 하기 위해 변경 내용을 구현 하지는 않습니다.

### <a name="shutdown-process-flow"></a>프로세스 흐름 종료:

1. VirtualDisk cmdlet을 실행 하 고 HealthStatus 값이 정상 인지 확인 합니다.
2. 다음 cmdlet을 실행 하 여 노드를 드레이닝 합니다.

   ```powershell
   Suspend-ClusterNode -Drain
   ```
3. 다음 cmdlet을 실행 하 여 해당 노드에 디스크를 저장소 유지 관리 모드로 전환 합니다. 

   ```powershell
   Get-StorageFaultDomain -type StorageScaleUnit | Where-Object {$_.FriendlyName -eq "<NodeName>"} | Enable-StorageMaintenanceMode
   ```
4. **PhysicalDisk** cmdlet을 실행 하 고 OperationalStatus 값이 유지 관리 모드에 있는지 확인 합니다.
5. **컴퓨터 다시 시작** cmdlet을 실행 하 여 노드를 다시 시작 합니다.
6. 노드가 다시 시작 된 후 다음 cmdlet을 실행 하 여 저장소 유지 관리 모드에서 해당 노드의 디스크를 제거 합니다.

   ```powershell
   Get-StorageFaultDomain -type StorageScaleUnit | Where-Object {$_.FriendlyName -eq "<NodeName>"} | Disable-StorageMaintenanceMode
   ```
7. 다음 cmdlet을 실행 하 여 노드를 다시 시작 합니다.

   ```powershell
   Resume-ClusterNode
   ```
8. 다음 cmdlet을 실행 하 여 다시 동기화 작업의 상태를 확인 합니다.

   ```powershell
   Get-StorageJob
   ```

### <a name="disabling-live-dumps"></a>라이브 덤프 사용 안 함
메모리가 많은 시스템에서 라이브 덤프 생성의 효과를 완화 하 고 스트레스 상태를 유지 하려면 라이브 덤프 생성을 사용 하지 않도록 설정 하는 것이 좋습니다. 아래에는 세 가지 옵션이 제공 됩니다.

>[!Caution]
>이 절차는 Microsoft 지원이 문제를 조사 하는 데 필요한 진단 정보 수집을 방지할 수 있습니다. 지원 에이전트는 특정 문제 해결 시나리오에 따라 실시간 덤프 생성을 다시 사용 하도록 요청 해야 할 수 있습니다.

아래에 설명 된 대로 라이브 덤프를 사용 하지 않도록 설정 하는 방법에는 두 가지가 있습니다.

#### <a name="method-1-recommended-in-this-scenario"></a>방법 1 (이 시나리오에서 권장)
실시간 덤프 시스템 전체를 비롯 한 모든 덤프를 완전히 사용 하지 않도록 설정 하려면 다음 단계를 수행 합니다.

1. 다음 레지스트리 키를 만듭니다. HKLM\System\CurrentControlSet\Control\CrashControl\ForceDumpsDisabled
2. 새 **ForceDumpsDisabled** 키에서 GUARDEDHOST로 REG_DWORD 속성을 만든 다음 해당 값을 0x10000000로 설정 합니다.
3. 각 클러스터 노드에 새 레지스트리 키를 적용 합니다.

>[!NOTE]
>N 설정이 변경 내용을 적용 하려면 컴퓨터를 다시 시작 해야 합니다.

이 레지스트리 키가 설정 된 후에는 실시간 덤프 만들기가 실패 하 고 "STATUS_NOT_SUPPORTED" 오류가 생성 됩니다.

#### <a name="method-2"></a>방법 2
기본적으로 Windows 오류 보고는 7 일 마다 보고서 유형별 LiveDump 하나만 허용 하 고 5 일간 컴퓨터 당 LiveDump 1 개만 허용 합니다. 다음 레지스트리 키를 설정 하 여 컴퓨터에서 한 LiveDump 사용 하도록 설정 하 여 변경할 수 있습니다.
```
reg add "HKLM\Software\Microsoft\Windows\Windows Error Reporting\FullLiveKernelReports" /v SystemThrottleThreshold /t REG_DWORD /d 0xFFFFFFFF /f
```
```
reg add "HKLM\Software\Microsoft\Windows\Windows Error Reporting\FullLiveKernelReports" /v ComponentThrottleThreshold /t REG_DWORD /d 0xFFFFFFFF /f
```

*참고* 변경 내용을 적용 하려면 컴퓨터를 다시 시작 해야 합니다.

### <a name="method-3"></a>방법 3
이벤트 5120가 기록 되는 경우와 같이 라이브 덤프의 클러스터 생성을 사용 하지 않도록 설정 하려면 다음 cmdlet을 실행 합니다.

```powershell
(Get-Cluster).DumpPolicy = ((Get-Cluster).DumpPolicy -band 0xFFFFFFFFFFFFFFFE)
```
이 cmdlet은 컴퓨터를 다시 시작 하지 않고 모든 클러스터 노드에 즉시 영향을 주지 않습니다.

## <a name="slow-io-performance"></a>저속 IO 성능

IO 성능이 느려지는 경우 스토리지 공간 다이렉트 구성에서 캐시가 사용 되는지 확인 합니다. 

확인 하는 방법에는 두 가지가 있습니다. 


1. 클러스터 로그를 사용 합니다. 선택한 텍스트 편집기에서 클러스터 로그를 열고 "[= = = SBL Disks = = =]"를 검색 합니다. 이는 로그가 생성 된 노드의 디스크 목록입니다. 

     캐시 사용 디스크 예: 여기서 상태는 CacheDiskStateInitializedAndBound 이며 여기에는 GUID가 있습니다. 

   ```
   [=== SBL Disks ===]
    {26e2e40f-a243-1196-49e3-8522f987df76},3,false,true,1,48,{1ff348f1-d10d-7a1a-d781-4734f4440481},CacheDiskStateInitializedAndBound,1,8087,54,false,false,HGST    ,HUH721010AL4200 ,        7PG3N2ER,A21D,{d5e27a3b-42fb-410a-81c6-9d8cc12da20c},[R/M 0 R/U 0 R/T 0 W/M 0 W/U 0 W/T 0],
    ```

    캐시 사용 안 함: 여기에서 GUID가 없고 상태는 CacheDiskStateNonHybrid입니다. 
    ```
   [=== SBL Disks ===]
    {426f7f04-e975-fc9d-28fd-72a32f811b7d},12,false,true,1,24,{00000000-0000-0000-0000-000000000000},CacheDiskStateNonHybrid,0,0,0,false,false,HGST    ,HUH721010AL4200 ,        7PGXXG6C,A21D,{d5e27a3b-42fb-410a-81c6-9d8cc12da20c},[R/M 0 R/U 0 R/T 0 W/M 0 W/U 0 W/T 0],
    ```

    캐시 사용 안 함: 모든 디스크가 동일한 유형 인 경우에는 기본적으로 사용 되지 않습니다. 여기에서 GUID가 없고 상태는 CacheDiskStateIneligibleDataPartition입니다. 
    ```
    {d543f90c-798b-d2fe-7f0a-cb226c77eeed},10,false,false,1,20,{00000000-0000-0000-0000-000000000000},CacheDiskStateIneligibleDataPartition,0,0,0,false,false,NVMe    ,INTEL SSDPE7KX02,  PHLF7330004V2P0LGN,0170,{79b4d631-976f-4c94-a783-df950389fd38},[R/M 0 R/U 0 R/T 0 W/M 0 W/U 0 W/T 0], 
    ```  
2. SDDCDiagnosticInfo에서 Get-PhysicalDisk 사용
    1. "$D = Export-clixml GetPhysicalDisk"를 사용 하 여 XML 파일을 엽니다.
    2. "Ipmo 저장소" 실행
    3. "$d"를 실행 합니다. 사용법은 자동 선택입니다. 필기장이 아니라 다음과 같은 출력이 표시 됩니다. 

   |FriendlyName|  SerialNumber| MediaType| CanPool| OperationalStatus| HealthStatus| 사용법| Size|
   |-----------|------------|---------| -------| -----------------| ------------| -----| ----|
   |NVMe INTEL SSDPE7KX02| PHLF733000372P0LGN| SSD| False|   확인|                정상|      1\.82 TB 자동 선택|
   |NVMe INTEL SSDPE7KX02 |PHLF7504008J2P0LGN| SSD|  False|    확인|                정상| 자동 선택| 1.82 TB|
   |NVMe INTEL SSDPE7KX02| PHLF7504005F2P0LGN| SSD|  False|  확인|                정상| 자동 선택| 1.82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF7504002A2P0LGN| SSD| False| 확인|    정상| 자동 선택| 1.82 TB|
   |NVMe INTEL SSDPE7KX02| PHLF7504004T2P0LGN |SSD| False|확인|       정상| 자동 선택| 1.82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF7504002E2P0LGN| SSD| False| 확인|      정상| 자동 선택| 1.82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF7330002Z2P0LGN| SSD| False| 확인|      정상|자동 선택| 1.82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF733000272P0LGN |SSD| False| 확인|  정상| 자동 선택| 1.82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF7330001J2P0LGN |SSD| False| 확인| 정상| 자동 선택| 1.82 TB|
   |NVMe INTEL SSDPE7KX02| PHLF733000302P0LGN |SSD| False| 확인|정상| 자동 선택| 1.82 TB|
   |NVMe INTEL SSDPE7KX02| PHLF7330004D2P0LGN |SSD| False| 확인| 정상| 자동 선택 |1.82 TB|

## <a name="how-to-destroy-an-existing-cluster-so-you-can-use-the-same-disks-again"></a>동일한 디스크를 다시 사용할 수 있도록 기존 클러스터를 제거 하는 방법

스토리지 공간 다이렉트 클러스터에서 스토리지 공간 다이렉트를 사용 하지 않도록 설정 하 고 [정리 드라이브](deploy-storage-spaces-direct.md#step-31-clean-drives)에 설명 된 정리 프로세스를 사용 하면 클러스터 된 저장소 풀은 계속 오프 라인 상태로 유지 되 고 상태 관리 서비스는 클러스터에서 제거 됩니다.

다음 단계는 가상 저장소 풀을 제거 하는 것입니다. 
   ```powershell
   Get-ClusterResource -Name "Cluster Pool 1" | Remove-ClusterResource
   ```

이제 모든 노드에 대해 **PhysicalDisk** 를 실행 하면 풀에 있던 모든 디스크가 표시 됩니다. 예를 들어 4 개 노드 클러스터와 4 개의 SAS 디스크가 있는 랩에서 각 노드에 각각 100GB를 표시 합니다. 이 경우 저장소 공간 다이렉트를 사용 하지 않도록 설정 하 여 SBL (저장소 버스 계층)를 제거 하 고 필터를 유지 합니다. **PhysicalDisk**를 실행 하면 로컬 OS 디스크를 제외 하 고 4 개의 디스크를 보고 해야 합니다. 대신 16을 보고 했습니다. 이는 클러스터의 모든 노드에 대해 동일 합니다. **디스크 가져오기** 명령을 실행 하면이 샘플 출력에 표시 된 것 처럼 로컬에 연결 된 디스크의 번호가 0, 1, 2 등으로 표시 됩니다.

|Number| 이름| 일련 번호|HealthStatus|OperationalStatus|전체 크기| 파티션 스타일|
|-|-|-|-|-|-|-|-|
|0|Msft Virtu ...  ||정상 | 온라인|  127 GB| GPT|
||Msft Virtu ... ||정상| 오프라인| 100GB| RAW|
||Msft Virtu ... ||정상| 오프라인| 100GB| RAW|
||Msft Virtu ... ||정상| 오프라인| 100GB| RAW|
||Msft Virtu ... ||정상| 오프라인| 100GB| RAW|
|1|Msft Virtu ...||정상| 오프라인| 100GB| RAW|
||Msft Virtu ... ||정상| 오프라인| 100GB| RAW|
|2|Msft Virtu ...||정상| 오프라인| 100GB| RAW|
||Msft Virtu ... ||정상| 오프라인| 100GB| RAW|
||Msft Virtu ... ||정상| 오프라인| 100GB| RAW|
||Msft Virtu ... ||정상| 오프라인| 100GB| RAW|
||Msft Virtu ... ||정상| 오프라인| 100GB| RAW|
|4|Msft Virtu ...||정상| 오프라인| 100GB| RAW|
|3|Msft Virtu ...||정상| 오프라인| 100GB| RAW|
||Msft Virtu ... ||정상| 오프라인| 100GB| RAW|
||Msft Virtu ... ||정상| 오프라인| 100GB| RAW|
||Msft Virtu ... ||정상| 오프라인| 100GB| RAW|


## <a name="error-message-about-unsupported-media-type-when-you-create-an-storage-spaces-direct-cluster-using-enable-clusters2d"></a>Enable-clusters2d를 사용 하 여 스토리지 공간 다이렉트 클러스터를 만들 때 "지원 되지 않는 미디어 유형"에 대 한 오류 메시지  

**Enable-clusters2d** cmdlet을 실행 하면 다음과 유사한 오류가 표시 될 수 있습니다.

![시나리오 6 오류 메시지](media/troubleshooting/scenario-error-message.png)

이 문제를 해결 하려면 hba 어댑터가 HBA 모드로 구성 되어 있는지 확인 합니다. RAID 모드에서 HBA를 구성 하지 않아야 합니다.  

## <a name="enable-clusterstoragespacesdirect-hangs-at-waiting-until-sbl-disks-are-surfaced-or-at-27"></a>사용-ClusterStorageSpacesDirect가 ' SBL 디스크가 표시 될 때까지 대기 ' 또는 27%에서 중단 됩니다.

유효성 검사 보고서에 다음 정보가 표시 됩니다.

    Disk <identifier> connected to node <nodename> returned a SCSI Port Association and the corresponding enclosure device could not be found. The hardware is not compatible with Storage Spaces Direct (S2D), contact the hardware vendor to verify support for SCSI Enclosure Services (SES). 


문제는 디스크와 HBA 카드 사이에 있는 HPE SAS 확장기 카드를 사용 하는 것입니다. SAS 확장기는 확장기에 연결 된 첫 번째 드라이브와 확장기 자체 사이에 중복 ID를 만듭니다.  이는 HPE 스마트 배열 [컨트롤러 SAS 확장기 펌웨어에서 해결 되었습니다. 4.02](https://support.hpe.com/hpsc/swd/public/detail?sp4ts.oid=7304566&swItemId=MTX_ef8d0bf4006542e194854eea6a&swEnvOid=4184#tab3).

## <a name="intel-ssd-dc-p4600-series-has-a-non-unique-nguid"></a>Intel SSD DC P4600 시리즈에 고유 하지 않은 guid가 있습니다.
아래 예제에서 Intel SSD DC P4600 시리즈 장치가 0100000001000000E4D25C000014E214 또는 0100000001000000E4D25C0000EEE214와 같은 여러 네임 스페이스에 대해 비슷한 16 바이트를 보고 하는 것 처럼 보이는 문제가 나타날 수 있습니다.


|               uniqueid               | deviceid | MediaType | BusType |               serialnumber               |      크기      | canpool | #b1 | OperationalStatus |
|--------------------------------------|----------|-----------|---------|------------------------------------------|----------------|---------|--------------|-------------------|
|           5000CCA251D12E30           |    0     |    HDD    |   SAS   |                 7PKR197G                 | 10000831348736 |  False  |     HGST     |  HUH721010AL4200  |
| 0100000001000000E4D25C000014E214 |    4     |    SSD    |  NVMe   | 0100_0000_0100_0000_E4D2_5C00_0014_E214. | 1600321314816  |  True   |    INTEL     |   SSDPE2KE016T7   |
| 0100000001000000E4D25C000014E214 |    5     |    SSD    |  NVMe   | 0100_0000_0100_0000_E4D2_5C00_0014_E214. | 1600321314816  |  True   |    INTEL     |   SSDPE2KE016T7   |
| 0100000001000000E4D25C0000EEE214 |    6     |    SSD    |  NVMe   | 0100_0000_0100_0000_E4D2_5C00_00EE_E214. | 1600321314816  |  True   |    INTEL     |   SSDPE2KE016T7   |
| 0100000001000000E4D25C0000EEE214 |    7     |    SSD    |  NVMe   | 0100_0000_0100_0000_E4D2_5C00_00EE_E214. | 1600321314816  |  True   |    INTEL     |   SSDPE2KE016T7   |

이 문제를 해결 하려면 Intel 드라이브의 펌웨어를 최신 버전으로 업데이트 합니다.  2018 년 5 월의 펌웨어 버전 QDV101B1이 문제를 해결 하는 것으로 알려져 있습니다.

[INTEL Ssd 데이터 센터 도구의 2018 년 5 월 릴리스](https://downloadmirror.intel.com/27778/eng/Intel_SSD_Data_Center_Tool_3_0_12_Release_Notes_330715-026.pdf) 는 INTEL Ssd DC P4600 시리즈에 대 한 펌웨어 업데이트 QDV101B1를 포함 합니다.


## <a name="physical-disk-healthy-and-operational-status-is-removing-from-pool"></a>실제 디스크 "정상" 및 작동 상태는 "풀에서 제거"입니다. 

Windows Server 2016 스토리지 공간 다이렉트 클러스터에는 하나 이상의 실제 디스크에 대 한 HealthStatus가 "정상" 상태이 고, OperationalStatus는 "(풀에서 제거, 확인)" 이라고 표시 될 수 있습니다. 

"풀에서 제거"는 **PhysicalDisk** 가 호출 되었지만 상태를 유지 하기 위해 상태에 저장 되 고 제거 작업이 실패 하는 경우 복구를 허용 하는 경우 의도 집합입니다. 다음 방법 중 하나를 사용 하 여 수동으로 OperationalStatus를 정상으로 변경할 수 있습니다.

- 풀에서 실제 디스크를 제거한 다음 다시 추가 하십시오.
- [Clear-PhysicalDiskHealthData 스크립트](https://go.microsoft.com/fwlink/?linkid=2034205) 를 실행 하 여 의도를 지웁니다. 로 다운로드할 수 있습니다. TXT 파일. 로 저장 해야 합니다. PS1 파일을 실행할 수 있습니다.

스크립트를 실행 하는 방법을 보여 주는 몇 가지 예는 다음과 같습니다.

- 대상 매개 **변수** 를 사용 하 여 정상으로 설정 해야 하는 디스크를 지정 합니다. **WMI MSFT_PhysicalDisk** 또는 **PhysicalDisk**에서 일련 번호를 가져올 수 있습니다. (아래 일련 번호에 0을 사용 하는 것입니다.)

   ```powershell
   Clear-PhysicalDiskHealthData -Intent -Policy -SerialNumber 000000000000000 -Verbose -Force
    ```

- **UniqueId** 매개 변수를 사용 하 여 디스크를 지정 합니다 ( **WMI MSFT_PhysicalDisk** 또는 **PhysicalDisk**에서 다시 지정).

   ```powershell
   Clear-PhysicalDiskHealthData -Intent -Policy -UniqueId 00000000000000000 -Verbose -Force
   ```

## <a name="file-copy-is-slow"></a>파일 복사 속도가 느립니다.

파일 탐색기를 사용 하 여 가상 디스크에 큰 VHD를 복사 하는 데 문제가 있을 수 있습니다. 파일 복사본이 예상 보다 오래 걸리고 있습니다.

파일 탐색기, Robocopy 또는 Xcopy를 사용 하 여 가상 디스크에 대량 VHD를 복사 하는 것은 예상 된 성능 보다 느릴 수 있으므로 권장 되는 방법이 아닙니다. 복사 프로세스는 저장소 스택에서 더 낮은 위치에 배치 되 고 대신 로컬 복사 프로세스 처럼 동작 하는 스토리지 공간 다이렉트 스택을 통해 이동 하지 않습니다.

스토리지 공간 다이렉트 성능을 테스트 하려는 경우 VMFleet 및 Diskspd를 사용 하 여 서버를 로드 하 고 스트레스 테스트 하 여 기본 줄을 가져오고 스토리지 공간 다이렉트 성능의 기대를 설정 하는 것이 좋습니다.

## <a name="expected-events-that-you-would-see-on-rest-of-the-nodes-during-the-reboot-of-a-node"></a>노드를 다시 부팅 하는 동안 나머지 노드에 표시 되는 예상 이벤트입니다. 

이러한 이벤트는 무시 해도 됩니다. 

    Event ID 205: Windows lost communication with physical disk {XXXXXXXXXXXXXXXXXXXX }. This can occur if a cable failed or was disconnected, or if the disk itself failed. 

    Event ID 203: Windows lost communication with physical disk {xxxxxxxxxxxxxxxxxxxxxxxx }. This can occur if a cable failed or was disconnected, or if the disk itself failed. 

Azure Vm을 실행 하는 경우이 이벤트를 무시할 수 있습니다.

    Event ID 32: The driver detected that the device \Device\Harddisk5\DR5 has its write cache enabled. Data corruption may occur. 

## <a name="slow-performance-or-lost-communication-io-error-detached-or-no-redundancy-errors-for-deployments-that-use-intel-p3x00-nvme-devices"></a>Intel P3x00 NVMe 장치를 사용 하는 배포에 대 한 성능 저하 또는 "통신 끊김", "IO 오류", "분리 됨" 또는 "중복성 없음" 오류

"Maintenance 릴리스 8" 이전 펌웨어 버전을 사용 하는 P3x00 NVMe (NVM Express) 장치의 Intel 제품군에 따라 하드웨어를 사용 하는 일부 스토리지 공간 다이렉트 사용자에 게 영향을 주는 중요 한 문제가 확인 되었습니다. 

>[!NOTE]
> 개별 Oem에는 고유한 펌웨어 버전 문자열을 사용 하는 NVMe 장치의 Intel P3x00 제품군을 기반으로 하는 장치가 있을 수 있습니다. 최신 펌웨어 버전에 대 한 자세한 내용은 OEM에 문의 하세요.

Intel P3x00 NVMe 장치에 따라 배포에 하드웨어를 사용 하는 경우 사용 가능한 최신 펌웨어를 즉시 적용 하는 것이 좋습니다 (최소 유지 관리 릴리스 8). 이 [Microsoft 지원 문서](https://support.microsoft.com/help/4052341/slow-performance-or-lost-communication-io-error-detached-or-no-redunda) 에서는이 문제에 대 한 추가 정보를 제공 합니다. 
