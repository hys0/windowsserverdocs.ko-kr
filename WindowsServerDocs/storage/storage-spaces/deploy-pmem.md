---
title: 영구 메모리 이해 및 배포
description: 영구적 메모리가 무엇 인지, Windows Server 2019에서 저장소 공간 다이렉트를 사용 하 여 설정 하는 방법에 대 한 자세한 정보를 제공 합니다.
ms.prod: windows-server
ms.author: adagashe
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 1/27/2020
ms.localizationpriority: medium
ms.openlocfilehash: 2f5f88ac2ec728e176735ad58d9d67112583c527
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85469648"
---
# <a name="understand-and-deploy-persistent-memory"></a>영구 메모리 이해 및 배포

> 적용 대상: 시작

영구적 메모리 (또는 PMem)는 경제적인 대용량 및 지 속성의 고유한 조합을 제공 하는 새로운 유형의 메모리 기술입니다. 이 문서에서는 PMem의 배경 및 스토리지 공간 다이렉트을 사용 하 여 Windows Server 2019에 배포 하는 단계를 제공 합니다.

## <a name="background"></a>배경

PMem은 전원 주기를 통해 해당 콘텐츠를 유지 하는 비 휘발성 RAM (NVDIMM-N)의 유형입니다. 예기치 않은 정전이 발생 하거나 사용자가 시스템을 시작한 후 시스템 작동이 중단 되는 경우에도 메모리 내용이 유지 됩니다. 이 고유한 특징은 PMem을 저장소로 사용할 수도 있음을 의미 합니다. 이것은 사용자가 PMem을 "저장소 클래스 메모리"로 지칭 하는 이유입니다.

이러한 혜택 중 일부를 보려면 Microsoft Ignite 2018의 다음 데모를 살펴보겠습니다.

[![Microsoft Ignite 2018 Pmem 데모](http://img.youtube.com/vi/8WMXkMLJORc/0.jpg)](http://www.youtube.com/watch?v=8WMXkMLJORc)

내결함성 기능을 제공 하는 모든 저장소 시스템은 반드시 분산 된 쓰기 복사본을 만듭니다. 이러한 작업은 네트워크를 트래버스 하 고 백 엔드 쓰기 강화 합니다. 이러한 이유로, 일반적으로 가장 큰 IOPS 벤치 마크 번호는 읽기 전용을 측정 하 여 수행 됩니다. 특히 저장소 시스템에서 가능 하면 로컬 복사를 읽을 수 있는 일반적인 의미의 최적화가 있는 경우입니다. 스토리지 공간 다이렉트는이 작업을 위해 최적화 되어 있습니다.

**읽기 작업만 사용 하 여 측정 하는 경우 클러스터는 13798674 IOPS를 제공 합니다.**

![13.7 m IOPS 레코드 스크린샷](media/deploy-pmem/iops-record.png)

비디오를 자세히 시청 하는 경우 훨씬 더 jaw 된 것은 대기 시간입니다. 13.7 M s IOPS를 초과 하는 경우에도 Windows의 파일 시스템은 40 μs 보다 일관 된 대기 시간을 보고 합니다. (마이크로초의 경우 1 초에 해당 하는 1 1/1000000) 이 속도는 일반적인 모든 플래시 공급 업체 다니며 오늘 광고 하는 것 보다 더 빠른 크기의 순서입니다.

Windows Server 2019 및 Intel &reg; Optane &trade; DC 영구 메모리의 스토리지 공간 다이렉트은 혁신적인 성능을 제공 합니다. 예측 가능 하 고 매우 짧은 대기 시간과 함께 13.7 M IOPS에 대 한 업계 최고의 HCI 벤치 마크는 6.7 M IOPS의 이전 업계 최고의 벤치 마크를 2 배 이상 제공 합니다. 이번에는 &mdash; 2 년 전에는 12 개의 서버 노드만 25% 미만으로 필요 했습니다.

![IOPS 향상](media/deploy-pmem/iops-gains.png)

테스트 하드웨어는 3 방향 미러링과 구분 된 ReFS 볼륨, **12** x intel &reg; S2600WFT, **384 GiB** memory, 2 x 28-코어 "CascadeLake," **1.5 TB** intel &reg; OPTANE &trade; DC 영구적 메모리를 캐시로, **32 TB** NVMe (4 x 8 TB intel &reg; DC P4510)를 용량, **2** x Mellanox connectx-3-4 25 Gbps로 사용 하도록 구성 된 12-서버 클러스터 였습니다.

다음 표에서는 전체 성능 수치를 보여 줍니다.

| 벤치마크                   | 성능         |
|-----------------------------|---------------------|
| 4K 100% 무작위 읽기         | 1380만 IOPS   |
| 4K 90/10% 무작위 읽기/쓰기 | 945만 IOPS   |
| 2mb 순차 읽기         | 549 g b/초 처리량 |

### <a name="supported-hardware"></a>지원되는 하드웨어

다음 표에서는 Windows Server 2019 및 Windows Server 2016에 대해 지원 되는 영구 메모리 하드웨어를 보여 줍니다.

| 영구적 메모리 기술                                      | Windows Server 2016 | Windows Server 2019 |
|-------------------------------------------------------------------|--------------------------|--------------------------|
| 영구 모드의 **nvdimm-n**                                  | 지원됨                | 지원 여부                |
| **Intel Optane &trade; **앱 직접 모드의 DC 영구 메모리             | 지원되지 않음            | 지원됨                |
| **Intel Optane &trade; 메모리 모드의 DC 영구적 메모리** | 지원됨            | 지원 여부                |

> [!NOTE]
> Intel Optane는 *메모리* (휘발성) 및 *App Direct* (영구) 모드를 모두 지원 합니다.

> [!NOTE]
> &reg; &trade; 여러 네임 스페이스로 나뉜 앱 직접 모드에서 여러 Intel Optane PMem 모듈이 있는 시스템을 다시 시작 하는 경우 관련 된 논리 저장소 디스크의 일부 또는 전체에 대 한 액세스 권한이 손실 될 수 있습니다. 이 문제는 버전 1903 이전 버전의 Windows Server 2019 버전에서 발생 합니다.
>
> 이 액세스 손실는 PMem 모듈이 학습 되지 않거나 시스템이 시작 될 때 실패 하는 경우에 발생 합니다. 이러한 경우에는 실패 한 모듈에 실제로 매핑되지 않는 네임 스페이스를 포함 하 여 시스템의 모든 PMem 모듈에 있는 모든 저장소 네임 스페이스에 오류가 발생 합니다.
>
> 모든 네임 스페이스에 대 한 액세스를 복원 하려면 실패 한 모듈을 바꿉니다.
>
> Windows Server 2019 버전 1903 또는 최신 버전에서 모듈이 실패 하면 영향을 받는 모듈에 실제로 매핑되는 네임 스페이스에만 액세스할 수 있습니다. 다른 네임 스페이스는 영향을 받지 않습니다.

이제 영구 메모리를 구성 하는 방법을 살펴보겠습니다.

## <a name="interleaved-sets"></a>인터리브 집합

### <a name="understanding-interleaved-sets"></a>인터리브 집합 이해

NVDIMM-N은 데이터를 프로세서에 더 가깝게 배치 하는 표준 DIMM (메모리) 슬롯에 상주 합니다. 이 구성은 대기 시간을 줄이고 인출 성능을 향상 시킵니다. 처리량을 늘리기 위해 둘 이상의 NVDIMMs는 읽기/쓰기 작업을 위해 n 방향 인터리브 집합을 만듭니다. 가장 일반적인 구성은 양방향 또는 4 방향 인터리브입니다. 인터리브 집합을 사용 하면 여러 영구 메모리 장치가 Windows Server에 단일 논리 디스크로 표시 됩니다. 다음과 같이 Windows PowerShell **PmemDisk** cmdlet을 사용 하 여 이러한 논리 디스크의 구성을 검토할 수 있습니다.

```PowerShell
Get-PmemDisk

DiskNumber Size   HealthStatus AtomicityType CanBeRemoved PhysicalDeviceIds UnsafeShutdownCount
---------- ----   ------------ ------------- ------------ ----------------- -------------------
2          252 GB Healthy      None          True         {20, 120}         0
3          252 GB Healthy      None          True         {1020, 1120}      0
```

논리적 PMem 디스크 #2는 물리적 장치 Id20 및 Id120를 사용 하 고, 논리적 PMem 디스크 #3는 물리적 장치 Id1020 및 Id1120를 사용 하는 것을 볼 수 있습니다.

논리 드라이브에서 사용 하는 인터리브 집합에 대 한 추가 정보를 검색 하려면 **PmemPhysicalDevice** cmdlet을 실행 합니다.

```PowerShell
(Get-PmemDisk)[0] | Get-PmemPhysicalDevice

DeviceId DeviceType           HealthStatus OperationalStatus PhysicalLocation FirmwareRevision Persistent memory size Volatile memory size
-------- ----------           ------------ ----------------- ---------------- ---------------- ---------------------- --------------------
20       Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_C1     102005310        126 GB                 0 GB
120      Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_F1     102005310        126 GB                 0 GB
```

### <a name="configuring-interleaved-sets"></a>인터리브 집합 구성

인터리브 집합을 구성 하려면 시스템의 논리적 PMem 디스크에 할당 되지 않은 모든 영구 메모리 영역을 검토 하 여 시작 합니다. 이렇게 하려면 다음 PowerShell cmdlet을 실행 합니다.

```PowerShell
Get-PmemUnusedRegion

RegionId TotalSizeInBytes DeviceId
-------- ---------------- --------
       1     270582939648 {20, 120}
       3     270582939648 {1020, 1120}
```

장치 유형, 위치, 상태 및 작동 상태 등을 포함 하 여 시스템의 모든 PMem 장치 정보를 보려면 로컬 서버에서 다음 cmdlet을 실행 합니다.

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

사용 가능한 사용 가능한 PMem 지역이 있으므로 새 영구 메모리 디스크를 만들 수 있습니다. 사용 하지 않는 영역을 사용 하 여 다음 cmdlet을 실행 하 여 영구 메모리 디스크를 여러 개 만들 수 있습니다.

```PowerShell
Get-PmemUnusedRegion | New-PmemDisk
Creating new persistent memory disk. This may take a few moments.
```

이 작업이 완료 되 면 다음을 실행 하 여 결과를 볼 수 있습니다.

```PowerShell
Get-PmemDisk

DiskNumber Size   HealthStatus AtomicityType CanBeRemoved PhysicalDeviceIds UnsafeShutdownCount
---------- ----   ------------ ------------- ------------ ----------------- -------------------
2          252 GB Healthy      None          True         {20, 120}         0
3          252 GB Healthy      None          True         {1020, 1120}      0
```

PhysicalDisk을 실행할 수 있습니다. ** 여기서 MediaType** 은 동일한 결과를 얻기 위해 **PmemDisk** 대신 합니다. 새로 만든 PMem 디스크는 PowerShell 및 Windows 관리 센터에 표시 되는 드라이브와 일대일로 일치 합니다.

### <a name="using-persistent-memory-for-cache-or-capacity"></a>캐시 또는 용량에 영구적 메모리 사용

Windows Server 2019에 대 한 스토리지 공간 다이렉트는 영구적 메모리를 캐시 또는 용량 드라이브로 사용 하도록 지원 합니다. 캐시 및 용량 드라이브를 설정 하는 방법에 대 한 자세한 내용은 [스토리지 공간 다이렉트 캐시 이해](understand-the-cache.md)를 참조 하세요.

## <a name="creating-a-dax-volume"></a>DAX 볼륨 만들기

### <a name="understanding-dax"></a>DAX 이해

영구 메모리에 액세스 하는 방법에는 두 가지가 있습니다. 아래에 이 계정과 키의 예제가 나와 있습니다.

1. **직접 액세스 (DAX)**: 메모리와 같이 작동 하 여 가장 짧은 대기 시간을 가져옵니다. 앱은 스택을 무시 하 고 영구적 메모리를 직접 수정 합니다. DAX는 NTFS와 함께 사용 하는 경우에만 사용할 수 있습니다.
1. 응용 프로그램 호환성을 위해 저장소와 같이 작동 하는 **액세스를 차단**합니다. 이 구성 데이터는 스택을 통해 흐릅니다. NTFS 및 ReFS와 함께이 구성을 사용할 수 있습니다.

다음 그림은 DAX 구성의 예를 보여 줍니다.

![DAX 스택](media/deploy-pmem/dax.png)

### <a name="configuring-dax"></a>DAX 구성

영구적 메모리 디스크에 DAX 볼륨을 만들려면 PowerShell cmdlet을 사용 해야 합니다. **-Isdax** 스위치를 사용 하 여 DAX를 사용 하도록 볼륨을 포맷할 수 있습니다.

```PowerShell
Format-Volume -IsDax:$true
```

다음 코드 조각은 영구적 메모리 디스크에 DAX 볼륨을 만드는 데 도움이 됩니다.

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

영구적 메모리를 사용 하는 경우 모니터링 환경에는 몇 가지 차이점이 있습니다.

- 영구적 메모리는 실제 디스크 성능 카운터를 만들지 않으므로 Windows 관리 센터의 차트에 표시 되지 않습니다.
- 영구 메모리는 Storport 505 데이터를 만들지 않으므로 사전 이상 값 검색을 얻지 못합니다.

그 외에도 모니터링 환경은 다른 실제 디스크의 경우와 동일 합니다. 다음 cmdlet을 실행 하 여 영구 메모리 디스크의 상태를 쿼리할 수 있습니다.

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

**HealthStatus** 는 PMem 디스크가 정상 상태 인지 여부를 표시 합니다.

**UnsafeshutdownCount** 값은이 논리 디스크에 대 한 데이터 손실을 유발할 수 있는 종료 횟수를 추적 합니다. 이 디스크의 모든 기본 PMem 장치에 대 한 안전 하지 않은 종료 횟수의 합계입니다. 상태에 대 한 자세한 내용을 보려면 **PmemPhysicalDevice** cmdlet을 사용 하 여 **OperationalStatus**와 같은 정보를 찾습니다.

```PowerShell
Get-PmemPhysicalDevice

DeviceId DeviceType           HealthStatus OperationalStatus PhysicalLocation FirmwareRevision Persistent memory size Volatile memory size
-------- ----------           ------------ ----------------- ---------------- ---------------- ---------------------- --------------------
1020     Intel INVDIMM device Healthy      {Ok}              CPU2_DIMM_C1     102005310        126 GB                 0 GB
1120     Intel INVDIMM device Healthy      {Ok}              CPU2_DIMM_F1     102005310        126 GB                 0 GB
120      Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_F1     102005310        126 GB                 0 GB
20       Intel INVDIMM device Unhealthy    {HardwareError}   CPU1_DIMM_C1     102005310        126 GB                 0 GB
```

이 cmdlet은 비정상 상태인 영구적 메모리 장치를 표시 합니다. 비정상 장치 (**DeviceId** 20)는 이전 예제의 경우와 일치 합니다. BIOS의 **PhysicalLocation** 는 잘못 된 상태의 영구적 메모리 장치를 식별 하는 데 도움이 될 수 있습니다.

## <a name="replacing-persistent-memory"></a>영구적 메모리 바꾸기

이 문서에서는 영구적 메모리의 상태를 보는 방법을 설명 합니다. 오류가 발생 한 모듈을 교체 해야 하는 경우에는 PMem 디스크를 다시 프로 비전 해야 합니다 (앞에서 설명한 단계를 참조).

문제를 해결 하는 경우 **PmemDisk**를 사용 해야 할 수 있습니다. 이 cmdlet은 특정 영구 메모리 디스크를 제거 합니다. 다음 cmdlet을 실행 하 여 현재 PMem 디스크를 모두 제거할 수 있습니다.

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

> [!IMPORTANT]
> 영구적 메모리 디스크를 제거 하면 해당 디스크의 데이터가 손실 됩니다.

필요할 수 있는 다른 cmdlet은 **PmemPhysicalDevice**입니다. 이 cmdlet은 실제 영구적 메모리 장치에서 레이블 저장소 영역을 초기화 하 고 PMem 장치에서 손상 된 레이블 저장소 정보를 지울 수 있습니다.

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

> [!IMPORTANT]
> **PmemPhysicalDevice** 는 영구적 메모리의 데이터 손실을 일으킵니다. 영구적 메모리 관련 문제를 해결 하는 마지막 수단으로 사용 합니다.

## <a name="additional-references"></a>추가 참조

- [스토리지 공간 다이렉트 개요](storage-spaces-direct-overview.md)
- [Windows의 스토리지 클래스 메모리(NVDIMM-N) 상태 관리](storage-class-memory-health.md)
- [캐시 이해](understand-the-cache.md)
