---
ms.assetid: 5b5bab7a-727b-47ce-8efa-1d37a9639cba
title: "가상 컴퓨터 부하 분산 깊이 방문"
ms.prod: windows-server-threshold
ms.technology: storage-failover-clustering
ms.topic: article
author: bhattacharyaz
manager: eldenc
ms.author: subhatt
ms.date: 09/19/2016
ms.openlocfilehash: 6ee092a2e51e2181a2203bc263377c4a8ec60246
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="virtual-machine-load-balancing-deep-dive"></a>가상 컴퓨터 부하 분산 깊이 방문

> 에 해당: (세미콜론 연간 채널) Windows Server, Windows Server 2016

Windows Server 2016을 소개는 [가상 컴퓨터 부하 분산 기능](vm-load-balancing-overview.md) 노드의 클러스터 장애 조치의에서 사용을 최적화 하 합니다. 이 문서에서는 제어 하는 방법에 설명 <abbr title="가상 컴퓨터">VM</abbr> 부하 분산 합니다. 

## <a id="heuristics-for-balancing"></a>균형 조정 추론
<abbr title="가상 컴퓨터">VM</abbr> 다음 추론에 따라 노드의 로드 평가 가상 컴퓨터 부하 분산:
1. 현재 **메모리 압력**: 메모리가 Hyper-v 호스트에서 가장 일반적인 리소스 제한
2. <abbr title="중앙 처리 장치">CPU</abbr> **활용도** 평균 5 분 창 동안 노드의: 위해 최선을 다하고 과도 하 게 되셨습니다 클러스터 노드에서 완화

## <a id="controlling-aggressiveness-of-balancing"></a>균형 조정 수준 제어
사용 하 여 메모리 및 CPU 추론에 따라 균형 수준 구성할 수는 클러스터 일반적인 속성 'AutoBalancerLevel'에서 합니다. PowerShell에서 다음을 실행할 수준 제어 하려면:

```PowerShell
(Get-Cluster).AutoBalancerLevel = <value>
```

| AutoBalancerLevel | 수준 | 동작 |
|-------------------|----------------|----------|
| 1 (기본) | 낮은 | 호스트 80% 로드 된 경우 이동 |
| 2 | 보통 | 호스트 로드 70% 이상의 경우 이동 |
| 3 | 높은 | 호스트 로드 60% 이상의 경우 이동 | 

![균형 조정 수준 구성 PowerShell의 그래픽](media/vm-load-balancing/detailed-VM-load-balancing-1.jpg)

## <a name="controlling-abbr-titlevirtual-machinevmabbr-load-balancing"></a>제어 <abbr title="가상 컴퓨터">VM</abbr> 부하 분산
<abbr title="가상 컴퓨터">VM</abbr> 부하 분산 기본적으로 활성화 되어 있으며 부하 분산 발생 하는 경우 클러스터 일반적인 속성 'AutoBalancerMode'으로 구성할 수 있습니다. 제어 하려면 노드 관리 클러스터 조정 하는 경우:

### <a name="using-failover-cluster-manager"></a>클러스터 장애 조치 관리자를 사용 하 여 다음과 같습니다.
1. 클러스터 이름을 단추로 클릭 하 고 "속성" 옵션을 선택 합니다.  
    ![클러스터 장애 조치 클러스터 관리자 통해 재산을 선택 하는 그래픽](media/vm-load-balancing/detailed-VM-load-balancing-2.jpg)

2.  "분산" 창을 선택합니다  
    ![클러스터 장애 조치 관리자 통해 분산 옵션을 선택 하면의 그래픽](media/vm-load-balancing/detailed-VM-load-balancing-3.jpg)

### <a name="using-powershell"></a>PowerShell을 사용 하 여 다음과 같습니다.
다음 실행 합니다.
```powershell
(Get-Cluster).AutoBalancerMode = <value>
```

|AutoBalancerMode |동작| 
|:----------------:|:----------:|
|0| 사용 안 함| 
|1| 노드 가입에 잔액을 로드합니다| 
|2 (기본)| 부하 분산 노드 가입 켜고 30 분 마다 |

## <a name="abbr-titlevirtual-machinevmabbr-load-balancing-vs-system-center-virtual-machine-manager-dynamic-optimization"></a><abbr title="가상 컴퓨터">VM</abbr> 부하 분산 System Center 가상 컴퓨터 관리자 동적 최적화 대
노드 관리 기능을 제공 대상 배포 System Center 가상 컴퓨터 Manager를 않고도으로 기본 기능을 (<abbr title="System Center 가상 컴퓨터 Manager">SCVMM</abbr>). <abbr title="System Center 가상 컴퓨터의 관리자">SCVMM</abbr> 동적 최적화에 대 한 클러스터에서 가상 컴퓨터 부하 분산을 위한 권장 장치가 <abbr title="System Center 가상 컴퓨터 Manager">SCVMM</abbr> 배포 됩니다. <abbr title="System Center 가상 컴퓨터의 관리자">SCVMM</abbr> 자동으로 Windows Server를 비활성화 <abbr title="가상 컴퓨터">VM</abbr> 부하 분산 동적 최적화를 사용 합니다.

## <a name="see-also"></a>참조 하십시오
* [가상 컴퓨터 부하 분산 개요](vm-load-balancing-overview.md)
* [장애 조치 클러스터링](failover-clustering-overview.md)
* [Hyper-v 개요](../virtualization/hyper-v/Hyper-V-on-Windows-Server.md)
