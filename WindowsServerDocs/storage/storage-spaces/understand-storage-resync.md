---
title: 이해 하 고 저장소 재 동기화를 참조 하세요.
description: 저장소 재 동기화가 발생 하는 시기 및 Windows Server 2019에 표시 하는 방법에 대 한 자세한 정보입니다.
keywords: 저장소 공간 다이렉트, 저장소 재 동기화 재 동기화, 저장소, S2D
ms.prod: windows-server-threshold
ms.author: adagashe
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 01/14/2019
ms.localizationpriority: medium
ms.openlocfilehash: 81b1136a4b6a5cf8423a99e898b482a9b2849b5f
ms.sourcegitcommit: 748eccd10fc0c3c962d6e64ff6ead08017ac1947
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/15/2019
ms.locfileid: "9009668"
---
# 이해 하 고 저장소 재 동기화 모니터링

>적용 대상: Windows Server 2019

저장소 재 동기화 경고는 [저장소 공간 다이렉트](storage-spaces-direct-overview.md) 저장소 재 동기화 중인 때 오류를 발생 시킵니다. 상태 관리 서비스를 허용 하는 Windows Server 2019의 새로운 기능. 경고는 서버를 실수로 받아들이지 마세요 있도록 재 동기화 진행 중일 때 알리는에서 유용 아래쪽 (초래할 수 있습니다 여러 오류 도메인이 영향 다운 될 클러스터에 있는 결과). 

이 항목에서는 백그라운드 및 단계를 이해 하 고 저장소 공간 다이렉트를 사용 하 여 Windows Server 장애 조치 클러스터에서 저장소 재 동기화를 참조 하세요.

## 이해 재 동기화

저장소 동기화 가져오는 방법을 이해 하는 간단한 예제부터 살펴보겠습니다. 염두에 모든 비공유 (로컬 드라이브만) 분산된 저장소 솔루션으로 이러한 동작을 수행 합니다. 드라이브-온라인 상태가 될 때까지 업데이트 되지 않습니다 다음 하나의 서버 노드가, 중단 되 면 아래 확인할 수 있듯이 하이퍼 수렴 형 아키텍처의 경우도 마찬가지입니다. 

"HELLO" 문자열을 저장 하려고 가정 합니다. 

!["Hello" 문자열의 ASCII](media/understand-storage-resync/hello.png)

3 방향 미러 복원은 있다고 Asssuming,이 문자열의 복사본 세 개 했습니다. 이제 한다면 서버 #1 일시적으로 (에 대 한 관리)을 복사 #1 액세스할 수 없습니다 했습니다.

![복사 # 1에 액세스할 수 없습니다.](media/understand-storage-resync/copy1.png)

"도움말!"에서 "HELLO" 문자열 업데이트를 가정해 보겠습니다. 이때 합니다.

!["도움말!" 문자열의 ASCII](media/understand-storage-resync/help.png)

문자열을 업데이트 하 되 면 복사 #2 및 3 성공적으로 업데이트 됩니다. 하지만 복사 #1 여전히 액세스할 수 없습니다 서버 # 1은 용 때문에 아래쪽 일시적으로 (관리). 

![Gif #2 및 #2 복사에 쓰는 "](media/understand-storage-resync/write.gif)

이제 동기화 되는 데이터가 복사 #1 했습니다. 운영 체제 동기화 되 고 비트를 추적 하기 위해 추적 세밀 하 게 변경 영역을 사용 합니다. 서버 #1 다시 온라인 상태가 될 때이 방식으로 복사본 #2 또는 # 3에서에서 데이터를 읽고 #1 복사본의 데이터를 덮어쓰지 변경 내용을 동기화 할 수 있는 했습니다. 이 방법의 장점은 해야 한다는 사실을 데이터의 모든 서버 #2 또는 서버 # 3에서 데이터를 다시 동기화 하는 것이 아니라 부실를 복사 됩니다.

![#1 복사를 덮어쓰는 Gif "](media/understand-storage-resync/overwrite.gif)

따라서이 데이터 동기화 가져오는 방법을 설명 합니다. 하지만 어떻게이 표시 되나요 상위 수준? 이 예제는 세 가지 서버 하이퍼 수렴 형 클러스터 있다고 가정 합니다. 유지 관리 서버 #1 이면 아래쪽에 있는 것으로 표시 됩니다. 백업 서버 # 1을 가져오면 세밀 하 게 변경 영역 추적 (위에서 설명한)를 사용 하 여 해당 저장소의 모든 다시 동기화 시작 됩니다. 모든 서버 데이터를 모두 다시 동기화 되 면 표시 됩니다 최대 같습니다.

![재 동기화 admin 보기의 Gif "](media/understand-storage-resync/admin.gif)

## Windows Server 2019의 저장소 재 동기화를 모니터링 하는 방법

저장소 재 동기화 작동 하는 방법을 이해 했으므로 Windows Server 2019의 표시 하는 방법에 대해 살펴보겠습니다. 새 오류 저장소 재 동기화 중인 때 표시 되는 [상태 관리 서비스](../../failover-clustering/health-service-overview.md) 를 추가 했습니다.

PowerShell에서이 오류를 보려면 다음을 실행 합니다.

``` PowerShell
Get-HealthFault
```

Windows Server 2019의 새로운 오류 이며 PowerShell, 상태 오류를 토대로 클러스터 유효성 검사 보고서 및 다른 위치에 표시 됩니다. 

자세히 보기를 가져오려면 다음과 같이 PowerShell에서 시간 시리즈 데이터베이스를 쿼리할 수 있습니다.

```PowerShell
Get-ClusterNode | Get-ClusterPerf -ClusterNodeSeriesName ClusterNode.Storage.Degraded
```
다음은 몇 가지 출력 예제입니다.

```
Object Description: ClusterNode Server1

Series                       Time                Value Unit
------                       ----                ----- ----
ClusterNode.Storage.Degraded 01/11/2019 16:26:48     214 GB
```

특히, Windows Admin Center를 사용 하 여 상태 오류 상태 및 클러스터 노드의 색을 설정 합니다. 따라서이 새로운 오류 HCI 대시보드에서 클러스터 노드 (다시 동기화) (위쪽), 녹색, 녹색, 빨간색에서 직접 이동 하는 대신 노란색 (아래쪽) 빨간색에서 전환 하면 합니다.

![재 동기화 2016 vs 2019 보기의 이미지 "](media/understand-storage-resync/compare.png)

전체 저장소 재 동기화 진행 상황을 표시 하면 데이터의 양을 동기화 이며 시스템 순방향 진행 하는 여부를 정확 하 게 알 수 있습니다. Windows Admin Center를 열고 하 여 *대시보드에서*새 경고를 다음과 같이 표시 됩니다.

![Windows Admin Center에서 경고의 이미지 "](media/understand-storage-resync/alert.png)

경고는 서버를 실수로 받아들이지 마세요 있도록 재 동기화 진행 중일 때 알리는에서 유용 아래쪽 (초래할 수 있습니다 여러 오류 도메인이 영향 다운 될 클러스터에 있는 결과). 

Windows Admin Center의 *서버* 페이지로 이동 하 고 *인벤토리*를 클릭 한 다음 특정 서버를 선택 하는 경우 서버 단위로에서이 저장소 재 동기화 모양에 대 한 보다 세부적인된 보기를 얻을 수 있습니다. 정확한 숫자와 함께 *보라색* 줄에 수정 해야 하는 데이터 양을 나타납니다 서버로 이동 하 고 *저장소* 차트 바로 위에 있습니다. 이 금액 (더 많은 데이터 해야 재 수), 서버를 사용할 때를 증가 하 고 서버를 다시 온라인 상태가 될 때 점진적으로 저하 됩니다 (데이터를 동기화 되 고 됨). 복구는 0 되어야 하는 데이터의 양을, 저장소 때-다시 동기화를 수행 현재 위치는 자유롭게 하는 경우 서버를 중지 해야 합니다. Windows Admin Center에서 이러한 경험의 스크린샷은 다음과 같습니다.

![Windows Admin Center의 서버 보기의 이미지 "](media/understand-storage-resync/server.png)

## Windows Server 2016의 저장소 재 동기화를 확인 하는 방법

알 수 있듯이이 알림은 저장소 계층에서 과정과 대 한 통찰력을 얻는 방법에 대해 특히 유용 합니다. 저장소 공간에서 복구 작업 등의 장기 실행 저장소 모듈 작업에 대 한 정보를 반환 하는 Get StorageJob cmdlet에서 액세스할 수 있는 정보를 효과적으로 요약 되어 있습니다. 예는 다음과 같습니다.

```PowerShell
Get-StorageJob
```

출력 예는 다음과 같습니다.

```
Name                  ElapsedTime           JobState              PercentComplete       IsBackgroundTask
----                  -----------           --------              ---------------       ----------------
Regeneration          00:01:19              Running               50                    True

```

이 보기는 훨씬 더 세밀 하 게 볼륨당 나열 된 저장소 작업은 실행 되는 작업 목록을 표시 하 고 개별 진행 상황을 추적할 수 있습니다. 이 cmdlet은 Windows Server 2016 및 2019 모두에서 작동합니다.

## 참고 항목

- [유지 관리를 위해 서버를 오프라인으로 전환](maintain-servers.md)
- [저장소 공간 다이렉트 개요](storage-spaces-direct-overview.md)