---
title: 이해 하 고 영구 메모리 배포
description: 영구 메모리 및 설정 저장소 공간을 사용 하 여 Windows Server 2019에 직접 하는 방법에 대 한 자세한 정보.
keywords: 저장소 공간 다이렉트를 영구 메모리, pmem, S2D 저장소
ms.assetid: ''
ms.prod: ''
ms.author: adagashe
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 3/26/2019
ms.localizationpriority: ''
ms.openlocfilehash: ed4b2669ad35a2ce0f818c65f7024ce905d9e4d6
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280041"
---
---
# <a name="understand-and-deploy-persistent-memory"></a>이해 하 고 영구 메모리 배포

>적용 대상: Windows Server 2019

영구 메모리 (또는 PMem)는 새로운 유형의 메모리 기술 경제적인 큰 용량 및 지 속성의 고유한 조합을 제공 하는 경우 이 항목에서는 저장소 공간 다이렉트를 사용 하 여 Windows Server 2019를 사용 하 여 배포 하는 단계와 PMem에서 배경 정보를 제공 합니다.

## <a name="background"></a>배경

PMem 형식인의 비휘발성 DRAM (NVDIMM) DRAM의 속도 갖지만 전원 주기 (메모리 남아 시스템 전원 중단 하는 경우에는 예기치 않은 전원 손실, 사용자가 시작한 종료, 시스템 작동 중단 발생 시 메모리 내용을 유지 하는 등) 이 인해 중단 된 위치에서 다시 시작이 훨씬 더 빠른 RAM의 콘텐츠를 다시 로드할 필요가 없으므로 합니다. 다른 고유한 특징은 PMem 합니다 (저장소 클래스 메모리 참조 중인 PMem 들릴 수 있습니다. 이유) 저장소로도 사용할 수 있습니다 즉 바이트 주소를 지정할 수입니다.


이러한 혜택 중 일부를 보려면 살펴보겠습니다이 Microsoft Ignite 2018에서 데모:

[![Microsoft Ignite 2018 Pmem demo](http://img.youtube.com/vi/8WMXkMLJORc/0.jpg)](http://www.youtube.com/watch?v=8WMXkMLJORc)

반드시 내결함성을 제공 하는 모든 저장소 시스템에는 네트워크를 트래버스해야 하 고 백 엔드 쓰기 증폭을 초래 하는 쓰기의 분산 복사본입니다. 절대 최대 IOPS 벤치 마크 숫자 따라서 일반적으로 저장소 시스템에는 저장소 공간 다이렉트는 가능한 경우 로컬 복사본을 읽을 일반적인 최적화 하는 경우에 특히 읽기 전용을 사용 하 여 수행 됩니다.

**100% 읽기를 사용 하 여 클러스터 13,798,674 IOPS를 제공합니다.**

![13.7 m IOPS 레코드 스크린 샷](media/deploy-pmem/iops-record.png)

비디오를 밀접 하 게 보려면를 보면 thatwhat의도 더 즐기세요 대기 시간입니다: Windows에서 파일 시스템 보다 일관 되 게 작은 40 µs 대기 시간이 넘는 13.7 M IOPS에도 보고! (즉 기호 하나 1 초의 시간 (마이크로초)에 대 한 합니다.) 이것이 새로운 일반적인 모든 플래시 공급 업체 자랑 스럽게 보급 오늘 보다 빠르게 배입니다.

함께 획기적인 성능을 Windows Server 2019 및 Intel® Optane™ DC 영구 메모리 저장소 공간 다이렉트 제공 합니다. 이 업계 최고의 HCI 벤치 마크 13.7 m 개 IOPS, 예측 가능 하 고 매우 짧은 대기 시간으로는 2 배 이상의 우리의 이전 업계 최고의 벤치 마크 6.7 m IOPS. 게다가이 이번 필요 했습니다만 12 서버 노드를 25 %2 년 전 미만입니다.

![IOPS 향상](media/deploy-pmem/iops-gains.png)

사용 되는 하드웨어 3 방향 미러링을 사용 하 여 12 서버 클러스터 되어 ReFS 볼륨 구분 **12** x Intel® S2600WFT **384 GiB** 메모리, 코어 2 x 28 "CascadeLake" **1.5TB**Intel® Optane™ DC 영구 캐시 메모리 **32TB** 용량으로 (4 x 8 TB Intel® DC P4510) NVMe **2** Mellanox ConnectX 4 25 g b p s x

아래 표에 전체 성능 수치에 있습니다. 

| 벤치 마크                   | 성능         |
|-----------------------------|---------------------|
| 4k 100% 임의 읽기         | 13.8 백만 IOPS   |
| 4K 90/10% Random Read/Write | 9.45 백만 IOPS   |
| 2MB 순차적 읽기         | 549 g B/초 처리량 |

### <a name="supported-hardware"></a>지원 되는 하드웨어

아래 표에 Windows Server 2019 및 Windows Server 2016에 대 한 지원 되는 영구 메모리 하드웨어를 표시합니다. 메모리 내 모드 및 앱 직접 모드 모두 Intel Optane 특히 지원함을 참고 합니다. Windows Server 2019 혼합 모드 작업을 지원 합니다.

| 영구 메모리 기술                                      | Windows Server 2016 | Windows Server 2019 |
|-------------------------------------------------------------------|--------------------------|--------------------------|
| **Nvdimm-n** 앱 직접 모드에서                                       | 지원됨                | 지원됨                |
| **Intel Optane™ DC 영구 메모리** 앱 직접 모드에서             | 지원되지 않음            | 지원됨                |
| **Intel Optane™ DC 영구 메모리** 2-수준 메모리 모드 (2LM) | 지원되지 않음            | 지원됨                |

이제 영구 메모리를 구성 하는 방법에 설명 하겠습니다.

## <a name="interleave-sets"></a>인터리브 집합

### <a name="understanding-interleave-sets"></a>이해 인터리브 집합

Nvdimm-n 있는 표준 DIMM (메모리) 슬롯에서 프로세서 (즉, 대기 시간 단축 및 더 나은 성능을 페치)에 더 가까운 곳에 데이터 배치를 회수 합니다. 이 빌드하려면 인터리브 집합을를 두 개 이상의 NVDIMMs 향상 된 처리량에 대 한 스트라이프 읽기/쓰기 작업 수 있도록 설정 하는 N 방향 인터리빙을 만들 때. 가장 일반적인 설치 2 방향 또는 4 방향 인터리빙 됩니다.

종종 Windows 서버에 단일 논리 디스크로 표시 되는 여러 영구 메모리 장치를 확인 하는 플랫폼의 BIOS에서 인터리브 집합을 만들 수 있습니다. 실행 하 여 물리적 장치의 인터리브 집합을 포함 하는 각 영구 메모리 논리 디스크:

```PowerShell
Get-PmemDisk
```

출력 예는 다음과 같습니다.

```
DiskNumber Size   HealthStatus AtomicityType CanBeRemoved PhysicalDeviceIds UnsafeShutdownCount
---------- ----   ------------ ------------- ------------ ----------------- -------------------
2          252 GB Healthy      None          True         {20, 120}         0
3          252 GB Healthy      None          True         {1020, 1120}      0
```

논리적 pmem 디스크 # 2에 Id20 및 Id120 물리적 장치 있고 논리 pmem 디스크 3 Id1020 및 Id1120 물리적 장치를 볼 수 있습니다. 또한 Get-PmemPhysicalDevice 아래와 같이 설정 인터리브에서의 모든 실제 NVDIMMs를 가져오려고에 특정 pmem 디스크를 공급할 수 것입니다.


```PowerShell
(Get-PmemDisk)[0] | Get-PmemPhysicalDevice
```

출력 예는 다음과 같습니다.

```
DeviceId DeviceType           HealthStatus OperationalStatus PhysicalLocation FirmwareRevision Persistent memory size Volatile memory size
-------- ----------           ------------ ----------------- ---------------- ---------------- ---------------------- --------------------
20       Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_C1     102005310        126 GB                 0 GB
120      Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_F1     102005310        126 GB                 0 GB
```

### <a name="configuring-interleave-sets"></a>집합을 인터리브 구성

인터리브 집합을 구성 하려면 다음 PowerShell cmdlet을 실행 합니다.

```PowerShell
Get-PmemUnusedRegion

RegionId TotalSizeInBytes DeviceId
-------- ---------------- --------
       1     270582939648 {20, 120}
       3     270582939648 {1020, 1120}
```

이 시스템에 있는 영구 메모리 논리 디스크에 할당 되지 않은 모든 영구 메모리 지역을 보여 줍니다.

시스템에서 장치 유형, 위치 등의 모든 영구 메모리 장치 정보를 보려면 상태 및 작업 상태 등 실행할 수 있습니다 다음 cmdlet을 로컬 서버에서.

```PowerShell
Get-PmemPhysicalDevice

DeviceId DeviceType           HealthStatus OperationalStatus PhysicalLocation FirmwareRevision Persistent memory size Volatile
                                                                                                                      memory size
-------- ----------           ------------ ----------------- ---------------- ---------------- ---------------------- --------------
1020     Intel INVDIMM device Healthy      {Ok}              CPU2_DIMM_C1     102005310        126 GB                 0 GB
1120     Intel INVDIMM device Healthy      {Ok}              CPU2_DIMM_F1     102005310        126 GB                 0 GB
120      Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_F1     102005310        126 GB                 0 GB
20       Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_C1     102005310        126 GB                 0 GB
```

사용할 수 있는 사용 되지 않는 pmem 지역 있으므로 새 영구 메모리 디스크 만들 수 있습니다. 사용 되지 않은 영역을 사용 하 여 영구 메모리 디스크가 여러 개 만들 수 있습니다.

```PowerShell
Get-PmemUnusedRegion | New-PmemDisk
Creating new persistent memory disk. This may take a few moments.
```

이렇게 한 후에 실행 하 여 결과 볼 수 있습니다.

```PowerShell
Get-PmemDisk

DiskNumber Size   HealthStatus AtomicityType CanBeRemoved PhysicalDeviceIds UnsafeShutdownCount
---------- ----   ------------ ------------- ------------ ----------------- -------------------
2          252 GB Healthy      None          True         {20, 120}         0
3          252 GB Healthy      None          True         {1020, 1120}      0
```

에서는 실행 되었을 수 있습니다 주목할 만한 가치가 **Get-physicaldisk | 여기서 SCM MediaType-Eq** 대신 **Get PmemDisk** 동일한 결과를 가져옵니다. 새로 만든된 영구 메모리 디스크 1:1 PowerShell 및 Windows Admin Center 표시 되는 드라이브에 해당 합니다.

### <a name="using-persistent-memory-for-cache-or-capacity"></a>영구 메모리를 사용 하 여 캐시에 용량

Windows Server 2019에 저장소 공간 다이렉트는 영구 메모리를 사용 하 여 캐시 또는 용량 드라이브를 지원 합니다. 이 참조 하세요 [설명서](understand-the-cache.md) 캐시 및 용량 드라이브 설정에 대 한 자세한 내용은 합니다.

## <a name="creating-a-dax-volume"></a>DAX 볼륨 만들기

### <a name="understanding-dax"></a>DAX 이해

영구 메모리에 액세스 하는 방법은 두 가지가 있습니다. 구현되지 않은 것은 다음과 같습니다.

1. **직접 액세스 (DAX)** , 가장 낮은 대기 시간을 가져오려면 메모리 같은 작동 하는 합니다. 응용 프로그램 스택을 무시 하 고 영구 메모리를 직접 수정 합니다. 이 사용할 수 있도록만 NTFS를 사용 하 여 note 합니다.
2. **액세스 차단**, 응용 프로그램 호환성에 대 한 저장소와 같은 작동 하는 합니다. 이 설치에서 스택을 통해 데이터 흐름 및 NTFS 및 ReFS를 사용 하 여 사용할 수 있습니다.

아래 예를 확인할 수 있습니다.

![DAX 스택](media/deploy-pmem/dax.png)

### <a name="configuring-dax"></a>DAX를 구성합니다.

영구 메모리에 DAX 볼륨을 만들려면 PowerShell cmdlet을 사용 해야 합니다. 사용 하 여 합니다 **-IsDax** 스위치를 사용 하도록 설정 하는 DAX를 볼륨을 포맷할 수 있습니다.

```PowerShell
Format-Volume -IsDax:$true
```

다음 코드 조각은 영구 메모리 디스크에는 DAX 볼륨을 만들 수 있습니다.

```PowerShell
# Here we use the first pmem disk to create the volume as an example
$disk = (Get-PmemDisk)[0] | Get-PhysicalDisk | Get-Disk
# Initialize the disk to GPT if it is not initialized
If ($disk.partitionstyle -eq "RAW") {$disk | Initialize-Disk -PartitionStyle GPT}
# Create a partition with drive letter 'S' (can use any available drive letter)
$disk | New-Partition -DriveLetter S -UseMaximumSize


   DiskPath: \\?\scmld#ven_8980&dev_097a&subsys_89804151&rev_0018#3&1b1819f6&0&03018089fb63494db728d8418b3cbbf549997891#{53f56307-b6
bf-11d0-94f2-00a0c91efb8b}

PartitionNumber  DriveLetter Offset                                               Size Type
---------------  ----------- ------                                               ---- ----
2                S           16777216                                        251.98 GB Basic

# Format the volume with drive letter 'S' to DAX Volume
Format-Volume -FileSystem NTFS -IsDax:$true -DriveLetter S

DriveLetter FriendlyName FileSystemType DriveType HealthStatus OperationalStatus SizeRemaining      Size
----------- ------------ -------------- --------- ------------ ----------------- -------------      ----
S                        NTFS           Fixed     Healthy      OK                    251.91 GB 251.98 GB

# Verify the volume is DAX enabled
Get-Partition -DriveLetter S | fl


UniqueId             : {00000000-0000-0000-0000-000100000000}SCMLD\VEN_8980&DEV_097A&SUBSYS_89804151&REV_0018\3&1B1819F6&0&03018089F
                       B63494DB728D8418B3CBBF549997891:WIN-8KGI228ULGA
AccessPaths          : {S:\, \\?\Volume{cf468ffa-ae17-4139-a575-717547d4df09}\}
DiskNumber           : 2
DiskPath             : \\?\scmld#ven_8980&dev_097a&subsys_89804151&rev_0018#3&1b1819f6&0&03018089fb63494db728d8418b3cbbf549997891#{5
                       3f56307-b6bf-11d0-94f2-00a0c91efb8b}
DriveLetter          : S
Guid                 : {cf468ffa-ae17-4139-a575-717547d4df09}
IsActive             : False
IsBoot               : False
IsHidden             : False
IsOffline            : False
IsReadOnly           : False
IsShadowCopy         : False
IsDAX                : True                   # <- True: DAX enabled
IsSystem             : False
NoDefaultDriveLetter : False
Offset               : 16777216
OperationalStatus    : Online
PartitionNumber      : 2
Size                 : 251.98 GB
Type                 : Basic
```

## <a name="monitoring-health"></a>상태 모니터링

영구 메모리를 사용 하면 가지 모니터링 환경에서 몇 가지 차이점이 있습니다.

1. 영구 메모리 성능 카운터, 경우에 표시 되지 않습니다 있도록 Windows Admin Center 차트에 표시 되는 실제 디스크를 만들지 않습니다.
2. 자동 관리 이상 값 검색을 얻을 수 없습니다 있도록 영구 메모리 Storport 505 데이터를 만들지 않습니다.

외에도 모니터링 환경은 다른 실제 디스크와 동일 합니다. 실행 하 여 영구 메모리 디스크의 상태를 쿼리할 수 있습니다.

```PowerShell
Get-PmemDisk

DiskNumber Size   HealthStatus AtomicityType CanBeRemoved PhysicalDeviceIds UnsafeShutdownCount
---------- ----   ------------ ------------- ------------ ----------------- -------------------
2          252 GB Unhealthy    None          True         {20, 120}         2
3          252 GB Healthy      None          True         {1020, 1120}      0

Get-PmemDisk | Get-PhysicalDisk | select SerialNumber, HealthStatus, OperationalStatus, OperationalDetails

SerialNumber               HealthStatus OperationalStatus  OperationalDetails
------------               ------------ ------------------ ------------------
802c-01-1602-117cb5fc      Healthy      OK
802c-01-1602-117cb64f      Warning      Predictive Failure {Threshold Exceeded,NVDIMM_N Error}
```

**HealthStatus** 영구 메모리 디스크 정상 인지 하는 경우를 보여 줍니다. 합니다 **UnsafeshutdownCount** 종료가 논리 디스크에서 데이터 손실을 일으킬 수 있는 횟수를 추적 합니다. 이 디스크의 모든 기본 영구 메모리 장치를 안전 하지 않은 종료 수의 합계가 표시 됩니다. 또한 사용할 수는 아래 명령을 쿼리 상태 정보입니다. 합니다 **OperationalStatus** 하 고 **OperationalDetails** 상태에 대 한 자세한 정보를 제공 합니다.

영구 메모리 장치의 상태를 쿼리하려면:

```PowerShell
Get-PmemPhysicalDevice

DeviceId DeviceType           HealthStatus OperationalStatus PhysicalLocation FirmwareRevision Persistent memory size Volatile memory size
-------- ----------           ------------ ----------------- ---------------- ---------------- ---------------------- --------------------
1020     Intel INVDIMM device Healthy      {Ok}              CPU2_DIMM_C1     102005310        126 GB                 0 GB
1120     Intel INVDIMM device Healthy      {Ok}              CPU2_DIMM_F1     102005310        126 GB                 0 GB
120      Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_F1     102005310        126 GB                 0 GB
20       Intel INVDIMM device Unhealthy    {HardwareError}   CPU1_DIMM_C1     102005310        126 GB                 0 GB
```

영구 메모리 장치 정상이 아님을 보여 줍니다. 정상이 아닌 장치 (**DeviceId**) 20 위 예제의 경우 일치 합니다. 합니다 **PhysicalLocation** BIOS에서 식별할 수 있는 영구 메모리 장치가 잘못 된 상태입니다.

## <a name="replacing-persistent-memory"></a>영구 메모리를 대체합니다.

위의 영구 메모리의 상태를 확인 하는 방법을 설명 했습니다. 실패 한 모듈을 교체 해야 할 경우 영구 메모리 디스크를 다시 프로 비전 해야 합니다 (앞에서 설명한 것 단계 참조).

사용 해야이 문제를 해결 하는 경우 **제거 PmemDisk**, 특정 영구 메모리 디스크를 제거 합니다. 모든 현재 영구 디스크에서 제거할 수 있습니다.

```PowerShell
Get-PmemDisk | Remove-PmemDisk

cmdlet Remove-PmemDisk at command pipeline position 1
Supply values for the following parameters:
DiskNumber: 2

This will remove the persistent memory disk(s) from the system and will result in data loss.
Remove the persistent memory disk(s)?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): Y
Removing the persistent memory disk. This may take a few moments.
```

영구 메모리 디스크를 제거 하면 해당 디스크에 대해 데이터 손실을 확인 하는 것이 반드시 합니다.

해야 할 수 있습니다 다른 cmdlet은 **Initialize PmemPhysicalDevice**, 레이블 저장소 영역 영구 메모리 물리적 장치의 초기화 됩니다. 이 영구 메모리 장치에서 손상 된 레이블 저장소 정보를 제거할 수 있습니다.

```PowerShell
Get-PmemPhysicalDevice | Initialize-PmemPhysicalDevice

This will initialize the label storage area on the physical persistent memory device(s) and will result in data loss.
Initializes the physical persistent memory device(s)?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): A
Initializing the physical persistent memory device. This may take a few moments.
Initializing the physical persistent memory device. This may take a few moments.
Initializing the physical persistent memory device. This may take a few moments.
Initializing the physical persistent memory device. This may take a few moments.
```

반드시 관련 문제를 영구 메모리를 해결 하려면이 명령을 최후의 수단으로 사용할 수 해야 합니다. 영구 메모리에 데이터 손실이 발생 합니다.

## <a name="see-also"></a>참조

- [저장소 공간 다이렉트 개요](storage-spaces-direct-overview.md)
- [Windows의 저장소 클래스 메모리 (Nvdimm-n) 상태 관리](storage-class-memory-health.md)
- [캐시 이해](understand-the-cache.md)