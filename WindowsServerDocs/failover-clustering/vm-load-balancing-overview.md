---
ms.assetid: f0d4cecc-5a03-448c-bef9-86c4730b4eb0
title: "가상 컴퓨터 부하 분산 개요"
ms.prod: windows-server-threshold
ms.technology: storage-failover-clustering
ms.topic: article
author: bhattacharyaz
manager: eldenc
ms.author: subhatt
ms.date: 09/19/2016
ms.openlocfilehash: 0a106db25d476088898b914481e6041f20ce2e9e
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="virtual-machine-load-balancing-overview"></a>가상 컴퓨터 부하 분산 개요

> 에 해당: (세미콜론 연간 채널) Windows Server, Windows Server 2016

중요 한 개인 클라우드 배포 과제가 대문자 지출 (<abbr title="대문자 지출">설비투자</abbr>)을 사용해 서 해야 합니다. 매우 일반적으로 중복 개인 클라우드 배포 생산, 최고 교통 동안 아래 용량을 방지 하려면에 추가 있지만 이렇게 하면 향상 <abbr title="대문자 지출">설비투자</abbr>합니다. 중복에 대 한 필요성 짝이 맞지 않습니다 개인 구름 일부 노드 더 가상 컴퓨터를 호스트 하는 따른 (<abbr title="가상 컴퓨터">Vm</abbr>) (예: 갓 rebooted 서버) 작업량이 다른 하 고 있습니다.

## <a id="what-is-vm-load-balancing"></a>가상 컴퓨터 부하 분산은 무엇 인가요?
<abbr title="가상 컴퓨터">VM</abbr> 노드의 클러스터 장애 조치의에서 사용을 최적화 수 있도록 Windows Server 2016의 새로운 기능으로 상자에서 부하 분산입니다. 너무 많이 위해 최선을 다하고 노드 식별 하 고 다시 배포 <abbr title="가상 컴퓨터">Vm</abbr> 노드 확정 아래에 이러한 노드에서 합니다. 이 기능은의 주요 측면 중 일부는 다음과 같습니다.

* *0 가동 방법은*: <abbr title="가상 컴퓨터">Vm</abbr> 유휴 노드로 실시간 마이그레이션 됩니다.
* *기존 클러스터 환경 완벽 한 통합*: 바이러스 선호도, 오류 도메인 및 가능한 소유자와 같은 오류가 정책을 적용 됩니다.
* *균형 조정 추론*: <abbr title="가상 컴퓨터">VM</abbr> 메모리 압력 및 노드 cpu 합니다.
* *단위 제어*: 기본적으로 사용할 수 있습니다. 일정 한 간격으로 또는 주문형 활성화할 수 있습니다.
* *수준 임계값*: 배포의 특성을 기반으로 사용할 수 있는 세 개의 임계값 합니다.

## <a id="feature-in-action"></a>실행 중인 기능
### <a id="new-node-added"></a>클러스터 장애 조치 새 노드가 추가
![장애 조치 클러스터에 추가 되 고 새 노드의 그래픽](media/vm-load-balancing/overview-VM-load-balancing-1.png)

새 용량 장애 클러스터에 추가 하면는 <abbr title="가상 컴퓨터">VM</abbr> 부하 분산 기능 순서로 새로 추가 된 노드에서 기존 노드에서 용량 자동으로 조정 합니다.

1. 클러스터 장애 조치의에서 기존 노드에서 압력 평가 됩니다.
2. 임계값을 초과 하는 모든 노드 표시 됩니다.
3. 균형의 우선 순위를 확인 하려면 노드 최고 압력으로 표시 됩니다.
4. <abbr title="가상 컴퓨터">Vm</abbr> 하시 마이그레이션 라이브 (시간 아니요) 임계값 새로 추가 된 노드에서 클러스터 장애 조치를 초과 노드에서 합니다.

### <a id="recurring-load-balancing"></a>반복 부하 분산
![된 되풀이 VM의 그래픽 부하 분산](media/vm-load-balancing/overview-VM-load-balancing-2.png)

균형 조정 정기적으로 구성 된 경우 클러스터 노드에서 압력 30 분 마다 균형 조정에 대 한 평가 됩니다. 또는 압력 평가 주문형 될 수 있습니다. 흐름을 단계는 다음과 같습니다.

1. 압력 개인 클라우드 모든 노드에서 평가 됩니다.
2. 임계값와 미만 못한 배지를 초과 모든 노드 표시 됩니다.
3. 균형의 우선 순위를 확인 하려면 노드 최고 압력으로 표시 됩니다.
4. <abbr title="가상 컴퓨터">Vm</abbr> 하시 마이그레이션 라이브 (시간 아니요) 최소 임계값 노드로 임계값 초과 노드에서 합니다.

## <a name="see-also"></a>참조 하십시오
* [가상 컴퓨터 부하 분산 깊이 방문](vm-load-balancing-deep-dive.md)
* [장애 조치 클러스터링](failover-clustering-overview.md)
* [Hyper-v 개요](../virtualization/hyper-v/Hyper-V-on-Windows-Server.md)
