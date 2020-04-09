---
title: Windows Server 2016 및 Windows Server 2019에서 Hyper-v 확장성 계획
description: 'Hyper-v 및 가상 컴퓨터에서 추가 하거나 제거할 수 있는 구성 요소에 대해 지원 되는 최대 수를 나열 합니다 (예: 메모리 양과 가상 프로세서 수).'
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
author: kbdazure
ms.author: kathydav
ms.date: 09/28/2016
ms.openlocfilehash: 2eb75283f68a1d1e0c05397b67d9c012d0adc899
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860756"
---
# <a name="plan-for-hyper-v-scalability-in-windows-server-2016-and-windows-server-2019"></a>Windows Server 2016 및 Windows Server 2019에서 Hyper-v 확장성 계획

> 적용 대상: Windows Server 2016, Windows Server 2019
  
이 문서에서는 Hyper-v 호스트 또는 가상 컴퓨터 (예: 가상 프로세서 또는 검사점)에서 추가 하 고 제거할 수 있는 구성 요소의 최대 구성에 대 한 세부 정보를 제공 합니다. 배포를 계획할 때 각 가상 머신에 적용 되는 최대값 및 Hyper-v 호스트에 적용 되는 최대값을 고려 합니다. 

메모리 및 논리 프로세서의 최대값은 Windows Server 2012에서 가장 큰 것으로, machine learning 및 데이터 분석과 같은 새로운 시나리오를 지원 하기 위한 요청에 대 한 응답으로 제공 됩니다. Windows Server 블로그 최근 5.5 테라바이트의 4TB 메모리 내 데이터베이스를 실행 하는 128 가상 프로세서 및 메모리와 가상 컴퓨터의 성능 결과 게시 합니다. 성능은 물리적 서버 성능의 95% 이상입니다. 자세한 내용은 다음을 참조 하십시오. [메모리 내 트랜잭션 처리를 위해 Windows Server 2016 Hyper-v 대규모 VM 성능](https://blogs.technet.microsoft.com/windowsserver/2016/09/28/windows-server-2016-hyper-v-large-scale-vm-performance-for-in-memory-transaction-processing/)합니다. 다른 숫자는 Windows Server 2012에 적용 되는 것과 비슷합니다. Windows Server 2012 r 2에 대 한 \(최대값은 Windows Server 2012와 동일 합니다.\) 
  
> [!NOTE]  
> System Center VMM(Virtual Machine Manager)에 대한 자세한 내용은 [Virtual Machine Manager](https://technet.microsoft.com/system-center-docs/vmm/vmm)를 참조하세요. VMM은 별도로 판매되는 가상화된 데이터 센터를 관리하기 위한 Microsoft 제품입니다.  
  
## <a name="maximums-for-virtual-machines"></a>가상 컴퓨터의 최대값  
이러한 최대값은 각 가상 컴퓨터에 적용 됩니다. 모든 구성 요소를 두 세대의 가상 컴퓨터에서 사용할 수 있는 것은 아닙니다. 세대를 비교 하려면 [hyper-v에서 1 세대 또는 2 세대 가상 머신을 만들어야 하나요?](should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v.md) 를 참조 하세요. 
  
|구성 요소|최대값|참고|  
|-------------|-----------|---------|  
|검사점|50|사용 가능한 스토리지에 따라 실제 수가 이보다 적을 수 있습니다. 각 검사점은 실제 저장소를 사용 하는 .avhd 파일로 저장 됩니다.|  
|메모리|2 세대의 경우 12tb <br>1tb (1 세대)|특정 운영 체제의 요구 사항을 검토하여 최소 및 권장 용량을 확인할 수 있습니다.|  
|직렬(COM) 포트|2|None.|  
|가상 컴퓨터에 직접 연결된 실제 디스크의 크기|상황에 따라 다름|최대 크기는 게스트 운영 체제에 따라 결정됩니다.|  
|가상 파이버 채널 어댑터|4|각 가상 파이버 채널 어댑터를 서로 다른 가상 SAN에 연결하는 것이 가장 좋습니다.|  
|가상 플로피 디바이스|1개의 가상 플로피 드라이브|None.|
|가상 하드 디스크 용량|VHDX 형식의 경우 64 TB<br>VHD 형식의 2040 GB|각 가상 하드 디스크는 가상 하드 디스크에서 사용하는 형식에 따라 .vhdx 또는 .vhd 파일로 실제 미디어에 저장됩니다.|  
|가상 IDE 디스크|4|시작 디스크 (부팅 디스크 라고도 함)를 IDE 장치 중 하나에 연결 해야 합니다. 시동 디스크는 가상 하드 디스크이거나 가상 컴퓨터에 직접 연결된 실제 디스크일 수 있습니다.|  
|가상 프로세서|2 세대의 경우 240;<br>64 세대의 경우 1;<br>320 호스트 OS에서 사용할 수 있음 (루트 파티션)|게스트 운영 체제에서 지원되는 가상 프로세서 수는 이보다 적을 수 있습니다. 자세한 내용은 특정 운영 체제에 대해 게시 된 정보를 참조 하십시오.|
|가상 SCSI 컨트롤러|4|가상 SCSI 장치를 사용 하려면 지원 되는 게스트 운영 체제에 사용할 수 있는 integration services가 필요 합니다. 지원 되는 운영 체제에 대 한 자세한 내용은 [지원 되는 Linux 및 FreeBSD 가상 컴퓨터](../Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md) 및 [지원 되는 Windows 게스트 운영 체제](../supported-windows-guest-operating-systems-for-hyper-v-on-windows.md)를 참조 하세요.|  
|가상 SCSI 디스크|256|SCSI 컨트롤러마다 최대 64개의 디스크를 지원합니다. 즉, 각 가상 컴퓨터에 최대 256개의 가상 SCSI 디스크를 구성할 수 있습니다 (4개의 컨트롤러 x 컨트롤러당 64개의 디스크).|  
|가상 네트워크 어댑터|Windows Server 2016은 총 12 개를 지원 합니다.<br> -8 hyper-v 특정 네트워크 어댑터<br>-4 레거시 네트워크 어댑터 <br> Windows Server 2019은 68 합계를 지원 합니다. <br> -64 hyper-v 관련 네트워크 어댑터<br>-4 레거시 네트워크 어댑터  |Hyper-v 특정 네트워크 어댑터는 더 나은 성능을 제공 하며 integration services에 포함 된 드라이버가 필요 합니다. 자세한 내용은 [Windows Server에서 hyper-v 네트워킹 계획](plan-hyper-v-networking-in-windows-server.md)을 참조 하세요.|  
  
## <a name="maximums-for-hyper-v-hosts"></a>Hyper-v 호스트의 최대값  
이러한 최대값은 각 Hyper-v 호스트에 적용 됩니다.  
  
|구성 요소|최대값|참고|  
|-------------|-----------|---------|  
|논리 프로세서|512|이러한 두 가지 모두 펌웨어에서 사용 하도록 설정 해야 합니다.<p>-하드웨어 지원 가상화<br />-하드웨어 적용 DEP (데이터 실행 방지)<p>호스트 OS (루트 파티션)에는 최대 320 논리 프로세서만 표시 됩니다.|  
|메모리|24TB|None.|  
|네트워크 어댑터 팀(NIC 팀)|Hyper-V에서 부과하는 제한은 없음|자세한 내용은 [NIC 팀](../../../networking/technologies/nic-teaming/NIC-Teaming.md)을 참조 하세요.|  
|실제 네트워크 어댑터|Hyper-V에서 부과하는 제한은 없음|None.|  
|서버당 실행되는 가상 컴퓨터|1024|None.|  
|저장 공간|호스트 운영 체제에서 지원 되는 항목에 의해 제한 됩니다. Hyper-V에서 부과하는 제한은 없음|**참고:** Microsoft에서는 SMB 3.0를 사용할 때 NAS (네트워크 연결 저장소)를 지원 합니다. NFS 기반 스토리지 지원되지 않습니다.|
|서버당 가상 네트워크 스위치 포트|다양하며 Hyper-V에서 부과하는 제한은 없음|사용 가능한 컴퓨팅 리소스에 따라 실제 제한이 달라집니다.|  
|논리 프로세서당 가상 프로세서|Hyper-V에서 부과하는 속도는 없음|None.|  
|서버당 가상 프로세서|2048|None.|  
|가상 SAN(저장 영역 네트워크)|Hyper-V에서 부과하는 제한은 없음|None.|  
|가상 스위치|다양하며 Hyper-V에서 부과하는 제한은 없음|사용 가능한 컴퓨팅 리소스에 따라 실제 제한이 달라집니다.|  
 
## <a name="failover-clusters-and-hyper-v"></a>장애 조치(failover) 클러스터와 Hyper-V  
다음 표에서는 Hyper-v 및 장애 조치 (Failover) 클러스터링을 사용할 때 적용 되는 최대값을 보여 줍니다. 클러스터 된 환경에서 모든 가상 컴퓨터를 실행 하는 데 충분 한 하드웨어 리소스가 있는지 확인 하기 위해 용량 계획을 수행 하는 것이 중요 합니다.  

가상 컴퓨터에 대 한 새로운 기능을 비롯 한 장애 조치 (Failover) 클러스터링 업데이트에 대 한 자세한 내용은 [Windows Server 2016 장애 조치 (Failover) 클러스터링의 새로운](../../../failover-clustering/whats-new-in-failover-clustering.md)기능을 참조 하세요.

|구성 요소|최대값|참고|  
|-------------|-----------|---------|  
|클러스터당 노드|64|업데이트 적용 같은 유지 보수 작업과 장애 조치를 위해 예약할 노드의 수를 고려해 봅니다. 노드 하나를 장애 조치용으로 예약함으로써 다른 노드로 장애 조치하기까지 유휴 상태로 대기시킬 수 있도록 충분한 리소스 계획을 수립하는 것이 좋습니다. (수동 노드 라고도 합니다.) 추가 노드를 예약 하려는 경우이 수를 늘릴 수 있습니다. 활성 노드에 대 한 예약 된 노드의 비율 또는 승수는 권장 되지 않습니다. 유일한 요구 사항은 클러스터의 총 노드 수가 최대 64을 초과 하지 않아야 한다는 것입니다.|  
|클러스터 및 노드당 실행 가상 컴퓨터|클러스터당 8,000개|다음과 같이 한 노드에서 동시에 실행할 수 있는 가상 컴퓨터의 실제 수에 영향을 줄 수 있는 몇 가지 요인이 있습니다.<br />-각 가상 컴퓨터에 사용 되는 실제 메모리의 양입니다.<br />-네트워킹 및 저장소 대역폭.<br />-디스크 i/o 성능에 영향을 주는 디스크 스핀 들 수입니다.|  
  

