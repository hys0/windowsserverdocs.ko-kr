---
title: NIC 팀
description: 이 항목에서는 개요를 제공 네트워크 인터페이스 카드 (NIC) 팀의 Windows Server 2016에서. 1과 32 사이 그룹화 할 수 있습니다 NIC 팀 하나 이상의 소프트웨어 기반 가상 네트워크 어댑터에 실제 이더넷 네트워크 어댑터입니다. 이 가상 네트워크 어댑터에는 빠른 성능과 네트워크 어댑터 오류 발생 시 내결함성을 제공합니다.
manager: dougkim
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-nict
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: abded6f3-5708-4e35-9a9e-890e81924fec
ms.author: pashort
author: shortpatti
ms.date: 09/10/2018
ms.openlocfilehash: 367de10e8c77490ff27be81ddc05239f931ad1f4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860474"
---
# <a name="nic-teaming"></a>NIC 팀

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 개요를 제공 네트워크 인터페이스 카드 (NIC) 팀의 Windows Server 2016에서. 1과 32 사이 그룹화 할 수 있습니다 NIC 팀 하나 이상의 소프트웨어 기반 가상 네트워크 어댑터에 실제 이더넷 네트워크 어댑터입니다. 이 가상 네트워크 어댑터에는 빠른 성능과 네트워크 어댑터 오류 발생 시 내결함성을 제공합니다.  
  
>[!IMPORTANT]
>NIC 팀 구성원의 네트워크 어댑터가 동일한 물리적 호스트 컴퓨터에 설치 해야 합니다. 

> [!TIP]  
> 하나의 네트워크 어댑터를 포함 하는 NIC 팀 부하 분산 및 장애 조치를 제공할 수 없습니다. 그러나 하나의 네트워크 어댑터와 함께 사용할 수 있습니다 NIC 팀 네트워크 트래픽 분리에 대 한 가상 로컬 영역 네트워크 (Vlan)을 사용 중인 경우.  
  
NIC 팀에 네트워크 어댑터를 구성한 경우에 NIC 팀 솔루션 일반적인 코어, 다음 하나 이상의 가상 어댑터 (Nic [tNICs] 또는 팀 인터페이스 라고도 함)의 운영 체제를 제공 하는 연결 합니다. 

Windows Server 2016 팀 당 최대 32 팀 인터페이스를 지원 하므로 아웃 바운드 트래픽 (부하) Nic 간에 분배 하는 알고리즘의 여러 가지가 있습니다.  다음 그림은 여러 tNICs 인 NIC 팀을 보여 줍니다.  
  
![여러 tNICs NIC 팀](../../media/NIC-Teaming/nict_overview.jpg)  
  
또한 같은 스위치 또는 서로 다른 스위치에 그룹화 된 Nic를 연결할 수 있습니다. 서로 다른 스위치에 Nic를 연결 하는 경우 두 스위치가 모두 동일한 서브넷에 있어야 합니다.  
  
## <a name="availability"></a>가용성  
NIC 팀은 Windows Server 2016의 모든 버전에서 사용할 수 있습니다. 와 같은 클라이언트 운영 체제를 실행 하는 컴퓨터에서 NIC 팀을 관리 하려면 다양 한 도구를 사용할 수 있습니다. • Windows PowerShell cmdlet • 원격 데스크톱 • 원격 서버 관리 도구  
  
## <a name="supported-and-unsupported-nics"></a>지원 및 미지원 Nic   
Windows Server 2016에서 NIC 팀에서 (WHQL 테스트)는 Windows 하드웨어 규정 및 로고 테스트 경과 된 NIC를 사용할 수 있습니다.  
  
NIC 팀에서 없습니다 다음 Nic를 배치할 수 있습니다.
  
-   Hyper-v 가상 스위치 포트는 호스트 파티션에 Nic로 노출 하는 Hyper-v 가상 네트워크 어댑터입니다.  
  
    > [!IMPORTANT]  
    > 팀에서 호스트 파티션 (vNICs)에 노출 하는 Hyper-v 가상 Nic를 배치 하지 마십시오. 팀 vnics 호스트 파티션 내에서 모든 구성에서 지원 되지 않습니다. 팀 vNICs 하려고 수 완전히 손실 통신 네트워크 오류 발생 하는 경우.  
  
-   커널 디버그 네트워크 어댑터 (KDNIC)입니다.  
  
-   네트워크 부팅에 사용 되는 Nic입니다.  
  
-   이더넷, WWAN, WLAN/Wi-fi, 블루투스, Infiniband, Infiniband (IPoIB) Nic를 통해 인터넷 프로토콜을 포함 하 여 등 이외의 기술을 사용 하는 nic가 있습니다.  
  
## <a name="compatibility"></a>호환성  
NIC 팀은 다음과 같은 예외가 Windows Server 2016의 모든 네트워킹 기술과 호환 됩니다.  
  
-   **단일 루트 I/O 가상화 (SR-IOV)** 합니다. SR-IOV를 데이터 (가상화의 경우 표시 되는 호스트 운영 체제)에서 네트워킹 스택을 통과 하지 않고 NIC에 직접 배달 됩니다. 따라서 NIC 팀을 검사 하거나 데이터를 팀의 다른 경로로 리디렉션할 수 없는 합니다.  
  
-   **기본 호스트 서비스 품질 (QoS)** 합니다. 설정 하는 경우 네이티브 또는 호스트 시스템에서 QoS 정책 및 이러한 정책을 호출 최소 대역폭 제한, NIC 팀에 대 한 전반적인 처리량이 위치에 대역폭 정책 없이 것 보다 작습니다.  
  
-   **TCP Chimney**합니다. TCP Chimney 오프 로드는 NIC에 직접 전체 네트워킹 스택에서 때문에 NIC 팀과 TCP Chimney는 사용할 수 없습니다.  
  
-   **802.1 X 인증**합니다. 일부 스위치 802.1 X 인증 및 NIC 팀에서 동일한 포트 구성을 허용 하지 않기 때문에 802.1 X 인증 NIC 팀과 함께 사용 하지 해야 합니다.  
  
NIC 팀을 사용 하 여 Hyper-v 호스트에서 실행 되는 가상 머신 (Vm) 내에서 대 한 자세한 내용은 참조 하세요 [호스트 컴퓨터 또는 VM에서 새 NIC 팀 만들기](Create-a-New-NIC-Team-on-a-Host-Computer-or-VM.md)합니다.
  
## <a name="virtual-machine-queues-vmqs"></a>가상 머신 큐 (Vmq)  

Vmq는 각 VM에 대 한 큐를 할당 하는 NIC 기능입니다.  Hyper-v 사용 해야 언제 든 지 VMQ 설정할 수도 있습니다. Windows Server 2016 Vmq는 vPort에 할당 된 단일 큐를 사용 하 여 NIC 스위치 vPorts 동일한 기능을 제공 하려면 사용 합니다. 

스위치 구성 모드 및 부하 분산 알고리즘에 따라 NIC 팀 표시 (최소 큐 모드) 팀의 모든 어댑터에서 사용 가능 하 고 지원 되는 큐의 가장 작은 수 또는 사용할 수 있는 큐의 총 모든 팀 멤버 (큐의 Sum 모드)입니다.  

팀은 스위치 독립 팀 모드 Hyper-v 포트 모드 또는 동적 모드에 부하 분산을 설정 하는 경우 보고 큐의 수는 팀 멤버 (큐의 Sum 모드)에서 사용할 수 있는 모든 큐의 합계입니다. 그렇지 않은 경우 보고 큐의 수 (최소 큐 모드) 팀의 모든 구성원에서 지 원하는 큐의 가장 작은 수 경우

그 이유는 다음과 같습니다.  
  
-   스위치 독립 팀의 경우 Hyper-v 포트 모드 또는 동적 모드 Hyper-v 스위치 포트 (VM)에 대 한 인바운드 트래픽을 항상 동일한 팀 멤버에 도착 합니다. 호스트 수를 예측/제어 멤버 NIC 팀 특정 팀 멤버에 할당 하는 VMQ 큐에 대 한 보다 철저 하 게 될 수 있도록 특정 VM에 대 한 트래픽을 수신 합니다. NIC 팀을 Hyper-v 스위치를 사용 하 여 작업 정확 하 게 하나의 팀 구성원에는 VM에 대 한 VMQ를 설정 하 고 인바운드 트래픽이 해당 큐에 도달 하를 알아야 합니다.  
  
-   스위치 종속 모드 (정적 팀 또는 팀 LACP)에서 팀의 경우 팀에 연결 된 스위치 인바운드 트래픽 배포를 제어 합니다. 호스트의 NIC 팀 소프트웨어 있는 팀 멤버는 인바운드 트래픽을 VM에 대 한 가져옵니다 예측할 수 없습니다 및 스위치는 VM에 대 한 트래픽을 모든 팀 구성원 간에 배포 수 있습니다. NIC 팀 소프트웨어를 Hyper-v 스위치를 사용 하 여 작업의 결과에 모든 팀 멤버 VM에 대 한 큐 프로그램, 처럼 하나 뿐 아니라 팀 멤버.  
  
-   팀은 스위치 독립 모드 및 사용 하 여 주소 해시 부하 분산 경우 인바운드 트래픽을 항상는 nic 1 개 (기본 팀 구성원)-단지 한 팀 멤버에 모두 있습니다. 다른 팀 멤버는 인바운드 트래픽을 처리 되지, 이후와 프로그래밍 가져올 주 구성원으로 동일한 큐 주 구성원에 실패 하면 다른 팀 멤버를 사용 하 여 인바운드 트래픽을 집어 수 및 큐가 이미 진행에서 되도록 합니다.  

- 대부분의 Nic 수신 RSS (수신측 배율) 또는 VMQ, 하지만 하지 동시에 사용 되는 큐를 가집니다. 일부 VMQ 설정을 RSS 큐에 대 한 설정을 보이지만 기능에 따라 RSS 및 VMQ를 모두 사용 하 여 현재 사용 중인 일반 큐에 설정 됩니다. 각 NIC에는 고급 속성에서 값에 대 한 * RssBaseProcNumber 및 \*MaxRssProcessors 합니다. 다음은 시스템 성능을 향상 시키는 몇 가지 VMQ 설정입니다.  
  
-   각 NIC 있어야 이상적으로 * 보다 크거나 같은 RssBaseProcNumber 짝수 설정 2 (2). 첫 번째 물리적 프로세서 코어 0 (논리적 프로세서 0과 1)이 실제 프로세서에서 네트워크 처리 유도 해야 하므로 시스템 처리 과정의 대부분 일반적으로 수행 합니다. 일부 컴퓨터 아키텍처에는 실제 프로세서당 두 개의 논리 프로세서 없는 하므로 1 보다 크거나 같은 경우 이러한 컴퓨터의 기본 프로세서 이어야 합니다. 경우 확실 하지 않은 가정 호스트 2 개의 논리 프로세서를 사용 하 여 실제 프로세서 아키텍처 당 됩니다.  
  
-   팀이 큐의 Sum 모드인 경우 팀 구성원의 프로세서는 겹치지 않는 이어야 합니다. 예를 들어 4 코어와 호스트의 논리 프로세서가 8의 2 10Gbps Nic 팀을 사용 하 여 설정할 수 있습니다 2의 기본 프로세서를 사용 하 고 4 개의 코어를 사용 하 여 첫 번째 두 번째 6 기본 프로세서를 사용 하 여 2 개 코어를 사용 하 여 설정 됩니다.  
  
-   최소 큐 모드에서 팀은 팀 멤버에 의해 사용 되는 프로세서 집합 동일 해야 합니다.  

  
## <a name="hyper-v-network-virtualization-hnv"></a>Hyper-V 네트워크 가상화(HNV)  
NIC 팀은 완전히 호환 Hyper-v 네트워크 가상화 (HNV)를 사용 합니다.  NIC 팀 HNV 트래픽을 최적화 하는 방식으로 부하를 분산할 수 있는 NIC 팀 드라이버에 대 한 정보를 제공 하는 HNV 관리 시스템입니다.  
  
## <a name="live-migration"></a>실시간 마이그레이션  
Vm의 NIC 팀의 실시간 마이그레이션 영향을 주지 않습니다. VM의 NIC 팀 구성 여부 실시간 마이그레이션에 대 한 동일한 규칙이 있습니다.  


## <a name="virtual-local-area-networks-vlans"></a>Virtual Local Area Network (Vlan)
NIC 팀을 사용 하면 여러 팀 인터페이스가 만들면 호스트를 동시에 서로 다른 Vlan에 연결할 수 있습니다. 다음 지침을 사용 하 여 환경을 구성 합니다.
  
- NIC 팀을 사용 하기 전에 호스트 (promiscuous) 트렁크 모드를 사용 하 여 팀에 연결 된 물리적 스위치 포트를 구성 합니다. 실제 스위치는 트래픽을 수정 하지 않고 필터링에 대 한 호스트에 모든 트래픽을 전달 해야 합니다.  

- 고급 속성 설정 NIC를 사용 하 여 Nic에 VLAN 필터를 구성 하지 마세요. NIC 팀 소프트웨어 또는 Hyper-v 가상 스위치 (있는 경우) VLAN 필터링을 수행할 수 있습니다.  
  
### <a name="use-vlans-with-nic-teaming-in-a-vm"></a>VM에서 NIC 팀과 함께 사용 되는 Vlan  
팀에서 Hyper-v 가상 스위치에 연결할 때 Hyper-v 가상 스위치 대신 NIC 팀에서 모든 VLAN 분리 수행 되어야 합니다.  

다음 지침을 사용 하 여 NIC 팀을 사용 하 여 구성 된 VM에서 Vlan을 사용 하도록 계획:
  
-   Hyper-v 가상 스위치에서 여러 포트를 사용 하 여 VM을 구성 하 고 VLAN을 사용 하 여 각 포트를 연결 하는 일반적인된 방법은 VM에서 여러 Vlan을 지 원하는 경우 이렇게 하면 네트워크 통신 문제 때문에 VM에서 이러한 포트를 팀 하지 않습니다.  

-   VM에 여러 SR-IOV 가상 함수 (VFs) 하는 경우 VM에서 해당 팀을 구성 하기 전에 동일한 VLAN에 되는지 확인 합니다. 서로 다른 Vlan에 배치 해야 다른 VFs를 구성 하려면 쉽게 수 있으며 이렇게 하면 네트워크 통신 문제입니다.  
 
  
### <a name="manage-network-interfaces-and-vlans"></a>네트워크 인터페이스 및 Vlan 관리 
둘 이상의 VLAN 게스트 운영 체제에 노출 해야 하는 경우에 인터페이스에 할당 된 VLAN을 명확 하 게 이더넷 인터페이스 이름을 변경 하는 것이 좋습니다. 예를 들어, 연결 하는 경우 **이더넷** VLAN 12를 사용 하 여 인터페이스와 **이더넷 2** VLAN 48 인터페이스, 이더넷 인터페이스 이름 바꾸기에 **EthernetVLAN12** 및 다른 **EthernetVLAN48**합니다. 

Windows PowerShell 명령을 사용 하 여 인터페이스 이름 바꾸기 **이름 바꾸기 NetAdapter** 다음 절차를 수행 하 여:
  
1.  서버 관리자에서의 **속성** 네트워크 어댑터의 이름을 변경 하려는 경우 네트워크 어댑터 이름 오른쪽의 링크를 클릭 합니다. 
  
2.  이름 바꾸기 및 선택 하려는 네트워크 어댑터를 마우스 오른쪽 단추로 클릭 **이름 바꾸기**합니다.  
  
3.  네트워크 어댑터에 대 한 새 이름을 입력 하 고 ENTER 키를 누릅니다.  


## <a name="virtual-machines-vms"></a>Virtual Machines (Vm)

VM에서 NIC 팀을 사용 하려는 경우 외부 Hyper-v 가상 스위치에만 VM의 가상 네트워크 어댑터를 연결 해야 합니다. 이렇게 하면 VM이 실패 한 가상 스위치에 연결 된 실제 네트워크 어댑터 중 하나 또는 연결이 끊어진 경우 상황에도 네트워크 연결을 유지 합니다. 내부 또는 전용 Hyper-v 가상 스위치에 연결 된 가상 네트워크 어댑터 팀에서 네트워킹 VM에 대 한 실패 했을 때 스위치에 연결 하지 못합니다.  
  
Windows Server 2016에서 NIC 팀 Vm의 두 멤버가 포함 된 팀을 지원합니다. 규모가 큰 팀을 만들 수 있지만 더 큰 팀을 위한 지원 되지 않습니다. 모든 팀 멤버는 다른 외부 Hyper-v 가상 스위치에 연결 해야 하 고 VM의 네트워킹 인터페이스 팀을 허용 하도록 구성 해야 합니다.

  
VM에서 NIC 팀을 구성 하는 경우에 선택 해야는 **팀 모드** 의 _독립 스위치_ 와 **부하 분산 모드** 의 _주소 해시_.   
  
  
## <a name="sr-iov-capable-network-adapters"></a>SR IOV 가능 네트워크 어댑터  
Hyper-v 스위치를 통과 하지 않으면 문제가 또는 Hyper-v 호스트에서 NIC 팀 SR-IOV 트래픽은 보호할 수 없습니다.  VM NIC 팀 구성 옵션을 두 개의 외부 Hyper-v 가상 스위치를 구성할 수 있습니다, 각각 SR IOV 지원 NIC에 연결 된  
  
![NIC SR IOV 가능 네트워크 어댑터 팀](../../media/NIC-Teaming-in-Virtual-Machines--VMs-/nict_in_vm.jpg)  
  
각 VM에는 가상 함수 (VF)에서 하나 또는 두 개의 SR-IOV Nic, NIC 연결 끊기 (VF) 백업 어댑터로 기본 VF 으로부터 장애 조치가 발생할 경우 있을 수 있습니다. 또는 VM에는 다른 가상 스위치에 연결 된 NIC 및 비 VF vmNIC 하나에서 VF 있을 수 있습니다. VF와 관련 된 NIC의 연결이 끊어지거나, 트래픽이 다른 스위치로 연결의 손실 없이 장애 조치 수 있습니다.  
  
트래픽이 다른 vmNIC의 MAC 주소를 사용 하 여 전송 VM의 Nic 간에 장애 조치가 발생할 수 있습니다, NIC 팀을 사용 하 여 VM과 연결 된 각 Hyper-v 가상 스위치 포트 팀을 허용 하도록 설정 해야 합니다. 


## <a name="related-topics"></a>관련 항목

- [NIC 팀 MAC 주소 사용 및 관리](NIC-Teaming-MAC-Address-Use-and-Management.md): 스위치 독립 모드 주소 해시 또는 동적 부하 분산을 사용 하 여 NIC 팀을 구성한 경우 미디어 액세스 팀에서는 아웃 바운드 트래픽에 대해 기본 NIC 팀 구성원의 (MAC) 주소를 제어 합니다. 기본 NIC 팀 멤버가 팀 멤버의 초기 집합에서 운영 체제에서 선택한 네트워크 어댑터입니다.

- [NIC 팀 설정](nic-teaming-settings.md): 이 항목에서는 팀 같은 NIC 팀 속성의 개요를 제공 하 고 부하 분산 모드. 또한 제공 대기 어댑터 설정 및 기본 팀 인터페이스 속성에 대 한 세부 정보입니다. NIC 팀을 두 개 이상의 네트워크 어댑터가 있는 경우 내결함성을 위해 대기 어댑터를 지정할 필요가 없습니다.
  
- [호스트 컴퓨터 또는 VM에서 새 NIC 팀 만들기](Create-a-New-NIC-Team-on-a-Host-Computer-or-VM.md): 이 항목에서는 호스트 컴퓨터 또는 Windows Server 2016을 실행 중인 Hyper-v 가상 컴퓨터 (VM)에서 새 NIC 팀을 만듭니다.

- [NIC 팀 문제 해결](Troubleshooting-NIC-Teaming.md): 이 항목에서는 하드웨어와 물리적 스위치 securities에서 Windows PowerShell을 사용 하 여 네트워크 어댑터를 사용 하지 않도록 설정 또는 사용 하도록 설정 하면 NIC 팀을 해결 하는 방법을 설명 합니다. 
 
