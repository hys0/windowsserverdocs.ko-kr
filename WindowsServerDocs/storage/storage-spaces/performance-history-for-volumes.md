---
title: 볼륨에 대 한 성능 기록
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/09/2018
Keywords: 저장소 공간 다이렉트
ms.localizationpriority: medium
ms.openlocfilehash: fea1d3d67ab96d95b1699e8ac0129dba698477fe
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882954"
---
# <a name="performance-history-for-volumes"></a>볼륨에 대 한 성능 기록

> 적용 대상: Windows Server Insider Preview

이 하위 항목의 [저장소 공간 다이렉트에 대 한 성능 기록을](performance-history.md) 볼륨에 대해 수집 된 성능 기록 세부 정보에 설명 합니다. 성능 기록에 대 한 모든 공유 볼륨 (CSV (클러스터) 클러스터에서 사용할 수 있는 경우 OS에 사용할 수 없는 단, 볼륨 또는 기타 CSV가 아닌 저장소 부팅 합니다.

   > [!NOTE]
   > 새로 만든 또는 이름이 바뀐 볼륨을 시작 하려면 컬렉션에 대 일 분 정도 걸릴 수 있습니다.

## <a name="series-names-and-units"></a>계열 이름 및 단위

이 시리즈는 적합 한 모든 볼륨에 대 한 수집 됩니다.

| 시리즈                    | 단위             |
|---------------------------|------------------|
| `volume.iops.read`        | 초당       |
| `volume.iops.write`       | 초당       |
| `volume.iops.total`       | 초당       |
| `volume.throughput.read`  | 바이트 수 / 초 |
| `volume.throughput.write` | 바이트 수 / 초 |
| `volume.throughput.total` | 바이트 수 / 초 |
| `volume.latency.read`     | 초          |
| `volume.latency.write`    | 초          |
| `volume.latency.average`  | 초          |
| `volume.size.total`       | 바이트            |
| `volume.size.available`   | 바이트            |

## <a name="how-to-interpret"></a>해석 하는 방법

| 시리즈                    | 해석 하는 방법                                                              |
|---------------------------|-------------------------------------------------------------------------------|
| `volume.iops.read`        | 이 볼륨에서 완료 된 초당 읽기 작업 수입니다.                |
| `volume.iops.write`       | 이 볼륨에서 완료 된 초당 쓰기 작업 수입니다.               |
| `volume.iops.total`       | 총 읽기 또는 쓰기 작업 / 초가이 볼륨에서 완료. |
| `volume.throughput.read`  | 초당이 볼륨에서 읽을 데이터 양입니다.                            |
| `volume.throughput.write` | 초당이 볼륨에 기록 된 데이터 양입니다.                           |
| `volume.throughput.total` | 총 데이터 읽기 또는 초당이 볼륨에 쓰기 양입니다.        |
| `volume.latency.read`     | 이 볼륨에서 읽기 작업의 평균 대기 시간입니다.                          |
| `volume.latency.write`    | 이 볼륨에 쓰기 작업의 평균 대기 시간입니다.                           |
| `volume.latency.average`  | 이 볼륨에서 모든 작업의 평균 대기 시간입니다.                     |
| `volume.size.total`       | 볼륨의 총 저장소 용량입니다.                                     |
| `volume.size.available`   | 볼륨의 사용 가능한 저장소 용량입니다.                                 |

## <a name="where-they-come-from"></a>어디에서 생겨날

`iops.*`, `throughput.*`, 및 `latency.*` 시리즈에서 수집 되는 `Cluster CSVFS` 성능 카운터 집합입니다. 클러스터의 모든 서버 인스턴스가 소유권에 상관 없이 모든 CSV 볼륨에 대 한 합니다. 볼륨에 대해 기록 된 성능 기록을 `MyVolume` 의 집계는 `MyVolume` 클러스터의 모든 서버 인스턴스.

| 시리즈                    | 원본 카운터         |
|---------------------------|------------------------|
| `volume.iops.read`        | `Reads/sec`            |
| `volume.iops.write`       | `Writes/sec`           |
| `volume.iops.total`       | *위의 합계*     |
| `volume.throughput.read`  | `Read bytes/sec`       |
| `volume.throughput.write` | `Write bytes/sec`      |
| `volume.throughput.total` | *위의 합계*     |
| `volume.latency.read`     | `Avg. sec/Read`        |
| `volume.latency.write`    | `Avg. sec/Write`       |
| `volume.latency.average`  | *위의 평균* |

   > [!NOTE]
   > 카운터는 샘플링 되지 전체 간격을 측정 됩니다. 예를 들어 볼륨에 대 한 유휴 상태인 경우 9 초 하지만 완료 30 IOs 10 초에 해당 `volume.iops.total` 으로 기록 됩니다 초당 3 IOs 평균 10 초 간격입니다. 이렇게 하면 성능 기록과 모든 활동을 캡처하고 노이즈를 강력 합니다.

   > [!TIP]
   > 인기 있는에서 사용한 동일한 카운터 이들은 [VM Fleet](https://github.com/Microsoft/diskspd/blob/master/Frameworks/VMFleet/watch-cluster.ps1) 벤치 마크 프레임 워크입니다.

합니다 `size.*` 시리즈에서 수집 되는 `MSFT_Volume` 볼륨당 하나의 인스턴스만 있는 WMI 클래스입니다.

| 시리즈                    | Source 속성 |
|---------------------------|-----------------|
| `volume.size.total`       | `Size`          |
| `volume.size.available`   | `SizeRemaining` |

## <a name="usage-in-powershell"></a>PowerShell에서 사용

사용 된 [Get-volume](https://docs.microsoft.com/powershell/module/storage/get-volume) cmdlet:

```PowerShell
Get-Volume -FriendlyName <FriendlyName> | Get-ClusterPerf
```

## <a name="see-also"></a>참조

- [저장소 공간 다이렉트에 대 한 성능 기록](performance-history.md)
