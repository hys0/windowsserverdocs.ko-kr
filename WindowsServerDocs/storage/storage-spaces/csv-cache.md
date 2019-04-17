---
title: 저장소 공간 다이렉트에서 메모리 내 읽기 캐시
ms.prod: windows-server-threshold
ms.author: eldenc
ms.manager: siroy
ms.technology: storage-spaces
ms.topic: article
author: eldenchristensen
ms.date: 02/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7ed5894a569d4c42a3a4b0e018de5171f2c84a62
ms.sourcegitcommit: 5ed023a2ef3a9002daf41c7717feb1df186d2a14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2019
ms.locfileid: "9122056"
---
# CSV 인 메모리를 사용 하 여 저장소 공간 다이렉트를 사용 하 여 읽기 캐시
> 적용 대상: Windows Server 2016, Windows Server 2019

이 항목에서는 [저장소 공간 다이렉트](storage-spaces-direct-overview.md)의 성능을 향상 시키는 시스템 메모리를 사용 하는 방법을 설명 합니다.

저장소 공간 다이렉트는 클러스터 공유 볼륨 (CSV) 메모리 내 읽기 캐시 호환 됩니다. 시스템 메모리 읽기 캐시를 사용 하 여 버퍼링 되지 않은 I/O를 사용 하 여 VHD 또는 VHDX 파일에 액세스 하는 Hyper-v와 같은 응용 프로그램에 대 한 성능을 개선할 수 있습니다. (버퍼링 되지 않은 IOs는 Windows 캐시 관리자에 의해 캐시 되지 않은 모든 작업입니다.)

하이퍼 수렴 형 저장소 공간 다이렉트 배포에 대 한 데이터 위치 향상 메모리 캐시 서버 로컬 이므로: 최근 읽기 캐시 된 가상 컴퓨터 실행 되 고 있는 동일한 호스트에서 메모리에 얼마나 자주 감소 읽기 이동 네트워크를 통해 합니다. 따라서 더 낮은 대기 시간 및 저장소 성능이 향상 됩니다.

## 고려 사항

메모리에 읽기 캐시 가상 데스크톱 인프라 (VDI) 등의 읽기 집약적인 워크 로드에 대 한 가장 효과적입니다. 반대로, 워크 로드의 쓰기를 매우 많이 사용 인 경우 캐시 값 보다 더 많은 오버 헤드가 발생할 수 및 비활성화 해야 합니다.

CSV 인 메모리 읽기 캐시에 대 한 총 실제 메모리의 최대 80%를 사용할 수 있습니다.

  > [!TIP]
  > 하이퍼 수렴 형 배포에 대 한 위치를 계산 하 고 동일한 서버에서 실행 되는 저장소 가상 컴퓨터에 대 한 충분 한 메모리 주의 합니다. 메모리에 대 한 더 적은 경합으로 수렴 형된 스케일 아웃 파일 서버 (SoFS) 배포에 대 한이 적용 되지 않습니다.

  > [!NOTE]
  > DISKSPD 및 [VM 제](https://github.com/Microsoft/diskspd/tree/master/Frameworks/VMFleet) 결과가 발생할 수 있습니다 심각한 문제는 CSV 인 메모리와 같은 특정 microbenchmarking 도구 읽기 캐시 없이 것 보다 사용 합니다. 기본적으로 VM 제 10 지 브 가상 컴퓨터 – 약 1 t i b 당 VHDX-100 Vm에 대 한 총 다음 *균일 하 게 임의* 읽기를 수행 하 고 쓰기를 하나 만듭니다. 실제 워크 로드와 달리 읽기 메모리 캐시 유효 하지 않으며 방금 오버 헤드가 하므로 예측 가능한 또는 반복 패턴을 따르지 합니다.

## 읽기 캐시에서 메모리를 구성 합니다.

CSV 인 메모리 읽기 캐시는 동일한 기능을 사용 하 여 Windows Server 2016 및 Windows Server 2019에서 사용할 수 있습니다. Windows Server 2016에서이 기본적으로 꺼져 있습니다. Windows Server 2019의 켜져 기본적으로 1gb 할당 합니다.

| OS 버전          | 기본 CSV 캐시 크기 |
|---------------------|------------------------|
| WindowsServer 2016 | 0 (사용 안 함)           |
| WindowsServer 2019 | 1 지 브                   |

PowerShell을 사용 하 여 얼마나 많은 메모리를 할당을 보려면 다음을 실행 합니다.

```PowerShell
(Get-Cluster).BlockCacheSize
```

서버당 mebibytes (MiB)에서 값을 반환 합니다. 예를 들어 `1024` 1 gibibyte (지 브)를 나타냅니다.

할당 된 메모리를 변경 하려면 PowerShell을 사용 하 여이 값을 수정 합니다. 예를 들어 서버당 2 지 브를 할당 하려면 다음을 실행 합니다.

```PowerShell
(Get-Cluster).BlockCacheSize = 2048
```

변경 내용을 적용에 대 한 즉시 일시 중지 한 다음 CSV 볼륨을 다시 시작 하거나 서버 간에 이동 합니다. 예를 들어이 PowerShell 조각 위치를 각 CSV 다른 서버 노드를 다시 사용 합니다.

```PowerShell
Get-ClusterSharedVolume | ForEach {
    $Owner = $_.OwnerNode
    $_ | Move-ClusterSharedVolume
    $_ | Move-ClusterSharedVolume -Node $Owner
}
```

## 참고 항목

- [저장소 공간 다이렉트 개요](storage-spaces-direct-overview.md)
