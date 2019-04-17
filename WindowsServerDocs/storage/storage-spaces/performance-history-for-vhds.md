---
title: 가상 하드 디스크에 대 한 성능 기록
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/09/2018
Keywords: Storage Spaces Direct
ms.localizationpriority: medium
ms.openlocfilehash: 7a0d8d132b6a5ff42cbe78a22c67dd9fec397184
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/01/2018
ms.locfileid: "1589724"
---
# <a name="performance-history-for-virtual-hard-disks"></a>가상 하드 디스크에 대 한 성능 기록

> Windows Server 내부 인 미리 보기에 적용 됩니다.

이 하위 항목 [저장소 공간 직접에 대 한 성능](performance-history.md) 기록 가상 하드 디스크 (VHD) 파일에 대 한 성능 기록을 수집 자세하게에서 설명 합니다. 성능 기록이 실행 되는 클러스터 된 가상 컴퓨터에 연결 된 모든 VHD에 있습니다. 공유 VHDX 파일에 사용할 수 없는 성능 기록 VHD와 VHDX 형식에 사용할 수는.

   > [!NOTE]
   > 새로 만든 또는 이동 된 VHD 파일을 시작 하는 컬렉션에 대 한 몇 분정도 걸릴 수 있습니다.

## <a name="series-names-and-units"></a>계열 이름 및 단위

이러한 시리즈 가능한 모든 가상 하드 디스크에 대 한 수집 됩니다.

| 시리즈                    | Unit             |
|---------------------------|------------------|
| `vhd.iops.read`           | 초당       |
| `vhd.iops.write`          | 초당       |
| `vhd.iops.total`          | 초당       |
| `vhd.throughput.read`     | 초당 바이트 수 |
| `vhd.throughput.write`    | 초당 바이트 수 |
| `vhd.throughput.total`    | 초당 바이트 수 |
| `vhd.latency.average`     | 초          |
| `vhd.size.current`        |  바이트            |
| `vhd.size.maximum`        |  바이트            |

## <a name="how-to-interpret"></a>해석 하는 방법

| 시리즈                    | 해석 하는 방법                                                                                                 |
|---------------------------|------------------------------------------------------------------------------------------------------------------|
| `vhd.iops.read`           | 가상 하드 디스크에 의해 완료 초당 읽기 작업 수입니다.                                         |
| `vhd.iops.write`          | 가상 하드 디스크에 의해 완료 초당 쓰기 작업의 수입니다.                                        |
| `vhd.iops.total`          | 총 읽기 또는 쓰기 가상 하드 디스크에 의해 완료 초당 작업 합니다.                          |
| `vhd.throughput.read`     | 초당 가상 하드 디스크에서 읽는 데이터의 양입니다.                                                     |
| `vhd.throughput.write`    | 초당 가상 하드 디스크에 기록 하는 데이터 양입니다.                                                    |
| `vhd.throughput.total`    | 데이터베이스에서 읽거나 초당 가상 하드 디스크에 기록 된 데이터의 총 수량입니다.                                 |
| `vhd.latency.average`     | 또는 가상 하드 디스크에서 모든 작업의 평균 대기 시간입니다.                                              |
| `vhd.size.current`        | 가상 하드 디스크를 동적으로 확장 하는 경우의 현재 파일 크기를 지정 합니다. 고정 된 계열 수집 되지 않습니다. |
| `vhd.size.maximum`        | 가상 하드 디스크를 동적으로 확장 하는 경우의 최대 크기입니다. 고정 된 경우의 크기입니다.                  |

## <a name="where-they-come-from"></a>가져올 위치

`iops.*`, `throughput.*`, 및 `latency.*` 시리즈에서 수집 되는 `Hyper-V Virtual Storage Device` 여기서 가상 컴퓨터는 실행, VHD 또는 VHDX 당 하나의 인스턴스만 성능 카운터의 서버에서 설정 합니다.

| 시리즈                    | 원본 카운터         |
|---------------------------|------------------------|
| `vhd.iops.read`           | `Read Operations/Sec`  |
| `vhd.iops.write`          | `Write Operations/Sec` |
| `vhd.iops.total`          | *위의의 합*     |
| `vhd.throughput.read`     | `Read Bytes/sec`       |
| `vhd.throughput.write`    | `Write Bytes/sec`      |
| `vhd.throughput.total`    | *위의의 합*     |
| `vhd.latency.average`     | `Latency`              |

   > [!NOTE]
   > 카운터 하지 샘플링 하는 전체 간격을 통해 측정 됩니다. 예, VHD에 대 한 활성화 되지 않은 경우 9 초 하지만 완료 30 IOs 10 초에서 해당 `vhd.iops.total` 기록 되는 초당 3 IOs로 평균이 10 초 간격 중입니다. 이렇게 하면 해당 성능 기록 모든 활동 캡처하고 소음을 강력한 합니다.

## <a name="usage-in-powershell"></a>PowerShell에서 사용 현황

[Get VHD](https://docs.microsoft.com/powershell/module/hyper-v/get-vhd) cmdlet을 사용 하십시오.

```PowerShell
Get-VHD <Path> | Get-ClusterPerf
```

가상 컴퓨터에서 모든 VHD의 경로 보려면

```PowerShell
(Get-VM <Name>).HardDrives | Select Path
```

   > [!NOTE]
   > Get VHD cmdlet은 제공 되는 파일 경로 필요 합니다. 열거형은 지원 하지 않습니다.

## <a name="see-also"></a>참고 항목

- [저장소 공간 직접에 대 한 성능 기록](performance-history.md)
