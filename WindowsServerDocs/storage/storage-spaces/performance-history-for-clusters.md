---
title: 클러스터에 대 한 성능 기록
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8ee2e85723cc2449e8cb9c42ccb7d6b761482e3a
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474870"
---
# <a name="performance-history-for-clusters"></a>클러스터에 대 한 성능 기록

> 적용 대상: 시작

[스토리지 공간 다이렉트에 대 한 성능 기록](performance-history.md) 의이 하위 항목에서는 클러스터에 대해 수집 된 성능 기록에 대해 설명 합니다.

클러스터 수준에서 시작 되는 계열이 없습니다. 대신 서버 시리즈 (예:) `clusternode.cpu.usage` 는 클러스터의 모든 서버에 대해 집계 됩니다. 와 같은 볼륨 시리즈 `volume.iops.total` 는 클러스터의 모든 볼륨에 대해 집계 됩니다. 과 같은 드라이브 시리즈 `physicaldisk.size.total` 는 클러스터의 모든 드라이브에 대해 집계 됩니다.

## <a name="usage-in-powershell"></a>PowerShell에서 사용

[Get Cluster](https://docs.microsoft.com/powershell/module/failoverclusters/get-cluster) cmdlet을 사용 합니다.

```PowerShell
Get-Cluster | Get-ClusterPerf
```

## <a name="additional-references"></a>추가 참조

- [스토리지 공간 다이렉트에 대 한 성능 기록](performance-history.md)
