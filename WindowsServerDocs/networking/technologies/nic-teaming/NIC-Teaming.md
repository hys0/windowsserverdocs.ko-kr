---
title: NIC 팀
description: 이 항목에서는 네트워크 인터페이스 카드 (NIC) 팀 구성 Windows Server 2016에 대 한 개요입니다.
manager: brianlic
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
ms.openlocfilehash: 142f56153187368effdb802c0c1b50359fffc36a
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="nic-teaming"></a>NIC 팀

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목에서는 네트워크 인터페이스 카드 (NIC) 팀 구성 Windows Server 2016에 대 한 개요입니다.

> [!NOTE]  
> 이 항목 외에 다음과 같은 NIC 팀 콘텐츠를 사용할 수 있습니다.  
>   
> - [NIC 팀에서 가상 컴퓨터 및 #40; Vm & #41;](nict-vms.md)
> - [NIC 팀 및 가상 영역 로컬 네트워크 & #40; Vlan & #41;](nict-and-vlans.md)
> - [NIC 팀 MAC 주소 사용 및 관리](NIC-Teaming-MAC-Address-Use-and-Management.md)
> - [NIC 팀 문제 해결](Troubleshooting-NIC-Teaming.md) 
> - [새 NIC 팀 호스트 컴퓨터 또는 VM 만들기](Create-a-New-NIC-Team-on-a-Host-Computer-or-VM.md)
> - [NIC 팀에서 Windows PowerShell Cmdlet (NetLBFO)](https://technet.microsoft.com/library/jj130849.aspx)
> - TechNet 갤러리 다운로드: [Windows Server 2016 NIC 및 스위치 Embedded 팀 사용자 가이드](https://gallery.technet.microsoft.com/Windows-Server-2016-839cb607?redir=0)
  
## <a name="bkmk_over"></a>NIC 팀 개요  
NIC 팀 1과 2 30 물리적 이더넷 네트워크 어댑터에 하나 이상의 소프트웨어 기반 가상 네트워크 어댑터를 그룹화 할 수 있게 합니다. 이러한 가상 네트워크 어댑터 빠른 성능 및 네트워크 어댑터 오류가 발생할 경우 오류 허용 제공합니다.  
  
NIC 팀 멤버 네트워크 어댑터 모두 팀에 동일한 실제 호스트 컴퓨터에 설치 해야 합니다.  
  
> [!NOTE]  
> 네트워크 어댑터가 하나만 포함 된 NIC 팀 수 없는 부하 분산 및 장애 조치; 제공 그러나 네트워크 어댑터와 함께 사용할 수 있습니다 NIC 팀의 트래픽 분리에 대 한 가상 영역 로컬 네트워크 (Vlan)을 사용 중인 경우 합니다.  
  
NIC 팀에 네트워크 어댑터를 구성할 때 NIC 팀 솔루션 일반적인 코어, 다음 하나 이상의 가상 어댑터 (팀 Nic [tNICs] 또는 팀 인터페이스 라고도 함)의 운영 체제를 표시 하는 연결 합니다. Windows Server 2016 최대 32 팀 인터페이스 당 팀을 지원합니다. 알고리즘 Nic 사이의 아웃 바운드 교통 (부하)을 배포 하는 여러 가지가 있습니다.  
  
다음 그림에서는 NIC 팀 여러 tNICs 보여 줍니다.  
  
![여러 tNICs NIC 팀](../../media/NIC-Teaming/nict_overview.jpg)  
  
또한 동일한 스위치 하거나 다른 스위치 어댑터당된 Nic 연결할 수 있습니다. Nic 다른 스위치를 연결 하면 스위치 모두 같은 서브넷 켜져 있어야 합니다.  
  
## <a name="bkmk_avail"></a>NIC 팀 공급 일  
NIC 팀이 모든 버전의 Windows Server 2016에 사용할 수 있습니다. 또한 NIC 팀의 도구는 지원 되는 클라이언트 운영 체제를 실행 하는 컴퓨터에서 관리를 Windows PowerShell 명령, 원격 데스크톱 및 원격 서버 관리 도구를 사용할 수 있습니다.  
  
## <a name="bkmk_nics"></a>NIC 팀에 대 한 지원 되 고 지원 되지 않는 Nic  
이 테스트를 통과 로고 및 Windows 하드웨어 검증 (WHQL 테스트) Windows Server 2016에 NIC 팀의 모든 이더넷 NIC 사용할 수 있습니다.  
  
NIC 팀에 다음과 같은 Nic 배치할 수 없습니다.  
  
-   Hyper-v 가상 스위치를 포트에서 호스트 하는 파티션에 Nic로 표시 하는 Hyper-v 가상 네트워크 어댑터 합니다.  
  
    > [!IMPORTANT]  
    > 호스트 파티션 (vNICs)에서 제공 되는 Hyper-v 가상 Nic 팀에 배치 되어야 합니다. 호스트 파티션 내의 vNICs의 팀 구성 또는 조합을에서 지원 되지 않습니다. 팀 vNICs 하려고 네트워크 오류가 발생 하는 경우의 통신 완료 손실이 될 수 있습니다.  
  
-   커널 디버그 네트워크 어댑터 (KDNIC)입니다.  
  
-   네트워크를 통해 부팅 사용 중인 Nic 합니다.  
  
-   이더넷 WWAN, WLAN에서 Wi-fi, Bluetooth, Infiniband (IPoIB) Nic를 통해 인터넷 프로토콜을 포함 하 여 Infiniband 등 이외의 기술을 사용 하는 Nic 합니다.  
  
## <a name="bkmk_compat"></a>NIC 팀 호환성  
NIC 팀은 다음과 같은 제외 하 고 모든 네트워킹 기술 Windows Server 2016에 호환 됩니다.  
  
-   **(S R IOV) 단일 루트 I/O 가상화**합니다. S R IOV에 대 한 데이터 (호스트 운영 체제 virtualization의 경우)에서 네트워킹 스택 통과 하지 않고 NIC를 직접 제공 됩니다. 따라서 검사 하거나 팀의 다른 경로를 데이터 리디렉션합니다 NIC 팀 취해도있지 않습니다.  
  
-   **기본 호스트 (QoS) 서비스 품질**합니다. QoS 정책 설정에 네이티브 호스트 시스템과 정책 호출 최소 대역폭 제한, NIC 팀에 대 한 전체 처리량 장소에 대역폭 정책을 없이 것 보다 작은 됩니다.  
  
-   **TCP 정의**합니다. 정의 TCP는 TCP 정의 오프 NIC에 직접 전체 네트워킹 스택 로드 때문에 NIC 팀 지원 되지  
  
-   **802.1 X 인증**합니다. 802.1 X 인증 NIC 팀으로 사용할 수 없습니다. 일부 스위치 802.1 X 인증와 같은 포트에서 NIC 팀의 구성을 허용 하지 않습니다.  
  
NIC 팀 Vm (가상 컴퓨터)는 Hyper-v 호스트에서 실행 되는 내 사용에 대 한 자세한 내용은 [가상 컴퓨터 및 #40; NIC 팀 Vm & #41; ](../../technologies/nic-teaming/../../technologies/nic-teaming/NIC-Teaming-in-Virtual-Machines--VMs-.md).  
  
## <a name="bkmk_vmq"></a>NIC 팀, 가상 컴퓨터 큐 (VMQs)  
VMQ와 NIC 팀은 서로 연동 잘; Hyper-v를 사용 하도록 설정한 언제 든 지 VMQ 사용 하도록 설정 해야 합니다. 구성 모드로 전환 하 고 로드 배포 알고리즘 따라 NIC 팀는 두 가지 모든 팀원 (큐 Sum 모드) 큐 (분 큐 모드) 팀의 모든 어댑터에서 지원 되는 작은 번호로 사용할 수 있는 큐 수가 또는 사용할 수 있는 큐 총을 보여 주는 Hyper-v 스위치를 VMQ 기능입니다.  
  
특히, 팀이 스위치 독립에 Hyper-v 포트 모드 또는 동적 모드로 설정 되어 모드와 부하 분산 팀 경우 보고 큐 수가 팀원 (큐 Sum 모드;)에서 사용할 수 있는 모든 큐 총 그렇지 않으면 보고 큐 수 최소 개수의 큐 (분 큐 모드) 팀의 구성원에 의해 지원 됩니다.  
  
다음은 이유 때문이입니다.  
  
-   Hyper-v 포트 모드나 동적 모드 스위치 독립 팀이 Hyper-v 스위치 포트 (VM)에 대 한 인바인드 교통 같은 팀원에 도착 항상 합니다. 호스트 수 예측/제어 NIC 팀에서 특정 팀원 할당할 수 있는 VMQ 큐에 대 한 더 많은 진심으 감사 수 있도록 멤버 특정 VM에 대 한 교통량 받게 됩니다. NIC 팀, Hyper-v 스위치를 사용 하 여 작업 하나만 팀원에는 VMQ vm 설정 되며 인바인드 교통 큐 발생할가 있는지 확인 합니다.  
  
-   팀이 모든 종속 모드로 전환 (정적 팀 또는 LACP 팀)에 있을 때 팀에 연결 되어 있는 스위치 컨트롤 인바인드 교통 배포 됩니다. NIC 팀 소프트웨어 호스트의 있는 팀 멤버 받게 인바인드 교통 vm 예측 수 없는 하 고 스위치 배포 함을 교통량 VM에 대 한 모든 팀원 것일 수 있습니다. 결과 Hyper-v 스위치를 사용 하는 NIC 팀 소프트웨어의 모든 팀원 VM에 대 한 큐 프로그램을으로 하나 뿐 아니라 팀 멤버 합니다.  
  
-   팀 스위치 독립 모드로 설정 되어 주소 해시 로드 배포 알고리즘을 사용 하는 경우 인바인드 교통은 항상 켜지 하나만 팀원을 모두 한 NIC (주 팀 멤버)-합니다. 다른 팀 멤버와 프로그래밍 다운로드 인바인드 교통 다루는 되지 이후 동일한 큐 기본 멤버와 인바인드 교통 집어 팀원을 사용할 수 있습니다 고 큐 이미 있는 다른 기본 멤버 실패 합니다.  
  
대부분의 Nic 큐 수신 측면 크기 (RSS) 또는 VMQ, 있지만 모두 동시에 사용할 수 있는 했습니다. 일부 VMQ 설정을 RSS 큐에 대 한 설정을 수 있지만 RSS 및 VMQ 사용 하는 기능에 따라 현재 사용 중인 일반 큐에 설정이 정말입니다. 각 NIC, 속성의 고급에서 값이 * RssBaseProcNumber \*MaxRssProcessors 하 고 있습니다. 다음은 시스템 성능 향상을 제공 하는 몇 가지 VMQ 설정입니다.  
  
-   각 NIC 있어야 이상적는 * 보다 크거나 RssBaseProcNumber 설정 하는 숫자 2. 첫 번째 물리적 프로세서에서 대부분의 네트워크 처리가 물리적 프로세서를 사용 하지 steered 해야 있으므로 시스템 처리 일반적으로 Core 0 (논리적 프로세서 0과 1)을 하기 때문입니다. (일부 컴퓨터 아키텍처 없는 물리적 프로세서를 당 논리 프로세서 두 개 하므로 이러한 컴퓨터에 대 한 기본 프로세서 1 이상 이어야 합니다. 의심 스러운에서 것으로 간주 하 여 호스트 프로세서를 사용 하는 2 논리 물리적 프로세서를 아키텍처 당.)  
  
-   팀이 큐 합계 모드에 있으면 하는 범위까지 실용적, 겹치지 않는, 팀원의 프로세서 되어야 합니다. 예를 들어, 2 10Gbps Nic 팀과 4 코어 호스트 (논리적 8 프로세서)을 설정할 수 있습니다 2 기본 프로세서를 사용 하 고 4 코어;를 사용 하는 첫 번째 두 번째 6 기본 프로세서를 사용 하 고 2 코어 사용로 설정 됩니다.  
  
-   팀이 분 큐 모드에 사용 하 여 팀원 프로세서 세트 동일 해야 합니다.  
  
## <a name="bkmk_hnv"></a>NIC 팀 및 Hyper V 네트워크 가상화 (HNV)  
NIC 팀은 완전히 호환 Hyper-v 네트워크 가상화 (HNV)와 됩니다.  HNV 관리 시스템 NIC 팀 HNV 교통에 대 한 최적화 된 새로운 지 원하는 방식으로 로드 배포할 수 있도록 해 주는 NIC 팀 드라이버에 대 한 정보를 제공 합니다.  
  
## <a name="bkmk_live"></a>NIC 팀 하 고 실시간 마이그레이션  
NIC 팀 Vm에서 실시간 마이그레이션 영향을 주지 않습니다. NIC 팀 VM에서 구성 되어 있는지 여부 같은 규칙 실시간 마이그레이션에 대 한 존재 합니다.  
  
## <a name="see-also"></a>참조 하십시오  
[NIC 팀에서 가상 컴퓨터 및 #40; Vm & #41;](../../technologies/nic-teaming/../../technologies/nic-teaming/NIC-Teaming-in-Virtual-Machines--VMs-.md)  
  


