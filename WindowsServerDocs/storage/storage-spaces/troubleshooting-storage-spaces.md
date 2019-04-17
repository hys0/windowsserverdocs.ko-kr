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
ms.openlocfilehash: c7c9573732ff1cf5a998588b1aec81915c227ee2
ms.sourcegitcommit: 5d55c3ebd1ceee7229ea9a9989c69cf93757ed88
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/21/2019
ms.locfileid: "9256936"
---
# 저장소 공간 다이렉트 문제 해결

다음 정보를 사용 하 여 저장소 공간 다이렉트 배포 문제 해결 합니다.

일반적으로 다음 단계를 시작 합니다.

1. SSD의 메이커/모델은 Windows Server 카탈로그를 사용 하 여 Windows Server 2016 인증 되어 있는지 확인 합니다. 드라이브가 저장소 공간 다이렉트에 대 한 지원 되는 공급 업체에 확인 합니다.
2. 모든 결함이 있는 드라이브에 대 한 저장소를 검사 합니다. 저장소 관리 소프트웨어를 사용 하 여 드라이브의 상태를 확인 합니다. 드라이브 결함이 있는, 일 경우 해당 공급 업체와 협력 합니다. 
3. 저장소를 업데이트 하 고 필요한 경우 드라이브 펌웨어.
   모든 노드에 설치 된 최신 Windows 업데이트를 확인 합니다. Windows Server 2016에서 최신 업데이트를 얻을 수 있습니다 [https://aka.ms/update2016](https://aka.ms/update2016).
4. 네트워크 어댑터 드라이버와 펌웨어를 업데이트 합니다.
5. 클러스터 유효성 검사를 실행 하 고 저장소 공간 다이렉트 섹션을 검토, 캐시에 사용 되는 드라이브를 제대로 보고를 확인 하 고 오류 없이 합니다.

여전히 문제가 발생 하면, 아래 시나리오를 검토 합니다.

## 가상 디스크 리소스가 아니요 중복성 상태
노드 저장소 공간 다이렉트 시스템의 작동 중단 이나 정전이 오류로 인해 예기치 않게 다시 시작 합니다. 그런 다음 하나 이상의 가상 디스크를 온라인 상태로 수 및 설명 "중복 정보 충분 하지 않습니다."를 표시
    
|FriendlyName|ResiliencySettingName| OperationalStatus| HealthStatus| IsManualAttach|크기| PSComputerName|
|------------|---------------------| -----------------| ------------| --------------|-----| --------------|
|Disk4| 미러| 확인|  Healthy| True|  10TB|  노드 01.conto...|
|Disk3         |미러                 |확인                          |Healthy       |True            |10TB | 노드 01.conto...|
|디스크 2         |미러                 |중복               |Unhealthy     |True            |10TB | 노드 01.conto...|
|Disk1         |미러                 |{중복성 없음, 정비}  |Unhealthy     |True            |10TB | 노드 01.conto...| 

또한 가상 디스크를 온라인 상태로 하려고를 시도한 후 클러스터 로그 (DiskRecoveryAction)에 다음과 같은 정보가 기록 됩니다.  

```
[Verbose] 00002904.00001040::YYYY/MM/DD-12:03:44.891 INFO [RES] Physical Disk <DiskName>: OnlineThread: SuGetSpace returned 0.
[Verbose] 00002904.00001040:: YYYY/MM/DD -12:03:44.891 WARN [RES] Physical Disk < DiskName>: Underlying virtual disk is in 'no redundancy' state; its volume(s) may fail to mount.
[Verbose] 00002904.00001040:: YYYY/MM/DD -12:03:44.891 ERR [RES] Physical Disk <DiskName>: Failing online due to virtual disk in 'no redundancy' state. If you would like to attempt to online the disk anyway, first set this resource's private property 'DiskRecoveryAction' to 1. We will try to bring the disk online for recovery, but even if successful, its volume(s) or CSV may be unavailable. 
``` 

**아니요 중복성 작동 상태** 실패 한 디스크 또는 시스템 가상 디스크의 데이터에 액세스할 수 없는 경우 발생할 수 있습니다. 다시 부팅 노드에 노드에서 유지 관리 하는 동안 발생 하는 경우이 문제가 발생할 수 있습니다.
    
이 문제를 해결 하려면 다음이 단계를 따르세요.

1. CSV에서 영향을 받는 가상 디스크를 제거 합니다. 그러면 클러스터의 "사용 가능한 저장소" 그룹에 배치 되 고 "Physical Disk"의 ResourceType로 나타나기 시작

   ```powershell
   Remove-ClusterSharedVolume -name "VdiskName"
   ``` 
2. 사용 가능한 저장소 그룹을 소유 하 고 노드를 아니요 중복성 상태에 있는 모든 디스크에서 다음 명령을 실행 합니다. "사용 가능한 저장소" 그룹에 있는 노드를 식별 하 고 다음 명령을 실행할 수 있습니다.

   ```powershell
   Get-ClusterGroup
   ```
3. 디스크 복구 동작을 설정 하 고 디스크를 시작 합니다.
   ```powershell
   Get-ClusterResource "VdiskName" | Set-ClusterParameter -Name DiskRecoveryAction -Value 1
   Start-ClusterResource -Name "VdiskName"
   ```
4. 복구는 자동으로 시작 합니다. 복구 완료 될 때까지 기다립니다. 일시 중단 된 상태로 전환 하 고 다시 시작 될 수 있습니다. 진행률 모니터링: 
    - **Get StorageJob** 복구의 상태를 모니터링 하 고 완료 될 때 실행 됩니다.
    - **Get VirtualDisk** 를 실행 하 고 공간을 HealthStatus의 정상 반환 하는지 확인 합니다.
5. 복구 후 완료 되 고 가상 디스크가 정상, 가상 디스크 매개 변수를 다시 변경 됩니다.

   ```powershell
    Get-ClusterResource "VdiskName" | Set-ClusterParameter -Name DiskRecoveryAction -Value 0
   ```
6. 디스크가 오프 라인 및 적용 DiskRecoveryAction를 다시 온라인 다음을 수행 합니다.

   ```powershell
   Stop-ClusterResource "VdiskName"
   Start-ClusterResource "VdiskName"
   ``` 
7. CSV로 다시 영향을 받는 가상 디스크를 추가 합니다.

   ```powershell
   Add-ClusterSharedVolume -name "VdiskName"
   ```

**DiskRecoveryAction** 는 재정의 되는 검사 없이 읽기-쓰기 모드로 공간 볼륨을 연결할 수 있습니다. 속성을 사용 하면 볼륨을 온라인 상태로 없습니다 이유를 진단 수행할 수 있습니다. 유지 관리 모드로 매우 유사 하지만 실패 상태가 리소스에서 호출할 수 있습니다. 또한 액세스를 얻을 수 있는 "아니요 중복성"와 같은 경우에 도움이 될 수 있는 데이터에 액세스할 수 있습니다 모든 데이터를 복사 합니다. DiskRecoveryAction 속성은 22 2018 년 2 월 업데이트, KB 4077525에에서 추가 되었습니다.
    
    
## 클러스터에서 분리 된 상태 

**Get VirtualDisk** cmdlet을 실행 하면 저장소 공간 다이렉트 하나 이상의 가상 디스크에 대 한 OperationalStatus 분리 됩니다. 그러나 **Get-physicaldisk** cmdlet에서 보고 HealthStatus 모든 실제 디스크가 정상 상태의 있음을 나타냅니다.

다음은 **Get VirtualDisk** cmdlet의 출력의 예입니다.

|FriendlyName|  ResiliencySettingName|  OperationalStatus|   HealthStatus|  IsManualAttach|  크기|   PSComputerName|
|-|-|-|-|-|-|-|
|Disk4|         미러|                 확인|                  Healthy|       True|            10TB|  노드 01.conto...|
|Disk3|         미러|                 확인|                  Healthy|       True|            10TB|  노드 01.conto...|
|디스크 2|         미러|                 분리|            알 수 없음|       True|            10TB|  노드 01.conto...|
|Disk1|         미러|                 분리|            알 수 없음|       True|            10TB|  노드 01.conto...| 


또한 노드에서 다음 이벤트를 기록 될 수 있습니다.

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

**분리 된 작동 상태** 변경 영역 (DRT) 추적 로그 가득 찬 경우 발생할 수 있습니다. 저장소 공간 (DRT) 미러 공간에 대 한 추적 변경 영역 정전이 발생 하면 저장소 공간 다시 실행 하거나 실행 취소는 유연한로 다시 저장 공간을 가져오는 작업 수 있는지 확인 하려면 인플라이트 업데이트 메타 데이터를 기록 됩니다를 사용 하 여 및 전원 복원 되 고 시스템 백업 되 면 일관 된 상태입니다. DRT 로그 이면 전체 DRT 메타 데이터를 동기화 하 고 값이 플러시되 때까지 가상 디스크 온라인 할 수 없습니다. 이 프로세스를 완료 하려면 몇 시간이 걸릴 수 있는 전체 검사를 실행 해야 합니다.
    
이 문제를 해결 하려면 다음이 단계를 따르세요.
1. CSV에서 영향을 받는 가상 디스크를 제거 합니다.

   ```powershell
   Remove-ClusterSharedVolume -name "VdiskName"
   ``` 
2. 모든 디스크를 온라인 상태로 하지는에서 다음 명령을 실행 합니다. 

   ```powershell
   Get-ClusterResource -Name "VdiskName" | Set-ClusterParameter DiskRunChkDsk 7
   Start-ClusterResource -Name "VdiskName"
   ``` 
3. 분리 된 볼륨이 온라인 인 모든 노드에서 다음 명령을 실행 합니다. 

   ```powershell
   Get-ScheduledTask -TaskName "Data Integrity Scan for Crash Recovery" | Start-ScheduledTask 
   ```
   분리 된 볼륨은 온라인 되는 모든 노드에서이 작업을 시작 해야 합니다. 복구는 자동으로 시작 합니다. 복구 완료 될 때까지 기다립니다. 일시 중단 된 상태로 전환 하 고 다시 시작 될 수 있습니다. 진행률 모니터링: 
   - **Get StorageJob** 복구의 상태를 모니터링 하 고 완료 될 때 실행 됩니다.
   -  **Get VirtualDisk** 를 실행 하 고 공간을 HealthStatus의 정상 반환 확인 합니다.
    - "데이터 무결성 검사에 대 한 크래시 복구" 저장소 작업으로 표시 되지 않는 작업은 해당 하며 진행률 표시기가 없습니다. 작업을 표시 하는 경우 실행 중으로 실행 합니다. 완료 되 면 완료 된 표시 됩니다.
    
       또한 다음 cmdlet을 사용 하 여 실행 중인 스케줄 작업의 상태를 볼 수 있습니다. 
       ```powershell
       Get-ScheduledTask | ? State -eq running
       ``` 
4. "데이터 무결성 검사에 대 한 크래시 복구" 완료 되 면 곧바로 복구 완료 되 고 가상 디스크가 정상, 가상 디스크 매개 변수를 다시 변경 됩니다. 

   ```powershell
   Get-ClusterResource -Name "VdiskName" | Set-ClusterParameter DiskRunChkDsk 0 
   ```
5. CSV로 다시 영향을 받는 가상 디스크를 추가 합니다.    

   ```powershell
   Add-ClusterSharedVolume -name "VdiskName"
   ```  
**DiskRunChkdsk 값 7** 공간 볼륨을 연결 하 고 읽기 전용 모드로 파티션을 사용 됩니다. 이렇게 하면 자동으로 검색 하는 공간 및 자동 치료할 복구 트리거하여 합니다. 복구 실행 한 번 자동으로 탑재 합니다. 또한 복사할 수 있는 모든 데이터에 액세스 하는 데 도움이 될 수 있는 데이터에 액세스할 수 있습니다. 전체 DRT 로그와 같은 일부 오류 조건에 대 한 크래시를 복구 예약 된 작업에 대 한 데이터 무결성 검사를 실행 해야 합니다.
    
**크래시를 복구 작업에 대 한 데이터 무결성 검사** 를 동기화 하 고 변경 전체 영역 (DRT) 추적 로그 지우기 사용 됩니다. 이 작업을 완료 하는 데 몇 시간이 걸릴 수 있습니다. "데이터 무결성 검사에 대 한 크래시 복구" 저장소 작업으로 표시 되지 않는 작업은 해당 하며 진행률 표시기가 없습니다. 작업을 표시 하는 경우 실행 중으로 실행 합니다. 완료 되 면 완료로 표시 됩니다. 작업을 취소 하거나이 작업이 실행 되는 동안 노드를 다시 시작 하는 경우 작업이 처음부터 다시 시작 해야 합니다.

자세한 내용은 [저장소 공간 다이렉트 문제 해결 상태 및 작동 상태를](storage-spaces-states.md)참조 하세요.
    
## STATUS_IO_TIMEOUT c00000b5 5120 이벤트 

> [!Important]
> [Windows Server 2016 용 누적 업데이트 2018 년 10 월 18 일](https://support.microsoft.com/help/4462928) 또는 그 이후 버전을 설치 하려면 다음 저장소 유지 관리 모드 절차를 사용 하 여 권장는 수정 된 업데이트를 적용 하는 동안 이러한 현상이 발생 가능성을 줄이기 위해 때 노드 현재 설치 된 Windows Server 2016 누적 업데이트 출시 된 [2018 년 5 월 8](https://support.microsoft.com/help/4103723) 에서 [2018 년 10 월 9 일](https://support.microsoft.com/help/KB4462917)을 합니다.

[2018 년 10 월 9, KB 4462917](https://support.microsoft.com/help/4462917) 설치에서 [8 2018 KB 4103723 수](https://support.microsoft.com/help/4103723) 릴리스되는 누적 업데이트를 사용 하 여 Windows Server 2016에서 노드를 다시 시작한 후 이벤트 5120 STATUS_IO_TIMEOUT c00000b5 느낄 수 있습니다.

노드를 다시 시작 하면 이벤트 5120 시스템 이벤트 로그에 기록 되 고 다음과 같은 오류 코드 중 하나가 포함:

```
Event Source: Microsoft-Windows-FailoverClustering
Event ID: 5120
Description:    Cluster Shared Volume 'CSVName' ('Cluster Virtual Disk (CSVName)') has entered a paused state because of 'STATUS_IO_TIMEOUT(c00000b5)'. All I/O will temporarily be queued until a path to the volume is reestablished. 

Cluster Shared Volume ‘CSVName’ ('Cluster Virtual Disk (CSVName)') has entered a paused state because of 'STATUS_CONNECTION_DISCONNECTED(c000020c)'. All I/O will temporarily be queued until a path to the volume is reestablished.    
```

이벤트 5120 기록 되 면 추가 현상이 발생할 또는 성능 영향을 미칠 수 있는 디버깅 정보를 수집 하 라이브 덤프 생성 됩니다. 라이브 덤프 생성 잠시 스냅숏을 메모리 덤프 파일에 쓸 수 있도록 만듭니다. 시스템 메모리를 많이 고 스트레스 아래에 있는 노드를 클러스터 멤버십 삭제를 로깅하도록 다음 이벤트 1135로 인해 발생할 수 있습니다.

```
Event source: Microsoft-Windows-FailoverClustering
Event ID: 1135  
Description: Cluster node 'NODENAME'was removed from the active failover cluster membership. The Cluster service on this node may have stopped. This could also be due to the node having lost communication with other active nodes in the failover cluster. Run the Validate a Configuration wizard to check your network configuration. If the condition persists, check for hardware or software errors related to the network adapters on this node. Also check for failures in any other network components to which the node is connected such as hubs, switches, or bridges.
```

저장소 공간 다이렉트 클러스터 간 SMB 네트워크 세션에 대 한 SMB 복원 처리를 추가 하려면 2018 년 5 월 8 일 누적 업데이트에서 변경 내용을 도입 되었습니다. 이렇게 복원 력을 위해 임시 네트워크 오류를 개선 하 고 RoCE 네트워크 정체를 처리 하는 방법을 개선 합니다.

이러한 향상 된이 기능 노드를 다시 시작할 때 SMB 연결 다시 연결 하려고 시도 하면 시간 제한 및 대기 시간을 증가 실수로 했습니다. 이러한 문제 스트레스에서 관리 되는 시스템에 영향을 줄 수 있습니다. 계획 되지 않은 가동 중지 시간 동안 최대 60 초 IO 일시 중지도 관찰 된 시스템 시간 제한에 대 한 연결을 기다리는 동안 합니다.

이 문제를 해결 하려면 [2018 년 10 월 18, Windows Server 2016 용 누적 업데이트](https://support.microsoft.com/help/4462928) 또는 그 이후 버전을 설치 합니다.

*참고* 이 업데이트는이 문제를 해결 하려면 SMB 연결 시간 초과 사용 하 여 CSV 제한 시간을 맞춥니다. 변경 내용을 해결 섹션에 언급 된 라이브 덤프 생성을 비활성화 하려면 구현 하지 않습니다.
    
### 종료 프로세스 흐름:

1. Get VirtualDisk cmdlet을 실행 하 고 HealthStatus 값 정상 인지 확인 합니다.
2. 다음 cmdlet을 실행 하 여 노드를 소모 합니다.

   ```powershell
   Suspend-ClusterNode -Drain
   ```
3. 다음 cmdlet을 실행 하 여 저장소 유지 관리 모드에서 해당 노드에서 디스크를 배치 합니다. 

   ```powershell
   Get-StorageFaultDomain -type StorageScaleUnit | Where-Object {$_.FriendlyName -eq "<NodeName>"} | Enable-StorageMaintenanceMode
   ```
4. **Get-physicaldisk** cmdlet을 실행 하 고 해당 OperationalStatus 값은 유지 관리 모드에 있는지 확인 합니다.
5. 노드를 다시 시작 하는 **컴퓨터를 다시 시작할** cmdlet을 실행 합니다.
6. 노드를 다시 시작한 후 다음 cmdlet을 실행 하 여 저장소 유지 관리 모드에서 디스크 해당 노드를 제거 합니다.

   ```powershell
   Get-StorageFaultDomain -type StorageScaleUnit | Where-Object {$_.FriendlyName -eq "<NodeName>"} | Disable-StorageMaintenanceMode
   ```
7. 다음 cmdlet을 실행 하 여 노드를 다시 시작 합니다.

   ```powershell
   Resume-ClusterNode
   ```
8. 다음 cmdlet을 실행 하 여 재 동기화 작업의 상태를 확인 합니다.

   ```powershell
   Get-StorageJob
   ```

### 라이브 덤프를 사용 하지 않도록 설정
작업량이 많은 양의 메모리가 있는 고 수 있는 시스템에서 라이브 덤프 생성의 영향을 줄이려면 라이브 덤프 생성을 사용 하지 않도록 설정 하려면 또한 있습니다. 세 가지 옵션이 제공 됩니다.

>[!Caution]
>이 절차는이 문제를 조사 하려면 Microsoft 지원 해야 하는 진단 정보 수집을 방지할 수 있습니다. 지원 상담원이 특정 문제 해결 시나리오에 따라 라이브 덤프 생성을 다시 사용 하도록 설정 하 라는 요청을 할 수 있습니다.

아래 설명 된 대로 라이브 덤프를 사용 하지 않도록 설정 하는 방법은 두 가지 합니다.

#### 방법 1 (이 시나리오에서는 권장)
시스템 수준 라이브 덤프를 비롯 한 모든 덤프를 완전히 사용 하지 않으려면 다음이 단계를 따르세요.

1. 다음 레지스트리 키 만들기: HKLM\System\CurrentControlSet\Control\CrashControl\ForceDumpsDisabled
2. 새 **ForceDumpsDisabled** 키 아래에 REG_DWORD 속성으로 GuardedHost 만들고 0x10000000로 해당 값을 설정 합니다.
3. 각 클러스터 노드에 새 레지스트리 키를 적용 합니다.

>[!NOTE]
>Nregistry 변경 내용 적용 하려면 컴퓨터를 다시 시작 해야 합니다.

이 레지스트리 키가 설정, 라이브 후 덤프 만들기 실패 하 고 "STATUS_NOT_SUPPORTED" 오류가 발생 합니다.

#### 방법 2
기본적으로 Windows 오류 보고 하면 7 일 마다 보고서 종류에 따라 하나의 LiveDump 및 5 일 마다 컴퓨터당 하나의 LiveDump 있습니다. 만 하나의 LiveDump 컴퓨터 무제한 허용 하도록 다음 레지스트리 키를 설정 하 여 변경할 수 있습니다.
```
reg add "HKLM\Software\Microsoft\Windows\Windows Error Reporting\FullLiveKernelReports" /v SystemThrottleThreshold /t REG_DWORD /d 0xFFFFFFFF /f
```
```
reg add "HKLM\Software\Microsoft\Windows\Windows Error Reporting\FullLiveKernelReports" /v ComponentThrottleThreshold /t REG_DWORD /d 0xFFFFFFFF /f
```

*참고* 변경 내용 적용 하려면 컴퓨터를 다시 시작 해야 합니다.

### 메서드 3
라이브 덤프 (예: 이벤트 5120 기록 될 때)의 클러스터 생성을 비활성화 하려면 다음 cmdlet을 실행 합니다.

```powershell
(Get-Cluster).DumpPolicy = ((Get-Cluster).DumpPolicy -band 0xFFFFFFFFFFFFFFFE)
```
이 cmdlet 컴퓨터를 다시 시작 하지 않고 모든 클러스터 노드에서 즉각적인 효과가 있습니다.
    
## IO 성능 저하

IO 성능 저하를 표시 하는 경우 캐시 저장소 공간 다이렉트 구성에서 활성화 되어 있는지 확인 합니다. 

확인 하는 방법은 두 가지가 있습니다. 
     
 
1. 클러스터 로그를 사용 합니다. 선택한 텍스트 편집기에서 클러스터 로그를 열고 검색 "[=== SBL 디스크 ===]." 이 로그에서 생성 된 노드에 있는 디스크 목록이 됩니다. 

     캐시 사용 디스크 예: Note 여기 상태가 CacheDiskStateInitializedAndBound 및 여기 존재 GUID가 있습니다. 

   ```
   [=== SBL Disks ===]
    {26e2e40f-a243-1196-49e3-8522f987df76},3,false,true,1,48,{1ff348f1-d10d-7a1a-d781-4734f4440481},CacheDiskStateInitializedAndBound,1,8087,54,false,false,HGST    ,HUH721010AL4200 ,        7PG3N2ER,A21D,{d5e27a3b-42fb-410a-81c6-9d8cc12da20c},[R/M 0 R/U 0 R/T 0 W/M 0 W/U 0 W/T 0],
    ```

    캐시 사용할 수 없습니다: 여기 존재 하지 GUID 이며 CacheDiskStateNonHybrid 상태가 알 수 있습니다. 
    ```
   [=== SBL Disks ===]
    {426f7f04-e975-fc9d-28fd-72a32f811b7d},12,false,true,1,24,{00000000-0000-0000-0000-000000000000},CacheDiskStateNonHybrid,0,0,0,false,false,HGST    ,HUH721010AL4200 ,        7PGXXG6C,A21D,{d5e27a3b-42fb-410a-81c6-9d8cc12da20c},[R/M 0 R/U 0 R/T 0 W/M 0 W/U 0 W/T 0],
    ```

    캐시 사용할 수 없습니다: 때 모든 디스크는 동일한 유형의 경우 기본적으로 사용 되지 않습니다. 여기서 존재 하지 GUID 이며 CacheDiskStateIneligibleDataPartition 상태가 알 수 있습니다. 
    ```
    {d543f90c-798b-d2fe-7f0a-cb226c77eeed},10,false,false,1,20,{00000000-0000-0000-0000-000000000000},CacheDiskStateIneligibleDataPartition,0,0,0,false,false,NVMe    ,INTEL SSDPE7KX02,  PHLF7330004V2P0LGN,0170,{79b4d631-976f-4c94-a783-df950389fd38},[R/M 0 R/U 0 R/T 0 W/M 0 W/U 0 W/T 0], 
    ```  
2. Get-PhysicalDisk.xml는 SDDCDiagnosticInfo에서 사용 하 여
    1. 사용 하 여 XML 파일을 열고 "$d 가져오기 Clixml GetPhysicalDisk.XML ="
    2. "Ipmo 저장소" 실행
    3. "$d"를 실행 합니다. 자동 선택 저널 싶지 사용은 다음과 같은 출력이 표시 됩니다. 

   |FriendlyName|  SerialNumber| MediaType| CanPool| OperationalStatus| HealthStatus| 사용| 크기|
   |-----------|------------|---------| -------| -----------------| ------------| -----| ----|
   |NVMe INTEL SSDPE7KX02| PHLF733000372P0LGN| SSD| False|   확인|                Healthy|      1.82 t B 자동 선택|
   |NVMe INTEL SSDPE7KX02 |PHLF7504008J2P0LGN| SSD|  False|    확인|                Healthy| 자동 선택| 1.82 T B|
   |NVMe INTEL SSDPE7KX02| PHLF7504005F2P0LGN| SSD|  False|  확인|                Healthy| 자동 선택| 1.82 T B|
   |NVMe INTEL SSDPE7KX02 |PHLF7504002A2P0LGN| SSD| False| 확인|    Healthy| 자동 선택| 1.82 T B|
   |NVMe INTEL SSDPE7KX02| PHLF7504004T2P0LGN |SSD| False|확인|       Healthy| 자동 선택| 1.82 T B|
   |NVMe INTEL SSDPE7KX02 |PHLF7504002E2P0LGN| SSD| False| 확인|      Healthy| 자동 선택| 1.82 T B|
   |NVMe INTEL SSDPE7KX02 |PHLF7330002Z2P0LGN| SSD| False| 확인|      Healthy|자동 선택| 1.82 T B|
   |NVMe INTEL SSDPE7KX02 |PHLF733000272P0LGN |SSD| False| 확인|  Healthy| 자동 선택| 1.82 T B|
   |NVMe INTEL SSDPE7KX02 |PHLF7330001J2P0LGN |SSD| False| 확인| Healthy| 자동 선택| 1.82 T B|
   |NVMe INTEL SSDPE7KX02| PHLF733000302P0LGN |SSD| False| 확인|Healthy| 자동 선택| 1.82 T B|
   |NVMe INTEL SSDPE7KX02| PHLF7330004D2P0LGN |SSD| False| 확인| Healthy| 자동 선택 |1.82 T B|
    
## 동일한 디스크를 다시 사용할 수 있도록 기존 클러스터를 삭제 하는 방법

저장소 공간 다이렉트 클러스터에서 저장소 공간 다이렉트 사용 하지 않도록 설정 하 고 [새로 드라이브](deploy-storage-spaces-direct.md#step-31-clean-drives)에 설명 된 정리 프로세스를 사용 하 여 클러스터 저장소 풀에도 오프 라인 상태로 남아 및 상태 관리 서비스 클러스터에서 제거 됩니다.

다음 단계는 가상 저장소 풀을 제거 하려면: 
   ```powershell
   Get-ClusterResource -Name "Cluster Pool 1" | Remove-ClusterResource
   ```

이제 **Get-physicaldisk** 노드 중 하나를 실행 하면 풀에 있던 모든 디스크 표시 됩니다. 예를 들어 랩에서 100GB 각 노드마다에 제공 된 4 개의 SAS 디스크에 4-노드 클러스터로 합니다. 이 경우 저장소 공간 다이렉트 비활성화 된 후, **Get-physicaldisk**실행 하는 경우 (저장소 버스 계층) SBL 제거 되지만 필터는, 로컬 운영 체제 디스크를 제외 하는 4 개의 디스크 보고 해야 합니다. 대신 보고 16 대신 합니다. 클러스터의 모든 노드에 대해 동일합니다. **Get-disk** 명령을 실행 하면 로컬로 연결 된 디스크 0, 1, 2와 같이 번호가 지정, 출력이 예제와 같이 표시 됩니다.

|숫자| 식별 이름| 일련 번호|HealthStatus|OperationalStatus|전체 크기| 파티션 스타일|
|-|-|-|-|-|-|-|-|
|0|Msft Virtu...  ||Healthy | 온라인|  127 GB| GPT|
||Msft Virtu... ||Healthy| 오프라인| 100GB| 원시|
||Msft Virtu... ||Healthy| 오프라인| 100GB| 원시|
||Msft Virtu... ||Healthy| 오프라인| 100GB| 원시|
||Msft Virtu... ||Healthy| 오프라인| 100GB| 원시|
|1|Msft Virtu...||Healthy| 오프라인| 100GB| 원시|
||Msft Virtu... ||Healthy| 오프라인| 100GB| 원시|
|2|Msft Virtu...||Healthy| 오프라인| 100GB| 원시|
||Msft Virtu... ||Healthy| 오프라인| 100GB| 원시|
||Msft Virtu... ||Healthy| 오프라인| 100GB| 원시|
||Msft Virtu... ||Healthy| 오프라인| 100GB| 원시|
||Msft Virtu... ||Healthy| 오프라인| 100GB| 원시|
|4|Msft Virtu...||Healthy| 오프라인| 100GB| 원시|
|3|Msft Virtu...||Healthy| 오프라인| 100GB| 원시|
||Msft Virtu... ||Healthy| 오프라인| 100GB| 원시|
||Msft Virtu... ||Healthy| 오프라인| 100GB| 원시|
||Msft Virtu... ||Healthy| 오프라인| 100GB| 원시|

    
## "지원 되지 않는 미디어 형식"에 대 한 오류 메시지 Enable-clusters2d를 사용 하 여 저장소 공간 다이렉트 클러스터를 만들 때  

**Enable-clusters2d** cmdlet을 실행 하면 다음과 같은 오류가 표시 될 수 있습니다.

![시나리오 6 오류 메시지](media/troubleshooting/scenario-error-message.png)

이 문제를 해결 하려면 HBA 어댑터는 HBA 모드로 구성 되어 있는지 확인 합니다. 없음 HBA RAID 모드에서 구성 되어야 합니다.  
    
## Enable-clusterstoragespacesdirect 'SBL 것을 기다리는 동안 디스크 표시 되며' 또는 27%에 응답

유효성 검사 보고서에 다음 정보를 표시 합니다.

    Disk <identifier> connected to node <nodename> returned a SCSI Port Association and the corresponding enclosure device could not be found. The hardware is not compatible with Storage Spaces Direct (S2D), contact the hardware vendor to verify support for SCSI Enclosure Services (SES). 
    
  
디스크와 HBA 카드 사이는 패키지는 HPE SAS 확장기 카드에 문제가 있습니다. SAS 확장기 확장기 자체 확장에 연결 하는 첫 번째 드라이브 간에 중복 ID를 만듭니다.  이에서 해결 되었습니다 [패키지는 HPE 스마트 배열 컨트롤러 SAS 확장기 펌웨어: 4.02](https://support.hpe.com/hpsc/swd/public/detail?sp4ts.oid=7304566&swItemId=MTX_ef8d0bf4006542e194854eea6a&swEnvOid=4184#tab3)합니다.
    
## Intel SSD DC P4600 시리즈에 고유 하지 않은 NGUID
Intel SSD DC P4600 시리즈 장치 같습니다 0100000001000000E4D25C000014E214 또는 0100000001000000E4D25C0000EEE214 아래 예제에서와 같은 여러 네임 스페이스에 대 한 유사한 16 바이트 NGUID 보고 있는 문제를 볼 수 있습니다.

|고유 id| deviceid |MediaType| Bustype이| 일련 번호| size|canpool| friendlyname| OperationalStatus|
|-|-|-|-|-|-|-|-|-
|5000CCA251D12E30| 0| HDD| SAS| 7PKR197G|                  10000831348736 |False|HGST| HUH721010AL4200| 확인|
|eui.0100000001000000E4D25C000014E214 |4|SSD| NVMe|   0100_0000_0100_0000_E4D2_5C00_0014_E214 합니다.|1600321314816|True| INTEL| SSDPE2KE016T7|  확인|
|eui.0100000001000000E4D25C000014E214 |5|        SSD|       NVMe|    0100_0000_0100_0000_E4D2_5C00_0014_E214 합니다.|  1600321314816|    True| INTEL| SSDPE2KE016T7|  확인|
|eui.0100000001000000E4D25C0000EEE214| 6|        SSD|       NVMe|    0100_0000_0100_0000_E4D2_5C00_00EE_E214 합니다.|  1600321314816|    True| INTEL| SSDPE2KE016T7|  확인|
|eui.0100000001000000E4D25C0000EEE214| 7|        SSD|       NVMe|    0100_0000_0100_0000_E4D2_5C00_00EE_E214 합니다.|  1600321314816|    True| INTEL| SSDPE2KE016T7|  확인|

이 문제를 해결 하려면 최신 버전으로 Intel 드라이브의 펌웨어를 업데이트 합니다.  펌웨어 버전 QDV101B1 2018 년 5 월에서에서이 문제를 해결 하려면 알려져 있습니다.

[2018 년 5 월 릴리스 Intel SSD 데이터 센터 도구에 대 한](https://downloadmirror.intel.com/27778/eng/Intel_SSD_Data_Center_Tool_3_0_12_Release_Notes_330715-026.pdf) 펌웨어 업데이트를 QDV101B1, Intel SSD DC P4600 시리즈에 대 한 포함 되어 있습니다.

    
## 실제 디스크 "정상" 고 작동 상태는 "풀에서 제거" 

Windows Server 2016 저장소 공간 다이렉트 클러스터에서 표시 될 수 있습니다 하나 이상의 실제 디스크에 대 한 HealthStatus ","정상으로 OperationalStatus는 "(제거 확인 풀에서)." 

"풀에서 제거" 의도 설정은 **제거 PhysicalDisk** 호출 되었지만 상태를 유지 하 고 제거 작업이 실패 한 경우를 복구할 수 있도록 하는 상태에 저장 합니다. 다음 방법 중 하나를 사용 하 여 정상으로의 OperationalStatus 수동으로 변경할 수 있습니다.

- 풀에서 실제 디스크를 제거한 다음 다시 추가 합니다.
- 의도 지우기 [지우기 PhysicalDiskHealthData.ps1 스크립트](https://go.microsoft.com/fwlink/?linkid=2034205) 를 실행 합니다. (으로 다운로드할 수는 있습니다. TXT 파일입니다. 로 저장 해야는 합니다. PS1 파일을 실행할 수 있습니다.)

스크립트를 실행 하는 방법을 보여 주는 몇 가지 예는 다음과 같습니다.

- **SerialNumber** 매개 변수를 사용 하 여 정상으로 설정 해야 하는 디스크를 지정 합니다. **WMI MSFT_PhysicalDisk** 또는 **Get-physicaldisk**에서 일련 번호를 얻을 수 있습니다. (사용 0 아래 나열 된 일련 번호에 대 한.)
   
   ```powershell
   Clear-PhysicalDiskHealthData -Intent -Policy -SerialNumber 000000000000000 -Verbose -Force
    ```

- (다시에서 **WMI MSFT_PhysicalDisk** 또는 **Get-physicaldisk**) 디스크를 지정 하려면 **고유 Id** 매개 변수를 사용 합니다.

   ```powershell
   Clear-PhysicalDiskHealthData -Intent -Policy -UniqueId 00000000000000000 -Verbose -Force
   ```

## 파일 복사가 느립니다.

파일 탐색기를 사용 하 여 가상 디스크에 큰 VHD를 복사 하는 문제를 볼 수-파일 복사 작업이 예상 보다 오래 걸립니다.

파일 탐색기를 사용 하 여 Robocopy 또는 Xcopy 가상 디스크에 큰 VHD를 복사 하 아닙니다 하는 것이 좋습니다 이렇게 하면 성능 예상된 보다 느립니다. 복사가 낮은 저장소 스택에 놓이는 대신 로컬 복사본 프로세스 처럼 작동 하며 저장소 공간 다이렉트 스택 통과 하지 않도록 합니다.

저장소 공간 다이렉트 성능 테스트 하려는 경우 VMFleet 및 Diskspd 부하 및 스트레스 테스트를 사용 하는 것이 좋습니다 기준선 저장소 공간 다이렉트 성능 기대치를 설정 하는 서버입니다.

## 노드의 나머지 부분에 노드를 다시 부팅 하는 동안 발생할 수 있는 이벤트 필요 합니다. 

이러한 이벤트를 무시 해도 안전 합니다. 

    Event ID 205: Windows lost communication with physical disk {XXXXXXXXXXXXXXXXXXXX }. This can occur if a cable failed or was disconnected, or if the disk itself failed. 

    Event ID 203: Windows lost communication with physical disk {xxxxxxxxxxxxxxxxxxxxxxxx }. This can occur if a cable failed or was disconnected, or if the disk itself failed. 

Azure Vm를 실행 중인 경우이 이벤트를 무시할 수 있습니다.

    Event ID 32: The driver detected that the device \Device\Harddisk5\DR5 has its write cache enabled. Data corruption may occur. 
    
## 성능이 저하 되거나 "손실 되지 않은 통신이 가능" "IO Error", "분리" 또는 Intel P3x00 NVMe 장치를 사용 하는 배포에 대 한 "아니요 중복성" 오류

저장소 공간 다이렉트 사용자에 게는 Intel P3x00 장치 제품군에 NVMe (NVM Express) "유지 관리 릴리스 8." 전에 펌웨어 버전에 따라 하드웨어를 사용 하는 영향을 주는 중요 한 문제를 파악 했습니다. 

>[!NOTE]
> 개별 Oem Intel P3x00 일련의 고유한 펌웨어 버전 문자열과 함께 NVMe 장치를 기반으로 하는 장치를 보유할 수 있습니다. 자세한 내용은의 최신 펌웨어 버전에 대 한 OEM을 문의 하십시오.

하드웨어 Intel P3x00 NVMe 장치 패밀리를 기반으로 하 여 배포를 사용 하는 경우 사용 가능한 최신 펌웨어를 즉시 적용 하는 것이 좋습니다 (적어도 유지 관리 릴리스 8). 이 [Microsoft 지원 문서](https://support.microsoft.com/en-us/help/4052341/slow-performance-or-lost-communication-io-error-detached-or-no-redunda) 는이 문제에 대 한 추가 정보를 제공합니다. 
