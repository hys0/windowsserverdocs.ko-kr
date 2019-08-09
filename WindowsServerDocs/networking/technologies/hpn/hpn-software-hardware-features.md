---
title: SH(소프트웨어 및 하드웨어) 통합 기능 및 기술
description: 이러한 기능이 소프트웨어 및 하드웨어 구성 요소입니다. 소프트웨어는 기능이 작동 하기 위해 필요한 하드웨어 기능으로 연결 됩니다. 이러한 예로 VMMQ, VMQ, 송신 측 IPv4 체크섬 오프 로드, 및 RSS를 들 수 있습니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/12/2018
ms.openlocfilehash: 98857a5a6d665728c1aab2a6a2df64997d4166b0
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446218"
---
# <a name="software-and-hardware-sh-integrated-features-and-technologies"></a>SH(소프트웨어 및 하드웨어) 통합 기능 및 기술

이러한 기능이 소프트웨어 및 하드웨어 구성 요소입니다. 소프트웨어는 기능이 작동 하기 위해 필요한 하드웨어 기능으로 연결 됩니다. 이러한 예로 VMMQ, VMQ, 송신 측 IPv4 체크섬 오프 로드, 및 RSS를 들 수 있습니다.

>[!TIP]
>SH 및 호스트 기능은 설치 된 NIC에서 지 원하는 경우 사용할 수 있습니다. 아래 기능 설명에서는 NIC 기능을 지 원하는 경우를 구별 하는 방법을 설명 합니다.

## <a name="converged-nic"></a>수렴 형 된 NIC 

수렴 형 된 NIC에는 호스트 프로세스에 RDMA 서비스를 노출 하도록 Hyper-v 호스트에 가상 Nic를 허용 하는 기술입니다. Windows Server 2016 RDMA에 대 한 별도 Nic를 더 이상 필요합니다. 수렴 된 NIC 기능은를 호스트 파티션에 RDMA를 제공 하 고 공정 하 고 관리 하기 쉬운 방식으로 다른 TCP/UDP 트래픽을 RDMA 트래픽와 VM 간의 Nic의 대역폭을 공유 하는 호스트 파티션 (vNICs)에서 가상 Nic를 수 있습니다.

![SDN 사용 하 여 수렴 형 된 NIC](../../media/Converged-NIC/conv-nic-sdn.png)

VMM 또는 Windows PowerShell을 통해 수렴 된 NIC 작업을 관리할 수 있습니다. PowerShell cmdlet은 RDMA (아래 참조)에 사용 되는 동일한 cmdlet.

에 수렴 된 NIC 기능을 사용 합니다.

1.  DCB에 대해 호스트를 설정 해야 합니다.

2.  집합 팀의 경우 Nic 바인딩되어 또는 NIC에서 RDMA를 사용 하도록 설정 해야 Hyper-v 스위치에 있습니다. 

3.  호스트에 RDMA에 대 한 지정 된 vNICs에 RDMA를 사용 하도록 설정 해야 합니다. 

RDMA 및 SET에 대 한 자세한 내용은 참조 하세요. [원격 직접 메모리 액세스 (RDMA) 및 스위치 포함 된 팀 (SET)](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming)합니다.

## <a name="data-center-bridging-dcb"></a>DCB(데이터 센터 브리징) 

DCB는 데이터 센터에서 수렴 된 패브릭을 사용할 수 있는 Institute의 IEEE (Electrical and Electronics Engineers) 표준의 모음입니다. DCB는 인접 스위치가에서 공동 작업을 사용 하 여 호스트에서 하드웨어 큐 기반 대역폭 관리를 제공합니다. 저장소에 대 한 모든 트래픽을 데이터 네트워킹, 클러스터 간 프로세스 통신 (IPC) 및 관리 공유 동일한 이더넷 네트워크 인프라 Windows Server 2016에서 DCB 개별적으로 모든 NIC에 적용할 수 있습니다 하 고 Hyper-v에 바인딩된 Nic에 전환 합니다.

DCB에 대 한 Windows Server 우선 순위 기반 흐름 제어 PFC (), IEEE 802.1Qbb 표준화를 사용 합니다. PFC는 트래픽 클래스 내에서 오버플로 방지 하 여 (거의) 무손실 네트워크 패브릭을 만듭니다. Windows Server는 또한 향상 된 전송 선택 (ETS), IEEE 802.1Qaz 표준화를 사용 합니다. ETS 트래픽의 최대 8 개의 클래스에 대 한 예약 된 부분에 대역폭의 나누기 수 있습니다. 각 트래픽 클래스에는 자체 전송 큐 및 PFC를 사용 하 여 수 있습니다. 시작 하 고 클래스 내에 전송을 중지 합니다.

자세한 내용은 [데이터 센터 브리징 (DCB)](https://docs.microsoft.com/windows-server/networking/technologies/dcb/dcb-top)합니다.

## <a name="hyper-v-network-virtualization"></a>Hyper-V 네트워크 가상화

|                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **v1 (HNVv1)**       |                     Windows Server 2012에 도입 된, Hyper-v 네트워크 가상화 (HNV) 고객 네트워크 공유, 실제 네트워크 인프라의 가상화를 사용 합니다. 실제 네트워크 패브릭에서 필요한 최소한의 변화를 통해 HNV를 통해 서비스 공급자 배포 하 고 세 개의 클라우드에 걸쳐 아무 곳 이나 테 넌 트 작업을 마이그레이션하는 민첩성과: 서비스 공급자 클라우드, 프라이빗 클라우드 또는 Microsoft Azure 퍼블릭 클라우드입니다.                     |
| **v2 NVGRE (HNVv2 NVGRE)** | Microsoft는 Windows Server 2016 및 System Center Virtual Machine Manager RAS 게이트웨이, 소프트웨어 부하 분산, 네트워크 컨트롤러 등을 포함 하는 종단 간 네트워크 가상화 솔루션을 제공 합니다. 자세한 내용은 [Windows Server 2016에서 Hyper-v 네트워크 가상화 개요](https://technet.microsoft.com/windows-server-docs/networking/sdn/technologies/hyper-v-network-virtualization/hyperv-network-virtualization-overview-windows-server)합니다. |
| **v2 VxLAN (HNVv2 VxLAN)** |                                                                                                                                                                                        Windows Server 2016의 SDN-하는 확장을 통해 네트워크 컨트롤러 관리의 일부가입니다.                                                                                                                                                                                        |

---

## <a name="ipsec-task-offload-ipsecto"></a>IPsec 작업 오프 로드 (IPsecTO) 

IPsec 작업 오프 로드에는 IPsec 암호화 작업에 대 한 NIC의 프로세서를 사용 하려면 운영 체제를 사용 하도록 설정 하는 NIC 기능입니다.

>[!IMPORTANT] 
>IPsec 작업 오프 로드 대부분의 네트워크 어댑터에서 지원 되지 않는 레거시 기술 이며 기본적으로 비활성화 되어 파일이 위치 합니다.

## <a name="private-virtual-local-area-network-pvlan"></a>가상 로컬 영역 네트워크 PVLAN (사설)입니다. 

Pvlan 동일한 가상화 서버에서 가상 컴퓨터 사이 에서만 통신을 허용합니다. 개인 가상 네트워크를 실제 네트워크 어댑터에 바인딩되지 않습니다. 개인 가상 네트워크는 관리 운영 체제와 외부 네트워크 간에 네트워크 트래픽을 가상화 서버에서 모든 외부 네트워크 트래픽을에서 격리 됩니다. 이 유형의 네트워크는 격리된 테스트 도메인과 같은 격리된 네트워킹 환경을 만들어야 할 경우에 유용합니다. Hyper-v 및 SDN 스택을 PVLAN 격리 포트 모드만을 지원합니다.

PVLAN 격리에 대 한 세부 정보를 참조 하세요. [System Center: Virtual Machine Manager 엔지니어링 블로그](https://blogs.technet.microsoft.com/scvmm/2013/06/04/logical-networks-part-iv-pvlan-isolation/)합니다.

## <a name="remote-direct-memory-access-rdma"></a>RDMA(원격 직접 메모리 액세스) 

RDMA는 CPU 사용량을 최소화 하는 높은 처리량, 대기 시간이 짧은 통신을 제공 하는 네트워킹 기술입니다. RDMA에 직접 또는 응용 프로그램 메모리에서 데이터를 전송 하려면 네트워크 어댑터를 사용 하 여 0 복사 네트워킹을 지원 합니다. RDMA 가능 NIC (실제 또는 가상)는 RDMA는 RDMA 클라이언트에 노출할 수 의미 합니다. RDMA 지원 RDMA 가능 NIC를 스택으로 RDMA 인터페이스를 공개 하는 반면, 의미 합니다.

RDMA에 대 한 자세한 내용은 참조 하세요. [원격 직접 메모리 액세스 (RDMA) 및 스위치 포함 된 팀 (SET)](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming)합니다.

## <a name="receive-side-scaling-rss"></a>Receive Side Scaling (RSS) 

RSS는 스트림의 다른 집합을 분리 하 고 처리를 위해 서로 다른 프로세서에 전달 하는 NIC 기능입니다. RSS는 처리, 매우 높은 데이터 요금이 크기를 조정 하는 호스트를 사용 하도록 설정 하면 네트워킹 평행 화 합니다. 

자세한 내용은 참조 하세요. [수신 RSS (수신측 배율)](https://docs.microsoft.com/windows-hardware/drivers/network/introduction-to-receive-side-scaling)합니다.

## <a name="single-root-input-output-virtualization-sr-iov"></a>단일 루트 입출력 가상화 (SR-IOV) 

SR-IOV에는 Hyper-v 호스트를 통과 하지 않고 VM에 NIC에서 직접 이동 하려면 VM 트래픽을 허용 합니다. SR-IOV는 VM에 대 한 성능 향상을 놀라운 이지만 호스트가 해당 파이프를 관리 하는 데 사용할 수 없는 합니다. 호스트에서 SR-IOV를 신뢰할 수 있는 워크 로드를 정상적으로 작동 하는 경우 및 일반적으로 유일한 VM 임을만 사용 합니다.

SR-IOV를 사용 하는 트래픽과 Hyper-v 스위치를 무시 즉 정책에 예를 들어, Acl 또는 대역폭 관리를 적용 되지 않습니다. SR-IOV 트래픽은 전달할 수 없습니다 모든 네트워크 가상화 기능을 통해 NV GRE 또는 VxLAN 캡슐화를 적용할 수 없습니다. 특정 상황에서 잘 신뢰할 수 있는 워크 로드에만 SR-IOV를 사용 합니다. 또한 호스트 정책, 대역폭 관리 및 가상화 기술을 사용할 수 없습니다.

나중에 두 가지 기술을 SR-IOV 하면: 일반 흐름 테이블 (GFT) 및 하드웨어 QoS 오프 로드 (NIC에서 대역폭 관리)-Nic는 에코 시스템에서 지원 되 면 합니다. 이러한 두 기술의 조합이 없게 SR-IOV 모든 Vm에 대 한 유용한 정책, 가상화 및 대역폭 관리 규칙을 적용 하면 및 전달할 수 있습니다 결과 뛰어난 나갑니다에서 일반에서 sr-iov 응용 프로그램입니다.

자세한 내용은 참조 하세요. [개요의 단일 루트 I/O 가상화 (SR-IOV)](https://docs.microsoft.com/windows-hardware/drivers/network/overview-of-single-root-i-o-virtualization--sr-iov-)합니다.

## <a name="tcp-chimney-offload"></a>TCP Chimney 오프 로드

TCP Chimney 오프 로드, 라고도 TCP 엔진 오프 로드 (TOE)에 호스트 NIC를 처리 하는 모든 TCP 오프 로드를 허용 하는 기술 Windows Server TCP 스택의 더 거의 항상 이므로 TOE 엔진 보다 효율적인 TCP Chimney 오프 로드를 사용 하 여 권장 되지 않습니다.

>[!IMPORTANT]
>TCP Chimney 오프 로드 사용 되지 않는 기술입니다. 사용 하지 않는 TCP Chimney 오프 로드 앞으로 지 원하는 Microsoft 중지 될 수 있습니다 하는 대로 하는 것이 좋습니다.

## <a name="virtual-local-area-network-vlan"></a>Virtual Local Area Network (VLAN) 

VLAN은 분할을 사용 하려면 lan 여러 Vlan에 고유한 주소 공간을 사용 하 여 각 이더넷 프레임 헤더에 대 한 확장입니다. Windows Server 2016의 Hyper-v 스위치 또는 Nic 팀에 팀 인터페이스를 설정 하 여 포트에서 Vlan 설정 됩니다. 자세한 내용은 [NIC 팀 및 Virtual Local Area Network (Vlan)](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nict-and-vlans)합니다.

## <a name="virtual-machine-queue-vmq"></a>VMQ(가상 컴퓨터 큐) 

Vmq는 각 VM에 대 한 큐를 할당 하는 NIC 기능입니다. Hyper-v 사용 해야 언제 든 지 VMQ 설정할 수도 있습니다. Windows Server 2016 Vmq는 vPort에 할당 된 단일 큐를 사용 하 여 NIC 스위치 vPorts 동일한 기능을 제공 하려면 사용 합니다. 자세한 내용은 [Virtual Receive Side Scaling (vRSS)](https://docs.microsoft.com/windows-server/networking/technologies/vrss/vrss-top) 하 고 [NIC 팀](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming)합니다.

## <a name="virtual-machine-multi-queue-vmmq"></a>가상 머신 다중 큐 (VMMQ) 

VMMQ는 다른 실제 프로세서에서 처리 하는 각 여러 큐를 분산 하 여 VM의 트래픽을 허용 하는 NIC 기능입니다. 그러면 vRSS VM에 상당한 네트워킹 대역폭을 제공 하기 위해 허용 하는 것으로 트래픽은 VM에 여러 LPs에 전달 됩니다.

---