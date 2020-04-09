---
title: 스토리지 공간 다이렉트 메모리 내 읽기 캐시
ms.prod: windows-server
ms.author: eldenc
manager: siroy
ms.technology: storage-spaces
ms.topic: article
author: eldenchristensen
ms.date: 02/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: d9ebc40b69373dafbebdb87f2abe624a5a7a4375
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858956"
---
# <a name="using-storage-spaces-direct-with-the-csv-in-memory-read-cache"></a>CSV 메모리 내 읽기 캐시와 스토리지 공간 다이렉트 사용
> 적용 대상: Windows Server 2016, Windows Server 2019

이 항목에서는 시스템 메모리를 사용 하 여 [스토리지 공간 다이렉트](storage-spaces-direct-overview.md)의 성능을 높이는 방법에 대해 설명 합니다.

스토리지 공간 다이렉트은 CSV (클러스터 공유 볼륨) 메모리 내 읽기 캐시와 호환 됩니다. 시스템 메모리를 사용 하 여 읽기 캐시는 Hyper-v와 같은 응용 프로그램의 성능을 향상 시킬 수 있습니다 .이는 버퍼링 되지 않은 i/o를 사용 하 여 VHD 또는 VHDX 파일에 액세스 합니다. 버퍼링 되지 않은 IOs는 Windows Cache Manager에서 캐시 되지 않는 작업입니다.

메모리 내 캐시는 서버 로컬 이므로 하이퍼 수렴 형 스토리지 공간 다이렉트 배포에 대 한 데이터 집약성이 향상 됩니다. 최근 읽기는 가상 머신이 실행 되는 호스트의 메모리에 캐시 되므로 네트워크를 통한 읽기 빈도를 줄일 수 있습니다. 이로 인해 대기 시간이 단축 되 고 저장소 성능이 향상 됩니다.

## <a name="planning-considerations"></a>계획 시 고려 사항

메모리 내 읽기 캐시는 VDI (가상 데스크톱 인프라)와 같은 읽기 집약적인 작업에 가장 효과적입니다. 반대로 작업 부하가 매우 많은 경우 캐시는 값 보다 더 많은 오버 헤드를 발생 시킬 수 있으므로 사용 하지 않도록 설정 해야 합니다.

CSV 메모리 내 읽기 캐시에 대해 최대 80%의 총 실제 메모리를 사용할 수 있습니다.

  > [!TIP]
  > 계산 및 저장소가 동일한 서버에서 실행 되는 하이퍼 수렴 형 배포의 경우 가상 컴퓨터에 충분 한 메모리를 남겨 두세요. 메모리 경합을 줄이고 수렴 형 스케일 아웃 파일 서버 (SoFS) 배포의 경우에는 적용 되지 않습니다.

  > [!NOTE]
  > DISKSPD 및 [VM](https://github.com/Microsoft/diskspd/tree/master/Frameworks/VMFleet) 등의 특정 마이크로 벤치마킹 도구를 사용 하는 경우 이외에는 CSV 메모리 내 읽기 캐시를 사용 하는 경우 더 나쁜 결과가 발생할 수 있습니다. 기본적으로 VM은 가상 컴퓨터당 1 10 GiB VHDX를 만든 후 100 Vm에 대 한 약 1 TiB 합계를 생성 한 후 *일관 된 임의* 읽기 및 쓰기를 수행 합니다. 실제 워크 로드와 달리 읽기는 예측 가능 하거나 반복적인 패턴을 따르지 않으므로 메모리 내 캐시가 유효 하지 않으며 오버 헤드가 발생 합니다.

## <a name="configuring-the-in-memory-read-cache"></a>메모리 내 읽기 캐시 구성

CSV 메모리 내 읽기 캐시는 동일한 기능을 가진 Windows Server 2016 및 Windows Server 2019에서 모두 사용할 수 있습니다. Windows Server 2016에서는 기본적으로 해제 되어 있습니다. Windows Server 2019에서는 기본적으로 1gb가 할당 되어 있습니다.

| OS 버전          | 기본 CSV 캐시 크기 |
|---------------------|------------------------|
| Windows Server 2016 | 0 (사용 안 함)           |
| Windows Server 2019 | GiB 1                   |

PowerShell을 사용 하 여 할당 된 메모리의 양을 확인 하려면 다음을 실행 합니다.

```PowerShell
(Get-Cluster).BlockCacheSize
```

반환 되는 값은 서버 당 mebibytes (MiB)에 있습니다. 예를 들어 `1024`은 1 개 gid bibyte (GiB)를 나타냅니다.

할당 되는 메모리의 양을 변경 하려면 PowerShell을 사용 하 여이 값을 수정 합니다. 예를 들어 서버당 2 GiB를 할당 하려면 다음을 실행 합니다.

```PowerShell
(Get-Cluster).BlockCacheSize = 2048
```

변경 내용이 즉시 적용 되려면 CSV 볼륨을 일시 중지 했다가 다시 시작 하거나 서버 간에 이동 합니다. 예를 들어 다음 PowerShell 조각을 사용 하 여 각 CSV를 다른 서버 노드로 이동 하 고 다시 다시 합니다.

```PowerShell
Get-ClusterSharedVolume | ForEach {
    $Owner = $_.OwnerNode
    $_ | Move-ClusterSharedVolume
    $_ | Move-ClusterSharedVolume -Node $Owner
}
```

## <a name="see-also"></a>참고 항목

- [스토리지 공간 다이렉트 개요](storage-spaces-direct-overview.md)
