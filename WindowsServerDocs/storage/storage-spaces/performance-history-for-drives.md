---
title: 드라이브에 대 한 성능 기록
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7e1620f7010d4f37713de20f2b4c12f100be61dc
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474770"
---
# <a name="performance-history-for-drives"></a>드라이브에 대 한 성능 기록

> 적용 대상: 시작

[스토리지 공간 다이렉트에 대 한 성능 기록](performance-history.md) 의이 하위 항목에서는 드라이브에 대해 수집 된 성능 기록에 대해 자세히 설명 합니다. 성능 기록은 버스 또는 미디어 유형에 관계 없이 클러스터 저장소 하위 시스템의 모든 드라이브에 대해 사용할 수 있습니다. 그러나 OS 부팅 드라이브에는 사용할 수 없습니다.

   > [!NOTE]
   > 다운 된 서버에서 드라이브에 대 한 성능 기록을 수집할 수 없습니다. 서버를 다시 시작 하면 수집이 자동으로 다시 시작 됩니다.

## <a name="series-names-and-units"></a>계열 이름 및 단위

이러한 시리즈는 모든 적격 드라이브에 대해 수집 됩니다.

| 계열                          | 단위             |
|---------------------------------|------------------|
| `physicaldisk.iops.read`        | 초당       |
| `physicaldisk.iops.write`       | 초당       |
| `physicaldisk.iops.total`       | 초당       |
| `physicaldisk.throughput.read`  | 초당 바이트 수 |
| `physicaldisk.throughput.write` | 초당 바이트 수 |
| `physicaldisk.throughput.total` | 초당 바이트 수 |
| `physicaldisk.latency.read`     | 초          |
| `physicaldisk.latency.write`    | 초          |
| `physicaldisk.latency.average`  | 초          |
| `physicaldisk.size.total`       | 바이트            |
| `physicaldisk.size.used`        | 바이트            |

## <a name="how-to-interpret"></a>해석 방법

| 계열                          | 해석 방법                                                            |
|---------------------------------|-----------------------------------------------------------------------------|
| `physicaldisk.iops.read`        | 드라이브에서 완료 한 초당 읽기 작업 수입니다.                |
| `physicaldisk.iops.write`       | 드라이브에서 완료 한 초당 쓰기 작업 수입니다.               |
| `physicaldisk.iops.total`       | 드라이브에서 완료 한 초당 총 읽기 또는 쓰기 작업 수입니다. |
| `physicaldisk.throughput.read`  | 초당 드라이브에서 읽은 데이터의 양입니다.                            |
| `physicaldisk.throughput.write` | 초당 드라이브에 쓴 데이터 양입니다.                           |
| `physicaldisk.throughput.total` | 초당 드라이브에서 읽거나 쓴 총 데이터 양입니다.        |
| `physicaldisk.latency.read`     | 드라이브에서 읽기 작업의 평균 대기 시간입니다.                          |
| `physicaldisk.latency.write`    | 드라이브에 쓰기 작업의 평균 대기 시간입니다.                           |
| `physicaldisk.latency.average`  | 드라이브에 대 한 모든 작업의 평균 대기 시간입니다.                     |
| `physicaldisk.size.total`       | 드라이브의 총 저장소 용량입니다.                                    |
| `physicaldisk.size.used`        | 드라이브의 사용 된 저장소 용량입니다.                                     |

## <a name="where-they-come-from"></a>원본 위치

`iops.*`, `throughput.*` 및 계열은 드라이브가 `latency.*` 연결 된 `Physical Disk` 서버에 설정 된 성능 카운터에서 장치당 하나씩 수집 됩니다. 이러한 카운터는로 측정 되며 `partmgr.sys` Windows 소프트웨어 스택 및 네트워크 홉을 많이 포함 하지 않습니다. 장치 하드웨어 성능을 나타냅니다.

| 계열                          | 원본 카운터           |
|---------------------------------|--------------------------|
| `physicaldisk.iops.read`        | `Disk Reads/sec`         |
| `physicaldisk.iops.write`       | `Disk Writes/sec`        |
| `physicaldisk.iops.total`       | `Disk Transfers/sec`     |
| `physicaldisk.throughput.read`  | `Disk Read Bytes/sec`    |
| `physicaldisk.throughput.write` | `Disk Write Bytes/sec`   |
| `physicaldisk.throughput.total` | `Disk Bytes/sec`         |
| `physicaldisk.latency.read`     | `Avg. Disk sec/Read`     |
| `physicaldisk.latency.write`    | `Avg. Disk sec/Writes`   |
| `physicaldisk.latency.average`  | `Avg. Disk sec/Transfer` |

   > [!NOTE]
   > 카운터는 샘플링 되지 않고 전체 간격으로 측정 됩니다. 예를 들어 드라이브가 9 초 동안 유휴 상태 이지만 10 초 내에 30 개의 Io를 완료 하는 경우 `physicaldisk.iops.total` 이 10 초 간격 동안 평균 초당 3 개의 io로 기록 됩니다. 이렇게 하면 성능 기록이 모든 활동을 캡처하고 소음에 대해 강력 하 게 됩니다.

`size.*`계열은 `MSFT_PhysicalDisk` WMI의 클래스에서 하나씩 수집 됩니다.

| 계열                          | Source 속성        |
|---------------------------------|------------------------|
| `physicaldisk.size.total`       | `Size`                 |
| `physicaldisk.size.used`        | `VirtualDiskFootprint` |

## <a name="usage-in-powershell"></a>PowerShell에서 사용

[PhysicalDisk](https://docs.microsoft.com/powershell/module/storage/get-physicaldisk) cmdlet을 사용 합니다.

```PowerShell
Get-PhysicalDisk -SerialNumber <SerialNumber> | Get-ClusterPerf
```

## <a name="additional-references"></a>추가 참조

- [스토리지 공간 다이렉트에 대 한 성능 기록](performance-history.md)
