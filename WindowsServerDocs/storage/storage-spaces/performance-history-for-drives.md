---
title: 드라이브에 대 한 성능 기록
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
Keywords: 저장소 공간 다이렉트
ms.localizationpriority: medium
ms.openlocfilehash: d162275a885dac79e7efe749328ebdca471fcad1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879194"
---
# <a name="performance-history-for-drives"></a>드라이브에 대 한 성능 기록

> 적용 대상: Windows Server Insider Preview

이 하위 항목의 [저장소 공간 다이렉트에 대 한 성능 기록을](performance-history.md) 드라이브에 대 한 수집 된 성능 기록 세부 정보에 설명 합니다. 성능 기록, 버스에 관계 없이 클러스터 저장소 하위 시스템에서 모든 드라이브에 대 한 사용 가능한 되었거나 미디어 유형입니다. 그러나 OS 부팅 드라이브에 대해 사용할 수 없는 경우

   > [!NOTE]
   > 성능 기록 드라이브 아래에 있는 서버에 대해 수집할 수 없습니다. 컬렉션을 고 서버가 다시 시작 되 면 자동으로 재개 합니다.

## <a name="series-names-and-units"></a>계열 이름 및 단위

이 시리즈는 모든 적격 드라이브에 대 한 수집 됩니다.

| 시리즈                          | 단위             |
|---------------------------------|------------------|
| `physicaldisk.iops.read`        | 초당       |
| `physicaldisk.iops.write`       | 초당       |
| `physicaldisk.iops.total`       | 초당       |
| `physicaldisk.throughput.read`  | 바이트 수 / 초 |
| `physicaldisk.throughput.write` | 바이트 수 / 초 |
| `physicaldisk.throughput.total` | 바이트 수 / 초 |
| `physicaldisk.latency.read`     | 초          |
| `physicaldisk.latency.write`    | 초          |
| `physicaldisk.latency.average`  | 초          |
| `physicaldisk.size.total`       | 바이트            |
| `physicaldisk.size.used`        | 바이트            |

## <a name="how-to-interpret"></a>해석 하는 방법

| 시리즈                          | 해석 하는 방법                                                            |
|---------------------------------|-----------------------------------------------------------------------------|
| `physicaldisk.iops.read`        | 드라이브에 완료 된 초당 읽기 작업 수입니다.                |
| `physicaldisk.iops.write`       | 드라이브에 완료 된 초당 쓰기 작업 수입니다.               |
| `physicaldisk.iops.total`       | 총 읽기 또는 쓰기 드라이브에 완료 하는 초당 작업. |
| `physicaldisk.throughput.read`  | 초당 드라이브에서 읽은 데이터 양입니다.                            |
| `physicaldisk.throughput.write` | 초당 드라이브에 기록 된 데이터 양입니다.                           |
| `physicaldisk.throughput.total` | 총 읽기 또는 초당 드라이브에 기록 된 데이터 양입니다.        |
| `physicaldisk.latency.read`     | 드라이브에서 읽기 작업의 평균 대기 시간입니다.                          |
| `physicaldisk.latency.write`    | 드라이브에 쓰기 작업의 평균 대기 시간입니다.                           |
| `physicaldisk.latency.average`  | 드라이브에서 모든 작업의 평균 대기 시간입니다.                     |
| `physicaldisk.size.total`       | 드라이브의 총 저장소 용량입니다.                                    |
| `physicaldisk.size.used`        | 드라이브의 사용된 된 저장소 용량입니다.                                     |

## <a name="where-they-come-from"></a>어디에서 생겨날

`iops.*`, `throughput.*`, 및 `latency.*` 시리즈에서 수집 되는 `Physical Disk` 드라이브가 연결 되어 있는 서버를 설정 하는 성능 카운터, 드라이브 당 하나의 인스턴스. 이러한 카운터에서 측정 됩니다 `partmgr.sys` Windows 소프트웨어 스택의 많은 또는 모든 네트워크 홉을 포함 하지 마십시오. 장치 하드웨어 성능 대표 됩니다.

| 시리즈                          | 원본 카운터           |
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
   > 카운터는 샘플링 되지 전체 간격을 측정 됩니다. 예를 들어, 드라이브에 대 한 유휴 상태인 경우 9 초 하지만 완료 30 IOs 10 초에 해당 `physicaldisk.iops.total` 으로 기록 됩니다 초당 3 IOs 평균 10 초 간격입니다. 이렇게 하면 성능 기록과 모든 활동을 캡처하고 노이즈를 강력 합니다.

`size.*` 시리즈에서 수집 되는 `MSFT_PhysicalDisk` 드라이브 마다 하나의 인스턴스만 있는 WMI 클래스입니다.

| 시리즈                          | Source 속성        |
|---------------------------------|------------------------|
| `physicaldisk.size.total`       | `Size`                 |
| `physicaldisk.size.used`        | `VirtualDiskFootprint` |

## <a name="usage-in-powershell"></a>PowerShell에서 사용

사용 된 [Get-physicaldisk](https://docs.microsoft.com/powershell/module/storage/get-physicaldisk) cmdlet:

```PowerShell
Get-PhysicalDisk -SerialNumber <SerialNumber> | Get-ClusterPerf
```

## <a name="see-also"></a>참조

- [저장소 공간 다이렉트에 대 한 성능 기록](performance-history.md)
