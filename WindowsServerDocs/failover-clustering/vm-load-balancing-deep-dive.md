---
ms.assetid: 5b5bab7a-727b-47ce-8efa-1d37a9639cba
title: 가상 컴퓨터 부하 분산 심층 살펴보기
ms.prod: windows-server
ms.technology: storage-failover-clustering
ms.topic: article
author: bhattacharyaz
manager: eldenc
ms.author: subhatt
ms.date: 09/19/2016
ms.openlocfilehash: 972e86d5f49f92d090eed1d4130544d0269c1309
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392225"
---
# <a name="virtual-machine-load-balancing-deep-dive"></a>가상 컴퓨터 부하 분산 심층 살펴보기

> 적용 대상: Windows Server 2019, Windows Server 2016

[가상 컴퓨터 부하 분산 기능은](vm-load-balancing-overview.md) 장애 조치 (Failover) 클러스터의 노드 사용률을 최적화 합니다. 이 문서에서는 VM 부하 분산을 구성 하 고 제어 하는 방법을 설명 합니다. 

## <a id="heuristics-for-balancing"></a>분산 추론
가상 컴퓨터 부하 분산은 다음 추론을 기반으로 노드의 부하를 평가 합니다.
1. 현재 **메모리 부족**: 메모리는 Hyper-v 호스트에서 가장 일반적인 리소스 제약 조건입니다.
2. 5 분 동안 평균 노드의 CPU **사용률** : 오버 커밋된 클러스터의 노드를 완화 합니다.

## <a id="controlling-aggressiveness-of-balancing"></a>분산 강도 제어
메모리 및 CPU 추론을 기반으로 하는 분산의 강도는 클러스터 일반 속성인 ' AutoBalancerLevel '를 사용 하 여 구성할 수 있습니다. 강도를 제어 하려면 PowerShell에서 다음을 실행 합니다.

```PowerShell
(Get-Cluster).AutoBalancerLevel = <value>
```

| AutoBalancerLevel | 쯤 | 동작 |
|-------------------|----------------|----------|
| 1(기본값) | 낮음 | 호스트가 80% 이상 로드 되 면 이동 |
| 2 | 보통 | 호스트가 70% 이상 로드 되 면 이동 |
| 3 | 높음 | 호스트가 평균 보다 5% 이상일 때 평균 노드 및 이동 | 

![분산 강도를 구성 하는 PowerShell의 그래픽](media/vm-load-balancing/detailed-VM-load-balancing-1.jpg)

## <a name="controlling-vm-load-balancing"></a>VM 부하 분산 제어
VM 부하 분산은 기본적으로 사용 하도록 설정 되며, 부하 분산은 클러스터 공통 속성인 ' AutoBalancerMode '로 구성할 수 있습니다. 노드가 클러스터의 균형을 조정 하는 시기를 제어 하려면:

### <a name="using-failover-cluster-manager"></a>장애 조치(Failover) 클러스터 관리자 사용:
1. 클러스터 이름을 마우스 오른쪽 단추로 클릭 하 고 "속성" 옵션을 선택 합니다.  
    ![장애 조치(Failover) 클러스터 관리자를 통해 클러스터의 속성을 선택 하는 그래픽](media/vm-load-balancing/detailed-VM-load-balancing-2.jpg)

2.  "부하 분산 장치" 창을 선택 합니다.  
    ![장애 조치(Failover) 클러스터 관리자를 통해 분산 장치 옵션을 선택 하는 그래픽](media/vm-load-balancing/detailed-VM-load-balancing-3.jpg)

### <a name="using-powershell"></a>PowerShell 사용:
다음을 실행 합니다.
```powershell
(Get-Cluster).AutoBalancerMode = <value>
```

|AutoBalancerMode |동작| 
|:----------------:|:----------:|
|0| 사용 안 함| 
|1| 노드 조인의 부하 분산| 
|2 (기본값)| 노드 조인과 30 분 마다 부하 분산 |

## <a name="vm-load-balancing-vs-system-center-virtual-machine-manager-dynamic-optimization"></a>VM 부하 분산 및 System Center Virtual Machine Manager 동적 최적화
노드 수준 기능은 System Center Virtual Machine Manager (SCVMM) 없이 배포를 대상으로 하는 기본 기능을 제공 합니다. Scvmm 동적 최적화는 SCVMM 배포를 위해 클러스터에서 가상 컴퓨터 부하를 분산 하는 데 권장 되는 메커니즘입니다. 동적 최적화를 사용 하도록 설정 하면 SCVMM에서 자동으로 Windows Server VM 부하 분산을 사용 하지 않도록 설정 합니다.

## <a name="see-also"></a>관련 항목
* [가상 컴퓨터 부하 분산 개요](vm-load-balancing-overview.md)
* [장애 조치(failover) 클러스터링](failover-clustering-overview.md)
* [Hyper-v 개요](../virtualization/hyper-v/Hyper-V-on-Windows-Server.md)
