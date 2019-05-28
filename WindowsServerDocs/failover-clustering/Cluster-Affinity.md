---
title: 클러스터 선호도
ms.prod: windows-server-threshold
ms.manager: eldenc
ms.technology: failover-clustering
ms.topic: article
author: johnmarlin-msft
ms.date: 03/07/2019
description: 이 문서에서는 장애 조치 클러스터 선호도 및 antiAffinity 수준 설명
ms.openlocfilehash: a38d53f6aed1ca634d41822f4486779f6d279ec0
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476062"
---
# <a name="cluster-affinity"></a>클러스터 선호도

> 적용 대상: Windows Server 2019, Windows Server 2016

장애 조치 클러스터 노드 간에 이동 하 고 실행할 수 있는 다양 한 역할을 포함할 수 있습니다.  경우 특정 역할 (예: 가상 머신, 리소스 그룹, 등) 동일한 노드에서 실행 되지 해야 하는 경우가 있습니다.  리소스 사용량, 메모리 사용량 등 때문일 수 있습니다.  예를 들어, 메모리 및 CPU를 많이 사용 하는 두 개의 가상 컴퓨터가 및 가상 컴퓨터 중 하나 또는 모두 두 개의 가상 머신을 동일한 노드에서 실행 하는 경우 성능 영향 문제가 있을 수 있습니다.  이 문서에서는 설명 하는 클러스터 antiaffinity 수준 및 방법을 사용할 수 있습니다.

## <a name="what-is-affinity-and-antiaffinity"></a>선호도 및 AntiAffinity 무엇 인가요?

선호도 (i, e, 가상 머신, 리소스 그룹, 등)에 함께 유지 되도록 두 개 이상의 역할 간의 관계를 설정 하는 설정 하는 규칙.  AntiAffinity 동일 하지만 시도 하 고 서로 다른 지정된 된 역할을 유지 하는 데 사용 됩니다.  장애 조치 클러스터는 해당 역할에 대 한 AntiAffinity를 사용합니다.  구체적으로 [AntiAffinityClassNames](https://docs.microsoft.com/previous-versions/windows/desktop/mscs/groups-antiaffinityclassnames) 동일한 노드에서 실행 되지 않는 역할에 정의 된 매개 변수입니다.  

## <a name="antiaffinityclassnames"></a>AntiAffinityClassnames

AntiAffinityClassNames 매개 변수는 그룹의 속성을 보면 및 기본적으로 비어 있습니다.  아래 예제에서 Group1 및 Group2를 반드시 동일한 노드에서 실행에서 분리 해야 합니다.  속성을 보려면 PowerShell 명령 및 결과 다음과 같습니다.

    PS> Get-ClusterGroup Group1 | fl AntiAffinityClassNames
    AntiAffinityClassNames : {}

    PS> Get-ClusterGroup Group2 | fl AntiAffinityClassNames
    AntiAffinityClassNames : {}

기본적으로 이러한 역할 수를 함께 실행 또는 떨어져 AntiAffinityClassNames 정의 되지 않습니다 이후.  목표 구분할 수 있도록 하는 것입니다.  동일 하도록 하기만 하면, AntiAffinityClassNames에 대 한 값을 원하는 수 있도록 수 있습니다.  Group1 및 Group2는 도메인 컨트롤러 가상 머신에서 실행 되 고 이러한 가장 서비스 될 다른 노드에서 실행 되 가정해 보겠습니다.  이러한 도메인 컨트롤러와 되므로 클래스 이름에 대 한 DC 사용 됩니다.  값을 설정 하려면 PowerShell 명령 및 결과 다음과 같습니다.

    PS> $AntiAffinity = New-Object System.Collections.Specialized.StringCollection
    PS> $AntiAffinity.Add("DC")
    PS> (Get-ClusterGroup -Name "Group1").AntiAffinityClassNames = $AntiAffinity
    PS> (Get-ClusterGroup -Name "Group2").AntiAffinityClassNames = $AntiAffinity

    PS> Get-ClusterGroup "Group1" | fl AntiAffinityClassNames
    AntiAffinityClassNames : {DC}

    PS> Get-ClusterGroup "Group2" | fl AntiAffinityClassNames
    AntiAffinityClassNames : {DC}

시간을 설정 했으므로 장애 조치 클러스터링 떨어져 유지 하려고 합니다.  

AntiAffinityClassName "soft" 블록입니다.  즉를 유지 하기 위해 시도 않지만 수 없는 경우 여전히 허용 됩니다 동일한 노드에서 실행 되도록 합니다.  예를 들어 그룹 2 개 노드 장애 조치 클러스터에서 실행 됩니다.  하나의 노드를 유지 관리를 위해 중단 해야 하는 경우 두 그룹은 실행 되어 동일한 노드에서 의미 합니다.  이 경우이 사용할 수 있는 것입니다.  가장 이상적인 되지 않을 수 있지만 두 virtial 컴퓨터 적절 한 성능 범위 내에서 계속 실행 됩니다.

## <a name="i-need-more"></a>자세한 내용은 함

언급 했 듯이 AntiAffinityClassNames는 소프트 블록.  하지만 하드 블록 필요한 경우에 어떨까요?  에 가상 컴퓨터를 실행할 수 없습니다 동일한 노드 이 고, 그렇지 성능에 영향을 발생 하 고 일부 서비스가 중단 될 수 있는 문제가 발생 됩니다.

이러한 경우 ClusterEnforcedAntiAffinity의 추가 클러스터 속성을 있습니다.  이 antiaffinity 수준이 못합니다 희생이 따르더라도 동일한 AntiAffinityClassNames 값 동일한 노드에서 실행 합니다.

속성 및 값을 보려면 PowerShell 명령 (및 결과) 다음과 같습니다.

    PS> Get-Cluster | fl ClusterEnforcedAntiAffinity
    ClusterEnforcedAntiAffinity : 0

"0" 이면이 불가능 하 고 적용할 필요가 값입니다.  "1"의 값 사용 하도록 설정 하 고 하드 블록입니다.  이 하드 블록을 사용 하도록 설정 하는 명령 (및 결과):

    PS> (Get-Cluster).ClusterEnforcedAntiAffinity = 1
    ClusterEnforcedAntiAffinity : 1

두 가지 모두를 설정 하면 그룹 함께 온라인 상태로 차단 됩니다.  동일한 노드에 해당 하는 경우 표시 되는 것에서 장애 조치 클러스터 관리자입니다.

![클러스터 선호도](media\Cluster-Affinity\Cluster-Affinity-1.png)

그룹의 PowerShell 목록에이 볼 수 있습니다.

    PS> Get-ClusterGroup

    Name       State
    ----       -----
    Group1     Offline(Anti-Affinity Conflict)
    Group2     Online

## <a name="additional-comments"></a>추가 설명

- 필요에 따라 적절 한 AntiAffinity 설정을 사용 하는 것을 확인 합니다.
- 에 유의 ClusterEnforcedAntiAffinity, 2-노드 시나리오에서 경우 한 노드가 다운 된 경우 두 그룹도 실행 되지 않습니다.  

- 기본 설정 소유자 그룹에서 사용할 3 개 이상의 노드 클러스터에서 AntiAffinity를 사용 하 여 결합할 수 있습니다.
- AntiAffinityClassNames 및 ClusterEnforcedAntiAffinity 설정의 리소스를 재생 한 후만 수행 됩니다. I.E. 두 그룹 경우 동일한 노드에서 온라인으로 설정 된 경우 둘 다 계속 온라인 상태로 유지 되지만, 값을 설정할 수 있습니다.



