---
title: 이해 하 고 다시 동기화 저장소를 참조 하세요.
description: 저장소 다시 동기화가 발생 하는 경우 Windows Server 2019에 확인 하는 방법에 대 한 자세한 정보.
keywords: 저장소 공간 다이렉트, 저장소 다시 동기화를 다시 동기화에 S2D 저장소
ms.prod: windows-server-threshold
ms.author: adagashe
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 01/14/2019
ms.localizationpriority: medium
ms.openlocfilehash: 81b1136a4b6a5cf8423a99e898b482a9b2849b5f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813464"
---
# <a name="understand-and-monitor-storage-resync"></a>저장소 재 동기화 이해 및 모니터링

>적용 대상: Windows Server 2019

저장소 동기화 경고는의 새로운 기능인 [저장소 공간 다이렉트](storage-spaces-direct-overview.md) 상태 관리 서비스 저장소를 다시 동기화 하는 경우 오류를 throw 할 수 있도록 Windows Server 2019에 합니다. 경고를 알리는 다시 동기화 진행 중일 때 더 많은 서버를 실수로 오프 없는 되도록 유용 아래쪽 (일으킬 수 있는 영향을 받는 여러 장애 도메인 다운 클러스터 생성). 

이 항목에서는 배경 및 이해 하 고 저장소 공간 다이렉트를 사용 하 여 Windows Server 장애 조치 클러스터에 저장소 다시 동기화를 참조 하는 단계를 제공 합니다.

## <a name="understanding-resync"></a>다시 동기화 이해

저장소 동기화 가져오는 방법을 이해 하는 간단한 예제로 시작 해 보겠습니다. 항상 염두에서에 모든 공유 안 함 (로컬 드라이브만) 이러한 동작을 수행 하는 분산된 저장소 솔루션입니다. 하나의 서버 노드에 다운 후-다시 온라인 상태가 될 때까지 해당 드라이브를 업데이트 하지 않습니다 하는 경우 아래 볼 수 있듯이이 하이퍼 수렴 형 아키텍처 마찬가지입니다. 

"HELLO" 문자열을 저장 하려고 한다는 것을 가정 합니다. 

!["Hello" 문자열의 ASCII](media/understand-storage-resync/hello.png)

3 방향 미러 복원 력 있는 Asssuming,이 문자열의 세 복사본이 있습니다. 이제 한다면 서버 #1 (에 대해 일시적으로 유지 관리), #1 복사를 액세스할 수 없습니다 했습니다.

![#1 복사본에 액세스할 수 없습니다.](media/understand-storage-resync/copy1.png)

"도움말!"이 문자열 "HELLO"에서 업데이트를 가정 합니다. 지금은.

!["Help!" 문자열의 ASCII](media/understand-storage-resync/help.png)

문자열을 업데이트 한 후 # 2와 #3 복사 성공적으로 업데이트 됩니다. 그러나 복사 #1 여전히 액세스할 수 없습니다 서버 #1 다운 되어 일시적으로 (예:은 유지 관리). 

![# 2와 # 2에 복사할 작성 Gif "](media/understand-storage-resync/write.gif)

이제 동기화 된 데이터는 #1 복사를 했습니다. 운영 체제는 세부적인 영역 동기화 되지 않은 비트를 추적 하기 위해 추적을 사용 합니다. 서버 # 1을 다시 온라인 상태가 되 면 이러한 방식으로 2 또는 3의 복사본에서 데이터를 읽고 복사 # 1에서에서 데이터를 덮어쓰지 변경 내용을 동기화 할 수 있습니다. 이 방식의 장점은 있는 모든 서버 2 또는 3 서버에서 데이터를 다시 동기화 하는 것이 아니라, 부실 데이터를 복사 해야 한다는 점입니다.

![# 1에 복사할 덮어쓰기의 Gif "](media/understand-storage-resync/overwrite.gif)

따라서 데이터 동기화 가져오는 방법을 설명 합니다. 그러나이 어떻게 표시 되나요 높은 수준에서? 이 예제에서는 3 명의 서버 하이퍼 수렴 형 클러스터 있다는 것에 대 한 가정 합니다. 서버 #1 이면 유지 관리 종료 중인 것으로 표시 됩니다. 백업 서버 # 1를 가져오면 모든 세부적인 업데이트할 영역 추적 (위에 설명 됨)를 사용 하 여 해당 저장소를 다시 동기화 시작 됩니다. 모든 서버 표시할 데이터를 모두 다시 동기화 되 면 최대으로 합니다.

![다시 동기화의 관리 보기의 Gif "](media/understand-storage-resync/admin.gif)

## <a name="how-to-monitor-storage-resync-in-windows-server-2019"></a>Windows Server 2019에 저장소 다시 동기화를 모니터링 하는 방법

저장소 동기화의 작동 원리를 이해 했으므로 Windows Server 2019에 나타납니다이 하는 방법을 살펴 보겠습니다. 새 오류를 추가 했습니다 합니다 [Health Service](../../failover-clustering/health-service-overview.md) 방법을 사용 하면 저장소를 다시 동기화 하는 경우.

PowerShell에서이 오류를 보려면 다음을 실행 합니다.

``` PowerShell
Get-HealthFault
```

Windows Server 2019에서 새 오류 이며 PowerShell을 기반으로 상태 오류 클러스터 유효성 검사 보고서에 다른 곳에 표시 됩니다. 

대 한 자세한 보기를 가져오려면 다음과 같이 PowerShell에는 시계열 데이터베이스를 쿼리할 수 있습니다.

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

특히 Windows Admin Center 상태 오류를 사용 하 여 상태 및 클러스터 노드의 색을 설정 합니다. 따라서이 새로운 오류 HCI 대시보드에서 클러스터 노드 (다시 동기화) (위쪽), 녹색, 녹색, 빨간색에서 바로 이동 하는 대신 노랑 빨강 (아래쪽) 전환 하면 합니다.

![다시 동기화의 2016 vs 2019 뷰의 이미지 "](media/understand-storage-resync/compare.png)

전체 저장소 다시 동기화 진행 상황을 표시 하면 얼마나 많은 데이터를 동기화 하 고 시스템 진행 여부 것을 정확 하 게 파악할 수 있습니다. Windows Admin Center 열고로 이동 합니다 *대시보드*, 새 경고를 다음과 같이 표시 됩니다.

![Windows Admin Center 경고의 이미지 "](media/understand-storage-resync/alert.png)

경고를 알리는 다시 동기화 진행 중일 때 더 많은 서버를 실수로 오프 없는 되도록 유용 아래쪽 (일으킬 수 있는 영향을 받는 여러 장애 도메인 다운 클러스터 생성). 

로 이동 하는 경우는 *서버* Windows Admin Center 페이지를 클릭 *인벤토리*, 특정 서버를 선택 하 고이 저장소 동기화 서버 단위로 표시 되는 방식과의 자세한 보기를 가져올 수 있습니다. 서버로 이동 하 고 확인 하는 경우는 *저장소* 차트에서 복구 해야 하는 데이터의 양이 표시 됩니다는 *자주색* 정확한 수를 사용 하 여 줄 바로 위에 있습니다. 이 크기는 서버 (더 많은 데이터 요구를 재 동기화 수)를 사용할 때 늘리고 서버를 다시 온라인 상태가 되 면를 점진적으로 감소 (데이터를 동기화 되는). 경우는 0을 복구 해야 하는 데이터를 저장소 용량은-를 다시 동기화를 수행할 수 있습니다 이제 해야 할 경우 서버를 중지 해야 합니다. Windows Admin Center이 환경의 스크린샷 아래에 나와 있습니다.

![Windows Admin Center server 뷰의 이미지 "](media/understand-storage-resync/server.png)

## <a name="how-to-see-storage-resync-in-windows-server-2016"></a>Windows Server 2016의 저장소 다시 동기화를 확인 하는 방법

알 수 있듯이이 경고 한 통찰력을 저장소 계층에서 발생 하는 데 특히 유용 합니다. 효과적으로 저장소 공간에서 복구 작업 같은 장기 실행 저장소 모듈 작업에 대 한 정보를 반환 하는 Get-storagejob cmdlet에서 가져올 수 있는 정보를 요약 합니다. 예제는 다음과 같습니다.

```PowerShell
Get-StorageJob
```

출력 예는 다음과 같습니다.

```
Name                  ElapsedTime           JobState              PercentComplete       IsBackgroundTask
----                  -----------           --------              ---------------       ----------------
Regeneration          00:01:19              Running               50                    True

```

나열 된 저장소 작업은 볼륨 기준으로, 실행 중인 작업의 목록을 볼 수 있습니다 및 개별 진행 상황을 추적할 수 있으므로이 뷰는 훨씬 더 세부적인. 이 cmdlet은 Windows Server 2016 및 2019 둘 다에서 작동합니다.

## <a name="see-also"></a>참조

- [유지 관리를 위해 서버를 오프 라인](maintain-servers.md)
- [저장소 공간 다이렉트 개요](storage-spaces-direct-overview.md)