---
title: RAS 게이트웨이 GRE 터널 처리량 및 성능
description: IT (정보 기술) 전문가를 위한이 항목에서는 RAS Gateway GRE (제네릭 라우팅 캡슐화) 터널에 대 한 처리량 성능 정보를 제공 합니다.
manager: brianlic
ms.prod: windows-server
ms.date: ''
ms.technology: networking-ras
ms.topic: article
ms.assetid: c051b2ec-de0f-49d1-82b9-5742b259cd7c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 79a6e822c3ff36f789a7a08b8cd56163014185a4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404690"
---
# <a name="ras-gateway-gre-tunnel-throughput-and-performance"></a>RAS 게이트웨이 GRE 터널 처리량 및 성능

>적용 대상: Windows Server \(반기 채널\)

이 항목을 사용 하 여 원격 액세스 서버 \(원격 액세스 서버에 대 한 자세한 내용은 Windows Server 버전 1709의 GRE\) 터널 성능 \(네트워크에서 정의 되지 않은 네트워킹 \(SDN\) 기반 테스트 환경에서\) 합니다.

RAS 게이트웨이는 단일 테 넌 트 모드 또는 다중 테 넌 트 모드에서 사용할 수 있는 소프트웨어 라우터 및 게이트웨이입니다. 이 항목에서는 장애 조치 클러스터링을 사용 하는 단일 테 넌 트 모드, 고가용성 구성에 대해 설명 합니다. 이 항목에 제공 된 GRE 터널 성능 통계는 singele 테 넌 트 및 다중 테 넌 트 모드의 RAS 게이트웨이에 유효 합니다.

>[!NOTE]
>장애 조치 (Failover) 클러스터링은 여러 서버를 장애 조치 (Failover) 클러스터로 그룹화 할 수 있는 Windows Server 기능입니다. 자세한 내용은 [장애 조치 (Failover) 클러스터링](../../../failover-clustering/failover-clustering-overview.md) 을 참조 하세요.

단일 테 넌 트 모드를 사용 하면 모든 규모의 조직이 게이트웨이를 외부 또는 인터넷\-\(연결 된 VPN\) 서버로 배포할 수 있습니다. 단일 테 넌 트 모드에서는 실제 서버 또는 가상 컴퓨터 \(VM\)에 RAS 게이트웨이를 배포할 수 있습니다. 이 항목에서는 장애 조치 (failover) 클러스터에 구성 된 두 개의 Virtual Machines \(Vm\)에서 RAS 게이트웨이 배포에 대해 설명 합니다.

>[!IMPORTANT]
>GRE 터널은 캡슐화를 제공 하지만 암호화는 제공 하지 않으므로 GRE로 구성 된 RAS 게이트웨이를 인터넷에 지 게이트웨이로 사용 하면 안 됩니다. GRE 터널을 사용한 RAS 게이트웨이의 최상의 사용에 대 한 자세한 내용은 [Windows Server의 GRE 터널링](gre-tunneling-windows-server.md)을 참조 하세요.

GRE는 인터넷 프로토콜 인터네트워크를 통해\-지점 링크에\-가상 지점 내에서 다양 한 네트워크 계층 프로토콜을 캡슐화 할 수 있는 경량 터널링 프로토콜입니다. Microsoft GRE 구현은 IPv4 및 IPv6을 모두 캡슐화 합니다.

자세한 내용은 [ras](https://docs.microsoft.com/windows-server/remote/remote-access/ras-gateway/ras-gateway#bkmk_deploy)gateway 항목에서 **Ras gateway 배포 시나리오** 섹션을 참조 하세요. 

다음 그림에 표시 된이 테스트 시나리오에서 측정 되는 트래픽 흐름은 조직 인트라넷 2에서 조직 인트라넷 1로 이동 합니다. 테 넌 트 워크 로드 Vm은 RAS Gateway를 사용 하 여 인트라넷 2에서 인트라넷 1로 네트워크 트래픽을 전송 합니다.

![RAS 게이트웨이 GRE 터널 테스트 시나리오 개요](../../media/GRE-Tunnel-Perf/Gre-Infrastructure.jpg)

## <a name="test-environment-configuration"></a>테스트 환경 구성

이 섹션에서는 테스트 환경 및 RAS 게이트웨이 구성에 대 한 정보를 제공 합니다.

테스트 환경에서 RAS 게이트웨이 Vm은 고가용성을 위해 장애 조치 (failover) 클러스터의\-Hyper-v 호스트에 배포 됩니다.

### <a name="hyper-v-host-configuration"></a>하이퍼\-V 호스트 구성

두 개의 하이퍼\-V 호스트는 다음과 같은 방식으로 테스트 시나리오를 지원 하도록 구성 됩니다. 

- 두 개의 이중\-홈 물리적 컴퓨터는 Windows Server, 버전 1709을 사용 하 여 구성 됩니다.
- 두 서버 각각의 실제 네트워크 어댑터 두 개는 서로 다른 서브 네트워크에 연결 되어 있습니다. 둘 다 조직 인트라넷의 서브넷을 나타냅니다. 네트워크와 지원 하드웨어는 모두 10gbps의 용량이 있습니다.
- 물리적 서버의 하이퍼스레딩을 사용 하지 않도록 설정 되었습니다. 이는 실제 Nic의 최대 처리량을 제공 합니다.
- 하이퍼\-V 서버 역할은 두 서버에 모두 설치 되 고, 각각의 실제 네트워크 어댑터에 대해 하나씩, 두 개의 외부\-Hyper-v 가상 스위치를 사용 하 여 구성 됩니다.
- 두 서버는 동일한 인트라넷에 연결 되므로 서버는 서로 통신할 수 있습니다.
- 하이퍼\-V 호스트는 인트라넷 네트워크를 통해 장애 조치 (failover) 클러스터에 구성 됩니다. 

>[!NOTE]
>자세한 내용은 참조 [Hyper-v 가상 스위치](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/hyper-v-virtual-switch)합니다.

### <a name="vm-configuration"></a>VM 구성

두 Vm은 다음과 같은 방식으로 테스트 시나리오를 지원 하도록 구성 됩니다.

- 각 서버에서 Windows Server를 실행 하는 VM (버전 1709)을 설치 합니다. 각 VM은 10 개 코어와 8gb RAM으로 구성 됩니다.
- 또한 각 VM은 두 개의 가상 네트워크 어댑터를 사용 하 여 구성 됩니다. 한 가상 네트워크 어댑터는 인트라넷 1 가상 스위치에 연결 되 고 다른 가상 네트워크 어댑터는 인트라넷 2 가상 스위치에 연결 됩니다.
- 각 VM에는 RAS 게이트웨이가 설치 되 고 GRE\-기반 VPN 서버로 구성 됩니다.
- 게이트웨이 Vm은 장애 조치 (failover) 클러스터에 구성 됩니다. 클러스터 된 경우 한 VM은 활성 상태이 고 다른 VM은 수동입니다.

### <a name="workload-hyper-v-hosts-and-vms"></a>워크 로드 하이퍼\-V 호스트 및 Vm

이 테스트를 위해 두 개의 워크 로드 하이퍼\-V 호스트가 인트라넷에 설치 되어 있고 각 호스트에 하나의 VM이 설치 되어 있습니다. 사용자 고유의 테스트 환경에서이 테스트를 복제 하는 경우 용도에 맞게 적절 한 수의 워크 로드 서버와 Vm을 설치할 수 있습니다.

- 워크 로드 하이퍼\-V 호스트에는 조직 인트라넷에 연결 된 실제 네트워크 어댑터가 하나 이상 설치 되어 있습니다.
- \-Hyper-v 가상 스위치에서 각 호스트에 하나의 가상 스위치가 생성 됩니다. 외부 스위치는 인트라넷에 연결 된 하나의 네트워크 어댑터에 바인딩되어 있습니다.
- 워크 로드 Vm은 2gb RAM 및 2 코어를 사용 하 여 구성 됩니다.
- 워크 로드 Vm에는 각각 인트라넷 가상 스위치에 연결 된 가상 네트워크 어댑터가 하나씩 있습니다.

### <a name="traffic-generator-tool"></a>트래픽 생성기 도구

이 테스트에 사용 되는 트래픽 생성기 도구는 ctsTraffic 도구입니다. 이 도구의 Git 리포지토리는 [https://github.com/Microsoft/ctsTraffic](https://github.com/Microsoft/ctsTraffic)에 있습니다.

## <a name="ras-gateway-performance"></a>RAS 게이트웨이 성능

이 섹션의 그림에서는 여러 TCP 연결이 있는 GRE 터널 처리량의 작업 관리자 표시를 보여 줍니다.

GRE RAS 게이트웨이로 구성 된 다중\-코어 Vm에서 최대 2.0 Gbps의 처리량을 달성할 수 있습니다.

### <a name="gre-tunnel-performance-with-multiple-tcp-sessions"></a>여러 TCP 세션의 GRE 터널 성능

여러 TCP 세션에서 CPU 사용률이 100%에 도달 하 고 GRE 터널의 최대 처리량은 2.0 Gbps입니다.

다음 그림은 두 RAS 게이트웨이 Vm의 CPU 사용률을 보여 줍니다. 활성 VM 인 RAS 게이트웨이 VM #1은 왼쪽에 있고, 수동 VM, RAS 게이트웨이 VM #2는 오른쪽에 있습니다.

![작업 관리자의 게이트웨이 VM CPU 사용률](../../media/GRE-Tunnel-Perf/Gre-Tunnel-01.jpg)

다음 그림에서는 RAS 게이트웨이 Vm의 이더넷 네트워크 처리량을 보여 줍니다. 활성 VM 인 RAS 게이트웨이 VM #1은 왼쪽에 있고, 수동 VM, RAS 게이트웨이 VM #2는 오른쪽에 있습니다.

![작업 관리자의 게이트웨이 VM 이더넷 네트워크 처리량](../../media/GRE-Tunnel-Perf/Gre-Tunnel-02.jpg)


### <a name="gre-tunnel-performance-with-one-tcp-connection"></a>TCP 연결이 하나인 GRE 터널 성능

테스트 구성이 여러 TCP 세션에서 단일 TCP 세션으로 변경 되 면 하나의 CPU 코어만 RAS 게이트웨이 Vm의 최대 용량에 도달 합니다.

GRE 터널의 최대 처리량은 400-500 Mbps 사이입니다.

다음 그림은 두 RAS 게이트웨이 Vm의 CPU 사용률을 보여 줍니다. 활성 VM 인 RAS 게이트웨이 VM #1은 왼쪽에 있고, 수동 VM, RAS 게이트웨이 VM #2는 오른쪽에 있습니다.

![작업 관리자의 게이트웨이 VM CPU 사용률](../../media/GRE-Tunnel-Perf/Gre-Tunnel-03.jpg)


다음 그림에서는 RAS 게이트웨이 Vm의 이더넷 네트워크 처리량을 보여 줍니다. 활성 VM 인 RAS 게이트웨이 VM #1은 왼쪽에 있고, 수동 VM, RAS 게이트웨이 VM #2는 오른쪽에 있습니다.

![작업 관리자의 게이트웨이 VM 이더넷 네트워크 처리량](../../media/GRE-Tunnel-Perf/Gre-Tunnel-04.jpg)

RAS 게이트웨이 성능에 대 한 자세한 내용은 [소프트웨어 정의 네트워크에서 Hnv 게이트웨이 성능 튜닝](https://docs.microsoft.com/windows-server/administration/performance-tuning/subsystem/software-defined-networking/hnv-gateway-performance)을 참조 하세요.