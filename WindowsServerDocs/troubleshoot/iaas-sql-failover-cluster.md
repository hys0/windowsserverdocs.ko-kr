---
title: 장애 조치 기준 네트워크 임계값 조정
description: 이 문서에서는 장애 조치 (failover) 클러스터 네트워크의 임계값을 조정 하는 솔루션을 소개 합니다.
ms.prod: windows-server
ms.technology: server-general
ms.date: 05/28/2020
author: Deland-Han
ms.author: delhan
ms.openlocfilehash: c0e2f0309049f0271a223c2a23012eb2efa8d843
ms.sourcegitcommit: ef089864980a1d4793a35cbf4cbdd02ce1962054
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/28/2020
ms.locfileid: "84150171"
---
# <a name="iaas-with-sql-alwayson---tuning-failover-cluster-network-thresholds"></a>SQL AlwaysOn을 사용한 IaaS - 장애 조치(failover) 클러스터 네트워크 임계값 조정

이 문서에서는 장애 조치 (failover) 클러스터 네트워크의 임계값을 조정 하는 솔루션을 소개 합니다.

## <a name="symptom"></a>증상

AlwaysOn SQL Server를 사용 하 여 IaaS에서 Windows 장애 조치 (Failover) 클러스터 노드를 실행 하는 경우 클러스터 설정을 보다 낮은 모니터링 상태로 변경 하는 것이 좋습니다. 기본 클러스터 설정은 제한적 이며 불필요 한 중단을 유발할 수 있습니다. 기본 설정은 온-프레미스 네트워크에서 매우 조정 되도록 설계 되었으며, Windows Azure (IaaS)와 같은 다중 테 넌 트 환경에 의해 발생 하는 발생 한 대기 시간의 가능성을 고려 하지 않습니다.

Windows Server 장애 조치 (Failover) 클러스터링은 Windows 클러스터에 있는 노드의 네트워크 연결 및 상태를 지속적으로 모니터링 합니다.  네트워크를 통해 노드에 연결할 수 없는 경우 애플리케이션 및 서비스를 복구하고 클러스터의 다른 노드에서 온라인 상태로 전환하기 위해 복구 작업이 수행됩니다. 클러스터 노드 간 통신 대기 시간으로 인해 다음과 같은 오류가 발생할 수 있습니다.  

> 오류 1135 (시스템 이벤트 로그)

클러스터 노드 **Node1** 이 활성 장애 조치 (failover) 클러스터 멤버 자격에서 제거 되었습니다. 이 노드의 클러스터 서비스 중지 되었을 수 있습니다. 이는 노드가 장애 조치 (failover) 클러스터의 다른 활성 노드와 통신이 끊어진 경우에도 발생할 수 있습니다. 구성 유효성 검사 마법사를 실행 하 여 네트워크 구성을 확인 합니다. 상태가 지속 되 면이 노드의 네트워크 어댑터와 관련 된 하드웨어 또는 소프트웨어 오류를 확인 합니다. 또한 허브, 스위치 또는 브리지와 같이 노드가 연결 된 다른 모든 네트워크 구성 요소에서 오류를 확인 합니다.

클러스터 로그 예:

```console
0000ab34.00004e64::2014/06/10-07:54:34.099 DBG   [NETFTAPI] Signaled NetftRemoteUnreachable event, local address 10.xx.x.xxx:3343 remote address 10.x.xx.xx:3343
0000ab34.00004b38::2014/06/10-07:54:34.099 INFO  [IM] got event: Remote endpoint 10.xx.xx.xxx:~3343~ unreachable from 10.xx.x.xx:~3343~
0000ab34.00004b38::2014/06/10-07:54:34.099 INFO  [IM] Marking Route from 10.xxx.xxx.xxxx:~3343~ to 10.xxx.xx.xxxx:~3343~ as down
0000ab34.00004b38::2014/06/10-07:54:34.099 INFO  [NDP] Checking to see if all routes for route (virtual) local fexx::xxx:5dxx:xxxx:3xxx:~0~ to remote xxx::cxxx:xxxd:xxx:dxxx:~0~ are down
0000ab34.00004b38::2014/06/10-07:54:34.099 INFO  [NDP] All routes for route (virtual) local fxxx::xxxx:5xxx:xxxx:3xxx:~0~ to remote fexx::xxxx:xxxx:xxxx:xxxx:~0~ are down
0000ab34.00007328::2014/06/10-07:54:34.099 INFO  [CORE] Node 8: executing node 12 failed handlers on a dedicated thread
0000ab34.00007328::2014/06/10-07:54:34.099 INFO  [NODE] Node 8: Cleaning up connections for n12.
0000ab34.00007328::2014/06/10-07:54:34.099 INFO  [Nodename] Clearing 0 unsent and 15 unacknowledged messages.
0000ab34.00007328::2014/06/10-07:54:34.099 INFO  [NODE] Node 8: n12 node object is closing its connections
0000ab34.00008b68::2014/06/10-07:54:34.099 INFO  [DCM] HandleNetftRemoteRouteChange
0000ab34.00004b38::2014/06/10-07:54:34.099 INFO  [IM] Route history 1: Old: 05.936, Message: Response, Route sequence: 150415, Received sequence: 150415, Heartbeats counter/threshold: 5/5, Error: Success, NtStatus: 0 Timestamp: 2014/06/10-07:54:28.000, Ticks since last sending: 4
0000ab34.00007328::2014/06/10-07:54:34.099 INFO  [NODE] Node 8: closing n12 node object channels
0000ab34.00004b38::2014/06/10-07:54:34.099 INFO  [IM] Route history 2: Old: 06.434, Message: Request, Route sequence: 150414, Received sequence: 150402, Heartbeats counter/threshold: 5/5, Error: Success, NtStatus: 0 Timestamp: 2014/06/10-07:54:27.665, Ticks since last sending: 36
0000ab34.0000a8ac::2014/06/10-07:54:34.099 INFO  [DCM] HandleRequest: dcm/netftRouteChange
0000ab34.00004b38::2014/06/10-07:54:34.099 INFO  [IM] Route history 3: Old: 06.934, Message: Response, Route sequence: 150414, Received sequence: 150414, Heartbeats counter/threshold: 5/5, Error: Success, NtStatus: 0 Timestamp: 2014/06/10-07:54:27.165, Ticks since last sending: 4
0000ab34.00004b38::2014/06/10-07:54:34.099 INFO  [IM] Route history 4: Old: 07.434, Message: Request, Route sequence: 150413, Received sequence: 150401, Heartbeats counter/threshold: 5/5, Error: Success, NtStatus: 0 Timestamp: 2014/06/10-07:54:26.664, Ticks since last sending: 36
```

```console
0000ab34.00007328::2014/06/10-07:54:34.100 INFO    <realLocal>10.xxx.xx.xxx:~3343~</realLocal>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO    <realRemote>10.xxx.xx.xxx:~3343~</realRemote>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO    <virtualLocal>fexx::xxxx:xxxx:xxxx:xxxx:~0~</virtualLocal>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO    <virtualRemote>fexx::xxxx:xxxx:xxxx:xxxx:~0~</virtualRemote>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO    <Delay>1000</Delay>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO    <Threshold>5</Threshold>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO    <Priority>140481</Priority>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO    <Attributes>2147483649</Attributes>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO  </struct mscs::FaultTolerantRoute>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO   removed
```

```console
0000ab34.0000a7c0::2014/06/10-07:54:38.433 ERR   [QUORUM] Node 8: Lost quorum (3 4 5 6 7 8)
0000ab34.0000a7c0::2014/06/10-07:54:38.433 ERR   [QUORUM] Node 8: goingAway: 0, core.IsServiceShutdown: 0
0000ab34.0000a7c0::2014/06/10-07:54:38.433 ERR   lost quorum (status = 5925)
```

## <a name="cause"></a>원인

클러스터의 연결 상태를 구성 하는 데 사용 되는 두 가지 설정이 있습니다.

**Delay** – 노드 간에 클러스터 하트 비트를 전송 하는 빈도를 정의 합니다.  지연 시간은 다음 하트 비트가 전송 되기 전의 시간 (초)입니다.  동일한 클러스터 내에서 동일한 서브넷의 노드와 서로 다른 서브넷에 있는 노드 간에는 서로 다른 지연이 있을 수 있습니다.

**임계값** – 클러스터가 복구 작업을 수행 하기 전에 누락 된 하트 비트 수를 정의 합니다.  임계값은 하트 비트 수입니다.  동일한 클러스터 내에서 동일한 서브넷에 있고 서로 다른 서브넷에 있는 노드 간에는 서로 다른 임계값이 있을 수 있습니다.

기본적으로 Windows Server 2016은 **SameSubnetThreshold** 을 10으로 설정 하 고 **SameSubnetDelay** 를 1000 밀리초로 설정 합니다. 예를 들어 10 초 동안 연결 모니터링이 실패 하면 장애 조치 (failover) 임계값에 도달 하 여 클러스터 멤버 자격에서 제거 되는 노드를 연결할 수 없습니다. 그러면 리소스가 클러스터에서 사용 가능한 다른 노드로 이동 합니다. 클러스터 오류 1135 (위)를 포함 하 여 클러스터 오류가 보고 됩니다.

## <a name="resolution"></a>해결 방법

IaaS 환경에서 클러스터 네트워크 구성 설정을 완화 합니다.

### <a name="steps-to-verify-current-configuration"></a>현재 구성을 확인 하는 단계

현재 클러스터 네트워크 구성 설정에서 get cluster 명령을 사용 합니다.

```powershell
C:\Windows\system32> get-cluster | fl *subnet*
```

각 지원 OS에 대 한 기본값, 최소값, 최대값 및 권장 값

|   |OS|최소값|최대값|기본값|권장|
|---|---|---|---|---|---|
|CrossSubnetThreshold|2008 R2|3|20|5|20|
|교차 서브넷 임계값|2012|3|120|5|20|
|교차 서브넷 임계값|2012 R2|3|120|5|20|
|교차 서브넷 임계값|2016|3|120|20|20|
|SameSubnet 임계값|2008 R2|3|10|5|10|
|SameSubnet 임계값|2012|3|120|5|10
|SameSubnet 임계값|2012 R2|3|120|5|10|
|SameSubnetThreshold|2016|3|120|10|10|
|||||||

임계값에 대 한 값은 다음 문서에 설명 된 대로 배포 범위에 대 한 현재 권장 사항을 반영 합니다.

[Windows Server 2012 r 2에서 장애 조치 (failover) 클러스터 네트워크 임계값 미세 조정](https://support.microsoft.com/en-us/help/3153887/fine-tuning-failover-cluster-network-thresholds-in-windows-server-2012)

**임계값** 은 클러스터에서 복구 작업을 수행 하기 전에 누락 된 하트 비트 수를 정의 합니다.  임계값은 하트 비트 수입니다.  동일한 클러스터 내에서 동일한 서브넷의 노드와 서로 다른 서브넷에 있는 노드 간에는 서로 다른 임계값이 있을 수 있습니다.

## <a name="recommendations-for-changing-to-more-relaxed-settings-for-multi-tenant-environments-like-azure-iaas"></a>Azure (IaaS)와 같은 다중 테 넌 트 환경에 대 한 보다 완화 되는 설정 변경에 대 한 권장 사항

> [!NOTE]
> 클러스터 네트워크 구성 설정을 조정 하 여 클러스터 환경의 복원 력을 높이면 가동 중지 시간이 증가할 수 있습니다. 자세한 내용은 [장애 조치 (Failover) 클러스터 네트워크 임계값 조정](https://techcommunity.microsoft.com/t5/failover-clustering/tuning-failover-cluster-network-thresholds/ba-p/371834)을 참조 하세요.

1. 더 완화 되는 설정으로 수정:

    > [!NOTE]
    > 클러스터 임계값을 변경 하면 즉시 적용 되며 클러스터 나 리소스를 다시 시작할 필요가 없습니다.

    AlwaysOn 가용성 그룹의 동일한 서브넷 및 지역 간 배포 모두에 대해 다음 설정을 사용 하는 것이 좋습니다.

    ```powershell
    C:\Windows\system32> (get-cluster).SameSubnetThreshold = 20
    ```

    ```powershell
    C:\Windows\system32> (get-cluster).CrossSubnetThreshold = 20
    ```

2. 변경 내용을 확인 합니다.

    ```powershell
    C:\Windows\system32> get-cluster | fl *subnet*
    ```

    :::image type="content" source="media/iaas-sql-failover-cluster/cmd.png" alt-text="cmd" border="false":::

## <a name="references"></a>참조

Windows 클러스터 네트워크 구성 설정을 조정 하는 방법에 대 한 자세한 내용은 [장애 조치 (Failover) 클러스터 네트워크 임계값 조정](https://techcommunity.microsoft.com/t5/failover-clustering/tuning-failover-cluster-network-thresholds/ba-p/371834)을 참조 하세요.

Cluster.exe를 사용 하 여 Windows 클러스터 네트워크 구성 설정을 조정 하는 방법에 대 한 자세한 내용은 [장애 조치 (Failover) 클러스터용 클러스터 네트워크를 구성 하는 방법](/previous-versions/office/exchange-server-2007/bb690953(v=exchg.80)?redirectedfrom=MSDN)을 참조 하세요.
