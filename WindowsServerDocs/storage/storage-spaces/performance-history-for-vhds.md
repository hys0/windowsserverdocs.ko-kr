---
title: 가상 하드 디스크에 대 한 성능 기록
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 18694975e48d199f2f690aebe8af2a4613a4b1f0
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474710"
---
# <a name="performance-history-for-virtual-hard-disks"></a>가상 하드 디스크에 대 한 성능 기록

> 적용 대상: 시작

[스토리지 공간 다이렉트에 대 한 성능 기록](performance-history.md) 의이 하위 항목에서는 VHD (가상 하드 디스크) 파일에 대해 수집 된 성능 기록에 대해 자세히 설명 합니다. 실행 중인 클러스터 된 가상 컴퓨터에 연결 된 모든 VHD에 대 한 성능 기록을 사용할 수 있습니다. VHD 및 VHDX 형식 모두에 대해 성능 기록을 사용할 수 있지만 공유 VHDX 파일에는 사용할 수 없습니다.

   > [!NOTE]
   > 새로 만들었거나 이동한 VHD 파일에 대해 수집이 시작 되는 데 몇 분 정도 걸릴 수 있습니다.

## <a name="series-names-and-units"></a>계열 이름 및 단위

이러한 시리즈는 적합 한 모든 가상 하드 디스크에 대해 수집 됩니다.

| 계열                    | 단위             |
|---------------------------|------------------|
| `vhd.iops.read`           | 초당       |
| `vhd.iops.write`          | 초당       |
| `vhd.iops.total`          | 초당       |
| `vhd.throughput.read`     | 초당 바이트 수 |
| `vhd.throughput.write`    | 초당 바이트 수 |
| `vhd.throughput.total`    | 초당 바이트 수 |
| `vhd.latency.average`     | 초          |
| `vhd.size.current`        | 바이트            |
| `vhd.size.maximum`        | 바이트            |

## <a name="how-to-interpret"></a>해석 방법

| 계열                    | 해석 방법                                                                                                 |
|---------------------------|------------------------------------------------------------------------------------------------------------------|
| `vhd.iops.read`           | 가상 하드 디스크에서 완료 한 초당 읽기 작업 수입니다.                                         |
| `vhd.iops.write`          | 가상 하드 디스크에서 완료 한 초당 쓰기 작업 수입니다.                                        |
| `vhd.iops.total`          | 가상 하드 디스크에서 완료 한 초당 총 읽기 또는 쓰기 작업 수입니다.                          |
| `vhd.throughput.read`     | 가상 하드 디스크에서 읽은 초당 데이터의 양입니다.                                                     |
| `vhd.throughput.write`    | 초당 가상 하드 디스크에 쓴 데이터의 양입니다.                                                    |
| `vhd.throughput.total`    | 초당 가상 하드 디스크에서 읽거나 쓴 총 데이터 양입니다.                                 |
| `vhd.latency.average`     | 가상 하드 디스크에 대 한 모든 작업의 평균 대기 시간입니다.                                              |
| `vhd.size.current`        | 가상 하드 디스크의 현재 파일 크기 (동적 확장의 경우)입니다. 고정 된 경우 계열이 수집 되지 않습니다. |
| `vhd.size.maximum`        | 동적으로 확장 하는 경우 가상 하드 디스크의 최대 크기입니다. 고정 된 경우는 크기입니다.                  |

## <a name="where-they-come-from"></a>원본 위치

`iops.*`, `throughput.*` 및 시리즈는 `latency.*` `Hyper-V Virtual Storage Device` 가상 머신이 실행 되는 서버에 설정 된 성능 카운터에서 수집 됩니다 (VHD 또는 VHDX 당 인스턴스 하나).

| 계열                    | 원본 카운터         |
|---------------------------|------------------------|
| `vhd.iops.read`           | `Read Operations/Sec`  |
| `vhd.iops.write`          | `Write Operations/Sec` |
| `vhd.iops.total`          | *위의 합계*     |
| `vhd.throughput.read`     | `Read Bytes/sec`       |
| `vhd.throughput.write`    | `Write Bytes/sec`      |
| `vhd.throughput.total`    | *위의 합계*     |
| `vhd.latency.average`     | `Latency`              |

   > [!NOTE]
   > 카운터는 샘플링 되지 않고 전체 간격으로 측정 됩니다. 예를 들어 VHD가 9 초 동안 비활성 상태 이지만 10 초 내에 30 개의 Io를 완료 하는 경우 `vhd.iops.total` 이 10 초 간격 동안 평균 초당 3 개의 io로 기록 됩니다. 이렇게 하면 성능 기록이 모든 활동을 캡처하고 소음에 대해 강력 하 게 됩니다.

## <a name="usage-in-powershell"></a>PowerShell에서 사용

다음을 [사용 합니다.](https://docs.microsoft.com/powershell/module/hyper-v/get-vhd)

```PowerShell
Get-VHD <Path> | Get-ClusterPerf
```

가상 머신에서 모든 VHD의 경로를 가져오려면 다음을 수행 합니다.

```PowerShell
(Get-VM <Name>).HardDrives | Select Path
```

   > [!NOTE]
   > 가져올 VHD cmdlet에는 파일 경로를 제공 해야 합니다. 열거를 지원 하지 않습니다.

## <a name="additional-references"></a>추가 참조

- [스토리지 공간 다이렉트에 대 한 성능 기록](performance-history.md)
