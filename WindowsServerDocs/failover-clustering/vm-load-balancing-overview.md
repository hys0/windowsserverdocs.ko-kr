---
ms.assetid: f0d4cecc-5a03-448c-bef9-86c4730b4eb0
title: 가상 머신 부하 분산 개요
ms.prod: windows-server-threshold
ms.technology: storage-failover-clustering
ms.topic: article
author: bhattacharyaz
manager: eldenc
ms.author: subhatt
ms.date: 09/19/2016
ms.openlocfilehash: 125dd7421cc1876c07983016498a9689d8a507ac
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65475985"
---
# <a name="virtual-machine-load-balancing-overview"></a>가상 머신 부하 분산 개요

> 적용 대상: Windows Server 2019, Windows Server 2016

사설 클라우드 배포에 대 한 주요 고려 사항은 자본 지출을 (<abbr title="자본 지출을">CapEx</abbr>) 프로덕션으로 이동 해야 합니다. 매우 일반적인 프로덕션 환경에서 최대 트래픽 중 언더 용량을 방지 하려면 사설 클라우드 배포에 중복성을 추가 하는 것이 증가 하지만 <abbr title="자본 지출을">CapEx</abbr>. 중복성을 위해 필요한 일부 노드에 더 많은 가상 컴퓨터 호스트는 불균형된 사설 클라우드를 통해 생성 됩니다 (<abbr title="가상 컴퓨터">Vm</abbr>) (예: 새로 다시 부팅된 하는 서버) 사용 미달 상태 다른 및 합니다.

<strong>빠른 비디오 개요</strong><br>(6 분)<br>
> [!VIDEO https://channel9.msdn.com/Blogs/windowsserver/Virtual-Machine-Load-Balancing-in-Windows-Server-2016/player]

## <a id="what-is-vm-load-balancing"></a>가상 머신 부하 분산 하는 것이 무엇입니까?
<abbr title="가상 컴퓨터">VM</abbr> 부하 분산 기능은 상자에서 Windows Server 2019에 Windows Server 2016의 장애 조치 클러스터의 노드 사용률을 최적화할 수 있습니다. 오버 커밋된 노드를 식별 하 고 다시 배포 <abbr title="가상 컴퓨터">Vm</abbr> 노드에 커밋된 해당 노드에서 합니다. 이 기능의 가장 중요 한 측면 중 일부는 다음과 같습니다.

* *무중단 솔루션 이므로*: <abbr title="가상 컴퓨터">Vm</abbr> 유휴 노드로 실시간 마이그레이션 됩니다.
* *기존 클러스터 환경과의 원활한 통합*: 선호도 방지, 장애 도메인 및 가능한 소유자와 같은 오류 정책은 적용 됩니다.
* *균형 조정에 대 한 추론*: <abbr title="가상 컴퓨터">VM</abbr> 메모리 부족 및 노드의 CPU 사용률입니다.
* *세분화 된 제어*: 기본적으로 사용하도록 설정되어 있습니다. 요청 시 또는 일정 한 간격으로 활성화할 수 있습니다.
* *강도 임계값*: 세 개의 임계값 사용 가능한 배포의 특징을 기반으로 합니다.

## <a id="feature-in-action"></a>작업의 기능
### <a id="new-node-added"></a>새 노드를 장애 조치 클러스터에 추가 됩니다.
![장애 조치 클러스터에 추가할 새 노드는 그래픽](media/vm-load-balancing/overview-VM-load-balancing-1.png)

장애 조치 클러스터에 새 용량을 추가 하는 경우는 <abbr title="가상 머신">VM</abbr> 부하 분산 기능은 다음 순서 대로 새로 추가 된 노드를 기존 노드에서 용량을 자동으로 분산 합니다.

1. 장애 조치 클러스터의 기존 노드에서 압력 평가 됩니다.
2. 임계값을 초과 하는 모든 노드가 식별 됩니다.
3. 가장 높은 압력을 포함 하는 노드는 분산의 우선 순위를 결정할 식별 됩니다.
4. <abbr title="가상 컴퓨터">Vm</abbr> 된 실시간 마이그레이션 (중단 시간 없이) 노드에서 장애 조치 클러스터의 새로 추가 된 노드에 대 한 임계값을 초과 합니다.

### <a id="recurring-load-balancing"></a>되풀이 부하 분산
![되풀이 VM 부하 분산의 그래픽](media/vm-load-balancing/overview-VM-load-balancing-2.png)

정기적으로 분산을 위해 구성 되 면 클러스터 노드에 대 한 압력 분산 30 분 마다 평가 됩니다. 또는 압력 요청 시 평가 될 수 있습니다. 흐름 단계는 다음과 같습니다.

1. 압력 사설 클라우드의 모든 노드에 대해 평가 됩니다.
2. 임계값 및 임계값을 초과 하는 모든 노드가 식별 됩니다.
3. 가장 높은 압력을 포함 하는 노드는 분산의 우선 순위를 결정할 식별 됩니다.
4. <abbr title="가상 컴퓨터">Vm</abbr> 된 실시간 마이그레이션 (중단 시간 없이) 노드의 최소 임계값 아래에 임계값을 초과 합니다.

## <a name="see-also"></a>관련 항목
* [가상 머신 부하 분산 심층 분석](vm-load-balancing-deep-dive.md)
* [장애 조치(failover) 클러스터링](failover-clustering-overview.md)
* [Hyper-v 개요](../virtualization/hyper-v/Hyper-V-on-Windows-Server.md)
