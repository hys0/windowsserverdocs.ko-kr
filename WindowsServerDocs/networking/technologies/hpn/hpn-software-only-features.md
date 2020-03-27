---
title: SO(소프트웨어 전용) 기능 및 기술
description: 이러한 기능은 OS의 일부로 구현 되며 기본 NIC와는 독립적입니다. 이러한 기능에는 최적의 작업을 위해 NIC를 조정 해야 하는 경우가 있습니다. 이러한 예로는 vmQoS (Virtual Machines 서비스 품질), Access Control 목록 (Acl) 및 NIC 팀과 같은 Hyper-v 이외의 기능과 같은 Hyper-v 기능이 있습니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 09/20/2018
ms.openlocfilehash: a83a36ce7a47f0ebde35bf93bdca20796dd37a28
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80316888"
---
# <a name="software-only-so-features-and-technologies"></a>SO(소프트웨어 전용) 기능 및 기술
소프트웨어 전용 기능은 OS의 일부로 구현 되며 기본 NIC와는 독립적입니다. 이러한 기능에는 최적의 작업을 위해 NIC를 조정 해야 하는 경우가 있습니다. 이러한 예로는 vmQoS (Virtual Machines 서비스 품질), Access Control 목록 (Acl) 및 NIC 팀과 같은 Hyper-v 이외의 기능과 같은 Hyper-v 기능이 있습니다.

## <a name="access-control-lists-acls"></a>Access Control 목록 (Acl)

VM에 대 한 보안을 관리 하기 위한 Hyper-v 및 SDNv1 기능입니다. 이 기능은 가상화 되지 않은 Hyper-v 스택과 HVNv1 스택에 적용 됩니다. [Get-vmnetworkadapteracl](https://docs.microsoft.com/powershell/module/hyper-v/add-vmnetworkadapteracl?view=win10-ps) 및 [get-vmnetworkadapteracl](https://docs.microsoft.com/powershell/module/hyper-v/remove-vmnetworkadapteracl?view=win10-ps) PowerShell cmdlet을 통해 hyper-v 스위치 acl을 관리할 수 있습니다.

## <a name="extended-acls"></a>확장 Acl

Hyper-v 가상 스위치 확장 Acl을 사용 하면 Hyper-v 가상 스위치 확장 포트 Acl을 구성 하 여 방화벽 보호를 제공 하 고 데이터 센터에서 테 넌 트 Vm에 대 한 보안 정책을 적용할 수 있습니다. 포트 Acl은 Vm 내에서가 아니라 Hyper-v 가상 스위치에 구성 되므로 관리자는 다중 테 넌 트 환경의 모든 테 넌 트에 대 한 보안 정책을 관리할 수 있습니다.

[Add-vmnetworkadapterextendedacl](https://docs.microsoft.com/powershell/module/hyper-v/add-vmnetworkadapterextendedacl?view=win10-ps) 및 [add-vmnetworkadapterextendedacl](https://docs.microsoft.com/powershell/module/hyper-v/remove-vmnetworkadapteracl?view=win10-ps) PowerShell cmdlet을 통해 hyper-v 스위치 확장 acl을 관리할 수 있습니다.

>[!TIP] 
>이 기능은 HNVv1 스택에 적용 됩니다. SDN 스택의 Acl의 경우 아래의 소프트웨어 정의 네트워킹 SDN) Acl을 참조 하세요.

이 라이브러리의 확장 포트 Access Control 목록에 대 한 자세한 내용은 [확장 포트 Access Control 목록을 사용 하 여 보안 정책 만들기](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/Create-Security-Policies-with-Extended-Port-Access-Control-Lists)를 참조 하세요.

## <a name="nic-teaming"></a>NIC 팀

NIC 연결이 라고도 하는 NIC 팀은 호스트에서 단일 NIC 포트로 인식 하는 엔터티에 대 한 여러 NIC 포트의 집계입니다. NIC 팀은 단일 NIC 포트 (또는 연결 된 케이블)의 오류를 방지 합니다. 또한 더 빠른 처리량을 위해 네트워크 트래픽을 집계 합니다. 자세한 내용은 [NIC 팀](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming)을 참조 하세요.

Windows Server 2016에서는 다음과 같은 두 가지 방법으로 팀을 구성할 수 있습니다.

1.  Windows Server 2012 팀 솔루션

2.  Windows Server 2016 스위치 포함 된 팀 (SET)


## <a name="rsc-in-the-vswitch"></a>VSwitch의 RSC

VSwitch의 RSC (수신 세그먼트 통합)는 동일한 스트림의 일부이 고 네트워크 인터럽트 사이에 도착 하는 패킷을 받아서 단일 패킷으로 결합 한 후 운영 체제에 전달 하는 기능입니다. Windows Server 2019의 가상 스위치에는이 기능이 있습니다. 이 기능에 대 한 자세한 내용은 [vSwitch의 수신 세그먼트 결합](https://docs.microsoft.com/windows-server/networking/technologies/hpn/rsc-in-the-vswitch)을 참조 하세요.

## <a name="software-defined-networking-sdn-acls"></a>SDN (소프트웨어 정의 네트워킹) Acl

Windows Server 2016의 SDN 확장은 Acl을 지 원하는 향상 된 방법을 제공 합니다. Windows Server 2016 SDN v2 스택에서 SDN Acl은 Acl 및 확장 Acl 대신 사용 됩니다. 네트워크 컨트롤러를 사용 하 여 SDN Acl을 관리할 수 있습니다. 

## <a name="sdn-quality-of-service-qos"></a>SDN 서비스 품질 (QoS)

Windows Server 2016의 SDN 확장은 5 튜플 기반으로 대역폭 제어 (송신 예약, 송신 제한 및 수신 제한)를 제공 하는 방법을 개선 했습니다. 일반적으로 이러한 정책은 vNIC 또는 vmNIC 수준에서 적용 되지만 훨씬 더 구체적인 방법으로 만들 수 있습니다. Windows Server 2016 SDN v2 스택에서 vmQoS 대신 SDN QoS가 사용 됩니다. 네트워크 컨트롤러를 사용 하 여 SDN QoS를 관리할 수 있습니다.

## <a name="switch-embedded-teaming-set"></a>스위치가 포함 된 팀 (설정)

집합은 Windows Server 2016에 Hyper-v 및 네트워킹 SDN (소프트웨어) 스택을 포함 하는 환경에서 사용할 수 있는 대체 NIC 팀 솔루션. 일부 NIC 팀 기능은 Hyper-v 가상 스위치에 통합 하는 설정 합니다. 이 라이브러리의 스위치 포함 팀에 대 한 자세한 내용은 [RDMA (원격 직접 메모리 액세스) 및 스위치 포함 된 팀 (설정)](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming)을 참조 하세요.

## <a name="virtual-receive-side-scaling-vrss"></a>vRSS(가상 수신측 배율)

소프트웨어 vRSS는 vm의 LPs (여러 논리 프로세서)에서 VM을 대상으로 하는 들어오는 트래픽을 분산 하는 데 사용 됩니다. 소프트웨어 vRSS는 단일 LP가 처리할 수 있는 것 보다 더 많은 네트워킹 트래픽을 처리 하는 기능을 VM에 제공 합니다. 자세한 내용은 [vRSS (가상 수신측 배율)](https://docs.microsoft.com/windows-server/networking/technologies/vrss/vrss-top)를 참조 하세요.

## <a name="virtual-machine-quality-of-service-vmqos"></a>가상 컴퓨터의 vmQoS (서비스 품질)

Virtual Machine 서비스 품질은 스위치가 각 VM에서 생성 된 트래픽에 대 한 제한을 설정할 수 있도록 하는 Hyper-v 기능입니다. 또한 VM이 외부 네트워크 연결에서 대역폭을 예약할 수 있도록 하 여 한 VM이 다른 VM의 대역폭을 결핍 수 없습니다. Windows Server 2016 SDN v2 스택에서 SDN QoS는 vmQoS를 대체 합니다.

vmQoS는 송신 한도와 송신 예약을 설정할 수 있습니다. Hyper-v 스위치를 만들기 전에 송신 예약 모드 (상대적 가중치 또는 절대 대역폭)를 결정 해야 합니다.

-  새-VMSwitch PowerShell cmdlet의 – MinimumBandwidthMode 매개 변수를 사용 하 여 송신 예약 모드를 확인 합니다.

-  VMNetworkAdapter PowerShell cmdlet의 –이 maximumbandwidth 매개 변수를 사용 하 여 송신 한도 값을 설정 합니다.

-  Set VMNetworkAdapter PowerShell cmdlet의 다음 매개 변수 중 하나를 사용 하 여 송신 예약 값을 설정 합니다.

   -  MinimumBandwidthMode cmdlet의 – 매개 변수가 절대적 이면 Set VMNetworkAdapter cmdlet에서 – MinimumBandwidthAbsolute 매개 변수를 설정 합니다.

   -  MinimumBandwidthMode cmdlet의 – 매개 변수가 가중치 이면 Set VMNetworkAdapter cmdlet에서 – MinimumBandwidthWeight 매개 변수를 설정 합니다.

이 기능에 사용 되는 알고리즘의 제한 사항 때문에 가장 높은 가중치가 나 절대 대역폭을 가장 낮은 가중치가 나 절대 대역폭의 20 배 이상으로 사용 하지 않는 것이 좋습니다. 더 많은 제어가 필요한 경우 SDN 스택과 SDN QoS 기능을 사용 하는 것이 좋습니다.


---