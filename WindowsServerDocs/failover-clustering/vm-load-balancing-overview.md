---
ms.assetid: f0d4cecc-5a03-448c-bef9-86c4730b4eb0
title: 가상 컴퓨터 부하 분산 개요
ms.prod: windows-server
ms.technology: storage-failover-clustering
ms.topic: article
author: bhattacharyaz
manager: eldenc
ms.author: subhatt
ms.date: 09/19/2016
ms.openlocfilehash: 1fea9e6297399a5081eb8fef1876f1b11d23c745
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71360984"
---
# <a name="virtual-machine-load-balancing-overview"></a>가상 컴퓨터 부하 분산 개요

> 적용 대상: Windows Server 2019, Windows Server 2016

사설 클라우드 배포에 대 한 주요 고려 사항은 자본 지출 (<abbr title="자본 지출">CapEx</abbr>)를 프로덕션으로 이동 하는 데 필요 합니다. 프로덕션 환경에서 사용량이 많은 트래픽 중에는 용량을 방지 하기 위해 사설 클라우드 배포에 중복성을 추가 하는 것이 매우 일반적 이지만 <abbr title="자본 지출">CapEx</abbr>을 선택합니다. 중복성 요구는 일부 노드가 더 많은 Virtual Machines를 호스팅하는 불균형 사설 클라우드에 의해 좌우 됩니다.<abbr title="가상 컴퓨터">VM</abbr>) 및 기타 항목 (예: 새로 다시 부팅 된 서버)을 사용할 수 없습니다.

<strong>빠른 비디오 개요</strong><br>(6 분)<br>
> [!VIDEO https://channel9.msdn.com/Blogs/windowsserver/Virtual-Machine-Load-Balancing-in-Windows-Server-2016/player]

## <a id="what-is-vm-load-balancing"></a>가상 컴퓨터 부하 분산 이란?
<abbr title="가상 컴퓨터">VM</abbr> 부하 분산은 장애 조치 (Failover) 클러스터의 노드 사용률을 최적화할 수 있는 Windows Server 2019 및 Windows Server 2016의 기본 기능입니다. 과도 하 게 커밋된 노드를 식별 하 고 다시 배포 합니다. <abbr title="가상 컴퓨터">VM</abbr> 이러한 노드는 커밋된 노드를 대상으로 합니다. 이 기능의 몇 가지 두드러진 몇 가지 측면은 다음과 같습니다.

* *가동 중지 시간이 0 인 솔루션은*다음과 같습니다. <abbr title="가상 머신">VM</abbr> 는 유휴 노드로 실시간 마이그레이션됩니다.
* *기존 클러스터 환경과의 원활한 통합*: 선호도 방지, 장애 도메인 및 가능한 소유자와 같은 오류 정책이 적용 됩니다.
* *분산 추론*: <abbr title="가상 컴퓨터">VM</abbr> 노드의 메모리 부족 및 CPU 사용률입니다.
* *세부적인 제어*: 기본적으로 사용하도록 설정되어 있습니다. 요청 시 또는 정기적으로 활성화 될 수 있습니다.
* *강도 임계값*: 배포의 특징에 따라 세 가지 임계값을 사용할 수 있습니다.

## <a id="feature-in-action"></a>작동 중인 기능
### <a id="new-node-added"></a>새 노드가 장애 조치 (Failover) 클러스터에 추가 됩니다.
![장애 조치 (Failover) 클러스터에 추가 되는 새 노드의 그래픽](media/vm-load-balancing/overview-VM-load-balancing-1.png)

장애 조치 (Failover) 클러스터에 새 용량을 추가 하는 경우 <abbr title="가상 컴퓨터">VM</abbr> 부하 분산 기능은 기존 노드의 용량을 다음과 같은 순서로 새로 추가 된 노드에 자동으로 분산 합니다.

1. 압력은 장애 조치 (Failover) 클러스터의 기존 노드에서 평가 됩니다.
2. 임계값을 초과 하는 모든 노드가 식별 됩니다.
3. 가장 높은 압력의 노드는 분산의 우선 순위를 결정 하는 것으로 식별 됩니다.
4. <abbr title="가상 머신">VM</abbr> 는 장애 조치 (Failover) 클러스터에서 새로 추가 된 노드로 임계값을 초과 하는 노드의 실시간 마이그레이션 (중단 시간 없음)입니다.

### <a id="recurring-load-balancing"></a>반복 부하 분산
![반복 VM 부하 분산 그래픽](media/vm-load-balancing/overview-VM-load-balancing-2.png)

정기적으로 분산 되도록 구성 된 경우 클러스터 노드의 압력은 30 분 마다 분산 될 수 있도록 평가 됩니다. 또는 요청 시 압력을 평가할 수 있습니다. 단계의 흐름은 다음과 같습니다.

1. 압력은 사설 클라우드의 모든 노드에서 평가 됩니다.
2. 임계값을 초과 하는 모든 노드와 그 아래 임계값이 식별 됩니다.
3. 가장 높은 압력의 노드는 분산의 우선 순위를 결정 하는 것으로 식별 됩니다.
4. <abbr title="가상 머신">VM</abbr> 최소 임계값을 초과 하는 노드에 대 한 임계값을 초과 하는 노드의 실시간 마이그레이션 (중단 시간 없음)입니다.

## <a name="see-also"></a>관련 항목
* [가상 컴퓨터 부하 분산 심층 살펴보기](vm-load-balancing-deep-dive.md)
* [장애 조치(failover) 클러스터링](failover-clustering-overview.md)
* [Hyper-v 개요](../virtualization/hyper-v/Hyper-V-on-Windows-Server.md)
