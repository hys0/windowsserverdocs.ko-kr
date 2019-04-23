---
title: Windows Server Hyper-v 네트워킹 계획
description: Hyper-v의 기본 네트워킹에 대 한 필요 하 고 지침에 대 한 링크를 제공 합니다. 무엇에 대해 설명 합니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
author: KBDAzure
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 83c014b917566a78796d061dd88962966ec0c9ab
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829874"
---
# <a name="plan-for-hyper-v-networking-in-windows-server"></a>Windows Server Hyper-v 네트워킹 계획

>적용 대상: Microsoft Hyper-V Server 2016, Windows Server 2016, Microsoft Hyper-V Server 2019, Windows Server 2019
  
Hyper-v의 네트워킹에 대 한 기본적인 이해를 사용 하면 가상 컴퓨터를 위한 네트워킹 계획 수 있습니다. 이 문서에서는 시점과 다른 서버 기능 및 역할을 사용 하 여 Hyper-v를 사용 하 여 실시간 마이그레이션을 사용 하는 경우에 몇 가지 네트워킹 고려 사항 다룹니다.  
  
## <a name="hyper-v-networking-basics"></a>Hyper-v 네트워킹 기본 사항  
Hyper-v의 기본 네트워킹은 매우 간단 합니다. 두 부분으로 가상 스위치 및 가상 네트워크 어댑터를 사용합니다. 각 가상 머신에 대 한 네트워킹 설정 중 하나 이상이 필요 합니다. 가상 스위치는 이더넷 기반 네트워크에 연결합니다. 가상 네트워크 어댑터 포트 네트워크를 사용 하려면 가상 컴퓨터 수 있도록 하는 가상 스위치에 연결 합니다.  
  
기본 네트워킹을 설정 하는 가장 쉬운 방법은 Hyper-v를 설치할 때 가상 스위치를 만드는 경우 그런 다음 가상 컴퓨터를 만든 경우 스위치에 연결할 수 있습니다. 스위치를 자동으로 연결할 가상 컴퓨터에 가상 네트워크 어댑터를 추가 합니다. 자세한 내용은 [Hyper-v 가상 컴퓨터에 대 한 가상 스위치 만들기](../get-started/Create-a-virtual-switch-for-Hyper-V-virtual-machines.md)합니다.  
  
다양 한 네트워킹을 처리 하려면 가상 스위치 및 가상 네트워크 어댑터를 추가할 수 있습니다. 모든 스위치는 Hyper-v 호스트의 일부 이지만 하나의 가상 컴퓨터에 속한 각 가상 네트워크 어댑터입니다.  
  
가상 스위치는 소프트웨어 기반의 계층 2 이더넷 네트워크 스위치입니다. 모니터링, 제어 및 (32–128kb 트래픽을 뿐만 아니라 보안 및 진단에 대 한 기본 제공 기능을 제공 합니다.  플러그 인, 라고도 설치 하 여 기본 제공 기능 집합에 추가할 수 있습니다 *확장*합니다. 이러한 독립 소프트웨어 공급 업체에서 제공 됩니다. 스위치 및 확장에 대 한 자세한 내용은 참조 하세요. [Hyper-v 가상 스위치](../../hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md)합니다.  
  
### <a name="switch-and-network-adapter-choices"></a>스위치 및 네트워크 어댑터 선택  
Hyper-v는 세 가지 유형의 가상 스위치 및 두 가지 유형의 가상 네트워크 어댑터를 제공합니다. 하나를 만들 때 원하는 각 선택할 수 있습니다. 가상 스위치 및 가상 네트워크 어댑터 만들기 및 관리에 Hyper-v 관리자 또는 Windows PowerShell 용 Hyper-v 모듈을 사용할 수 있습니다. 일부 고급 네트워킹 기능을 확장된 포트 액세스 제어 목록 (Acl)와 같이 관리할 수만 있습니다 Hyper-v 모듈의 cmdlet을 사용 하 여 합니다.  
  
만든 후 가상 스위치 또는 가상 네트워크 어댑터에 일부 변경 가능 합니다. 예를 들어 기존 스위치를 다른 형식으로 변경할 수 있지만 그렇게 스위치에 연결 된 모든 가상 컴퓨터의 네트워킹 기능에 영향을 줍니다.  따라서 있습니다 아마도 없습니다 실수 한 경우가 아니면이 작업을 수행 하거나 테스트 해야 합니다. 또 다른 예로, 다른 네트워크에 연결 하려는 경우 수행할 수 있는 다른 스위치에 가상 네트워크 어댑터를 연결할 수 있습니다. 그러나 다른 가상 네트워크 어댑터의 형식을 변경할 수 없습니다. 형식을 변경 하는 대신 다른 가상 네트워크 어댑터를 추가 하 고 적절 한 유형을 선택 합니다.  
  
가상 스위치 유형은 다음과 같습니다.  
  
-   **외부 가상 스위치** -실제 네트워크 어댑터에 바인딩하여 유선, 실제 네트워크에 연결 합니다.  
  
-   **내부 가상 스위치** -만 호스트와 가상 컴퓨터 간에 가상 스위치에 있는 호스트에서 실행 중인 가상 컴퓨터에서 사용할 수 있는 네트워크에 연결 합니다.  
  
-   **개인 가상 스위치** -가상 스위치에는 호스트와 가상 컴퓨터 간에 네트워킹을 제공 하지 않는 호스트에서 실행 하 여 가상 컴퓨터에서만 사용할 수 있는 네트워크에 연결 합니다.  
  
가상 네트워크 어댑터를 형식은 다음과 같습니다.  
  
-   **Hyper-v 특정 네트워크 어댑터** -1 세대와 2 세대 가상 컴퓨터에 대해 사용할 수 있습니다. Hyper-v 용으로 설계 된 하 고 Hyper-v 통합 서비스에 포함 된 드라이버가 필요 합니다. 이 유형의 네트워크 어댑터를 더 빠른 네트워크 부팅 해야 하거나 지원 되지 않는 게스트 운영 체제를 실행 하는 경우가 아니면 권장 되는 선택 되 고 있습니다. 필요한 드라이버 지원 되는 게스트 운영 체제에 대해서만 제공 됩니다. Hyper-v 관리자에서 및 네트워킹 cmdlet,이 형식은 것 이라고 네트워크 어댑터.  
  
-   **레거시 네트워크 어댑터** -1 세대 가상 컴퓨터에만 사용할 수 있습니다. Intel 21140 기반 PCI 빠른 이더넷 어댑터를 에뮬레이션 하 고 따라서 네트워크 부팅에 사용할 수 있습니다 Windows 배포 서비스와 같은 서비스에서 운영 체제를 설치할 수 있습니다.  
  
## <a name="hyper-v-networking-and-related-technologies"></a>Hyper-v 네트워킹 및 관련된 기술  
최신 Windows Server 버전에서 Hyper-v에 대 한 네트워킹을 구성 하는 데 더 많은 옵션을 제공 하는 향상 된 기능을 도입 했습니다. 예를 들어, 수렴 형 네트워킹에 대 한 Windows Server 2012 지원이 추가 되었습니다. 이렇게 하면 하나의 외부 가상 스위치를 통해 네트워크 트래픽을 라우팅합니다. Windows Server 2016에 Hyper-v 가상 스위치에 바인딩된 네트워크 어댑터에서 원격 직접 메모리 액세스 (RDMA)를 허용 하 여 빌드합니다. 이 구성을 사용 하 여 또는 없이 스위치 포함 된 팀 (SET)에 사용할 수 있습니다. 자세한 내용은 참조 하세요 [Remote Direct Memory Access &#40;RDMA&#41; 및 스위치 포함 팀 &#40;설정&#41;](../../hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)  
  
일부 기능은 특정 네트워킹 구성에 의존 하거나 특정 구성에서 더 잘 수행 합니다. 계획 또는 네트워크 인프라를 업데이트 하는 경우 이러한 것이 좋습니다.  
  
**장애 조치 클러스터링** -가상 스위치에서 클러스터 트래픽을 격리 하 고 Hyper-v의 QoS (서비스 품질)를 사용 하 하는 것이 좋습니다. 세부 정보를 참조 하세요. [Hyper-v 클러스터에 대 한 네트워크 권장 사항](https://technet.microsoft.com/library/dn550728.aspx)  
  
**실시간 마이그레이션** -성능 옵션을 사용 하 여 네트워크 및 CPU 사용량 및 실시간 마이그레이션을 완료 하는 데 걸리는 시간을 줄일 수 있습니다. 자세한 내용은 [장애 조치 클러스터링이 없는 실시간 마이그레이션에 대해 호스트 설정](../deploy/set-up-hosts-for-live-migration-without-failover-clustering.md)합니다.  
  
**저장소 공간 다이렉트** -이 기능은 RDMA SMB3.0 네트워크 프로토콜에 기반 합니다. 자세한 내용은 참조 하세요 [Windows Server 2016에서 저장소 공간 다이렉트](../../../storage/storage-spaces/storage-spaces-direct-overview.md)합니다.