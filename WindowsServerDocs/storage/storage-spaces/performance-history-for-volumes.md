---
title: 볼륨에 대 한 성능 기록
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5f6acf062d2dba7c2a1a04d8a3f7cb4d7bd51a4d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856136"
---
# <a name="performance-history-for-volumes"></a>볼륨에 대 한 성능 기록

> 적용 대상: Windows Server 2019

[스토리지 공간 다이렉트에 대 한 성능 기록](performance-history.md) 의이 하위 항목에서는 볼륨에 대해 수집 된 성능 기록에 대해 자세히 설명 합니다. 성능 기록은 클러스터의 모든 CSV (클러스터 공유 볼륨)에서 사용할 수 있습니다. 그러나 OS 부팅 볼륨 또는 다른 비 CSV 저장소에는 사용할 수 없습니다.

   > [!NOTE]
   > 새로 만들어지거나 이름이 바뀐 볼륨에 대해 수집이 시작 되는 데 몇 분 정도 걸릴 수 있습니다.

## <a name="series-names-and-units"></a>계열 이름 및 단위

이러한 시리즈는 적격 한 모든 볼륨에 대해 수집 됩니다.

| 계열                    | 단위             |
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
| `volume.size.total`       | 바이트            |
| `volume.size.available`   | 바이트            |

## <a name="how-to-interpret"></a>해석 방법

| 계열                    | 해석 방법                                                              |
|---------------------------|-------------------------------------------------------------------------------|
| `volume.iops.read`        | 이 볼륨에서 완료 한 초당 읽기 작업 수입니다.                |
| `volume.iops.write`       | 이 볼륨에서 완료 한 초당 쓰기 작업 수입니다.               |
| `volume.iops.total`       | 이 볼륨에서 완료 한 초당 읽기 또는 쓰기 작업의 총 수입니다. |
| `volume.throughput.read`  | 초당이 볼륨에서 읽은 데이터의 양입니다.                            |
| `volume.throughput.write` | 초당이 볼륨에 쓴 데이터 양입니다.                           |
| `volume.throughput.total` | 초당이 볼륨에서 읽거나 쓴 총 데이터 양입니다.        |
| `volume.latency.read`     | 이 볼륨에서 읽기 작업의 평균 대기 시간입니다.                          |
| `volume.latency.write`    | 이 볼륨에 대 한 쓰기 작업의 평균 대기 시간입니다.                           |
| `volume.latency.average`  | 이 볼륨에 대 한 모든 작업의 평균 대기 시간입니다.                     |
| `volume.size.total`       | 볼륨의 총 저장소 용량입니다.                                     |
| `volume.size.available`   | 볼륨의 사용 가능한 저장소 용량입니다.                                 |

## <a name="where-they-come-from"></a>원본 위치

`iops.*`, `throughput.*`및 `latency.*` 계열은 `Cluster CSVFS` 성능 카운터 집합에서 수집 됩니다. 클러스터의 모든 서버에는 소유권에 관계 없이 모든 CSV 볼륨에 대 한 인스턴스가 있습니다. 볼륨 `MyVolume`에 대해 기록 된 성능 기록은 클러스터의 모든 서버에 있는 `MyVolume` 인스턴스의 집합체입니다.

| 계열                    | 원본 카운터         |
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
   > 카운터는 샘플링 되지 않고 전체 간격으로 측정 됩니다. 예를 들어 볼륨이 9 초 동안 유휴 상태 이지만 10 초 내에 30 개의 Io를 완료 하는 경우 해당 `volume.iops.total`는 10 초 간격 동안 평균 초당 3 개의 Io로 기록 됩니다. 이렇게 하면 성능 기록이 모든 활동을 캡처하고 소음에 대해 강력 하 게 됩니다.

   > [!TIP]
   > 이러한 카운터는 인기 있는 [VM](https://github.com/Microsoft/diskspd/blob/master/Frameworks/VMFleet/watch-cluster.ps1) 및 벤치 마크 프레임 워크에서 사용 하는 것과 동일한 카운터입니다.

`size.*` 시리즈는 WMI의 `MSFT_Volume` 클래스 (볼륨당 하나의 인스턴스)에서 수집 됩니다.

| 계열                    | Source 속성 |
|---------------------------|-----------------|
| `volume.size.total`       | `Size`          |
| `volume.size.available`   | `SizeRemaining` |

## <a name="usage-in-powershell"></a>PowerShell에서 사용

[Get 볼륨](https://docs.microsoft.com/powershell/module/storage/get-volume) cmdlet을 사용 합니다.

```PowerShell
Get-Volume -FriendlyName <FriendlyName> | Get-ClusterPerf
```

## <a name="see-also"></a>참고 항목

- [스토리지 공간 다이렉트에 대 한 성능 기록](performance-history.md)
