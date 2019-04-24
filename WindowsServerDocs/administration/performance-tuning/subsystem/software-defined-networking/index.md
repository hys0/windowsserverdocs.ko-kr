---
title: 성능 조정 소프트웨어 정의 네트워크
description: SDN(소프트웨어 정의 네트워크) 성능 조정 가이드라인
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: grcusanz; AnPaul
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: dfb8d997c6e04381e5be0ba2c3a7ca27a851df50
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59891324"
---
# <a name="performance-tuning-software-defined-networks"></a>성능 조정 소프트웨어 정의 네트워크

Windows Server 2016의 SDN(소프트웨어 정의 네트워킹)은 네트워크 컨트롤러, Hyper-V 호스트, 소프트웨어 부하 분산 장치 게이트웨이 및 HNV 게이트웨이의 조합으로 구성됩니다.  각 구성 요소 튜닝에 대한 내용은 다음 섹션을 참조하세요.

## <a name="network-controller"></a>네트워크 컨트롤러

네트워크 컨트롤러는 Windows Server 역할입니다. SDN을 사용하도록 구성된 호스트에서 실행되고 네트워크 컨트롤러가 제어하는 Virtual Machines에서 사용하도록 설정해야 합니다.

고가용성 및 최대 성능을 위해서는 네트워크 컨트롤러 3개가 사용되는 VM이면 충분합니다.  각 VM의 크기는 [소프트웨어 정의 네트워크 인프라 계획](../../../../networking/sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md) 항목의 SDN 인프라 가상 머신 역할 요구 사항 섹션에 제공된 지침에 따라 지정해야 합니다.

### <a name="sdn-quality-of-service-qos"></a>SDN 서비스 품질 (QoS)

가상 머신 트래픽의 우선 순위가 효율적이고 공정하게 지정되도록 하려면, 워크로드 가상 머신에서 SDN QoS를 구성하는 것이 좋습니다.  SDN QoS 구성에 대한 자세한 내용은 [테넌트 VM 네트워크 어댑터에 대한 QoS 구성](../../../../networking/sdn/manage/Configure-QoS-for-Tenant-VM-Network-Adapter.md) 항목을 참조하세요.

## <a name="hyper-v-host-networking"></a>Hyper-V 호스트 네트워킹

[Hyper-V 서버 성능 조정](../../role/remote-desktop/session-hosts.md) 가이드의 [Hyper-V 네트워크 I/O 성능](#netio) 섹션에 제공된 지침은 SDN을 사용할 때 적용할 수 있지만 이 섹션의 내용은 SDN을 사용할 때 최상의 성능을 보장하기 위해 따라야 하는 추가 지침입니다.

### <a name="physical-network-adapter-nic-teaming"></a>실제 네트워크 어댑터(NIC) 팀

최상의 성능과 장애 조치 기능을 위해서는 실제 네트워크 어댑터를 팀으로 구성하는 것이 좋습니다.  SDN을 사용하는 경우 SET(스위치 포함 팀)로 팀을 만들어야 합니다.  

최적의 팀 멤버 수는 2입니다. 가상화된 트래픽이 인바운드 및 아웃바운드 방향 양쪽 모두의 팀 멤버로 분산됩니다.  팀 멤버는 2를 초과할 수 있습니다. 다만, 인바운드 트래픽은 최대 2개의 어댑터로 분산됩니다.  아웃바운드 트래픽은 동적 부하 분산의 기본값이 가상 스위치에 구성되어있는 경우 항상 모든 어댑터로 분산됩니다.


### <a name="encapsulation-offloads"></a>오프로드 캡슐화

SDN은 패킷을 캡슐화하여 네트워크를 가상화합니다.  최적의 성능을 위해서는 사용되는 캡슐화 형식에 대한 하드웨어 오프로드를 네트워크 어댑터가 지원하는 것이 중요합니다.  한 가지 캡슐화 형식이 다른 캡슐화 형식보다 성능 이점이 크지는 않습니다.  네트워크 컨트롤러를 사용할 때 기본 캡슐화 형식은 VXLAN입니다.

다음 PowerShell cmdlet을 사용하여 네트워크 컨트롤러를 통해 사용되는 캡슐화 형식을 확인할 수 있습니다.

``` syntax
    (Get-NetworkControllerVirtualNetworkConfiguration -connectionuri $uri).properties.networkvirtualizationprotocol
```

최상의 성능을 위해, VXLAN이 반환되면 실제 네트워크 어댑터가 VXLAN 작업 오프로드를 지원하는지 확인해야 합니다.  NVGRE가 반환되면 실제 네트워크 어댑터가 NVGRE 작업 오프로드를 지원해야 합니다.

### <a name="mtu"></a>MTU

캡슐화로 인해 각 패킷에 바이트가 더 추가됩니다.  이러한 패킷의 조각화를 방지하라면 실제 네트워크가 Jumbo 프레임을 사용하도록 구성되어야 합니다.  MTU 값 9234는 VXLAN 또는 NVGRE의 권장 크기이며, 캡슐화된 패킷이 전송될 VLAN의 호스트 포트(L2) 및 라우터 인터페이스(L3)의 물리적 인터페이스에 대한 물리적 스위치에 구성되어야 합니다.  여기에는 Transit, HNV 공급자 및 관리 네트워크가 포함됩니다.

Hyper-V 호스트의 MTU는 네트워크 어댑터를 통해 구성되며, Hyper-V 호스트에서 실행되는 네트워크 컨트롤러 호스트 에이전트는 네트워크 어댑터 드라이버에서 지원되는 경우 캡슐화 오버헤드를 자동으로 조정합니다.  

트래픽이 게이트웨이를 통해 가상 네트워크에서 나가면, 캡슐화가 제거되고 VM에서 보낸 원래 MTU가 사용됩니다.

### <a name="single-root-io-virtualization-sr-iov"></a>SR-IOV(단일 루트 IO 가상화)

SDN은 가상 스위치의 전달 스위치 확장을 사용하여 Hyper-V 호스트에 구현됩니다.  이 스위치 확장으로 패킷을 처리하려면, 네트워크 컨트롤러와 함께 사용하도록 구성된 가상 네트워크 인터페이스에 SR-IOV를 사용하면 안됩니다. SR-IOV를 사용하면 VM 트래픽이 가상 스위치를 우회하기 때문입니다.

원하는 경우 SR-IOV를 가상 스위치에서 사용하도록 설정할 수도 있으며, 네트워크 컨트롤러가 제어하지 않는 VM 네트워크 어댑터에서 사용할 수 있습니다.  이러한 SR-IOV VM은 SR-IOV를 사용하지 않는 네트워크 컨트롤러로 제어되는 VM과 동일한 가상 스위치에 공존할 수 있습니다.

40Gbit 네트워크 어댑터를 사용하는 경우, SLB(소프트웨어 부하 분산) 게이트웨이가 최대 처리량을 달성할 수 있도록 가상 스위치에서 SR-IOV를 활성화하는 것이 좋습니다.  이 내용은 [소프트웨어 부하 분산 장치 게이트웨이](slb-gateway-performance.md) 섹션에 자세히 설명되어 있습니다.

## <a name="hnv-gateways"></a>HNV 게이트웨이

SDN에서 사용할 HNV 게이트웨이 조정에 대한 정보는 [HVN 게이트웨이](hnv-gateway-performance.md) 섹션에서 찾을 수 있습니다.

## <a name="software-load-balancer-slb"></a>SLB(소프트웨어 부하 분산 장치)

SLB 게이트웨이는 네트워크 컨트롤러 및 SDN에만 사용할 수 있습니다.  SLB 게이트웨이에 사용할 SDN 조정에 대한 자세한 정보는 [소프트웨어 부하 분산 장치 게이트웨이](slb-gateway-performance.md) 섹션에서 찾을 수 있습니다.
