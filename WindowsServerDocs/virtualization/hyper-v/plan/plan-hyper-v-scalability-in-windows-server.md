---
title: Windows Server 2016의 Hyper-v 확장성에 대 한 계획
description: 최대 수를 지원 되는 구성 요소를 추가 하거나 Hyper-v 및 virtual machines에서 제거할 수는 얼마나 많은 메모리 등 가상 프로세서 수입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
author: KBDAzure
ms.author: kathydav
ms.date: 09/28/2016
ms.openlocfilehash: 03a464269c8aea29c226dee776f0dfacfe48743a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850264"
---
# <a name="plan-for-hyper-v-scalability-in-windows-server-2016"></a>Windows Server 2016의 Hyper-v 확장성에 대 한 계획

> 적용 대상: Windows Server 2016
  
이 문서에서는 구성 요소를 추가 하 고 Hyper-v 호스트 또는 가상 프로세서 또는 검사점 같은 해당 가상 컴퓨터에서 제거할 수 있습니다에 대 한 최대 구성에 대 한 세부 정보를 제공 합니다. 배포를 계획할 때에 각 가상 컴퓨터 뿐만 아니라 Hyper-v 호스트에 적용 되는 것에 적용 되는 최대값을 것이 좋습니다. 

메모리 및 논리적 프로세서에 대 한 최대값은 machine learning 및 데이터 분석과 같은 새로운 시나리오를 지원 하기 위해 요청에 따라에서 Windows Server 2012에서 가장 큰 증가 합니다. Windows Server 블로그 최근 5.5 테라바이트의 4TB 메모리 내 데이터베이스를 실행 하는 128 가상 프로세서 및 메모리와 가상 컴퓨터의 성능 결과 게시 합니다. 성능 실제 서버의 성능의 95% 보다 큽니다. 자세한 내용은 다음을 참조 하십시오. [메모리 내 트랜잭션 처리를 위해 Windows Server 2016 Hyper-v 대규모 VM 성능](https://blogs.technet.microsoft.com/windowsserver/2016/09/28/windows-server-2016-hyper-v-large-scale-vm-performance-for-in-memory-transaction-processing/)합니다. 다른 번호는 Windows Server 2012에 적용 되는 것과 비슷합니다. \(Windows Server 2012 R2에 대 한 최대값 된 Windows Server 2012와 동일 합니다.\) 
  
> [!NOTE]  
> System Center VMM(Virtual Machine Manager)에 대한 자세한 내용은 [Virtual Machine Manager](https://technet.microsoft.com/system-center-docs/vmm/vmm)를 참조하세요. VMM은 별도로 판매되는 가상화된 데이터 센터를 관리하기 위한 Microsoft 제품입니다.  
  
## <a name="maximums-for-virtual-machines"></a>가상 머신에 대 한 최대값  
이러한 최대값 각 가상 컴퓨터에 적용 됩니다. 일부 구성 요소는 두 세대의 가상 컴퓨터가 사용할 수 있습니다. 세대의 비교를 참조 하세요. [Hyper-v에 1 또는 2 세대 가상 컴퓨터를 만들 해야?](should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v.md) 
  
|구성 요소|최대값|참고|  
|-------------|-----------|---------|  
|검사점|50|사용 가능한 저장소에 따라 실제 수가 이보다 적을 수 있습니다. 각 검사점은 실제 저장소를 사용 하는.avhd 파일로 저장 됩니다.|  
|메모리|12TB; 2 세대 <br>1 세대 1 TB|특정 운영 체제의 요구 사항을 검토하여 최소 및 권장 용량을 확인할 수 있습니다.|  
|직렬(COM) 포트|2|없음|  
|가상 컴퓨터에 직접 연결된 실제 디스크의 크기|상황에 따라 다름|최대 크기는 게스트 운영 체제에 따라 결정됩니다.|  
|가상 파이버 채널 어댑터|4|각 가상 파이버 채널 어댑터를 서로 다른 가상 SAN에 연결하는 것이 가장 좋습니다.|  
|가상 플로피 장치|1개의 가상 플로피 드라이브|없음|
|가상 하드 디스크 용량|VHDX 형식으로의 경우 64TB<br>VHD 형식에 대 한 2040GB|각 가상 하드 디스크는 가상 하드 디스크에서 사용하는 형식에 따라 .vhdx 또는 .vhd 파일로 실제 미디어에 저장됩니다.|  
|가상 IDE 디스크|4|IDE 장치 중 하나에 시동 디스크 (부팅 디스크 라고도 함)를 연결 해야 합니다. 시동 디스크는 가상 하드 디스크이거나 가상 컴퓨터에 직접 연결된 실제 디스크일 수 있습니다.|  
|가상 프로세서|240; 2 세대<br>1 세대 64<br>320 호스트 OS (루트 파티션)에 사용할 수 있습니다.|게스트 운영 체제에서 지원되는 가상 프로세서 수는 이보다 적을 수 있습니다. 자세한 내용은 특정 운영 체제에 대 한 게시 된 정보를 참조 하세요.|
|가상 SCSI 컨트롤러|4|가상 SCSI 장치 지원 되는 게스트 운영 체제에 사용할 수 있는 통합 서비스에 필요 합니다. 운영 체제를 지원 세부 정보를 참조 하세요 [지원 되는 Linux 및 FreeBSD virtual machines](../Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md) 하 고 [지원 되는 Windows 게스트 운영 체제](../supported-windows-guest-operating-systems-for-hyper-v-on-windows.md)합니다.|  
|가상 SCSI 디스크|256|SCSI 컨트롤러마다 최대 64개의 디스크를 지원합니다. 즉, 각 가상 컴퓨터에 최대 256개의 가상 SCSI 디스크를 구성할 수 있습니다 (4개의 컨트롤러 x 컨트롤러당 64개의 디스크).|  
|가상 네트워크 어댑터|총 12:<br> -8에서 Hyper-v 특정 네트워크 어댑터<br>-4 레거시 네트워크 어댑터|Hyper-v 특정 네트워크 어댑터 더 나은 성능을 제공 하 고 integration services에 포함 하는 드라이버가 필요 합니다. 자세한 내용은 [Windows Server에서 Hyper-v 네트워킹에 대 한 계획](plan-hyper-v-networking-in-windows-server.md)합니다.|  
  
## <a name="maximums-for-hyper-v-hosts"></a>Hyper-v 호스트에 대 한 최대값  
이러한 최대값 각 Hyper-v 호스트에 적용 됩니다.  
  
|구성 요소|최대값|참고|  
|-------------|-----------|---------|  
|논리 프로세서|512|펌웨어 둘 다 사용할 수 있어야 합니다.<br /><br />-하드웨어 기반 가상화<br />-하드웨어 적용 데이터 실행 방지 (DEP)<br /><br />호스트 OS (루트 파티션)는 최대 320 개의 논리 프로세서에만 표시|  
|메모리|24TB|없음|  
|네트워크 어댑터 팀(NIC 팀)|Hyper-V에서 부과하는 제한은 없음|자세한 내용은 참조 하세요 [NIC 팀](../../../networking/technologies/nic-teaming/NIC-Teaming.md)합니다.|  
|실제 네트워크 어댑터|Hyper-V에서 부과하는 제한은 없음|없음|  
|서버당 실행되는 가상 컴퓨터|1024|없음|  
|스토리지|호스트 운영 체제에서 원하는 것으로 제한 됩니다. Hyper-V에서 부과하는 제한은 없음|**참고:** SMB 3.0을 사용 하는 경우 Microsoft network attached storage (NAS)를 지원 합니다. NFS 기반 저장소 지원되지 않습니다.|
|서버당 가상 네트워크 스위치 포트|다양하며 Hyper-V에서 부과하는 제한은 없음|사용 가능한 컴퓨팅 리소스에 따라 실제 제한이 달라집니다.|  
|논리 프로세서당 가상 프로세서|Hyper-V에서 부과하는 속도는 없음|없음|  
|서버당 가상 프로세서|2048|없음|  
|가상 SAN(저장 영역 네트워크)|Hyper-V에서 부과하는 제한은 없음|없음|  
|가상 스위치|다양하며 Hyper-V에서 부과하는 제한은 없음|사용 가능한 컴퓨팅 리소스에 따라 실제 제한이 달라집니다.|  
 
## <a name="failover-clusters-and-hyper-v"></a>장애 조치(failover) 클러스터와 Hyper-V  
이 표에 Hyper-v 및 장애 조치 클러스터링을 사용 하는 경우 적용 되는 최대 구성이 나와 있습니다. 클러스터 된 환경에서 모든 가상 컴퓨터를 실행 하려면 충분 한 하드웨어 리소스가 있을 수 있도록 용량 계획을 수행 하는 것이 반드시 합니다.  

장애 조치 클러스터링, virtual machines에 대 한 새 기능에 대 한 업데이트에 알아보려면 [What's New in Windows Server 2016의 장애 조치 클러스터링](../../../failover-clustering/whats-new-in-failover-clustering.md)합니다.

|구성 요소|최대값|참고|  
|-------------|-----------|---------|  
|클러스터당 노드|64|업데이트 적용 같은 유지 보수 작업과 장애 조치를 위해 예약할 노드의 수를 고려해 봅니다. 노드 하나를 장애 조치용으로 예약함으로써 다른 노드로 장애 조치하기까지 유휴 상태로 대기시킬 수 있도록 충분한 리소스 계획을 수립하는 것이 좋습니다. 이러한 노드를 종종 패시브 노드라고도 합니다. 노드를 더 예약하려면 이 수를 늘릴 수 있습니다. 권장 되는 비율 또는 승수 액티브 노드 대비 예약 된 노드의 없습니다. 유일한 요구 사항인 총 클러스터의 노드 수가 최대 64 개를 초과할 수 없습니다.|  
|클러스터 및 노드당 실행 가상 컴퓨터|클러스터당 8,000개|여러 가지 요인 실행할 수 있습니다. 있습니다 동시에 한 노드에서 같은 가상 컴퓨터의 실제 수에 영향을 줄 수 있습니다.:<br />-각 가상 컴퓨터에서 사용 중인 실제 메모리의 양입니다.<br />-네트워킹 및 저장소 대역폭입니다.<br />-디스크 스핀 들 수, 디스크 I/O 성능에 영향을 줍니다.|  
  

