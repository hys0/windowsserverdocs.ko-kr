---
title: SH(소프트웨어 및 하드웨어) 통합 기능 및 기술
description: 이러한 기능에는 소프트웨어와 하드웨어 구성 요소가 모두 있습니다. 이 소프트웨어는 기능을 작동 하는 데 필요한 하드웨어 기능에 깊이 됩니다. 이러한 예로는 VMMQ, VMQ, 송신 측 IPv4 체크섬 오프 로드 및 RSS가 있습니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/12/2018
ms.openlocfilehash: 2f6bb2190dbaa432d20f445c90a560843d6cf4e5
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70871936"
---
# <a name="software-and-hardware-sh-integrated-features-and-technologies"></a>SH(소프트웨어 및 하드웨어) 통합 기능 및 기술

이러한 기능에는 소프트웨어와 하드웨어 구성 요소가 모두 있습니다. 이 소프트웨어는 기능을 작동 하는 데 필요한 하드웨어 기능에 깊이 됩니다. 이러한 예로는 VMMQ, VMQ, 송신 측 IPv4 체크섬 오프 로드 및 RSS가 있습니다.

>[!TIP]
>설치 된 NIC에서 지원 되는 경우 SH 및 호 기능을 사용할 수 있습니다. 아래 기능 설명은 NIC가 기능을 지원 하는지 여부를 확인 하는 방법을 다룹니다.

## <a name="converged-nic"></a>수렴 형 NIC 

수렴 형 NIC는 Hyper-v 호스트의 가상 Nic가 RDMA 서비스를 호스트 프로세스에 노출할 수 있도록 하는 기술입니다. Windows Server 2016에는 더 이상 RDMA를 위한 별도의 Nic가 필요 하지 않습니다. 수렴 형 NIC 기능을 사용 하면 호스트 파티션 (vNICs)의 가상 Nic가 RDMA를 호스트 파티션에 노출 하 고 RDMA 트래픽과 VM 및 기타 TCP/UDP 트래픽 간의 Nic 대역폭을 공평 하 고 관리 하기 쉬운 방식으로 공유할 수 있습니다.

![SDN에서 수렴 형 NIC](../../media/Converged-NIC/conv-nic-sdn.png)

VMM 또는 Windows PowerShell을 통해 수렴 형 NIC 작업을 관리할 수 있습니다. PowerShell cmdlet은 RDMA에 사용 되는 것과 동일한 cmdlet입니다 (아래 참조).

수렴 형 NIC 기능을 사용 하려면:

1.  DCB에 대 한 호스트를 설정 해야 합니다.

2.  NIC에서 RDMA를 사용 하도록 설정 하거나, 집합 팀의 경우 Nic가 Hyper-v 스위치에 바인딩되어 있는지 확인 합니다. 

3.  호스트에서 RDMA에 대해 지정 된 vNICs에서 RDMA를 사용 하도록 설정 해야 합니다. 

RDMA 및 설정에 대 한 자세한 내용은 [rdma (원격 직접 메모리 액세스) 및 스위치 포함 된 팀 (설정)](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming)을 참조 하세요.

## <a name="data-center-bridging-dcb"></a>DCB(데이터 센터 브리징) 

DCB은 데이터 센터에서 수렴 된 패브릭을 사용할 수 있도록 하는 IEEE (전기 및 전자 제품 엔지니어)의 집합입니다. DCB는 인접 스위치의 협력을 통해 호스트에서 하드웨어 큐 기반 대역폭 관리를 제공 합니다. 저장소, 데이터 네트워킹, 클러스터 IPC (프로세스 간 통신) 및 관리에 대 한 모든 트래픽은 동일한 이더넷 네트워크 인프라를 공유 합니다. Windows Server 2016에서 DCB는 임의의 NIC에 개별적으로 적용 될 수 있으며, Hyper-v 스위치에 바인딩된 Nic에도 적용 될 수 있습니다.

DCB의 경우 Windows Server는 IEEE 802.1 Qbb에서 표준화 된 PFC (우선 순위 기반 흐름 제어)를 사용 합니다. PFC는 트래픽 클래스 내에서 오버플로를 방지 하 여 (거의) 무손실 네트워크 패브릭을 만듭니다. 또한 Windows Server는 IEEE 802.1 Qaz에서 표준화 된 (향상 된 전송 선택)를 사용 합니다. 작업을 사용 하면 최대 8 개의 트래픽 클래스에 대해 대역폭을 예약 된 부분으로 나눌 수 있습니다. 각 트래픽 클래스에는 자체 전송 큐가 있고 PFC를 사용 하 여 클래스 내에서 전송을 시작 하 고 중지할 수 있습니다.

자세한 내용은 [데이터 센터 브리징 (DCB) (영문)](https://docs.microsoft.com/windows-server/networking/technologies/dcb/dcb-top)을 참조 하세요.

## <a name="hyper-v-network-virtualization"></a>Hyper-V 네트워크 가상화

|                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **v1 (HNVv1)**       |                     Windows Server 2012에 도입 된 Hyper-v 네트워크 가상화 (HNV)는 공유 된 실제 네트워크 인프라를 기반으로 고객 네트워크를 가상화 할 수 있도록 합니다. 실제 네트워크 패브릭에서 필요한 최소한의 변화를 통해 HNV를 통해 서비스 공급자 배포 하 고 세 개의 클라우드에 걸쳐 아무 곳 이나 테 넌 트 작업을 마이그레이션하는 민첩성과: 서비스 공급자 클라우드, 프라이빗 클라우드 또는 Microsoft Azure 공용 클라우드입니다.                     |
| **v2 NVGRE (HNVv2 NVGRE)** | Windows Server 2016 및 System Center Virtual Machine Manager에서 Microsoft는 RAS 게이트웨이, 소프트웨어 부하 분산, 네트워크 컨트롤러 등을 포함 하는 종단 간 네트워크 가상화 솔루션을 제공 합니다. 자세한 내용은 [Windows Server 2016의 Hyper-v 네트워크 가상화 개요](https://technet.microsoft.com/windows-server-docs/networking/sdn/technologies/hyper-v-network-virtualization/hyperv-network-virtualization-overview-windows-server)를 참조 하세요. |
| **v2 VxLAN (HNVv2 VxLAN)** |                                                                                                                                                                                        Windows Server 2016에서는 네트워크 컨트롤러를 통해 관리 하는 SDN 확장의 일부입니다.                                                                                                                                                                                        |

---

## <a name="ipsec-task-offload-ipsecto"></a>IPsec 작업 오프 로드 (IPsecTO) 

IPsec 작업 오프 로드는 운영 체제에서 NIC의 프로세서를 사용 하 여 IPsec 암호화 작업을 수행할 수 있도록 하는 NIC 기능입니다.

>[!IMPORTANT] 
>IPsec 작업 오프 로드는 대부분의 네트워크 어댑터에서 지원 되지 않는 레거시 기술로, 존재 하는 경우 기본적으로 사용 하지 않도록 설정 됩니다.

## <a name="private-virtual-local-area-network-pvlan"></a>개인 virtual Local Area Network (PVLAN). 

PVLANs은 동일한 가상화 서버의 가상 컴퓨터 간에만 통신할 수 있도록 허용 합니다. 개인 가상 네트워크는 실제 네트워크 어댑터에 바인딩되지 않습니다. 개인 가상 네트워크는 가상화 서버의 모든 외부 네트워크 트래픽 및 관리 운영 체제와 외부 네트워크 간의 네트워크 트래픽에 격리 됩니다. 이 유형의 네트워크는 격리된 테스트 도메인과 같은 격리된 네트워킹 환경을 만들어야 할 경우에 유용합니다. Hyper-v 및 SDN 스택은 PVLAN 격리 된 포트 모드만 지원 합니다.

PVLAN 격리에 대 한 자세한 내용은 [System Center: Virtual Machine Manager 엔지니어링 블로그](https://blogs.technet.microsoft.com/scvmm/2013/06/04/logical-networks-part-iv-pvlan-isolation/).

## <a name="remote-direct-memory-access-rdma"></a>RDMA(원격 직접 메모리 액세스) 

RDMA는 CPU 사용량을 최소화 하는 높은 처리량, 짧은 대기 시간 통신을 제공 하는 네트워킹 기술입니다. RDMA는 네트워크 어댑터가 응용 프로그램 메모리에 직접 데이터를 전송할 수 있도록 하 여 제로 복사 네트워킹을 지원 합니다. RDMA 지원 이란 NIC (실제 또는 가상)가 rdma 클라이언트에 RDMA를 노출할 수 있음을 의미 합니다. 반면 RDMA를 사용 하면 rdma 지원 NIC가 스택에 RDMA 인터페이스를 노출 하는 것을 의미 합니다.

RDMA에 대 한 자세한 정보는 rdma ( [원격 직접 메모리 액세스) 및 스위치 포함 된 팀 (SET)](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming)을 참조 하세요.

## <a name="receive-side-scaling-rss"></a>Receive Side Scaling (RSS) 

RSS는 다양 한 스트림 집합을 분리 하 고 처리를 위해 다른 프로세서에 전달 하는 NIC 기능입니다. RSS는 네트워킹 처리를 데이터가 아니라 호스트가 매우 높은 데이터 요금으로 확장 될 수 있도록 합니다. 

자세한 내용은 [RSS (수신측 배율)](https://docs.microsoft.com/windows-hardware/drivers/network/introduction-to-receive-side-scaling)를 참조 하세요.

## <a name="single-root-input-output-virtualization-sr-iov"></a>단일 루트 입/출력 가상화 (SR-IOV) 

SR-IOV를 사용 하면 Hyper-v 호스트를 통과 하지 않고도 VM 트래픽을 NIC에서 VM으로 직접 이동할 수 있습니다. SR-IOV는 VM에 대 한 성능 향상을 제공 하지만 호스트가 해당 파이프를 관리 하는 기능은 없습니다. 워크 로드가 잘 동작 하 고, 신뢰할 수 있으며, 일반적으로 호스트의 유일한 VM 인 경우에만 SR-IOV를 사용 합니다.

SR-IOV를 사용 하는 트래픽은 Hyper-v 스위치를 우회 합니다. 즉, Acl 또는 대역폭 관리와 같은 모든 정책이 적용 되지 않습니다. 또한 SR-IOV 트래픽은 네트워크 가상화 기능을 통해 전달 될 수 없으므로 NV-GRE 또는 VxLAN 캡슐화를 적용할 수 없습니다. 특정 상황에서 잘 신뢰할 수 있는 작업에 대해서만 SR-IOV를 사용 합니다. 또한 호스트 정책, 대역폭 관리 및 가상화 기술을 사용할 수 없습니다.

향후에는 두 가지 기술을 통해 SR-IOV를 사용할 수 있습니다. GFT (Generic Flow Tables) 및 하드웨어 QoS 오프 로드 (NIC의 대역폭 관리) – 에코 시스템의 Nic가 이러한 기능을 지원 합니다. 이러한 두 기술을 조합 하 여 SR-IOV를 모든 Vm에 유용 하 게 사용할 수 있으며, 정책, 가상화 및 대역폭 관리 규칙이 적용 될 수 있으며, SR-IOV의 일반 응용 프로그램에서 뛰어난 나갑니다을 얻을 수 있습니다.

자세한 내용은 [단일 루트 I/o 가상화 (sr-iov) 개요](https://docs.microsoft.com/windows-hardware/drivers/network/overview-of-single-root-i-o-virtualization--sr-iov-)를 참조 하세요.

## <a name="tcp-chimney-offload"></a>TCP Chimney 오프 로드

Tcp (가) (TCP 엔진 오프 로드) 라고도 하는 TCP Chimney 오프 로드는 호스트가 모든 TCP 처리를 NIC로 오프 로드 하는 데 사용할 수 있는 기술입니다. Windows Server TCP 스택은 거의 항상 서 수 엔진 보다 더 효율적 이므로 TCP Chimney 오프 로드를 사용 하지 않는 것이 좋습니다.

>[!IMPORTANT]
>TCP Chimney 오프 로드는 더 이상 사용 되지 않는 기술입니다. Microsoft에서 나중에 지원 하지 않을 수 있으므로 TCP Chimney 오프 로드를 사용 하지 않는 것이 좋습니다.

## <a name="virtual-local-area-network-vlan"></a>VLAN (Virtual Local Area Network) 

VLAN은 이더넷 프레임 헤더에 대 한 확장으로, 각각 고유한 주소 공간을 사용 하 여 LAN을 여러 Vlan으로 분할할 수 있도록 합니다. Windows Server 2016에서 Vlan은 Hyper-v 스위치의 포트에 설정 되거나 NIC 팀 팀에서 팀 인터페이스를 설정 하 여 설정 됩니다. 자세한 내용은 [NIC 팀 및 vlan (Virtual Local Area network)](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nict-and-vlans)을 참조 하세요.

## <a name="virtual-machine-queue-vmq"></a>VMQ(가상 컴퓨터 큐) 

Vmq는 각 VM에 대 한 큐를 할당 하는 NIC 기능입니다. 언제 든 지 Hyper-v를 사용할 수 있습니다. VMQ도 사용 하도록 설정 해야 합니다. Windows Server 2016에서 Vmq는 동일한 기능을 제공 하기 위해 Vports에 할당 된 단일 큐로 NIC 스위치 vPorts를 사용 합니다. 자세한 내용은 [vRSS (가상 수신측 배율)](https://docs.microsoft.com/windows-server/networking/technologies/vrss/vrss-top) 및 [NIC 팀](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming)을 참조 하세요.

## <a name="virtual-machine-multi-queue-vmmq"></a>가상 컴퓨터 다중 큐 (VMMQ) 

VMMQ는 VM에 대 한 트래픽을 서로 다른 실제 프로세서에서 처리 하는 여러 큐에 분산 시킬 수 있도록 하는 NIC 기능입니다. 그런 다음 트래픽은 vRSS에서와 같이 VM의 여러 LPs에 전달 되므로 VM에 상당한 네트워킹 대역폭을 제공할 수 있습니다.

---