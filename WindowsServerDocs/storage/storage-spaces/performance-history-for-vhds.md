---
title: 가상 하드 디스크 성능 기록
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/09/2018
Keywords: 저장소 공간 다이렉트
ms.localizationpriority: medium
ms.openlocfilehash: 7a0d8d132b6a5ff42cbe78a22c67dd9fec397184
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880404"
---
# <a name="performance-history-for-virtual-hard-disks"></a>가상 하드 디스크 성능 기록

> 적용 대상: Windows Server Insider Preview

이 하위 항목의 [저장소 공간 다이렉트에 대 한 성능 기록을](performance-history.md) 성능 기록을 수집 된 가상 하드 디스크 (VHD) 파일에 대 한 세부 정보에 설명 합니다. 성능 기록 실행, 클러스터 된 가상 머신에 연결 된 모든 VHD 제공 됩니다. 성능 기록 공유 VHDX 파일에 대해 사용할 수 있지만 VHD 및 VHDX 형식으로 제공 됩니다.

   > [!NOTE]
   > 새로 만들거나 이동 VHD 파일을 시작 하려면 컬렉션에 대 일 분 정도 걸릴 수 있습니다.

## <a name="series-names-and-units"></a>계열 이름 및 단위

이 시리즈는 적합 한 모든 가상 하드 디스크에 대해 수집 됩니다.

| 시리즈                    | 단위             |
|---------------------------|------------------|
| `vhd.iops.read`           | 초당       |
| `vhd.iops.write`          | 초당       |
| `vhd.iops.total`          | 초당       |
| `vhd.throughput.read`     | 바이트 수 / 초 |
| `vhd.throughput.write`    | 바이트 수 / 초 |
| `vhd.throughput.total`    | 바이트 수 / 초 |
| `vhd.latency.average`     | 초          |
| `vhd.size.current`        | 바이트            |
| `vhd.size.maximum`        | 바이트            |

## <a name="how-to-interpret"></a>해석 하는 방법

| 시리즈                    | 해석 하는 방법                                                                                                 |
|---------------------------|------------------------------------------------------------------------------------------------------------------|
| `vhd.iops.read`           | 가상 하드 디스크에서 완료 된 초당 읽기 작업 수입니다.                                         |
| `vhd.iops.write`          | 가상 하드 디스크에서 완료 된 초당 쓰기 작업 수입니다.                                        |
| `vhd.iops.total`          | 총 읽기 또는 가상 하드 디스크에서 완료 된 초당 쓰기 작업입니다.                          |
| `vhd.throughput.read`     | 초당 가상 하드 디스크에서 읽은 데이터 양입니다.                                                     |
| `vhd.throughput.write`    | 초당 가상 하드 디스크에 쓴 데이터 양입니다.                                                    |
| `vhd.throughput.total`    | 총 읽기 또는 초당 가상 하드 디스크에 쓴 데이터 양입니다.                                 |
| `vhd.latency.average`     | 가상 하드 디스크에서 모든 작업의 평균 대기 시간입니다.                                              |
| `vhd.size.current`        | 가상 하드 디스크를 동적으로 확장 하는 경우의 현재 파일 크기입니다. 고정 시리즈 수집 되지 않습니다. |
| `vhd.size.maximum`        | 동적으로 확장 하는 경우 가상 하드 디스크의 최대 크기입니다. 수정 하는 경우는 크기입니다.                  |

## <a name="where-they-come-from"></a>어디에서 생겨날

`iops.*`, `throughput.*`, 및 `latency.*` 시리즈에서 수집 되는 `Hyper-V Virtual Storage Device` 가상 머신이 실행 되는 VHD 또는 VHDX 당 하나의 인스턴스 인 서버에서 성능 카운터 집합.

| 시리즈                    | 원본 카운터         |
|---------------------------|------------------------|
| `vhd.iops.read`           | `Read Operations/Sec`  |
| `vhd.iops.write`          | `Write Operations/Sec` |
| `vhd.iops.total`          | *위의 합계*     |
| `vhd.throughput.read`     | `Read Bytes/sec`       |
| `vhd.throughput.write`    | `Write Bytes/sec`      |
| `vhd.throughput.total`    | *위의 합계*     |
| `vhd.latency.average`     | `Latency`              |

   > [!NOTE]
   > 카운터는 샘플링 되지 전체 간격을 측정 됩니다. 예를 들어, VHD에 대 한 활성화 되지 않은 경우 9 초 하지만 완료 30 IOs 10 초에 해당 `vhd.iops.total` 으로 기록 됩니다 초당 3 IOs 평균 10 초 간격입니다. 이렇게 하면 성능 기록과 모든 활동을 캡처하고 노이즈를 강력 합니다.

## <a name="usage-in-powershell"></a>PowerShell에서 사용

사용 된 [GET-VHD](https://docs.microsoft.com/powershell/module/hyper-v/get-vhd) cmdlet:

```PowerShell
Get-VHD <Path> | Get-ClusterPerf
```

가상 컴퓨터에서 모든 VHD의 경로 가져오려면:

```PowerShell
(Get-VM <Name>).HardDrives | Select Path
```

   > [!NOTE]
   > GET-VHD cmdlet은 파일 경로 제공 해야 합니다. 열거형은 지원 하지 않습니다.

## <a name="see-also"></a>참조

- [저장소 공간 다이렉트에 대 한 성능 기록](performance-history.md)
