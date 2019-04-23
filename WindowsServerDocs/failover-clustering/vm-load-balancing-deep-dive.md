---
ms.assetid: 5b5bab7a-727b-47ce-8efa-1d37a9639cba
title: 가상 머신 부하 분산 심층 분석
ms.prod: windows-server-threshold
ms.technology: storage-failover-clustering
ms.topic: article
author: bhattacharyaz
manager: eldenc
ms.author: subhatt
ms.date: 09/19/2016
ms.openlocfilehash: f90802a8e77ade0b9f282730e7cb61c73a246018
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853424"
---
# <a name="virtual-machine-load-balancing-deep-dive"></a>가상 머신 부하 분산 심층 분석

> 적용 대상: Windows Server (반기 채널), Windows Server 2016

Windows Server 2016을 소개 합니다 [가상 머신 부하 분산 기능](vm-load-balancing-overview.md) 장애 조치 클러스터의 노드 사용률을 최적화 하기 위해. 이 문서에서는 구성 및 제어 하는 방법을 설명 <abbr title="가상 머신">VM</abbr> 부하 분산 합니다. 

## <a id="heuristics-for-balancing"></a>균형 조정에 대 한 추론
<abbr title="가상 컴퓨터">VM</abbr> 다음과 같은 추론에 따라 노드의 부하를 평가 가상 머신 부하 분산:
1. 현재 **메모리 압력**: 메모리는 Hyper-v 호스트에서 가장 일반적인 리소스 제약 조건
2. <abbr title="중앙 처리 장치">CPU</abbr> **사용률** 5 분 창을 통해 평균을 계산 노드: 완화 되기 오버 커밋된 클러스터의 노드

## <a id="controlling-aggressiveness-of-balancing"></a>분산의 강도 제어합니다.
사용 하 여 메모리 및 CPU 추론을 기반으로 분산의 강도 구성할 수 있습니다는 클러스터 공용 속성 'AutoBalancerLevel'. PowerShell에서 다음을 실행 하는 강도 제어 합니다.

```PowerShell
(Get-Cluster).AutoBalancerLevel = <value>
```

| AutoBalancerLevel | 강도 | 동작 |
|-------------------|----------------|----------|
| 1(기본값) | 낮음 | 호스트 80% 이상 로드 된 경우 이동 |
| 2 | 보통 | 호스트가 로드할 70%를 초과 하는 경우 이동 |
| 3 | 높음 | 평균 노드 및 이동 평균 보다 5% 이상 호스트가 때 | 

![분산의 강도 구성 하는 PowerShell의 그래픽](media/vm-load-balancing/detailed-VM-load-balancing-1.jpg)

## <a name="controlling-abbr-titlevirtual-machinevmabbr-load-balancing"></a>제어 <abbr title="가상 머신">VM</abbr> 부하 분산
<abbr title="가상 컴퓨터">VM</abbr> 기본적으로 활성화 되어 부하 분산 및 부하 분산이 발생 하는 경우 클러스터 공용 속성 'AutoBalancerMode'으로 구성할 수 있습니다. 노드 공정성 클러스터를 분산 하는 경우를 제어 합니다.

### <a name="using-failover-cluster-manager"></a>장애 조치 클러스터 관리자를 사용 합니다.
1. 클러스터 이름 단추로 클릭 하 고 "Properties" 옵션을 선택 합니다.  
    ![장애 조치 클러스터 관리자를 통해 클러스터에 대 한 속성을 선택 하는 그래픽](media/vm-load-balancing/detailed-VM-load-balancing-2.jpg)

2.  "분산 장치" 창을 선택합니다  
    ![장애 조치 클러스터 관리자를 통해 분산 옵션을 선택 하는 그래픽](media/vm-load-balancing/detailed-VM-load-balancing-3.jpg)

### <a name="using-powershell"></a>PowerShell을 사용합니다.
다음을 실행 합니다.
```powershell
(Get-Cluster).AutoBalancerMode = <value>
```

|AutoBalancerMode |동작| 
|:----------------:|:----------:|
|0| 사용 안 함| 
|1| 부하 분산에 노드 조인| 
|2 (기본값)| 부하 분산에 노드 조인 하 고 30 분 마다 |

## <a name="abbr-titlevirtual-machinevmabbr-load-balancing-vs-system-center-virtual-machine-manager-dynamic-optimization"></a><abbr title="Virtual Machine">VM</abbr> vs 로드 균형 조정 합니다. System Center Virtual Machine Manager 동적 최적화
System Center Virtual Machine Manager 없이 배포를 겨냥 하는 기본 기능을 제공 하는 노드 공정성 기능 (<abbr title="System Center Virtual Machine Manager">SCVMM</abbr>). <abbr title="System Center Virtual Machine Manager">SCVMM</abbr> 동적 최적화에 대 한 클러스터에서 가상 머신 부하 분산을 위해 권장 되는 메커니즘은 <abbr title="System Center Virtual Machine Manager">SCVMM</abbr> 배포 합니다. <abbr title="System Center Virtual Machine Manager">SCVMM</abbr> Windows Server를 자동으로 비활성화 <abbr title="가상 머신">VM</abbr> 동적 최적화를 사용할 때 로드 균형 조정 합니다.

## <a name="see-also"></a>관련 항목
* [가상 머신 부하 분산 개요](vm-load-balancing-overview.md)
* [장애 조치 클러스터링](failover-clustering-overview.md)
* [Hyper-v 개요](../virtualization/hyper-v/Hyper-V-on-Windows-Server.md)
