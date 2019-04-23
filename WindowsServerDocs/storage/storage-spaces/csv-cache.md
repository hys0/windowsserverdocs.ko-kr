---
title: 저장소 공간 다이렉트에서 메모리 내 캐시 읽기
ms.prod: windows-server-threshold
ms.author: eldenc
ms.manager: siroy
ms.technology: storage-spaces
ms.topic: article
author: eldenchristensen
ms.date: 02/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7ed5894a569d4c42a3a4b0e018de5171f2c84a62
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850554"
---
# <a name="using-storage-spaces-direct-with-the-csv-in-memory-read-cache"></a>읽기 캐시를 CSV에 메모리를 사용 하 여 저장소 공간 다이렉트를 사용 하 여
> 적용 대상: Windows Server 2016, Windows Server 2019

이 항목의 성능을 향상 시키기 위해 시스템 메모리를 사용 하는 방법에 설명 합니다 [저장소 공간 다이렉트](storage-spaces-direct-overview.md)합니다.

저장소 공간 다이렉트 클러스터 공유 볼륨 (CSV) 메모리 내 캐시를 읽을 호환 됩니다. 캐시 읽기 시스템 메모리를 사용 하 여 버퍼링 되지 않은 I/O를 사용 하 여 VHD 또는 VHDX 파일에 액세스 하는 Hyper-v와 같은 응용 프로그램에 대 한 성능을 향상 시킬 수 있습니다. (버퍼링 되지 않은 IOs는 Windows 캐시 관리자에 의해 캐시 되지 않은 모든 작업입니다.)

하이퍼 수렴 형 저장소 공간 다이렉트 배포에 대 한 데이터 지역성 개선 하 여 메모리 내 캐시 서버 로컬 이므로: 최근 읽기는 캐시에서 가상 머신이 실행 되는 동일한 호스트의 메모리를 얼마나 자주 줄이는 읽기 이동 네트워크를 통해. 그러면 더 낮은 대기 시간 및 저장소 성능 향상 됩니다.

## <a name="planning-considerations"></a>계획 시 고려 사항

메모리 내 캐시는 가상 데스크톱 인프라 (VDI)와 같은 읽기 집약적인 워크 로드에 대 한 가장 효과적인 읽습니다. 반대로, 매우 쓰기 집약적 작업을 사용 하는 경우 캐시 값 보다 더 많은 오버 헤드가 발생할 수 있습니다 및 수 없게 됩니다.

CSV 메모리 내 캐시 읽기에 대 한 최대 총 실제 메모리의 80%를 사용할 수 있습니다.

  > [!TIP]
  > 하이퍼 수렴 형 배포의 경우 여기서 계산 하 고 동일한 서버에서 실행 되는 저장소 가상 머신에 대 한 메모리를 충분히 남기도록 않도록 주의 해야 합니다. 메모리에 대 한 경합이 줄어들고를 사용 하 여 수렴 형된 스케일 아웃 파일 서버 (SoFS) 배포에 대 한 다음이 적용 되지 않습니다.

  > [!NOTE]
  > DISKSPD 등의 특정 microbenchmarking 도구와 [VM Fleet](https://github.com/Microsoft/diskspd/tree/master/Frameworks/VMFleet) 더 심각한 결과가 발생할 수 있습니다 CSV를 사용 하 여 메모리에 읽기 캐시 하지 않고 보다 사용 합니다. 기본적으로 VM Fleet 10gib 인 VHDX 가상 컴퓨터당 – 약 1tib –에 100 개의 Vm에 대 한 총 및 수행 하나 만듭니다 *균일 하 게 임의* 에 쓰고 읽습니다. 실제 워크 로드와 달리 읽기 메모리 내 캐시가 유효 하지 않은 하 고 방금 오버 헤드를 초래 하므로 모든 예측이 나 반복적인 패턴을 수행 하지 않습니다.

## <a name="configuring-the-in-memory-read-cache"></a>읽기 캐시를 메모리 내 구성

CSV 메모리 내 캐시는 동일한 기능을 사용 하 여 Windows Server 2016 및 Windows Server 2019 모두에서 사용할 수 있는 읽습니다. Windows Server 2016에서 기본적으로 해제 되어 해당 합니다. Windows Server 2019에서는 기본적으로 1gb 할당 합니다.

| OS 버전          | 기본 CSV 캐시 크기 |
|---------------------|------------------------|
| Windows Server 2016 | 0 (해제)           |
| Windows Server 2019 | 1 GiB                   |

PowerShell을 사용 하 여 얼마나 많은 메모리를 할당을 확인 하려면 다음을 실행 합니다.

```PowerShell
(Get-Cluster).BlockCacheSize
```

반환 값은 서버당 mebibytes (MiB)에 있습니다. 예를 들어 `1024` 1 gibibyte (GiB)를 나타냅니다.

얼마나 많은 메모리가 할당을 변경 하려면 PowerShell을 사용 하 여이 값을 수정 합니다. 예를 들어, 서버당 2 GiB를 할당 하려면 다음을 실행 합니다.

```PowerShell
(Get-Cluster).BlockCacheSize = 2048
```

변경 내용이 적용 되려면 즉시 일시 중지 한 다음에 CSV 볼륨을 다시 시작 또는 서버 간에 이동 합니다. 예를 들어, 각 CSV 다른 서버 노드로 이동한 후 다시 PowerShell 조각을이 사용 합니다.

```PowerShell
Get-ClusterSharedVolume | ForEach {
    $Owner = $_.OwnerNode
    $_ | Move-ClusterSharedVolume
    $_ | Move-ClusterSharedVolume -Node $Owner
}
```

## <a name="see-also"></a>참조

- [저장소 공간 다이렉트 개요](storage-spaces-direct-overview.md)
