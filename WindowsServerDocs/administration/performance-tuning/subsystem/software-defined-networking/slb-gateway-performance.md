---
title: SLB Gateway의에서 성능 조정 소프트웨어 정의 네트워크
description: SDN 네트워크에 대 한 지침을 조정 하는 SLB 게이트웨이 성능
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: grcusanz; AnPaul
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: fede7d404ddbb4f465eff435cc340db1907ce9d2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829934"
---
# <a name="slb-gateway-performance-tuning-in-software-defined-networks"></a>SLB Gateway의에서 성능 조정 소프트웨어 정의 네트워크

소프트웨어 부하 분산 네트워크 컨트롤러 Vm, Hyper-v 가상 스위치 및 부하 분산 장치 Multixplexor (Mux) Vm 집합이 부하 분산 장치 관리자를 조합 하 여 제공 됩니다.

네트워크 컨트롤러를 구성 하려면 필요 없는 추가 성능 조정은 또는 부하 분산 기능 이외의 대 한 Hyper-v 호스트에서 설명 하는 합니다 [소프트웨어 정의 네트워킹](index.md) SR-IOV에 대 한 사용 하지 않는 한이 섹션은 아래 설명 된 대로 Muxes입니다.

## <a name="slb-mux-vm-configuration"></a>SLB Mux VM 구성

SLB Mux 가상 컴퓨터는 활성-활성 구성에 배포 됩니다.  즉, 모든 Mux VM에 배포 하 고 네트워크 컨트롤러에 추가 하는 들어오는 요청을 처리할 수 있습니다.  따라서 모든 연결의 총 집계 처리량은 배포 된 Mux Vm의 수로만 제한 됩니다.  

개별 연결 가상 IP (VIP)를 항상 전송 됩니다 동일한 Mux로 가정 muxes 수가 그대로 유지 되며 결과적으로 해당 처리량을 단일 Mux VM의 처리량으로 제한 됩니다.  Muxes는 VIP로 향하는 트래픽을 처리 합니다.  응답 패킷이 클라이언트에 전달 하는 실제 스위치에 대 한 응답을 전송 하는 VM에서 직접 이동 합니다.

일부 경우에서 요청의 원본 VIP를 관리 하는 같은 네트워크 컨트롤러에 추가 되는 SDN 호스트에서 시작 하는 경우 요청에 대 한 인바운드 경로 추가 최적화도 수행 됩니다에서 직접 이동 하는 대부분의 패킷을 수 있도록 하는 합니다 서버에 클라이언트 Mux VM을 완전히 무시 합니다.  수행이 최적화에 필요한 추가 구성은 없습니다.

각 SLB Mux VM의 SDN 인프라 가상 컴퓨터 역할 요구 사항 섹션에 제공 된 지침에 따라 크기 조정 해야 합니다 [소프트웨어 정의 네트워크 인프라 계획](../../../../networking/sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md) 항목입니다.

## <a name="single-root-io-virtualization-sr-iov"></a>단일 루트 입출력 가상화 (SR-IOV)

40Gbit 이더넷 사용 Mux VM에 대 한 프로세스 패킷이 가상 스위치 기능 Mux VM 처리량에 대 한 제한 요인이 됩니다.  이 때문에 SR-IOV 가상 스위치 병목 상태가 되지 않도록 하려면 SLB VM의 VM 네트워크 어댑터에서 사용할 수 있는지이 좋습니다.

SR-IOV를 사용 하려면를 설정 해야 해당 가상 스위치 가상 스위치를 만들 때.  이 예제에서는 스위치 포함 팀 (SET)를 구성 하 고 SR-IOV를 사용 하 여 가상 스위치를 만듭니다.
``` syntax
    new-vmswitch -Name SDNSwitch -EnableEmbeddedTeaming $true -NetAdapterName @("NIC1", "NIC2") -EnableIOV $true
```
그런 다음 데이터 트래픽을 처리 하는 SLB Mux VM의 가상 네트워크 어댑터에 사용할 수 있어야 합니다.  이 예제에서는 SR-IOV는 사용 하 게 모든 어댑터에서:
``` syntax
    get-vmnetworkadapter -VMName SLBMUX1 | set-vmnetworkadapter -IovWeight 50
```
