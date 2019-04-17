---
title: 드라이브에 대 한 성능 기록
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
Keywords: Storage Spaces Direct
ms.localizationpriority: medium
ms.openlocfilehash: d162275a885dac79e7efe749328ebdca471fcad1
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/01/2018
ms.locfileid: "1589758"
---
# <a name="performance-history-for-drives"></a>드라이브에 대 한 성능 기록

> Windows Server 내부 인 미리 보기에 적용 됩니다.

이 하위 항목 [저장소 공간 직접에 대 한 성능](performance-history.md) 기록 된 드라이브에 대해 수집 된 성능 기록 자세하게에서 설명 합니다. 성능 기록 버스에 관계 없이 클러스터 저장소 하위 시스템의 모든 드라이브에 대 한 교육은 또는 미디어를 입력 합니다. 그러나 OS 부팅 드라이브에 사용할 수는 없습니다.

   > [!NOTE]
   > 성능 기록 드라이브의 작동이 중지 하는 서버에 대해 수집할 수 없습니다. 서버가 다시 시작 되 면 컬렉션을 자동으로 재개 합니다.

## <a name="series-names-and-units"></a>계열 이름 및 단위

이러한 시리즈 가능한 모든 드라이브에 대 한 수집 됩니다.

| 시리즈                          | Unit             |
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
| `physicaldisk.size.total`       |  바이트            |
| `physicaldisk.size.used`        |  바이트            |

## <a name="how-to-interpret"></a>해석 하는 방법

| 시리즈                          | 해석 하는 방법                                                            |
|---------------------------------|-----------------------------------------------------------------------------|
| `physicaldisk.iops.read`        | 드라이브에 의해 완료 초당 읽기 작업 수입니다.                |
| `physicaldisk.iops.write`       | 드라이브에 의해 완료 초당 쓰기 작업 수입니다.               |
| `physicaldisk.iops.total`       | 총 읽기 또는 쓰기 드라이브에 의해 완료 초당 작업 합니다. |
| `physicaldisk.throughput.read`  | 초당 드라이브에서 읽는 데이터의 양입니다.                            |
| `physicaldisk.throughput.write` | 초당 드라이브에 기록 하는 데이터 양입니다.                           |
| `physicaldisk.throughput.total` | 데이터베이스에서 읽거나 초당 드라이브에 기록 된 데이터의 총 수량입니다.        |
| `physicaldisk.latency.read`     | 드라이브에서 읽기 작업의 평균 대기 시간입니다.                          |
| `physicaldisk.latency.write`    | 드라이브에 쓰기 작업의 평균 대기 시간입니다.                           |
| `physicaldisk.latency.average`  | 또는 드라이브에서 모든 작업의 평균 대기 시간입니다.                     |
| `physicaldisk.size.total`       | 드라이브의 총 저장 용량입니다.                                    |
| `physicaldisk.size.used`        | 드라이브의 사용 하는 저장 용량입니다.                                     |

## <a name="where-they-come-from"></a>가져올 위치

`iops.*`, `throughput.*`, 및 `latency.*` 시리즈에서 수집 되는 `Physical Disk` 서버에 드라이브 연결 된 위치를 설정 하는 성능 카운터, 드라이브 당 하나의 인스턴스. 이러한 카운터는로 측정 된 `partmgr.sys` 또는 Windows 소프트웨어 스택의 많은 네트워크 홉 포함 되지 않습니다. 장치 하드웨어 성능의 담당자에 게 있습니다.

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
   > 카운터 하지 샘플링 하는 전체 간격을 통해 측정 됩니다. 예, 드라이브에 대 한 유휴 상태 이면 9 초 하지만 완료 30 IOs 10 초에서 해당 `physicaldisk.iops.total` 기록 되는 초당 3 IOs로 평균이 10 초 간격 중입니다. 이렇게 하면 해당 성능 기록 모든 활동 캡처하고 소음을 강력한 합니다.

`size.*` 시리즈에서 수집 되는 `MSFT_PhysicalDisk` wmi, 드라이브 당 하나의 인스턴스만 클래스입니다.

| 시리즈                          | Source 속성        |
|---------------------------------|------------------------|
| `physicaldisk.size.total`       | `Size`                 |
| `physicaldisk.size.used`        | `VirtualDiskFootprint` |

## <a name="usage-in-powershell"></a>PowerShell에서 사용 현황

[Get PhysicalDisk](https://docs.microsoft.com/powershell/module/storage/get-physicaldisk) cmdlet을 사용 하십시오.

```PowerShell
Get-PhysicalDisk -SerialNumber <SerialNumber> | Get-ClusterPerf
```

## <a name="see-also"></a>참고 항목

- [저장소 공간 직접에 대 한 성능 기록](performance-history.md)
