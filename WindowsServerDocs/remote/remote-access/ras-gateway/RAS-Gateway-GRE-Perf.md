---
title: RAS 게이트웨이 GRE 터널 처리량 및 성능
description: IT (정보 기술) 전문가 위한이 항목에서는 RAS 게이트웨이 캡슐화 GRE (Generic Routing) 터널에 대 한 처리량 성능 정보를 제공 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.date: ''
ms.technology: networking-ras
ms.topic: article
ms.assetid: c051b2ec-de0f-49d1-82b9-5742b259cd7c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 73ae4e573d926f4a77b076c880c1d74ed69f032d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880764"
---
# <a name="ras-gateway-gre-tunnel-throughput-and-performance"></a>RAS 게이트웨이 GRE 터널 처리량 및 성능

>적용 대상: Windows Server \(반기 채널\)

원격 액세스 서버에 대해 자세히 알아보려면이 항목을 사용할 수 있습니다 \(RAS\) 게이트웨이 Generic Routing Encapsulation \(GRE\) Windows Server 버전 1709에는 비-소프트웨어 정의 네트워킹 성능적터널링\( SDN\) 기반된 테스트 환경입니다.

RAS 게이트웨이 소프트웨어 라우터 및 단일 테 넌 트 모드 또는 다중 테 넌 트 모드에서 사용할 수 있는 게이트웨이. 이 항목에서는 단일 테 넌 트 모드, 장애 조치 클러스터링과 고가용성 구성을 설명합니다. 이 항목에 표시 되는 GRE 터널 성능 통계 singele 테 넌 트와 다중 테 넌 트 모드에서 RAS 게이트웨이에 대 한 유효있지 않습니다.

>[!NOTE]
>장애 조치 클러스터링은 여러 서버가 하나의 내결함성 클러스터로 그룹화 할 수 있도록 하는 Windows Server 기능입니다. 자세한 내용은 참조 하세요. [장애 조치 클러스터링](../../../failover-clustering/failover-clustering-overview.md)

단일 테 넌 트 모드에서는 외부에서 또는 인터넷으로 게이트웨이 배포 하려면 모든 규모의 조직\-가장자리 가상 개인 네트워크 연결 \(VPN\) 서버. 단일 테 넌 트 모드에서 RAS 게이트웨이 실제 서버 또는 가상 컴퓨터에 배포할 수 있습니다 \(VM\)합니다. 이 항목에서는 두 개의 가상 머신에 RAS 게이트웨이 배포를 설명 \(Vm\) 장애 조치 클러스터에 구성 된 합니다.

>[!IMPORTANT]
>GRE 터널 캡슐화 하지만 하지 암호화를 제공 하므로 인터넷 edge 게이트웨이로 GRE를 사용 하 여 구성 하는 RAS 게이트웨이 사용 하지 마십시오. GRE 터널을 사용 하 여 RAS Gateway에 대 한 가장 대 한 자세한 내용은 참조 하세요 [Windows Server에서 GRE 터널링](gre-tunneling-windows-server.md)합니다.

GRE는 다양 한 네트워크 레이어 프로토콜이 가상 지점 내에서 캡슐화 할 수 있는 프로토콜을 터널링 하는 경량\-에\-인터넷 프로토콜 네트워크를 통해 링크를 가리킵니다. Microsoft GRE 구현에는 IPv4 및 IPv6 모두 캡슐화합니다.

자세한 내용은 섹션을 참조 하세요 **RAS 게이트웨이 배포 시나리오** 항목에서 [RAS 게이트웨이](https://docs.microsoft.com/windows-server/remote/remote-access/ras-gateway/ras-gateway#bkmk_deploy)합니다. 

다음 그림에 표시 되어,이 테스트 시나리오에서 측정 되는 트래픽 흐름 아웃 조직 인트라넷 2에서 조직 인트라넷 1로 이동 합니다. 테 넌 트 워크 로드 Vm 네트워크 트래픽을 인트라넷 2에서 인트라넷 1 RAS 게이트웨이 사용 하 여 보냅니다.

![RAS 게이트웨이 GRE 터널 테스트 시나리오 개요](../../media/GRE-Tunnel-Perf/Gre-Infrastructure.jpg)

## <a name="test-environment-configuration"></a>테스트 환경 구성

이 섹션에서는 테스트 환경 및 RAS 게이트웨이 구성에 대 한 정보를 제공 합니다.

테스트 환경에 RAS 게이트웨이 Vm 하이퍼에 배포 됩니다\-고가용성에 대 한 호스트를 장애 조치에서 클러스터입니다.

### <a name="hyper-v-host-configuration"></a>하이퍼\-V 호스트 구성

두 개의 하이퍼\-호스트는 다음과 같은 방법으로 테스트 시나리오를 지원 하도록 구성 됩니다. 

- 두 개의 듀얼\-홈된 물리적 컴퓨터를 Windows Server 버전 1709 사용 하 여 구성 됩니다
- 두 개의 실제 네트워크 어댑터 두 서버의 각 조직의 인트라넷 서브넷 둘 다 나타냅니다-다른 서브 네트워크에 연결 됩니다. 네트워크 및 지원 하드웨어 10gbps 용량이 둡니다.
- 물리적 서버에서 하이퍼 스레딩은 사용 하지 않도록 설정 합니다. 이 실제 Nic의 최대 처리량을 제공합니다.
- Hyper\-V 서버 역할 두 서버에 설치 되어 구성 된 두 개의 외부 하이퍼\-각 실제 네트워크 어댑터에 대 한 가상 스위치, V.
- 두 서버가 동일한 인트라넷에 연결 되어 있으므로 서버는 서로 통신할 수 있습니다.
- Hyper\-호스트 인트라넷 네트워크를 통해 장애 조치 클러스터에서 구성 됩니다. 

>[!NOTE]
>자세한 내용은 참조 [Hyper-v 가상 스위치](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/hyper-v-virtual-switch)합니다.

### <a name="vm-configuration"></a>VM 구성

두 Vm은 다음과 같은 방법으로 테스트 시나리오를 지원 하도록 구성 됩니다.

- 즉 VM은 설치 된 각 서버에서 Windows Server 버전 1709 실행 합니다. 각 VM은 10 개 코어와 8GB RAM 구성 됩니다.
- 또한 각 VM은 두 가상 네트워크 어댑터를 사용 하 여 구성 됩니다. 인트라넷 1 가상 스위치에 연결 되어 하나의 가상 네트워크 어댑터 및 다른 가상 네트워크 어댑터는 인트라넷 2 가상 스위치에 연결 합니다.
- 각 VM에 RAS 게이트웨이 설치 및 구성으로 GRE\-VPN 서버를 기반으로 합니다.
- 게이트웨이 Vm은 장애 조치 클러스터에서 구성 됩니다. 클러스터링 하는 경우 하나의 VM이 활성화 하 고 다른 VM이 수동입니다.

### <a name="workload-hyper-v-hosts-and-vms"></a>워크 로드 하이퍼\-V 호스트 및 Vm

이 테스트의 경우 두 워크 로드 하이퍼\-호스트 인트라넷에 설치 되 고 각 호스트에 설치 하는 하나의 VM에 있습니다. 자신의 테스트 환경에서이 테스트를 복제 하는 경우에 많은 워크 로드 서버 및 목적에 적합 한 Vm을 설치할 수 있습니다.

- 워크 로드 하이퍼\-호스트 조직 인트라넷에 연결 하는 설치 된 실제 네트워크 어댑터 하나가 있어야 합니다.
- 하이퍼에서\-V 가상 스위치를 각 호스트에 가상 스위치를 두 개 생성 됩니다. 스위치는 외부와 인트라넷에 연결 되는 하나의 네트워크 어댑터에 바인딩된 합니다.
- 워크 로드 Vm은 2GB RAM 및 2 개의 코어를 사용 하 여 구성 됩니다.
- 각 워크 로드 Vm 인트라넷 가상 스위치에 연결 된 가상 네트워크 어댑터가 하나 있어야 합니다.

### <a name="traffic-generator-tool"></a>트래픽 생성기 도구

이 테스트에 사용 되는 트래픽을 생성기 도구 ctsTraffic 도구가입니다. 이 도구에 대 한 Git 리포지토리에 위치한 [ https://github.com/Microsoft/ctsTraffic ](https://github.com/Microsoft/ctsTraffic)합니다.

## <a name="ras-gateway-performance"></a>RAS 게이트웨이 성능

이 섹션의 그림은 여러 TCP 연결과 GRE 터널 처리량의 작업 관리자 표시를 설명합니다.

다중에 최대 2.0 1.2gbps 이상의 처리량을 획득할 수\-GRE RAS 게이트웨이로 구성 된 Vm 코어입니다.

### <a name="gre-tunnel-performance-with-multiple-tcp-sessions"></a>여러 TCP 세션을 사용 하 여 GRE 터널 성능

여러 TCP 세션을 사용 하 여 CPU 사용률이 100%에 도달 하 고 GRE 터널에서 최대 처리량은 2.0 Gbps입니다.

다음 그림에서는 두 RAS 게이트웨이 Vm 모두에서 CPU 사용률을 보여 줍니다. 활성 VM에 RAS 게이트웨이 VM # 1에 왼쪽에 수동 VM에 RAS 게이트웨이 VM # 2에 오른쪽에 표시 됩니다.

![작업 관리자에서 게이트웨이 VM CPU 사용률](../../media/GRE-Tunnel-Perf/Gre-Tunnel-01.jpg)

다음 그림에서는 RAS 게이트웨이 Vm에 대 한 이더넷 네트워크 처리량을 보여 줍니다. 활성 VM에 RAS 게이트웨이 VM # 1에 왼쪽에 수동 VM에 RAS 게이트웨이 VM # 2에 오른쪽에 표시 됩니다.

![작업 관리자에서 게이트웨이 VM 이더넷 네트워크 처리량](../../media/GRE-Tunnel-Perf/Gre-Tunnel-02.jpg)


### <a name="gre-tunnel-performance-with-one-tcp-connection"></a>하나의 TCP 연결을 사용 하 여 GRE 터널 성능

여러 TCP 세션에서 단일 TCP 세션 변경 테스트 구성이 있는 하나의 CPU 코어에 RAS 게이트웨이 Vm에서 최대 용량에 도달 합니다.

GRE 터널에서 최대 처리량 400 ~ 500 Mbps 사이의 됩니다.

다음 그림에서는 두 RAS 게이트웨이 Vm 모두에서 CPU 사용률을 보여 줍니다. 활성 VM에 RAS 게이트웨이 VM # 1에 왼쪽에 수동 VM에 RAS 게이트웨이 VM # 2에 오른쪽에 표시 됩니다.

![작업 관리자에서 게이트웨이 VM CPU 사용률](../../media/GRE-Tunnel-Perf/Gre-Tunnel-03.jpg)


다음 그림에서는 RAS 게이트웨이 Vm에 대 한 이더넷 네트워크 처리량을 보여 줍니다. 활성 VM에 RAS 게이트웨이 VM # 1에 왼쪽에 수동 VM에 RAS 게이트웨이 VM # 2에 오른쪽에 표시 됩니다.

![작업 관리자에서 게이트웨이 VM 이더넷 네트워크 처리량](../../media/GRE-Tunnel-Perf/Gre-Tunnel-04.jpg)

RAS 게이트웨이 성능에 대 한 자세한 내용은 참조 하세요. [소프트웨어 정의 네트워크의 게이트웨이 성능 조정 HNV](https://docs.microsoft.com/windows-server/administration/performance-tuning/subsystem/software-defined-networking/hnv-gateway-performance)합니다.