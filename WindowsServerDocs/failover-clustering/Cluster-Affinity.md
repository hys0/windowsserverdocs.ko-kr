---
title: 클러스터 선호도
ms.prod: windows-server
manager: eldenc
ms.technology: failover-clustering
ms.topic: article
author: johnmarlin-msft
ms.author: johnmar
ms.date: 03/07/2019
description: 이 문서에서는 장애 조치 (failover) 클러스터 선호도 및 방지 선호도 수준을 설명 합니다.
ms.openlocfilehash: b0c2209680f3c34ac8376d5662620595aff92c0b
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720611"
---
# <a name="cluster-affinity"></a>클러스터 선호도

> 적용 대상: Windows Server 2019, Windows Server 2016

장애 조치 (failover) 클러스터는 노드 간에 이동 하 여 실행할 수 있는 다양 한 역할을 보유할 수 있습니다. 특정 역할 (즉, 가상 컴퓨터, 리소스 그룹 등)이 동일한 노드에서 실행 되지 않는 경우가 있습니다.  리소스 사용, 메모리 사용 등으로 인해 발생할 수 있습니다.  예를 들어 메모리와 CPU를 많이 사용 하는 두 개의 가상 컴퓨터가 있으며, 두 가상 컴퓨터가 동일한 노드에서 실행 중인 경우 가상 컴퓨터 중 하나 또는 둘 다에 성능 영향 문제가 있을 수 있습니다.  이 문서에서는 클러스터 방지 선호도 수준 및 사용 방법에 대해 설명 합니다.

## <a name="what-is-affinity-and-antiaffinity"></a>선호도 및 방지 선호도 란 무엇 인가요?

선호도는 둘 이상의 역할 (i, e, virtual machines, 리소스 그룹 등) 간의 관계를 설정 하 여 함께 유지 하는 규칙입니다.  방지 선호도는 동일 하지만 지정 된 역할을 서로 분리 하 여 유지 하는 데 사용 됩니다. 장애 조치 (Failover) 클러스터는 해당 역할에 대해 방지 선호도를 사용 합니다.  더 구체적으로 말하자면 역할에 정의 된 [AntiAffinityClassNames](https://docs.microsoft.com/previous-versions/windows/desktop/mscs/groups-antiaffinityclassnames) 매개 변수는 동일한 노드에서 실행 되지 않습니다.  

## <a name="antiaffinityclassnames"></a>AntiAffinityClassnames

그룹의 속성을 볼 때 AntiAffinityClassNames 매개 변수는 기본적으로 비어 있습니다.  아래 예제에서 Group1 및 Group2는 동일한 노드에서 실행 되는 것으로 구분 되어야 합니다.  속성을 보려면 PowerShell 명령 및 결과는 다음과 같습니다.

    PS> Get-ClusterGroup Group1 | fl AntiAffinityClassNames
    AntiAffinityClassNames : {}

    PS> Get-ClusterGroup Group2 | fl AntiAffinityClassNames
    AntiAffinityClassNames : {}

AntiAffinityClassNames는 기본값으로 정의 되지 않으므로 이러한 역할은 함께 또는 별도로 실행할 수 있습니다.  목표는 분리 되도록 유지 하는 것입니다.  AntiAffinityClassNames에 대 한 값은 원하는 대로 지정할 수 있으며 동일 해야 합니다.  Group1 및 Group2는 가상 머신에서 실행 되는 도메인 컨트롤러 이며, 서로 다른 노드에서 실행 되는 것이 가장 좋습니다.  이러한 도메인 컨트롤러는 도메인 컨트롤러 이므로 클래스 이름에 DC를 사용 합니다.  값을 설정 하기 위해 PowerShell 명령 및 결과는 다음과 같습니다.

    PS> $AntiAffinity = New-Object System.Collections.Specialized.StringCollection
    PS> $AntiAffinity.Add("DC")
    PS> (Get-ClusterGroup -Name "Group1").AntiAffinityClassNames = $AntiAffinity
    PS> (Get-ClusterGroup -Name "Group2").AntiAffinityClassNames = $AntiAffinity

    PS> Get-ClusterGroup "Group1" | fl AntiAffinityClassNames
    AntiAffinityClassNames : {DC}

    PS> Get-ClusterGroup "Group2" | fl AntiAffinityClassNames
    AntiAffinityClassNames : {DC}

이제 설정 되었으므로 장애 조치 (failover) 클러스터링은 분리를 유지 하려고 시도 합니다.  

AntiAffinityClassName 매개 변수는 "soft" 블록입니다.  즉, 서로 다른 것을 유지 하려고 시도 하지만, 불가능 한 경우에도 동일한 노드에서 실행 되도록 허용 합니다.  예를 들어 그룹은 2 개 노드 장애 조치 (failover) 클러스터에서 실행 됩니다.  유지 관리를 위해 한 노드가 작동 해야 하는 경우 두 그룹이 모두 동일한 노드에서 실행 되 고 있음을 의미 합니다.  이 경우이를 포함 하는 것이 좋습니다.  가장 적합 한 것은 아니지만 virtial 컴퓨터는 모두 적합 한 성능 범위 내에서 계속 실행 됩니다.

## <a name="i-need-more"></a>추가 필요

앞서 언급 했 듯이 AntiAffinityClassNames는 소프트 블록입니다.  하지만 하드 블록이 필요한 경우는 어떻게 되나요?  동일한 노드에서 가상 컴퓨터를 실행할 수 없습니다. 그렇지 않으면 성능 영향이 발생 하 고 일부 서비스가 중단 될 수 있습니다.

이러한 경우에는 ClusterEnforcedAntiAffinity의 추가 클러스터 속성이 있습니다.  이 방지 선호도 수준으로 동일한 노드에서 실행 되는 것과 동일한 AntiAffinityClassNames 값이 없는 모든 비용을 방지할 수 있습니다.

속성 및 값을 보려면 PowerShell 명령 (및 결과)은 다음과 같습니다.

    PS> Get-Cluster | fl ClusterEnforcedAntiAffinity
    ClusterEnforcedAntiAffinity : 0

"0" 값은 사용 하지 않도록 설정 되 고 적용 되지 않음을 의미 합니다.  "1" 값은이를 사용 하도록 설정 하 고는 하드 블록입니다.  이 하드 블록을 사용 하도록 설정 하려면 명령 및 결과는 다음과 같습니다.

    PS> (Get-Cluster).ClusterEnforcedAntiAffinity = 1
    ClusterEnforcedAntiAffinity : 1

이러한 두 설정이 모두 설정 되 면 그룹을 함께 온라인 상태로 전환 하지 못하게 됩니다.  동일한 노드에 있는 경우 장애 조치(Failover) 클러스터 관리자에서 볼 수 있습니다.

![클러스터 선호도](media/Cluster-Affinity/Cluster-Affinity-1.png)

그룹의 PowerShell 목록에 다음이 표시 됩니다.

    PS> Get-ClusterGroup

    Name       State
    ----       -----
    Group1     Offline(Anti-Affinity Conflict)
    Group2     Online

## <a name="additional-comments"></a>추가 설명

- 필요에 따라 적절 한 방지 선호도 설정을 사용 하 고 있는지 확인 합니다.
- 2 노드 시나리오와 ClusterEnforcedAntiAffinity에서 한 노드가 다운 된 경우 두 그룹은 실행 되지 않습니다.  

- 그룹에 기본 설정 소유자를 사용 하는 것은 3 개 이상의 노드 클러스터에서 선호도 방지와 결합 될 수 있습니다.
- AntiAffinityClassNames 및 ClusterEnforcedAntiAffinity 설정은 리소스 재활용 후에만 수행 됩니다. 핵. 설정할 수 있지만 두 그룹이 설정 시 동일한 노드에서 온라인 상태 이면 둘 다 온라인 상태로 유지 됩니다.
