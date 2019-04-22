---
title: 저장소 공간 다이렉트 문제 해결
description: 저장소 공간 다이렉트 배포 문제를 해결 하는 방법을 알아봅니다.
keywords: 저장소 공간
ms.prod: windows-server-threshold
ms.author: ''
ms.technology: storage-spaces
ms.topic: article
author: kaushika-msft
ms.date: 10/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: ecf3cb5703a90976dce15abbd0c9fdd1d4aa24ec
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812634"
---
# <a name="troubleshoot-storage-spaces-direct"></a>저장소 공간 다이렉트 해결

저장소 공간 다이렉트 배포 문제를 해결 하려면 다음 정보를 사용 합니다.

일반적으로 다음 단계를 시작 합니다.

1. SSD의 메이커/모델은 Windows Server 카탈로그를 사용 하 여 Windows Server 2016에 대해 인증을 확인 합니다. 저장소 공간 다이렉트에 대 한 드라이브는 지원 되는 공급 업체를 사용 하 여 확인 합니다.
2. 잘못 된 모든 드라이브에 대 한 저장소를 검사 합니다. 저장소 관리 소프트웨어를 사용 하 여 드라이브의 상태를 확인 합니다. 드라이브의 있는 경우 결함이 있는, 공급 업체와 함께 작동 합니다. 
3. 저장소를 업데이트 하 고 필요한 경우에 드라이브 펌웨어.
   모든 노드에 설치 된 최신 Windows 업데이트를 확인 합니다. Windows Server 2016에 대 한 최신 업데이트를 가져올 수 있습니다 [ https://aka.ms/update2016 ](https://aka.ms/update2016)합니다.
4. 네트워크 어댑터 드라이버 및 펌웨어를 업데이트 합니다.
5. 클러스터 유효성 검사를 실행 하 고 저장소 공간 다이렉트 섹션을 검토, 캐시에 사용 되는 드라이브는 올바르게 보고 확인 하 고 오류 없이 합니다.

여전히 문제가 발생 하는, 하는 경우 아래의 시나리오를 검토 합니다.

## <a name="virtual-disk-resources-are-in-no-redundancy-state"></a>가상 디스크 리소스가 없는 중복 상태
저장소 공간 다이렉트 시스템의 노드 작동 중단 이나 정전이 오류로 인해 예기치 않게 다시 시작합니다. 그런 다음 하나 이상의 가상 디스크를 온라인 상태로 전환 될 수 있습니다 하 고 설명을 "중복 정보가 부족 합니다."를 참조 하세요
    
|FriendlyName|ResiliencySettingName| OperationalStatus| HealthStatus| IsManualAttach|크기| PSComputerName|
|------------|---------------------| -----------------| ------------| --------------|-----| --------------|
|Disk4| Mirror| 확인|  정상| True|  10TB|  노드-01.conto...|
|Disk3         |Mirror                 |확인                          |정상       |True            |10TB | 노드-01.conto...|
|Disk2         |Mirror                 |중복 되지 않은               |Unhealthy     |True            |10TB | 노드-01.conto...|
|Disk1         |Mirror                 |{No Redundancy, InService}  |Unhealthy     |True            |10TB | 노드-01.conto...| 

또한 가상 디스크를 온라인 상태로 전환 하려고를 시도한 후 다음 정보를 (DiskRecoveryAction) 클러스터 로그에 기록 됩니다.  

```
[Verbose] 00002904.00001040::YYYY/MM/DD-12:03:44.891 INFO [RES] Physical Disk <DiskName>: OnlineThread: SuGetSpace returned 0.
[Verbose] 00002904.00001040:: YYYY/MM/DD -12:03:44.891 WARN [RES] Physical Disk < DiskName>: Underlying virtual disk is in 'no redundancy' state; its volume(s) may fail to mount.
[Verbose] 00002904.00001040:: YYYY/MM/DD -12:03:44.891 ERR [RES] Physical Disk <DiskName>: Failing online due to virtual disk in 'no redundancy' state. If you would like to attempt to online the disk anyway, first set this resource's private property 'DiskRecoveryAction' to 1. We will try to bring the disk online for recovery, but even if successful, its volume(s) or CSV may be unavailable. 
``` 

합니다 **No 중복 작업 상태** 디스크 실패 한 경우 또는 시스템 데이터 가상 디스크에 액세스할 수 없는 경우 발생할 수 있습니다. 이 문제는 노드에서 유지 관리 하는 동안 노드 다시 부팅 하는 경우에 발생할 수 있습니다.
    
이 문제를 해결 하려면 다음이 단계를 수행 합니다.

1. CSV에서 영향을 받는 가상 디스크를 제거 합니다. 그러면 클러스터의 "Available storage" 그룹에 배치 되 고 "Physical Disk"의 ResourceType 표시 시작

   ```powershell
   Remove-ClusterSharedVolume -name "VdiskName"
   ``` 
2. 사용 가능한 저장소 그룹을 소유한 노드에서 아니요 중복성 상태에 있는 모든 디스크에서 다음 명령을 실행 합니다. "Available Storage" 그룹은 어떤 노드를 식별 하려면 다음 명령을 실행 수 있습니다.

   ```powershell
   Get-ClusterGroup
   ```
3. 디스크 복구 동작을 설정 하 고 디스크를 시작 합니다.
   ```powershell
   Get-ClusterResource "VdiskName" | Set-ClusterParameter -Name DiskRecoveryAction -Value 1
   Start-ClusterResource -Name "VdiskName"
   ```
4. 복구를 자동으로 시작 해야 합니다. 복구가 완료 될 때까지 기다립니다. 일시 중단 된 상태로 전환 하 고 다시 시작 될 수 있습니다. 진행을 모니터링 합니다. 
    - 실행할 **Get-storagejob** 복구의 상태를 모니터링 하 고 완료 되 면 볼 수 있습니다.
    - 실행할 **Get-virtualdisk** 공간 HealthStatus의 상태가 정상인 반환 하는지 확인 합니다.
5. 복구 후 완료 되 고 가상 디스크는 정상, 가상 디스크 매개 변수를 다시 변경 됩니다.

   ```powershell
    Get-ClusterResource "VdiskName" | Set-ClusterParameter -Name DiskRecoveryAction -Value 0
   ```
6. 오프 라인 이며 다시 적용 DiskRecoveryAction 할 다음 온라인 디스크를 수행 합니다.

   ```powershell
   Stop-ClusterResource "VdiskName"
   Start-ClusterResource "VdiskName"
   ``` 
7. CSV로 다시 영향을 받는 가상 디스크를 추가 합니다.

   ```powershell
   Add-ClusterSharedVolume -name "VdiskName"
   ```

**DiskRecoveryAction** 는 공간 볼륨 검사 없이 읽기 / 쓰기 모드를 연결할 수 있는 재정의 스위치입니다. 속성을 사용 하는 볼륨이 온라인 상태가 되지 않습니다 이유를 진단을 수행할 수 있습니다. 유지 관리 모드 매우 유사 하지만 실패 함 상태인 리소스에 대해 호출할 수 있습니다. 또한 액세스를 얻을 수 있는 "No 중복성" 같은 상황에서 유용할 수 있는 데이터에 액세스할 수 있습니다 모든 데이터를 복사 합니다. DiskRecoveryAction 속성을 22 2018 년 2 월 업데이트 (kb) 4077525에에서 추가 되었습니다.
    
    
## <a name="detached-status-in-a-cluster"></a>클러스터에서 분리 된 상태 

실행 하는 경우는 **Get-virtualdisk** 하나 이상의 저장소 공간 다이렉트는 가상 디스크를 분리할 OperationalStatus cmdlet. 그러나 의해 보고 된 HealthStatus 합니다 **Get-physicaldisk** cmdlet 정상 상태로 있는 모든 실제 디스크를 나타냅니다.

다음은 출력의 예는 **Get-virtualdisk** cmdlet.

|FriendlyName|  ResiliencySettingName|  OperationalStatus|   HealthStatus|  IsManualAttach|  크기|   PSComputerName|
|-|-|-|-|-|-|-|
|Disk4|         Mirror|                 확인|                  정상|       True|            10TB|  노드-01.conto...|
|Disk3|         Mirror|                 확인|                  정상|       True|            10TB|  노드-01.conto...|
|Disk2|         Mirror|                 Detached|            알 수 없음|       True|            10TB|  노드-01.conto...|
|Disk1|         Mirror|                 Detached|            알 수 없음|       True|            10TB|  노드-01.conto...| 


또한 다음 이벤트 노드에 기록 될 수 있습니다.

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

합니다 **분리 된 작업 상태** 를 영역 (DRT) 추적 로그가 꽉 찬 경우 발생할 수 있습니다. 저장소 공간 영역 (DRT) 미러 공간에 대 한 추적을 사용 하 여 전원 오류가 발생 하는 경우 저장소 공간 다시 실행 하거나 실행 취소 작업에 유연한 저장소 공간을 다시 바인딩할 수 있도록 메타 데이터에 대 한 진행 중인 업데이트가 기록 됩니다 있는지 확인 하려면 전원이 복원 되 면 일관 된 상태와 시스템을 다시 작동 하며 DRT 로그가 꽉 차면 DRT 메타 데이터를 동기화 하 고 플러시될 때까지 가상 디스크가 온라인 상태가 없습니다. 이 프로세스를 완료 하려면 몇 시간이 걸릴 수 있는 전체 검색을 실행 해야 합니다.
    
이 문제를 해결 하려면 다음이 단계를 수행 합니다.
1. CSV에서 영향을 받는 가상 디스크를 제거 합니다.

   ```powershell
   Remove-ClusterSharedVolume -name "VdiskName"
   ``` 
2. 온라인 상태로 전환 하지 되는 모든 디스크에서 다음 명령을 실행 합니다. 

   ```powershell
   Get-ClusterResource -Name "VdiskName" | Set-ClusterParameter DiskRunChkDsk 7
   Start-ClusterResource -Name "VdiskName"
   ``` 
3. 분리 된 볼륨이 온라인 상태가 있는 모든 노드에서 다음 명령을 실행 합니다. 

   ```powershell
   Get-ScheduledTask -TaskName "Data Integrity Scan for Crash Recovery" | Start-ScheduledTask 
   ```
   이 태스크는 분리 된 볼륨이 온라인 상태가 되는 모든 노드를 시작 합니다. 복구를 자동으로 시작 해야 합니다. 복구가 완료 될 때까지 기다립니다. 일시 중단 된 상태로 전환 하 고 다시 시작 될 수 있습니다. 진행을 모니터링 합니다. 
   - 실행할 **Get-storagejob** 복구의 상태를 모니터링 하 고 완료 되 면 볼 수 있습니다.
   -  실행할 **Get-virtualdisk** 공간 반환 된 HealthStatus의 정상 상태 확인 합니다.
    - "데이터 무결성 검사에 대 한 크래시 복구" 저장소 작업으로 표시 되지 않는 작업은 이며 진행률 표시기가 없습니다. 태스크를 표시 하는 경우 실행 중으로 실행 합니다. 완료 되 면 완료 표시 됩니다.
    
       또한 다음 cmdlet을 사용 하 여 실행 중인 일정 작업의 상태를 볼 수 있습니다. 
       ```powershell
       Get-ScheduledTask | ? State -eq running
       ``` 
4. "데이터 무결성 검사에 대 한 크래시 복구" 완료 되 면 즉시 복구 완료 되 고 가상 디스크 정상, 가상 디스크 매개 변수를 다시 변경 됩니다. 

   ```powershell
   Get-ClusterResource -Name "VdiskName" | Set-ClusterParameter DiskRunChkDsk 0 
   ```
5. CSV로 다시 영향을 받는 가상 디스크를 추가 합니다.    

   ```powershell
   Add-ClusterSharedVolume -name "VdiskName"
   ```  
**DiskRunChkdsk 값 7** 공간 볼륨을 연결 하 고 읽기 전용 모드에서 파티션을 하는 데 사용 됩니다. 이 공간을 직접 검색 하 고 치료할 트리거하여 복구를 통해. 복구를 실행 하는 한 번 자동으로 탑재 합니다. 또한 모든 데이터를 복사할 수에 대 한 액세스는 데 도움이 될 수 있는 데이터에 액세스할 수 있습니다. 전체 DRT 로그와 같은 일부 오류 조건에 대 한 크래시 복구 예약 된 작업에 대 한 데이터 무결성 검사를 실행 해야 합니다.
    
**크래시 복구 작업에 대 한 데이터 무결성 검사** 동기화 및 전체 영역 (DRT) 추적 로그의 선택을 취소 하는 데 사용 됩니다. 이 작업을 완료 하는 데 몇 시간이 걸릴 수 있습니다. "데이터 무결성 검사에 대 한 크래시 복구" 저장소 작업으로 표시 되지 않는 작업은 이며 진행률 표시기가 없습니다. 태스크를 표시 하는 경우 실행 중으로 실행 합니다. 완료 되 면 완료 된 것으로 표시 됩니다. 작업을 취소 하거나이 작업이 실행 되는 동안에 노드를 다시 시작 하는 경우 태스크는 처음부터 다시 시작 해야 합니다.

자세한 내용은 [저장소 공간 다이렉트 문제 해결 상태 및 작동 상태](storage-spaces-states.md)합니다.
    
## <a name="event-5120-with-statusiotimeout-c00000b5"></a>STATUS_IO_TIMEOUT c00000b5 5120 이벤트 

>[! 중요 한} 수정 된 업데이트를 적용 하는 동안 이러한 현상이 발생할 가능성을 줄이기 위해 것이 좋습니다 저장소 유지 관리 모드 아래 절차를 설치 하는 [2018 년 10 월 18 일 Windows Server 2016 용 누적 업데이트 ](https://support.microsoft.com/help/4462928) 노드에서 현재 설치 된 Windows Server 2016 누적 업데이트에서 출시 된 경우 이상 버전 [2018 년 5 월 8 일](https://support.microsoft.com/help/4103723) 하 [2018 년 10 월 9 일](https://support.microsoft.com/help/KB4462917)합니다.

Windows Server 2016에서에서 발표 된 누적 업데이트를 사용 하 여 노드를 다시 시작한 후 이벤트 5120 STATUS_IO_TIMEOUT c00000b5 사용 하 여 발생할 수 있습니다 [8 2018 년 5 월 KB 4103723](https://support.microsoft.com/help/4103723) 에 [2018 년 10 월 9, KB 4462917](https://support.microsoft.com/help/4462917)설치 합니다.

노드를 다시 시작 하면 다음 오류 코드 중 하나가 포함 되어 있습니다 이벤트 5120 시스템 이벤트 로그에 기록 됩니다.

```
Event Source: Microsoft-Windows-FailoverClustering
Event ID: 5120
Description:    Cluster Shared Volume 'CSVName' ('Cluster Virtual Disk (CSVName)') has entered a paused state because of 'STATUS_IO_TIMEOUT(c00000b5)'. All I/O will temporarily be queued until a path to the volume is reestablished. 

Cluster Shared Volume ‘CSVName’ ('Cluster Virtual Disk (CSVName)') has entered a paused state because of 'STATUS_CONNECTION_DISCONNECTED(c000020c)'. All I/O will temporarily be queued until a path to the volume is reestablished.    
```

이벤트 5120는 기록 되 면 추가 증상을 일으킵니다 또는 성능 영향을 미칠 수 있는 디버깅 정보를 수집 하는 라이브 덤프 생성 됩니다. 라이브 덤프 생성 잠시 스냅숏을 메모리 덤프 파일에 쓸 수 있도록 만듭니다. 시스템 메모리를 많이 고 스트레스 상태에서 노드를 클러스터 멤버 자격에서 삭제 하 고 기록할 다음 이벤트 1135로 인해 발생할 수 있습니다.

```
Event source: Microsoft-Windows-FailoverClustering
Event ID: 1135  
Description: Cluster node 'NODENAME'was removed from the active failover cluster membership. The Cluster service on this node may have stopped. This could also be due to the node having lost communication with other active nodes in the failover cluster. Run the Validate a Configuration wizard to check your network configuration. If the condition persists, check for hardware or software errors related to the network adapters on this node. Also check for failures in any other network components to which the node is connected such as hubs, switches, or bridges.
```

저장소 공간 다이렉트 클러스터 간 SMB 네트워크 세션에 대 한 SMB 복원 력 있는 처리를 추가 하려면 2018 년 5 월 8 일 누적 업데이트에서 변경 내용을 도입 되었습니다. 이렇게 일시적인 네트워크 오류에 대 한 탄력성 RoCE 네트워크 정체를 처리 하는 방법을 개선할 수 있습니다.

이러한 향상 된이 기능 또한 실수로 증가 SMB 연결에 다시 연결 하려고 하는 경우 시간 제한 및 제한 시간 대기 노드를 다시 시작할 때. 이러한 문제는 시스템은 부하가 발생할 수 있습니다. 계획 되지 않은 가동 중지 시간 중 최대 60 초 일시 중지 IO도 관찰 한 시스템 연결 제한 시간을 대기 하는 동안.

이 문제를 해결 하려면 설치 합니다 [2018 년 10 월 18 일 Windows Server 2016 용 누적 업데이트](https://support.microsoft.com/help/4462928) 이상 버전.

*참고* 이 업데이트에는이 문제를 해결 하려면 SMB 연결 시간 제한이 있는 CSV 제한 맞춥니다. 해결 방법 섹션에 언급 된 라이브 덤프 생성 하지 않으려면 변경 내용을 구현 하지 않습니다.
    
### <a name="shutdown-process-flow"></a>종료 프로세스 흐름:

1. Get-virtualdisk cmdlet을 실행 하 고 HealthStatus 값 정상 인지 확인 합니다.
2. 다음 cmdlet을 실행 하 여 노드를 드레이닝:

   ```powershell
   Suspend-ClusterNode -Drain
   ```
3. 다음 cmdlet을 실행 하 여 저장소 유지 관리 모드에서 해당 노드에서 디스크를 넣습니다. 

   ```powershell
   Get-StorageFaultDomain -type StorageScaleUnit | Where-Object {$_.FriendlyName -eq "<NodeName>"} | Enable-StorageMaintenanceMode
   ```
4. 실행 된 **Get-physicaldisk** cmdlet OperationalStatus 값을 유지 관리 모드 인지 확인 합니다.
5. 실행 합니다 **Restart-computer** 노드를 다시 시작 하는 cmdlet입니다.
6. 노드를 다시 시작한 후 다음 cmdlet을 실행 하 여 해당 노드에서 디스크 저장소 유지 관리 모드에서 제거 합니다.

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

### <a name="disabling-live-dumps"></a>라이브 덤프를 사용 하지 않도록 설정
라이브 덤프 생성 메모리가 많이 있고 부하가 시스템의 효과 완화 하려면 라이브 덤프 생성을 사용 하지 않도록 설정 하려면 또한 있습니다. 아래 세 가지 옵션이 제공 됩니다.

>[!Caution]
>이 절차는 Microsoft 지원이이 문제를 조사 해야 하는 진단 정보의 컬렉션을 방지할 수 있습니다. 지원 에이전트를 다시 특정 문제 해결 시나리오를 기반으로 하는 라이브 덤프 생성을 활성화 하도록 요청 해야 할 수 있습니다.

아래 설명 된 대로 라이브 덤프를 사용 하지 않도록 설정 하는 두 가지 방법 있습니다.

#### <a name="method-1-recommended-in-this-scenario"></a>메서드 1 (이 시나리오에 권장)
완전히 라이브 덤프 시스템 전체를 포함 하 여 모든 덤프를 사용 하지 않도록 설정 하려면 다음이 단계를 수행 합니다.

1. 다음 레지스트리 키를 만듭니다. HKLM\System\CurrentControlSet\Control\CrashControl\ForceDumpsDisabled
2. 새 **ForceDumpsDisabled** 키 GuardedHost,으로 REG_DWORD 속성을 만들고 다음 0x10000000로 해당 값을 설정 합니다.
3. 각 클러스터 노드에 새 레지스트리 키를 적용 합니다.

>[!NOTE]
>레지스트리 변경 내용을 적용 하려면 컴퓨터를 다시 시작 해야 합니다.

이 레지스트리 키 설정, 라이브 되 면 덤프 만들기는 실패 하 고 "STATUS_NOT_SUPPORTED" 오류가 생성 됩니다.

#### <a name="method-2"></a>방법 2
기본적으로 Windows 오류 보고 하면 보고서 형식에 따라 7 일 동안 하나의 LiveDump 및 5 일 마다 컴퓨터 당 하나만 LiveDump 있습니다. 다음 레지스트리 키만을 허용 하도록 하나 LiveDump 컴퓨터에서 영구적으로 설정 하 여 변경할 수 있습니다.
```
reg add "HKLM\Software\Microsoft\Windows\Windows Error Reporting\FullLiveKernelReports" /v SystemThrottleThreshold /t REG_DWORD /d 0xFFFFFFFF /f
```
```
reg add "HKLM\Software\Microsoft\Windows\Windows Error Reporting\FullLiveKernelReports" /v ComponentThrottleThreshold /t REG_DWORD /d 0xFFFFFFFF /f
```

*참고* 변경 내용을 적용 하려면 컴퓨터를 다시 시작 해야 합니다.

### <a name="method-3"></a>방법 3
라이브 덤프 (예: 이벤트 5120는 기록 되는 경우)의 클러스터 생성을 사용 하지 않으려면 다음 cmdlet을 실행 합니다.

```powershell
(Get-Cluster).DumpPolicy = ((Get-Cluster).DumpPolicy -band 0xFFFFFFFFFFFFFFFE)
```
이 cmdlet은 컴퓨터를 다시 시작 하지 않고 모든 클러스터 노드에서 즉시 영향을 미칩니다.
    
## <a name="slow-io-performance"></a>느린 IO 성능

IO 성능 저하, 표시 되는 경우에 캐시 저장소 공간 다이렉트 구성에서 사용 되는지 여부를 확인 합니다. 

두 가지 방법으로 검사할 수 있습니다. 
     
 
1. 클러스터 로그를 사용합니다. 원하는 텍스트 편집기에서 클러스터 로그를 열고 검색 "[=== SBL 디스크 ===]." 이 로그에 생성 된 노드에서 디스크 목록이 됩니다. 

     캐시는 디스크 예제를 사용 합니다. 상태가 CacheDiskStateInitializedAndBound을 여기 있는 GUID가 다음 note 합니다. 

   ```
   [=== SBL Disks ===]
    {26e2e40f-a243-1196-49e3-8522f987df76},3,false,true,1,48,{1ff348f1-d10d-7a1a-d781-4734f4440481},CacheDiskStateInitializedAndBound,1,8087,54,false,false,HGST    ,HUH721010AL4200 ,        7PG3N2ER,A21D,{d5e27a3b-42fb-410a-81c6-9d8cc12da20c},[R/M 0 R/U 0 R/T 0 W/M 0 W/U 0 W/T 0],
    ```

    캐시를 사용할 수 없습니다. 여기서 GUID가 없는 표시 되며 상태 CacheDiskStateNonHybrid 볼 수 있습니다. 
    ```
   [=== SBL Disks ===]
    {426f7f04-e975-fc9d-28fd-72a32f811b7d},12,false,true,1,24,{00000000-0000-0000-0000-000000000000},CacheDiskStateNonHybrid,0,0,0,false,false,HGST    ,HUH721010AL4200 ,        7PGXXG6C,A21D,{d5e27a3b-42fb-410a-81c6-9d8cc12da20c},[R/M 0 R/U 0 R/T 0 W/M 0 W/U 0 W/T 0],
    ```

    캐시를 사용할 수 없습니다. 동일한 형식 사례의 모든 디스크의 경우 기본적으로 사용 되지 않습니다. 여기서 GUID가 없는 표시 되며 상태 CacheDiskStateIneligibleDataPartition 볼 수 있습니다. 
    ```
    {d543f90c-798b-d2fe-7f0a-cb226c77eeed},10,false,false,1,20,{00000000-0000-0000-0000-000000000000},CacheDiskStateIneligibleDataPartition,0,0,0,false,false,NVMe    ,INTEL SSDPE7KX02,  PHLF7330004V2P0LGN,0170,{79b4d631-976f-4c94-a783-df950389fd38},[R/M 0 R/U 0 R/T 0 W/M 0 W/U 0 W/T 0], 
    ```  
2. Get-PhysicalDisk.xml는 SDDCDiagnosticInfo에서 사용 하 여
    1. 사용 하 여 XML 파일을 열고 "$d Import-clixml GetPhysicalDisk.XML ="
    2. "Ipmo 저장소"를 실행 합니다.
    3. "$d"를 실행 합니다. 사용 되지 저널 있습니다 Auto-select는 다음과 같은 출력이 표시 됩니다. 

   |FriendlyName|  SerialNumber| MediaType| CanPool| OperationalStatus| HealthStatus| 사용법| 크기|
   |-----------|------------|---------| -------| -----------------| ------------| -----| ----|
   |NVMe INTEL SSDPE7KX02| PHLF733000372P0LGN| SSD| False|   확인|                정상|      자동 선택 1.82 TB|
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
    
## <a name="how-to-destroy-an-existing-cluster-so-you-can-use-the-same-disks-again"></a>와 동일한 디스크를 다시 사용할 수 있도록 기존 클러스터를 삭제 하는 방법

저장소 공간 다이렉트 클러스터에서 한 번 저장소 공간 다이렉트를 사용 하지 않도록 하에 설명 된 정리 프로세스를 사용 하 여 [드라이브 청소](deploy-storage-spaces-direct.md#step-31-clean-drives), 오프 라인 상태로 남아 클러스터 된 저장소 풀 및 상태 관리 서비스에서 제거 됩니다 클러스터입니다.

다음 단계는 가상 저장소 풀을 제거 하려면: 
   ```powershell
   Get-ClusterResource -Name "Cluster Pool 1" | Remove-ClusterResource
   ```

실행 하는 경우 이제 **Get-physicaldisk** 노드 중 하나에서 풀에 있던 모든 디스크를 확인할 수 있습니다. 예를 들어, 랩에서 4 개 노드 클러스터와 4 개의 SAS 디스크를 사용 하 여 각각 100GB 각 노드에 표시 됩니다. 이 경우 저장소 공간 다이렉트는 비활성화 되는 SBL (저장소 버스 계층)을 제거 되지만 필터를 실행 하는 경우 **Get-physicaldisk**, 로컬 OS 디스크를 제외 하는 4 개의 디스크를 보고 해야 합니다. 대신이 16 대신 보고 합니다. 클러스터의 모든 노드에 대해 동일합니다. 실행 하는 경우는 **Get-disk** 명령 예제 출력에서 볼 수 있듯이 로컬로 연결된 된 디스크 0, 1, 2, 등으로 번호가 표시 됩니다.

|Number| 이름| 일련 번호|HealthStatus|OperationalStatus|총 크기| 파티션 스타일|
|-|-|-|-|-|-|-|-|
|0|Msft Virtu...  ||정상 | 온라인|  127GB| GPT|
||Msft Virtu... ||정상| 오프라인| 100GB| RAW|
||Msft Virtu... ||정상| 오프라인| 100GB| RAW|
||Msft Virtu... ||정상| 오프라인| 100GB| RAW|
||Msft Virtu... ||정상| 오프라인| 100GB| RAW|
|1|Msft Virtu...||정상| 오프라인| 100GB| RAW|
||Msft Virtu... ||정상| 오프라인| 100GB| RAW|
|2|Msft Virtu...||정상| 오프라인| 100GB| RAW|
||Msft Virtu... ||정상| 오프라인| 100GB| RAW|
||Msft Virtu... ||정상| 오프라인| 100GB| RAW|
||Msft Virtu... ||정상| 오프라인| 100GB| RAW|
||Msft Virtu... ||정상| 오프라인| 100GB| RAW|
|4|Msft Virtu...||정상| 오프라인| 100GB| RAW|
|3|Msft Virtu...||정상| 오프라인| 100GB| RAW|
||Msft Virtu... ||정상| 오프라인| 100GB| RAW|
||Msft Virtu... ||정상| 오프라인| 100GB| RAW|
||Msft Virtu... ||정상| 오프라인| 100GB| RAW|

    
## <a name="error-message-about-unsupported-media-type-when-you-create-an-storage-spaces-direct-cluster-using-enable-clusters2d"></a>"지원 되지 않는 미디어 유형"에 대 한 오류 메시지 Enable-ClusterS2D를 사용 하 여 저장소 공간 다이렉트 클러스터를 만들 때  

실행 하면 다음과 유사한 오류가 표시 될 수 있습니다 합니다 **Enable-ClusterS2D** cmdlet:

![시나리오 6 오류 메시지](media/troubleshooting/scenario-error-message.png)

이 문제를 해결 하려면 HBA 어댑터 HBA 모드로 구성 된를 확인 합니다. 없는 HBA RAID 모드로 구성 되어야 합니다.  
    
## <a name="enable-clusterstoragespacesdirect-hangs-at-waiting-until-sbl-disks-are-surfaced-or-at-27"></a>Enable-clusterstoragespacesdirect 27% 또는 'SBL까지 디스크는 표시'에서 중단 됩니다.

유효성 검사 보고서에서 다음 정보를 표시 됩니다.

    Disk <identifier> connected to node <nodename> returned a SCSI Port Association and the corresponding enclosure device could not be found. The hardware is not compatible with Storage Spaces Direct (S2D), contact the hardware vendor to verify support for SCSI Enclosure Services (SES). 
    
  
디스크와 HBA 카드 사이 존재 하는 HPE SAS 확장기 카드를 사용 하 여 문제가입니다. SAS 확장기 확장기 및 자체 확장기에 연결 된 첫 번째 드라이브 간에 중복 된 ID를 만듭니다.  해결 되었습니다이 [HPE 스마트 배열 컨트롤러 SAS 확장기 펌웨어. 4.02](https://support.hpe.com/hpsc/swd/public/detail?sp4ts.oid=7304566&swItemId=MTX_ef8d0bf4006542e194854eea6a&swEnvOid=4184#tab3).
    
## <a name="intel-ssd-dc-p4600-series-has-a-non-unique-nguid"></a>Intel SSD DC P4600 계열에 고유 하지 않은 NGUID
Intel SSD DC P4600 시리즈 장치를 같습니다 0100000001000000E4D25C000014E214 또는 0100000001000000E4D25C0000EEE214 아래 예제에서와 같은 여러 네임 스페이스에 대 한 유사한 16 바이트 NGUID를 보고할 수 있는 문제를 확인할 수 있습니다.

|uniqueid| deviceid |MediaType| BusType| serialnumber| 크기|canpool| friendlyname| OperationalStatus|
|-|-|-|-|-|-|-|-|-
|5000CCA251D12E30| 0| HDD| SAS| 7PKR197G|                  10000831348736 |False|HGST| HUH721010AL4200| 확인|
|eui.0100000001000000E4D25C000014E214 |4|SSD| NVMe|   0100_0000_0100_0000_E4D2_5C00_0014_E214.|1600321314816|True| INTEL| SSDPE2KE016T7|  확인|
|eui.0100000001000000E4D25C000014E214 |5|        SSD|       NVMe|    0100_0000_0100_0000_E4D2_5C00_0014_E214.|  1600321314816|    True| INTEL| SSDPE2KE016T7|  확인|
|eui.0100000001000000E4D25C0000EEE214| 6|        SSD|       NVMe|    0100_0000_0100_0000_E4D2_5C00_00EE_E214.|  1600321314816|    True| INTEL| SSDPE2KE016T7|  확인|
|eui.0100000001000000E4D25C0000EEE214| 7|        SSD|       NVMe|    0100_0000_0100_0000_E4D2_5C00_00EE_E214.|  1600321314816|    True| INTEL| SSDPE2KE016T7|  확인|

이 문제를 해결 하려면 Intel 드라이브의 펌웨어를 최신 버전으로 업데이트 합니다.  펌웨어 버전 QDV101B1 2018 년 5 월에서에서이 문제를 해결 하려면 이라고 합니다.

합니다 [2018 년 5 월 릴리스의 Intel SSD 데이터 센터 도구](https://downloadmirror.intel.com/27778/eng/Intel_SSD_Data_Center_Tool_3_0_12_Release_Notes_330715-026.pdf) 펌웨어 업데이트 QDV101B1, Intel SSD DC P4600 시리즈에 포함 되어 있습니다.

    
## <a name="physical-disk-healthy-and-operational-status-is-removing-from-pool"></a>실제 디스크 "정상", 및 작동 상태는 "풀에서 제거" 

Windows Server 2016 저장소 공간 다이렉트 클러스터에서 나타날 수 있습니다 하나 이상의 물리적 디스크에 대 한 HealthStatus "정상"으로 OperationalStatus는 "(제거 확인, 풀에서)." 

"풀에서 제거" 의도 경우 설정 됩니다 **Remove-physicaldisk** 호출 되었지만 상태를 유지 관리 하 고 제거 작업이 실패할 경우 복구를 허용 하는 상태에 저장 합니다. 다음 방법 중 하나를 사용 하 여 정상 OperationalStatus는 수동으로 변경할 수 있습니다.

- 풀에서 실제 디스크를 제거 하 고 다시 추가 합니다.
- 실행 합니다 [Clear PhysicalDiskHealthData.ps1 스크립트](https://go.microsoft.com/fwlink/?linkid=2034205) 의도 선택을 취소 합니다. (으로 다운로드할 수는 있습니다. TXT 파일입니다. 로 저장 해야 하는 합니다. PS1 파일 전에 실행할 수 있습니다.)

스크립트를 실행 하는 방법을 보여 주는 몇 가지 예는 다음과 같습니다.

- 사용 된 **SerialNumber** 매개 변수를 정상으로 설정 해야 하는 디스크를 지정 합니다. 일련 번호를 가져올 수 있습니다 **WMI MSFT_PhysicalDisk** 하거나 **Get-physicaldisk**합니다. (것만 사용 하는 0으로 아래에 일련 번호에 대 한 합니다.)
   
   ```powershell
   Clear-PhysicalDiskHealthData -Intent -Policy -SerialNumber 000000000000000 -Verbose -Force
    ```

- 사용 된 **UniqueId** 디스크를 지정 하려면 매개 변수 (에서 다시 **WMI MSFT_PhysicalDisk** 또는 **Get-physicaldisk**).

   ```powershell
   Clear-PhysicalDiskHealthData -Intent -Policy -UniqueId 00000000000000000 -Verbose -Force
   ```

## <a name="file-copy-is-slow"></a>파일 복사가 느립니다.

파일 탐색기를 사용 하 여 가상 디스크에 대형 VHD를 복사 하는 문제를 볼 수 있습니다-파일 복사본을 예상 보다 오래 걸리고 있습니다.

파일 탐색기를 사용 하 여 가상 디스크에 큰 VHD를 복사할 Xcopy 또는 Robocopy 아닙니다 권장 되는 메서드를 이렇게 하면 예상 되는 성능 보다 느립니다. 복사 프로세스가 저장소 스택의 하위 위치 대신 로컬 복사가 처럼 작동 하며 저장소 공간 다이렉트 스택의 통과 하지 않습니다.

저장소 공간 다이렉트 성능을 테스트 하려는 경우 VMFleet 및 Diskspd를 사용 하 여 부하 및 스트레스 테스트 하는 것이 좋습니다는 기준선을 가져오고 저장소 공간 다이렉트 성능 기대치를 설정 하는 서버입니다.

## <a name="expected-events-that-you-would-see-on-rest-of-the-nodes-during-the-reboot-of-a-node"></a>노드 다시 부팅 하는 동안 노드의 나머지 부분에 표시 하는 이벤트를 예상 합니다. 

이러한 이벤트를 무시 해도 됩니다. 

    Event ID 205: Windows lost communication with physical disk {XXXXXXXXXXXXXXXXXXXX }. This can occur if a cable failed or was disconnected, or if the disk itself failed. 

    Event ID 203: Windows lost communication with physical disk {xxxxxxxxxxxxxxxxxxxxxxxx }. This can occur if a cable failed or was disconnected, or if the disk itself failed. 

Azure Vm을 실행 하는 경우에이 이벤트를 무시할 수 있습니다.

    Event ID 32: The driver detected that the device \Device\Harddisk5\DR5 has its write cache enabled. Data corruption may occur. 
    
## <a name="slow-performance-or-lost-communication-io-error-detached-or-no-redundancy-errors-for-deployments-that-use-intel-p3x00-nvme-devices"></a>성능 저하 또는 "Lost Communication," "IO Error", "분리 된" 또는 "No 중복성" Intel P3x00 NVMe 장치를 사용 하는 배포 오류

"유지 관리 릴리스 8." 이전 펌웨어 버전을 사용 하 여 장치 NVM (NVMe) Express Intel P3x00 제품군을 기반 하드웨어를 사용 하는 일부 저장소 공간 다이렉트의 사용자에 영향을 주는 중요 한 문제를 식별 했습니다. 

>[!NOTE]
> 개별 Oem 고유 펌웨어 버전 문자열을 사용 하 여 NVMe 장치는 Intel P3x00 제품군을 기반으로 하는 장치에 있을 수 있습니다. 자세한 최신 펌웨어 버전에 대 한 OEM에 문의 합니다.

하드웨어 기반 NVMe 장치는 Intel P3x00 제품군으로 배포를 사용 하는 경우 사용 가능한 최신 펌웨어를 즉시 적용 하는 것이 좋습니다 (적어도 유지 관리 릴리스 8). 이렇게 [Microsoft 지원 문서](https://support.microsoft.com/en-us/help/4052341/slow-performance-or-lost-communication-io-error-detached-or-no-redunda) 이 문제에 대 한 추가 정보를 제공 합니다. 
