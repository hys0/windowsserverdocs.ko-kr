---
title: Windows Server에서 Hyper-v 네트워킹 계획
description: Hyper-v의 기본 네트워킹에 필요한 사항을 설명 하 고 지침에 대 한 링크를 제공 합니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
author: KBDAzure
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: f09bc82d0dd47d3393dd05dcf03913db11e4c335
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392510"
---
# <a name="plan-for-hyper-v-networking-in-windows-server"></a>Windows Server에서 Hyper-v 네트워킹 계획

>적용 대상: Microsoft Hyper-V Server 2016, Windows Server 2016, Microsoft Hyper-V Server 2019, Windows Server 2019
  
Hyper-v의 네트워킹에 대 한 기본적인 이해를 통해 가상 컴퓨터에 대 한 네트워킹을 계획할 수 있습니다. 또한이 문서에서는 실시간 마이그레이션을 사용 하는 경우 및 다른 서버 기능 및 역할과 함께 Hyper-v를 사용할 때의 몇 가지 네트워킹 고려 사항에 대해 설명 합니다.  
  
## <a name="hyper-v-networking-basics"></a>Hyper-v 네트워킹 기본 사항  
Hyper-v의 기본 네트워킹은 매우 간단 합니다. 가상 스위치와 가상 네트워킹 어댑터의 두 부분을 사용 합니다. 가상 컴퓨터에 대 한 네트워킹을 설정 하려면 각각 하나 이상이 필요 합니다. 가상 스위치는 모든 이더넷 기반 네트워크에 연결 됩니다. 가상 네트워크 어댑터는 가상 스위치의 포트에 연결 하 여 가상 컴퓨터에서 네트워크를 사용할 수 있도록 합니다.  
  
기본 네트워킹을 설정 하는 가장 쉬운 방법은 Hyper-v를 설치할 때 가상 스위치를 만드는 것입니다. 그런 다음 가상 컴퓨터를 만들 때 스위치에 연결할 수 있습니다. 스위치에 연결 하면 가상 컴퓨터에 가상 네트워크 어댑터가 자동으로 추가 됩니다. 자세한 내용은 [hyper-v 가상 컴퓨터에 대 한 가상 스위치 만들기](../get-started/Create-a-virtual-switch-for-Hyper-V-virtual-machines.md)를 참조 하세요.  
  
여러 유형의 네트워킹을 처리 하려면 가상 스위치 및 가상 네트워크 어댑터를 추가할 수 있습니다. 모든 스위치는 Hyper-v 호스트의 일부 이지만 각 가상 네트워크 어댑터는 하나의 가상 컴퓨터에만 속합니다.  
  
가상 스위치는 소프트웨어 기반 계층 2 이더넷 네트워크 스위치입니다. 또한 트래픽을 모니터링 하 고 제어 하 고 분할 하며 보안 및 진단을 위한 기본 제공 기능을 제공 합니다.  *확장*이라고 하는 플러그 인을 설치 하 여 기본 제공 기능 집합에를 추가할 수 있습니다. 이러한 기능은 독립 소프트웨어 공급 업체에서 사용할 수 있습니다. 스위치 및 확장에 대 한 자세한 내용은 [Hyper-v 가상 스위치](../../hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md)를 참조 하세요.  
  
### <a name="switch-and-network-adapter-choices"></a>스위치 및 네트워크 어댑터 선택  
Hyper-v는 세 가지 유형의 가상 스위치와 두 가지 유형의 가상 네트워크 어댑터를 제공 합니다. 만들 때 원하는 항목 중 하나를 선택 합니다. Hyper-v 관리자 또는 Windows PowerShell 용 Hyper-v 모듈을 사용 하 여 가상 스위치 및 가상 네트워크 어댑터를 만들고 관리할 수 있습니다. 확장 포트 Acl (액세스 제어 목록)과 같은 일부 고급 네트워킹 기능은 Hyper-v 모듈의 cmdlet을 사용 해야만 관리할 수 있습니다.  
  
가상 스위치 또는 가상 네트워크 어댑터를 만든 후에 변경할 수 있습니다. 예를 들어 기존 스위치를 다른 유형으로 변경할 수 있지만,이 작업은 해당 스위치에 연결 된 모든 가상 머신의 네트워킹 기능에 영향을 줍니다.  따라서 실수를 하거나 테스트 해야 할 경우를 제외 하 고이 작업을 수행 하지 않는 것이 좋습니다. 또 다른 예로 가상 네트워크 어댑터를 다른 스위치에 연결할 수 있습니다. 다른 스위치는 다른 네트워크에 연결 하려는 경우에 사용할 수 있습니다. 그러나 가상 네트워크 어댑터는 한 유형에 서 다른 유형으로 변경할 수 없습니다. 형식을 변경 하는 대신 다른 가상 네트워크 어댑터를 추가 하 고 적절 한 유형을 선택 합니다.  
  
가상 스위치 유형은 다음과 같습니다.  
  
-   **외부 가상 스위치** -실제 네트워크 어댑터에 바인딩하여 유선 실제 네트워크에 연결 합니다.  
  
-   **내부 가상 스위치** -가상 스위치를 포함 하는 호스트에서 실행 되는 가상 컴퓨터 및 호스트와 가상 컴퓨터 간에 사용할 수 있는 네트워크에 연결 합니다.  
  
-   **개인 가상 스위치** -가상 스위치를 포함 하는 호스트에서 실행 되는 가상 컴퓨터에만 사용할 수 있는 네트워크에 연결 하지만 호스트와 가상 컴퓨터 간에 네트워킹을 제공 하지는 않습니다.  
  
가상 네트워크 어댑터 유형은 다음과 같습니다.  
  
-   **Hyper-v 특정 네트워크 어댑터** -1 세대 및 2 세대 가상 컴퓨터 모두에 사용할 수 있습니다. Hyper-v 용으로 특별히 설계 되었으며 Hyper-v integration services에 포함 된 드라이버가 필요 합니다. 네트워크로 부팅 하거나 지원 되지 않는 게스트 운영 체제를 실행 해야 하는 경우가 아니면이 유형의 네트워크 어댑터는 더 빠르고 권장 됩니다. 필요한 드라이버는 지원 되는 게스트 운영 체제에만 제공 됩니다. Hyper-v 관리자와 네트워킹 cmdlet에서이 유형을 네트워크 어댑터 라고 합니다.  
  
-   **레거시 네트워크 어댑터** -1 세대 가상 컴퓨터 에서만 사용할 수 있습니다. Intel 21140 기반 PCI Fast 이더넷 어댑터를 에뮬레이트합니다. Windows 배포 서비스와 같은 서비스에서 운영 체제를 설치할 수 있도록 네트워크를 부팅 하는 데 사용할 수 있습니다.  
  
## <a name="hyper-v-networking-and-related-technologies"></a>Hyper-v 네트워킹 및 관련 기술  
최신 Windows Server 릴리스는 Hyper-v에 대 한 네트워킹을 구성 하기 위한 추가 옵션을 제공 하는 향상 된 기능을 도입 했습니다. 예를 들어 Windows Server 2012에는 수렴 형 네트워킹에 대 한 지원이 도입 되었습니다. 이를 통해 하나의 외부 가상 스위치를 통해 네트워크 트래픽을 라우팅할 수 있습니다. Windows Server 2016는 Hyper-v 가상 스위치에 바인딩된 네트워크 어댑터에서 RDMA (원격 직접 메모리 액세스)를 허용 하 여이를 기반으로 합니다. 스위치 포함 된 팀 (설정)을 사용 하거나 사용 하지 않고이 구성을 사용할 수 있습니다. 자세한 내용은 [원격 &#40;직접 메모리 액세스&#41; RDMA 및 스위치 포함 팀 &#40;집합&#41; ](../../hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md) 을 참조 하세요.  
  
일부 기능은 특정 네트워크 구성을 사용 하거나 특정 구성에서 더 나은 성능을 제공 합니다. 네트워크 인프라를 계획 하거나 업데이트 하는 경우 다음을 고려 하세요.  
  
**장애 조치 (Failover) 클러스터링** -클러스터 트래픽을 격리 하 고 가상 스위치의 hyper-v QoS (서비스 품질)를 사용 하는 것이 가장 좋습니다. 자세한 내용은 [Hyper-v 클러스터에 대 한 네트워크 권장 사항](https://technet.microsoft.com/library/dn550728.aspx) 을 참조 하세요.  
  
**실시간 마이그레이션** -성능 옵션을 사용 하면 네트워크 및 CPU 사용량과 실시간 마이그레이션을 완료 하는 데 걸리는 시간을 줄일 수 있습니다. 자세한 내용은 [장애 조치 (Failover) 클러스터링이 없는 실시간 마이그레이션에 대 한 호스트 설정](../deploy/set-up-hosts-for-live-migration-without-failover-clustering.md)을 참조 하세요.  
  
**스토리지 공간 다이렉트** -이 기능은 smb 3.0 네트워크 프로토콜 및 RDMA를 사용 합니다. 자세한 내용은 [Windows Server 2016의 스토리지 공간 다이렉트](../../../storage/storage-spaces/storage-spaces-direct-overview.md)을 참조 하세요.