---
title: 집약된 네트워크 인터페이스 카드 (NIC) 구성 가이드
description: 이 항목은 Windows Server 2016 용 수렴 NIC 구성 가이드의 일부입니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: d7642338-9b33-4dce-8100-8b2c38d7127a
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 42f7ef674da1754253ad72ae30ad505f29ba6a7d
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="converged-network-interface-card-nic-configuration-guide"></a>집약된 네트워크 인터페이스 카드 \(NIC\) 구성 가이드

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

집약된 네트워크 인터페이스 카드 \(NIC\)에서는 호스트 파티션 서비스 원격 직접 메모리 액세스 \(RDMA\) Hyper-v 게스트 TCP/IP 교통에 사용 하는 동일한 Nic에 액세스할 수 있도록 파티션 host\ 가상 NIC \(vNIC\) 통해 RDMA 노출 될 수 있습니다.

NIC 수렴 기능이 이전 RDMA 사용 하려고 하는 관리 \(host partition\) 서비스 대역폭 된 Hyper-v의 가상 스위치 바인딩된 Nic에서 사용할 수 있는 경우에 전용된 RDMA\ 지원 Nic를 사용 하 여 필요 했습니다.

NIC 수렴, 두 가지 작업으로 \ (관리 사용자 RDMA 및 게스트 traffic\) 서버에 더 적은 Nic 설치할 수 있습니다 동일한 실제 Nic, 공유할 수 있습니다.

Hyper-v 가상 스위치와 Windows Server 2016 Hyper-v 호스트 수렴 NIC를 배포 하는 경우 Hyper-v 호스트에서 vNICs RDMA 서비스 호스트 프로세스를 통해 RDMA를 사용 하 여 모든 Ethernet\ 기반 RDMA 기술을 통해를 제공 합니다.

>[!NOTE]
>NIC 수렴 기술을 사용 하 여 서버에 있는 인증 된 네트워크 어댑터 RDMA 지원 해야 합니다.

이 가이드에서는 두 가지 배포 서버 수렴 nic; 기본적인 배포 되는 단일 네트워크 어댑터를 설치 하는 어디에 대 한 명령 \(SET\) 스위치 Embedded 팀 팀 RDMA\ 지원 네트워크 어댑터를 통해 수렴 nic 배포 하는 서버에 있는 두 개 이상의 네트워크 어댑터 설치 지침의 다른 세트 하 고 있습니다.

이 가이드는 다음 항목이 포함 되어 있습니다.

- [단일 네트워크 어댑터를 사용 하 여 집약된 NIC 구성](cnic-single.md)
- [집약된 NIC 어댑터당된 NIC 구성](cnic-datacenter.md)
- [실제 스위치 구성 집약 nic](cnic-app-switch-config.md)
- [NIC 구성 수렴 문제 해결](cnic-app-troubleshoot.md)

## <a name="prerequisites"></a>필수

다음은 수렴 NIC.의 기본 및 Datacenter 배포 사항

>[!NOTE]
>이 가이드의 예는 Mellanox ConnectX 3 Pro 40 g b p s 이더넷 어댑터는 사용 하지만이 기능을 지 원하는 RDMA\ 가능 네트워크 어댑터 인증 Windows Server 중 하나를 사용할 수 있습니다. 호환 되는 네트워크 어댑터에 대 한 자세한 내용은 참조 Windows Server 카탈로그 항목 [LAN 카드](https://www.windowsservercatalog.com/results.aspx?&bCatID=1468&cpID=0&avc=85&ava=0&avt=0&avq=46&OR=1)합니다.

### <a name="basic-converged-nic-prerequisites"></a>기본 수렴 NIC 필수

이 기본 수렴 NIC 구성에 대 한이 가이드의 단계를 수행 하려면 다음이 필요 합니다.

- Windows Server 2016 Datacenter edition 또는 Windows Server 2016 Standard edition 실행 하는 두 가지 서버 합니다.
- 하나 RDMA 지원, 각 서버에 설치 된 네트워크 어댑터를 인증 합니다.
- Hyper-v 서버 역할 각 서버에 설치 되어야 합니다.

### <a name="datacenter-converged-nic-prerequisites"></a>Datacenter 수렴 NIC 필수

이 데이터 센터 수렴 NIC 구성에 대 한이 가이드의 단계를 수행 하려면 다음이 필요 합니다.

- Windows Server 2016 Datacenter edition 또는 Windows Server 2016 Standard edition 실행 하는 두 가지 서버 합니다.
- 두 개의 RDMA 지원, 인증 각 서버에 설치 된 네트워크 어댑터가 합니다.
- Hyper-v 서버 역할 각 서버에 설치 되어야 합니다.
- 잘 알고 있어야 스위치 Embedded 팀 \(SET\)와 Windows Server 2016에 Hyper-v 및 소프트웨어 정의 네트워킹 (SDN) 스택 포함 하는 환경에서 사용할 수 있는 NIC 팀 솔루션을 대신 사용 되 합니다. NIC 팀 기능을 일부 Hyper-v의 가상 스위치에 통합 하는 설정 합니다. 자세한 내용은 참조 [원격 직접 메모리 액세스 (RDMA) 및 스위치 Embedded 팀 (설정)](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)합니다.

