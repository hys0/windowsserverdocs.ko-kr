---
title: 클러스터에 대 한 성능 기록
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7a5eec986d6e7d633f1917c599ab6fcd244c7008
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856206"
---
# <a name="performance-history-for-clusters"></a>클러스터에 대 한 성능 기록

> 적용 대상: Windows Server 2019

[스토리지 공간 다이렉트에 대 한 성능 기록](performance-history.md) 의이 하위 항목에서는 클러스터에 대해 수집 된 성능 기록에 대해 설명 합니다.

클러스터 수준에서 시작 되는 계열이 없습니다. 대신 서버 시리즈 (예: `clusternode.cpu.usage`)는 클러스터의 모든 서버에 대해 집계 됩니다. `volume.iops.total`와 같은 볼륨 시리즈는 클러스터의 모든 볼륨에 대해 집계 됩니다. `physicaldisk.size.total`와 같은 드라이브 시리즈는 클러스터의 모든 드라이브에 대해 집계 됩니다.

## <a name="usage-in-powershell"></a>PowerShell에서 사용

[Get Cluster](https://docs.microsoft.com/powershell/module/failoverclusters/get-cluster) cmdlet을 사용 합니다.

```PowerShell
Get-Cluster | Get-ClusterPerf
```

## <a name="see-also"></a>참고 항목

- [스토리지 공간 다이렉트에 대 한 성능 기록](performance-history.md)
