---
title: 수렴 형된 네트워크 인터페이스 카드 (NIC) 구성 지침
description: 수렴 형된 네트워크 인터페이스 카드 (NIC)를 사용 하는 호스트 파티션에 서비스 원격 직접 메모리 액세스 (RDMA) TCP/IP 트래픽에 사용 하는 Hyper-v 게스트는 동일한 Nic에 액세스할 수 있도록 호스트 파티션에 가상 NIC (vNIC)를 통해 RDMA를 노출할 수 있습니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: d7642338-9b33-4dce-8100-8b2c38d7127a
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/13/2018
ms.openlocfilehash: e9f5180285dda790e11cec543a109d0cb58edd2d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838844"
---
# <a name="converged-network-interface-card-nic-configuration-guidance"></a>네트워크 인터페이스 카드를 수렴 형 \(NIC\) 구성 지침

>적용 대상: Windows Server (반기 채널), Windows Server 2016

수렴 형된 네트워크 인터페이스 카드 \(NIC\) 호스트를 통해 RDMA를 노출할 수 있도록\-가상 NIC를 파티션 \(vNIC\) 호스트 파티션 서비스 원격 직접 메모리 액세스에 액세스할 수 있도록 \(RDMA\) TCP/IP 트래픽에 사용 하는 Hyper-v 게스트는 동일한 Nic에 있습니다.

수렴 된 NIC 기능을 관리 하기 전에 \(파티션을 호스팅하\) RDMA를 사용 하려는 서비스 전용된 RDMA를 사용 하는 데 필요한 된\-지원 Nic에서 Hyper-v에 바인딩된 Nic의 대역폭 있던 경우에 가상 스위치입니다.

수렴 된 NIC에 두 워크 로드를 사용 하 여 \(RDMA와 게스트 트래픽 관리 사용자\) 더 적은 수의 Nic에는 서버에 설치 하면 동일한 실제 Nic를 공유할 수 있습니다.

Windows Server 2016 Hyper-v 호스트 및 Hyper-v 가상 스위치를 사용 하 여 수렴 형 된 NIC를 배포할 때 Hyper-v 호스트에서 Vnic 모든 이더넷을 통한 RDMA를 사용 하는 호스트 프로세스에 RDMA 서비스를 노출 하는\-RDMA 기술을 기반으로 합니다.

>[!NOTE]
>수렴 된 NIC 기술을 사용 하려면 서버에서 인증 된 네트워크 어댑터는 RDMA를 지원 해야 합니다.

이 가이드에서는 두 서버에 있는 수렴 된 NIC의 기본 배포는 단일 네트워크 어댑터를 설치 하는 배포에 대 한 지침 제공 팀 하는 스위치 포함 된 수렴 형 된 NIC의 배포는 다른 서버 두 개 이상의 네트워크 어댑터가 설치 되어 있는 지침 집합 \(설정할\) RDMA 팀\-가능 네트워크 어댑터입니다.


## <a name="prerequisites"></a>사전 요구 사항

다음은 기본 및 데이터 센터 NIC. 수렴 형 배포에 대 한 필수 구성 요소

>[!NOTE]
>제공 된 예제에서 Mellanox connectx-3 Pro 40 Gbps 이더넷 어댑터를 사용 하지만 RDMA를 인증 하는 Windows Server 중 하나를 사용할 수 있습니다\-가능 네트워크 어댑터는이 기능을 지원 합니다. 호환 되는 네트워크 어댑터에 대 한 자세한 내용은 Windows Server 카탈로그 항목을 참조 하세요 [LAN 카드](https://www.windowsservercatalog.com/results.aspx?&bCatID=1468&cpID=0&avc=85&ava=0&avt=0&avq=46&OR=1)합니다.

### <a name="basic-converged-nic-prerequisites"></a>기본 NIC 수렴 형 필수 구성 요소

기본 NIC 수렴 형 구성에 대 한이 가이드의 단계를 수행 하려면 다음이 필요 합니다.

- Windows Server 2016 Datacenter edition 또는 Windows Server 2016 Standard edition을 실행 하는 두 서버.
- 하나의 RDMA 지원, 각 서버에 설치 된 네트워크 어댑터를 인증 합니다.
- Hyper-v 서버 역할을 각 서버에 설치 합니다.

### <a name="datacenter-converged-nic-prerequisites"></a>데이터 센터 수렴 된 NIC 필수 구성 요소

데이터 센터 수렴 된 NIC 구성에 대 한이 가이드의 단계를 수행 하려면 다음이 필요 합니다.

- Windows Server 2016 Datacenter edition 또는 Windows Server 2016 Standard edition을 실행 하는 두 서버.
- 각 서버에 설치 된 네트워크 어댑터 두 RDMA 지원, 인증 합니다.
- Hyper-v 서버 역할을 각 서버에 설치 합니다.
- 스위치 포함 된 팀 익숙해야 \(설정\), Windows Server 2016에 Hyper-v 및 네트워킹 SDN (소프트웨어) 스택을 포함 하는 환경에서 사용 되는 솔루션 팀 NIC를 대체 합니다. 일부 NIC 팀 기능은 Hyper-v 가상 스위치에 통합 하는 설정 합니다. 자세한 내용은 [원격 직접 메모리 액세스 (RDMA) 및 스위치 포함 된 팀 (SET)](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)합니다.

## <a name="related-topics"></a>관련 항목
- [단일 네트워크 어댑터로 수렴 형 된 NIC 구성](cnic-single.md)
- [수렴 형 된 NIC 팀으로 구성 된 NIC 구성](cnic-datacenter.md)
- [수렴 형 된 NIC에 대 한 물리적 스위치 구성](cnic-app-switch-config.md)
- [수렴 형 NIC 구성 문제 해결](cnic-app-troubleshoot.md)

---