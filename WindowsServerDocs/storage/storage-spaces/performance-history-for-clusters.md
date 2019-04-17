---
title: 클러스터에 대 한 성능 기록
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
Keywords: Storage Spaces Direct
ms.localizationpriority: medium
ms.openlocfilehash: 68596cbdcf8593cd3017c8ae5d0836891c78229c
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/01/2018
ms.locfileid: "1894322"
---
# <a name="performance-history-for-clusters"></a>클러스터에 대 한 성능 기록

> Windows Server 내부 인 미리 보기에 적용 됩니다.

이 하위 항목 [저장소 공간 직접에 대 한 성능](performance-history.md) 기록 클러스터에 대해 수집 된 성능 기록을 설명 합니다.

클러스터 수준에서 발생 하는 없는 시리즈가 있습니다. 대신, 서버 시리즈와 같은 `clusternode.cpu.usage`, 클러스터의 모든 서버에 대해 집계 됩니다. 볼륨 시리즈와 같은 `volume.iops.total`, 클러스터의 모든 볼륨에 대해 집계 됩니다. 시리즈, 같은 드라이브 및 `physicaldisk.size.total`, 클러스터의 모든 드라이브에 대해 집계 됩니다.

## <a name="usage-in-powershell"></a>PowerShell에서 사용 현황

[Get 클러스터](https://docs.microsoft.com/powershell/module/failoverclusters/get-cluster) cmdlet을 사용 하십시오.

```PowerShell
Get-Cluster | Get-ClusterPerf
```

## <a name="see-also"></a>참고 항목

- [저장소 공간 직접에 대 한 성능 기록](performance-history.md)
