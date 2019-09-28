---
title: 소프트웨어 정의 네트워크에서 SLB 게이트웨이 성능 튜닝
description: SDN 네트워크에 대 한 SLB 게이트웨이 성능 조정 지침
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: grcusanz; AnPaul
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 9a0d239da2ca321333ec757db22bbaf9a9b8ba30
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383463"
---
# <a name="slb-gateway-performance-tuning-in-software-defined-networks"></a>소프트웨어 정의 네트워크에서 SLB 게이트웨이 성능 튜닝

소프트웨어 부하 분산은 네트워크 컨트롤러 Vm, Hyper-v 가상 스위치 및 Mux (Load Balancer Multixplexor) Vm의 부하 분산 장치 관리자 조합으로 제공 됩니다.

아래에 설명 된 대로 Muxes에 대 한 SR-IOV를 사용 하지 않는 경우 [소프트웨어 정의 네트워킹](index.md) 섹션에서 설명한 것 외에도 부하 분산을 위해 네트워크 컨트롤러나 hyper-v 호스트를 구성 하는 데 추가 성능 조정이 필요 하지 않습니다.

## <a name="slb-mux-vm-configuration"></a>SLB Mux VM 구성

SLB Mux 가상 머신은 활성-활성 구성으로 배포 됩니다.  이는 네트워크 컨트롤러에 배포 되 고 추가 되는 모든 Mux VM이 들어오는 요청을 처리할 수 있음을 의미 합니다.  따라서 모든 연결의 총 집계 처리량은 배포한 Mux Vm 수에 의해서만 제한 됩니다.  

VIP (가상 IP)에 대 한 개별 연결은 항상 동일한 Mux로 전송 되며, muxes 수가 일정 하 게 유지 되 면 처리량은 단일 Mux VM의 처리량으로 제한 됩니다.  Muxes는 VIP로 향하는 인바운드 트래픽만 처리 합니다.  응답 패킷은 클라이언트에 전달 하는 실제 스위치로 응답을 보내는 VM에서 직접 이동 합니다.

경우에 따라 VIP를 관리 하는 것과 동일한 네트워크 컨트롤러에 추가 된 SDN 호스트에서 요청 원본을 만든 경우 요청에 대 한 인바운드 경로를 추가로 최적화할 수 있습니다 .이를 통해 대부분의 패킷이 클라이언트에서 서버에 대 한 Mux를 완전히 무시 합니다.  이 최적화를 수행 하는 데 필요한 추가 구성은 없습니다.

각 SLB Mux VM은 [소프트웨어 정의 네트워크 인프라 계획](../../../../networking/sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md) 항목의 SDN 인프라 가상 머신 역할 요구 사항 섹션에 제공 된 지침에 따라 크기를 조정 해야 합니다.

## <a name="single-root-io-virtualization-sr-iov"></a>단일 루트 IO 가상화 (SR-IOV)

40Gbit 이더넷을 사용할 때 가상 스위치가 Mux VM에 대 한 패킷을 처리 하는 기능은 Mux VM 처리량에 대 한 제한 요인이 됩니다.  따라서 가상 스위치에 병목 현상이 발생 하지 않도록 SLB VM의 VM 네트워크 어댑터에서 SR-IOV를 사용 하도록 설정 하는 것이 좋습니다.

SR-IOV를 사용 하도록 설정 하려면 가상 스위치를 만들 때 가상 스위치에서 sr-iov를 사용 하도록 설정 해야 합니다.  이 예제에서는 스위치 포함 된 팀 (SET) 및 SR-IOV를 사용 하 여 가상 스위치를 만듭니다.
``` syntax
    new-vmswitch -Name SDNSwitch -EnableEmbeddedTeaming $true -NetAdapterName @("NIC1", "NIC2") -EnableIOV $true
```
그런 다음 데이터 트래픽을 처리 하는 SLB Mux VM의 가상 네트워크 어댑터에서 사용 하도록 설정 해야 합니다.  이 예제에서 SR-IOV는 모든 어댑터에서 사용 하도록 설정 됩니다.
``` syntax
    get-vmnetworkadapter -VMName SLBMUX1 | set-vmnetworkadapter -IovWeight 50
```
