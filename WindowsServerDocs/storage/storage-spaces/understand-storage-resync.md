---
title: 저장소 다시 동기화 이해 및 참조
description: 저장소 다시 동기화가 발생 하는 경우와 Windows Server 2019에서이를 확인 하는 방법에 대 한 자세한 정보입니다.
ms.prod: windows-server
ms.author: adagashe
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 01/14/2019
ms.localizationpriority: medium
ms.openlocfilehash: 79e5e1e9daba005a086c16dd1d8e3e3f9a28a8a2
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85473420"
---
# <a name="understand-and-monitor-storage-resync"></a>스토리지 다시 동기화 이해 및 모니터링

>적용 대상: 시작

저장소 다시 동기화 경고는 상태 관리 서비스 다시 동기화 때 오류를 발생 시킬 수 있도록 하는 Windows Server 2019에 [스토리지 공간 다이렉트](storage-spaces-direct-overview.md) 의 새로운 기능입니다. 이 경고는 다시 동기화가 발생 하는 경우에 알려 주는 데 유용 합니다. 따라서 실수로 서버를 더 이상 사용 하지 않아도 됩니다 .이로 인해 여러 장애 도메인에 영향을 줄 수 있으므로 클러스터가 중단 됩니다.

이 항목에서는 스토리지 공간 다이렉트 사용 하 여 Windows Server 장애 조치 (failover) 클러스터에서 저장소 다시 동기화를 이해 하 고 확인 하는 배경 및 단계를 제공

## <a name="understanding-resync"></a>다시 동기화 이해

저장소를 동기화 하지 않는 방법을 이해 하는 간단한 예제부터 살펴보겠습니다. 모든 비공유 (로컬 드라이브만) 분산 저장소 솔루션은이 동작을 수행 합니다. 아래 표시 된 것 처럼 한 서버 노드가 다운 되 면 온라인 상태가 될 때까지 드라이브가 업데이트 되지 않습니다 .이는 하이퍼 수렴 형 아키텍처에 적용 됩니다.

"HELLO" 문자열을 저장 하려고 한다고 가정 합니다.

![문자열 "hello"의 ASCII](media/understand-storage-resync/hello.png)

3 방향 미러 복원 력이 있는 경우이 문자열의 복사본이 3 개 있습니다. 이제 서버 #1 일시적으로 (유지 관리의 경우) 사용 하는 경우 복사 #1에 액세스할 수 없습니다.

![복사 #1에 액세스할 수 없음](media/understand-storage-resync/copy1.png)

문자열을 "HELLO"에서 "HELP!"로 업데이트 한다고 가정 합니다. 지금은

![문자열 "help!"의 ASCII](media/understand-storage-resync/help.png)

문자열을 업데이트 한 후 #2 복사 하 고 #3 성공적으로 업데이트 됩니다. 그러나 서버 #1 일시적으로 다운 (유지 관리) 되기 때문에 복사 #1에는 액세스할 수 없습니다.

![#2 및 #2를 복사 하기 위한 쓰기 Gif](media/understand-storage-resync/write.gif)

이제 데이터가 동기화 되지 않은 복사 #1 있습니다. 운영 체제는 세분화 된 더티 영역 추적을 사용 하 여 동기화 되지 않은 비트를 추적 합니다. 이러한 방식으로 서버 #1 다시 온라인 상태가 되 면 복사 #2에서 데이터를 읽거나 #3 복사 #1에서 데이터를 덮어써서 변경 내용을 동기화 할 수 있습니다. 이 방법의 장점은 서버 #2 또는 서버 #3의 모든 데이터를 다시 동기화 하는 것이 아니라 오래 된 데이터만 복사 하면 된다는 것입니다.

![#1 복사 하기 위해 덮어쓰는 Gif](media/understand-storage-resync/overwrite.gif)

따라서 데이터가 동기화 되지 않는 방법을 설명 합니다. 그러나이는 상위 수준에서 어떻게 표시 되나요? 이 예에서는 서버 하이퍼 수렴 형 클러스터가 3 개 있다고 가정 합니다. 서버 #1 유지 관리 중인 경우 다운 된 것으로 표시 됩니다. 서버 #1 백업을 실행 하면 세분화 된 더티 지역 추적 (위에서 설명 함)을 사용 하 여 모든 저장소 다시 동기화 시작 됩니다. 데이터가 다시 동기화 되 면 모든 서버가 위쪽으로 표시 됩니다.

![다시 동기화의 관리 보기의 Gif "](media/understand-storage-resync/admin.gif)

## <a name="how-to-monitor-storage-resync-in-windows-server-2019"></a>Windows Server 2019에서 저장소 다시 동기화를 모니터링 하는 방법

저장소 다시 동기화가 작동 하는 방법을 이해 했으므로 이제 Windows Server 2019에 표시 되는 방식을 살펴보겠습니다. 저장소를 다시 동기화 때 표시 되는 [상태 관리 서비스](../../failover-clustering/health-service-overview.md) 에 새 오류를 추가 했습니다.

PowerShell에서이 오류를 보려면 다음을 실행 합니다.

``` PowerShell
Get-HealthFault
```

이는 Windows Server 2019의 새로운 오류 이며 PowerShell, 클러스터 유효성 검사 보고서 및 상태 오류를 기반으로 하는 다른 위치에 표시 됩니다.

좀 더 자세히 보기 위해 다음과 같이 PowerShell에서 시계열 데이터베이스를 쿼리할 수 있습니다.

```PowerShell
Get-ClusterNode | Get-ClusterPerf -ClusterNodeSeriesName ClusterNode.Storage.Degraded
```
다음은 몇 가지 예제 출력입니다.

```
Object Description: ClusterNode Server1

Series                       Time                Value Unit
------                       ----                ----- ----
ClusterNode.Storage.Degraded 01/11/2019 16:26:48     214 GB
```

특히 Windows 관리 센터는 상태 오류를 사용 하 여 클러스터 노드의 상태 및 색을 설정 합니다. 따라서이 새로운 오류는 HCI 대시보드에서 클러스터 노드가 빨간색에서 녹색으로 직접 이동 하는 대신 red (down)에서 노랑 (다시 동기화)으로 녹색 (위쪽)으로 전환 하는 원인이 됩니다.

![2016 vs 2019의 다시 동기화 보기 이미지](media/understand-storage-resync/compare.png)

전체 저장소 다시 동기화 진행률을 표시 하 여 동기화 되지 않은 데이터의 양과 시스템이 진행 중인지 여부를 정확 하 게 파악할 수 있습니다. Windows 관리 센터를 열고 *대시보드로*이동 하면 다음과 같이 새 경고가 표시 됩니다.

![Windows 관리 센터에서 경고 이미지](media/understand-storage-resync/alert.png)

이 경고는 다시 동기화가 발생 하는 경우에 알려 주는 데 유용 합니다. 따라서 실수로 서버를 더 이상 사용 하지 않아도 됩니다 .이로 인해 여러 장애 도메인에 영향을 줄 수 있으므로 클러스터가 중단 됩니다.

Windows 관리 센터에서 *서버* 페이지로 이동 하는 경우 *인벤토리*를 클릭 한 다음 특정 서버를 선택 하면이 저장소 다시 동기화가 서버 별로 어떻게 표시 되는지 자세히 확인할 수 있습니다. 서버를 탐색 하 여 *저장소* 차트를 살펴보면 위와 정확히 일치 하는 *자주색* 줄에서 복구 해야 하는 데이터의 양이 표시 됩니다. 이 크기는 서버가 다운 되 면 증가 하 고 (더 많은 데이터를 resynced 해야 함) 서버가 다시 온라인 상태가 되 면 (데이터가 동기화 되는 경우) 점진적으로 감소 합니다. 복구 해야 하는 데이터의 양이 0 인 경우 저장소는 다시 동기화 됩니다. 필요한 경우 서버를 무료로 사용할 수 있습니다. Windows 관리 센터에서이 환경의 스크린샷은 다음과 같습니다.

![Windows 관리 센터의 서버 뷰 이미지 "](media/understand-storage-resync/server.png)

## <a name="how-to-see-storage-resync-in-windows-server-2016"></a>Windows Server 2016에서 저장소 다시 동기화를 확인 하는 방법

여기에서 볼 수 있듯이이 경고는 저장소 계층에서 발생 하는 상황에 대 한 전체적인 보기를 가져오는 데 특히 유용 합니다. 저장소 공간에 대 한 복구 작업과 같은 장기 실행 저장소 모듈 작업에 대 한 정보를 반환 하는 Get StorageJob cmdlet에서 얻을 수 있는 정보를 효과적으로 요약 합니다. 아래에 예가 나와 있습니다.

```PowerShell
Get-StorageJob
```

다음은 출력의 예입니다.

```
Name                  ElapsedTime           JobState              PercentComplete       IsBackgroundTask
----                  -----------           --------              ---------------       ----------------
Regeneration          00:01:19              Running               50                    True

```

이 보기는 나열 된 저장소 작업이 볼륨당, 실행 중인 작업의 목록을 볼 수 있으며, 개별 진행 상황을 추적할 수 있으므로이 보기는 훨씬 더 세부적입니다. 이 cmdlet은 Windows Server 2016 및 2019 모두에서 작동 합니다.

## <a name="additional-references"></a>추가 참조

- [유지 관리를 위해 서버를 오프라인으로 전환](maintain-servers.md)
- [스토리지 공간 다이렉트 개요](storage-spaces-direct-overview.md)