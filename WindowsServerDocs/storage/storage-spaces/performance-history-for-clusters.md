---
title: 클러스터에 대 한 성능 기록
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
Keywords: 저장소 공간 다이렉트
ms.localizationpriority: medium
ms.openlocfilehash: 68596cbdcf8593cd3017c8ae5d0836891c78229c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818774"
---
# <a name="performance-history-for-clusters"></a>클러스터에 대 한 성능 기록

> 적용 대상: Windows Server Insider Preview

이 하위 항목의 [저장소 공간 다이렉트에 대 한 성능 기록을](performance-history.md) 클러스터에 대 한 수집 된 성능 기록에 설명 합니다.

클러스터 수준에서 발생 하는 계열이 있는 합니다. 대신, server 시리즈와 같은 `clusternode.cpu.usage`, 클러스터의 모든 서버에 대해 집계 됩니다. 볼륨 시리즈와 같은 `volume.iops.total`, 클러스터의 모든 볼륨에 대해 집계 됩니다. 시리즈와 같은 드라이브 및 `physicaldisk.size.total`, 클러스터의 모든 드라이브에 대해 집계 됩니다.

## <a name="usage-in-powershell"></a>PowerShell에서 사용

사용 된 [Get 클러스터](https://docs.microsoft.com/powershell/module/failoverclusters/get-cluster) cmdlet:

```PowerShell
Get-Cluster | Get-ClusterPerf
```

## <a name="see-also"></a>참조

- [저장소 공간 다이렉트에 대 한 성능 기록](performance-history.md)
