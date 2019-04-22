---
title: SO(소프트웨어 전용) 기능 및 기술
description: 이러한 기능 OS의 일부로 구현 되 고의 기본 NIC와 무관 합니다. 경우에 따라 이러한 기능 몇 가지 최적의 작업에 대 한 NIC의 조정 필요 합니다. 이러한 예로 hyper-v 가상 컴퓨터의 서비스 품질 (vmQoS), 액세스 제어 목록 (Acl) 및 NIC 팀과 같은 비 Hyper-v 기능 등이 있습니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/20/2018
ms.openlocfilehash: 504bc92971e778b468812dc4064fa6f0afff87ad
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823784"
---
# <a name="software-only-so-features-and-technologies"></a>SO(소프트웨어 전용) 기능 및 기술
소프트웨어 전용 기능 OS의 일부로 구현 되 고의 기본 NIC와 무관 합니다. 경우에 따라 이러한 기능 몇 가지 최적의 작업에 대 한 NIC의 조정 필요 합니다. 이러한 예로 hyper-v 가상 컴퓨터의 서비스 품질 (vmQoS), 액세스 제어 목록 (Acl) 및 NIC 팀과 같은 비 Hyper-v 기능 등이 있습니다.

## <a name="access-control-lists-acls"></a>액세스 제어 목록 (Acl)

VM에 대 한 보안 관리를 위해 Hyper-v 및 SDNv1 기능입니다. 이 기능은 Hyper-v 가상화 되지 않은 스택 및 HVNv1 스택에 적용 됩니다. Hyper-v를 관리할 수 있습니다 Acl을 통해 전환할 [Add-vmnetworkadapteracl](https://docs.microsoft.com/powershell/module/hyper-v/add-vmnetworkadapteracl?view=win10-ps) 하 고 [Remove-vmnetworkadapteracl](https://docs.microsoft.com/powershell/module/hyper-v/remove-vmnetworkadapteracl?view=win10-ps) PowerShell cmdlet.

## <a name="extended-acls"></a>확장된 Acl

Hyper-v 가상 스위치 확장 Acl을 사용 하 여 Hyper-v 가상 스위치 확장 포트 Acl을 방화벽 보호를 제공 하 고 테 넌 트 Vm 데이터 센터에서 보안 정책을 적용를 구성할 수 있습니다. Vm 내에서 아니라 Hyper-v 가상 스위치에서 포트 Acl을 구성 하기 때문에 관리자는 다중 테 넌 트 환경에서 모든 테 넌 트에 대 한 보안 정책을 관리할 수 있습니다.

Hyper-v 스위치 확장 Acl을 통해 관리할 수 있습니다 합니다 [Add-vmnetworkadapterextendedacl](https://docs.microsoft.com/powershell/module/hyper-v/add-vmnetworkadapterextendedacl?view=win10-ps) 하 고 [Remove-vmnetworkadapterextendedacl](https://docs.microsoft.com/powershell/module/hyper-v/remove-vmnetworkadapteracl?view=win10-ps) PowerShell cmdlet.

>[!TIP] 
>이 기능은 HNVv1 스택에 적용 됩니다. SDN 스택의 Acl에 대 한 참조 SDN 소프트웨어 방식 네트워킹) 아래 Acl.

확장 포트 액세스 제어 목록에이 라이브러리에 대 한 자세한 내용은 참조 하십시오 [포트 액세스 제어 목록 확장 보안 정책 만들기](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/Create-Security-Policies-with-Extended-Port-Access-Control-Lists)합니다.

## <a name="nic-teaming"></a>NIC 팀

Nic, NIC 본딩 라고도 하는 것이 호스트는 단일 NIC 포트에 게 엔터티로 여러 NIC 포트의 집계. NIC 팀은 단일 NIC 포트 (또는 연결 된 케이블)의 오류 로부터 보호 합니다. 또한 더 빠른 처리량에 대 한 네트워크 트래픽을 집계합니다. 자세한 내용은 참조 하세요. [NIC 팀](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming)합니다.

Windows Server 2016을 사용 하 여 팀 작업을 수행 하는 두 가지 방법으로 해야 합니다.

1.  Windows Server 2012 팀 솔루션

2.  Windows Server 2016 스위치 포함 팀 (SET)


## <a name="rsc-in-the-vswitch"></a>VSwitch의 RSC

수신 세그먼트 (RSC) vSwitch의 동일한 부분이 패킷 스트림 및 네트워크 인터럽트 간의 도착 하는 기능이 며 운영 체제에 게 배달 하기 전에 단일 패킷을에 결합 합니다. Windows Server 2019에서 가상 스위치에이 기능이 있습니다. 이 기능에 대 한 자세한 내용은 참조 하세요. [vSwitch의 수신 세그먼트 병합](https://docs.microsoft.com/windows-server/networking/technologies/hpn/rsc-in-the-vswitch)입니다.

## <a name="software-defined-networking-sdn-acls"></a>소프트웨어 정의 네트워킹 (SDN) Acl

Windows Server 2016의 SDN 확장 Acl을 지원 하는 방법을 향상 되었습니다. Windows Server 2016 SDN v2 스택을 SDN Acl Acl 및 Acl 확장 하는 대신 사용 됩니다. SDN Acl을 관리 하려면 네트워크 컨트롤러를 사용할 수 있습니다. 

## <a name="sdn-quality-of-service-qos"></a>SDN 서비스 품질 (QoS)

Windows Server 2016의 SDN 확장에는 5 튜플을 기준 (송신 예약, 송신 제한 및 수신 제한) 대역폭 제어를 제공 하는 방법을 향상 되었습니다. 일반적으로 이러한 정책은 vNIC 또는 vmNIC 수준에서 적용 하지만 훨씬 더 특정 만들 수 있습니다. Windows Server 2016 SDN v2 스택을 SDN QoS vmQoS 대신 사용 됩니다. SDN QoS를 관리 하려면 네트워크 컨트롤러를 사용할 수 있습니다.

## <a name="switch-embedded-teaming-set"></a>스위치가 포함 된 팀 (설정)

집합은 Windows Server 2016에 Hyper-v 및 네트워킹 SDN (소프트웨어) 스택을 포함 하는 환경에서 사용할 수 있는 대체 NIC 팀 솔루션. 일부 NIC 팀 기능은 Hyper-v 가상 스위치에 통합 하는 설정 합니다. 이 라이브러리의 스위치 포함 팀에 대 한 자세한 내용은 [원격 직접 메모리 액세스 (RDMA) 및 스위치 포함 된 팀 (SET)](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming)합니다.

## <a name="virtual-receive-side-scaling-vrss"></a>vRSS(가상 수신측 배율)

소프트웨어 vRSS는 VM의 여러 개의 논리적 프로세서 (LPs)에서 VM을 대상으로 하는 들어오는 트래픽을 분산 하는 데 사용 됩니다. 소프트웨어 vRSS 단일 LP 보다 더 많은 네트워크 트래픽을 처리할 수를 처리할 수는 VM을 제공 합니다. 자세한 내용은 [가상 수신측 배율 (vRSS)](https://docs.microsoft.com/windows-server/networking/technologies/vrss/vrss-top)합니다.

## <a name="virtual-machine-quality-of-service-vmqos"></a>가상 컴퓨터의 서비스 품질 (vmQoS)

Virtual Machine 서비스 품질 기능은 Hyper-v 스위치를 각 VM에서 생성 되는 트래픽에 대 한 제한을 설정할 수 있도록 합니다. 또한 하나의 VM에는 대역폭에 대 한 다른 VM 고갈 없습니다 있도록 외부 네트워크 연결 대역폭 용량을 예약 하는 VM 수 있습니다. Windows Server 2016 SDN v2 스택을 SDN QoS vmQoS를 대체합니다.

송신 제한 및 송신 예약 vmQoS 설정할 수 있습니다. Hyper-v 스위치를 만들기 전에 송신 예약 모드 (상대 가중치 또는 절대 대역폭)을 결정 합니다.

-  New-vmswitch PowerShell cmdlet의 – MinimumBandwidthMode 매개 변수를 사용 하 여 송신 예약 모드를 결정 합니다.

-  Set-vmnetworkadapter PowerShell cmdlet –이 MaximumBandwidth 매개 변수를 사용 하 여 송신 제한 값을 설정 합니다.

-  다음 매개 변수 중 하나를 사용 하 여 송신 예약 설정 VMNetworkAdapter PowerShell cmdlet에 대 한 값을 설정 합니다.

   -  New-vmswitch cmdlet의 – MinimumBandwidthMode 매개 변수를 절대 설정 VMNetworkAdapter cmdlet – MinimumBandwidthAbsolute 매개 변수를 설정 합니다.

   -  New-vmswitch cmdlet의 – MinimumBandwidthMode 매개 변수를 가중치 설정 VMNetworkAdapter cmdlet – MinimumBandwidthWeight 매개 변수를 설정 합니다.

이 기능에 사용 된 알고리즘에 대 한 제한 사항, 때문에 높은 가중치를 절대 대역폭 되지 않음을 20 번 넘게 가장 낮은 가중치 또는 절대 대역폭 하는 것이 좋습니다. 더 많은 컨트롤이 필요한 경우에 SDN 스택 및 SDN QoS 기능을 사용 하 여 하는 것이 좋습니다.


---