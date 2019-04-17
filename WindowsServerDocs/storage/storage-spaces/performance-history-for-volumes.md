---
title: 볼륨에 대 한 성능 기록
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/09/2018
Keywords: Storage Spaces Direct
ms.localizationpriority: medium
ms.openlocfilehash: fea1d3d67ab96d95b1699e8ac0129dba698477fe
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/01/2018
ms.locfileid: "1589707"
---
# <a name="performance-history-for-volumes"></a>볼륨에 대 한 성능 기록

> Windows Server 내부 인 미리 보기에 적용 됩니다.

이 하위 항목 [저장소 공간 직접에 대 한 성능](performance-history.md) 기록 볼륨에 대해 수집 된 성능 기록 자세하게에서 설명 합니다. 성능 기록에 대 한 모든 클러스터 공유 볼륨 (CSV) 클러스터에서 사용할 수는 있습니다. 그러나 운영 체제에 대해 사용할 수 없는 볼륨 또는 다른 비 CSV 저장소 부팅 합니다.

   > [!NOTE]
   > 새로 만든 또는 이름이 바뀐 볼륨에 대 한 시작 하는 컬렉션에 대 한 몇 분정도 걸릴 수 있습니다.

## <a name="series-names-and-units"></a>계열 이름 및 단위

이러한 시리즈 가능한 모든 볼륨에 대 한 수집 됩니다.

| 시리즈                    | Unit             |
|---------------------------|------------------|
| `volume.iops.read`        | 초당       |
| `volume.iops.write`       | 초당       |
| `volume.iops.total`       | 초당       |
| `volume.throughput.read`  | 초당 바이트 수 |
| `volume.throughput.write` | 초당 바이트 수 |
| `volume.throughput.total` | 초당 바이트 수 |
| `volume.latency.read`     | 초          |
| `volume.latency.write`    | 초          |
| `volume.latency.average`  | 초          |
| `volume.size.total`       |  바이트            |
| `volume.size.available`   |  바이트            |

## <a name="how-to-interpret"></a>해석 하는 방법

| 시리즈                    | 해석 하는 방법                                                              |
|---------------------------|-------------------------------------------------------------------------------|
| `volume.iops.read`        | 이 볼륨에 의해 완료 초당 읽기 작업 수입니다.                |
| `volume.iops.write`       | 이 볼륨에 의해 완료 초당 쓰기 작업 수입니다.               |
| `volume.iops.total`       | 총 읽기 또는 쓰기이 볼륨에 의해 완료 초당 작업 합니다. |
| `volume.throughput.read`  | 초당이 볼륨에서 읽는 데이터의 양입니다.                            |
| `volume.throughput.write` | 초당이 볼륨에 기록 하는 데이터 양입니다.                           |
| `volume.throughput.total` | 총 데이터베이스에서 읽거나 초당이 볼륨에 기록 하는 데이터 양입니다.        |
| `volume.latency.read`     | 이 볼륨에서 읽기 작업의 평균 대기 시간입니다.                          |
| `volume.latency.write`    | 이 볼륨에 쓰기 작업의 평균 대기 시간입니다.                           |
| `volume.latency.average`  | 또는이 볼륨에서 모든 작업의 평균 대기 시간입니다.                     |
| `volume.size.total`       | 볼륨의 총 저장 용량입니다.                                     |
| `volume.size.available`   | 볼륨의 사용 가능한 저장 용량입니다.                                 |

## <a name="where-they-come-from"></a>가져올 위치

`iops.*`, `throughput.*`, 및 `latency.*` 시리즈에서 수집 되는 `Cluster CSVFS` 성능 카운터 집합입니다. 클러스터의 모든 서버는 소유권에 관계 없이 모든 CSV 볼륨에 대 한 인스턴스여야 합니다. 볼륨에 대 한 성능 기록 기록 `MyVolume` 는의 집계는 `MyVolume` 클러스터의 모든 서버에서 인스턴스.

| 시리즈                    | 원본 카운터         |
|---------------------------|------------------------|
| `volume.iops.read`        | `Reads/sec`            |
| `volume.iops.write`       | `Writes/sec`           |
| `volume.iops.total`       | *위의의 합*     |
| `volume.throughput.read`  | `Read bytes/sec`       |
| `volume.throughput.write` | `Write bytes/sec`      |
| `volume.throughput.total` | *위의의 합*     |
| `volume.latency.read`     | `Avg. sec/Read`        |
| `volume.latency.write`    | `Avg. sec/Write`       |
| `volume.latency.average`  | *위의의 평균* |

   > [!NOTE]
   > 카운터 하지 샘플링 하는 전체 간격을 통해 측정 됩니다. 예, 볼륨에 대 한 유휴 상태 이면 9 초 하지만 완료 30 IOs 10 초에서 해당 `volume.iops.total` 기록 되는 초당 3 IOs로 평균이 10 초 간격 중입니다. 이렇게 하면 해당 성능 기록 모든 활동 캡처하고 소음을 강력한 합니다.

   > [!TIP]
   > 인기 있는 [VM 함 대](https://github.com/Microsoft/diskspd/blob/master/Frameworks/VMFleet/watch-cluster.ps1) 벤치 마크 프레임 워크에 의해 사용 되는 동일한 카운터는입니다.

`size.*` 시리즈에서 수집 되는 `MSFT_Volume` wmi, 볼륨 당 하나의 인스턴스만 클래스.

| 시리즈                    | Source 속성 |
|---------------------------|-----------------|
| `volume.size.total`       | `Size`          |
| `volume.size.available`   | `SizeRemaining` |

## <a name="usage-in-powershell"></a>PowerShell에서 사용 현황

[Get-볼륨](https://docs.microsoft.com/powershell/module/storage/get-volume) cmdlet을 사용 하십시오.

```PowerShell
Get-Volume -FriendlyName <FriendlyName> | Get-ClusterPerf
```

## <a name="see-also"></a>참고 항목

- [저장소 공간 직접에 대 한 성능 기록](performance-history.md)
