---
title: 수렴 형 NIC (네트워크 인터페이스 카드) 구성 지침
description: NIC (네트워크 인터페이스 카드)를 사용 하면 호스트 파티션 vNIC (가상 NIC)를 통해 RDMA를 노출 하 여 Hyper-v 게스트가 TCP/IP 트래픽에 사용 하는 것과 동일한 Nic에서 호스트 파티션 서비스가 RDMA (원격 직접 메모리 액세스)에 액세스할 수 있습니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: d7642338-9b33-4dce-8100-8b2c38d7127a
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 09/13/2018
ms.openlocfilehash: 8824a6c6189a447f97f285052af8e5c13a66e766
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312815"
---
# <a name="converged-network-interface-card-nic-configuration-guidance"></a>NIC\) 구성 지침을 \(수렴 형 네트워크 인터페이스 카드

>적용 대상: Windows Server(반기 채널), Windows Server 2016

NIC\) \(NIC를 사용 하면 호스트\-파티션 가상 NIC \(vNIC\)를 통해 RDMA를 노출 하 여 Hyper-v 게스트가 TCP/IP 트래픽에 사용 하는 것과 동일한 Nic에서 원격 직접 메모리 액세스 \(RDMA\)에 액세스할 수 있습니다.

Nic에서 Hyper-v 가상 스위치에 바인딩된 Nic를 사용할 수 있는 경우에도, 수렴 형 NIC 기능 이전에 RDMA를 사용 하고자 하는 관리 \(호스트 파티션\) 서비스에서 전용 RDMA\-지원 Nic를 사용 해야 했습니다.

수렴 형 NIC를 사용 하는 경우 RDMA 및 게스트\) 트래픽의 관리 사용자 \(두 작업은 동일한 실제 Nic를 공유할 수 있으므로 서버에 Nic를 줄일 수 있습니다.

Windows Server 2016 Hyper-v 호스트와 Hyper-v 가상 스위치를 사용 하 여 수렴 형 NIC를 배포할 경우 Hyper-v 호스트의 vNICs는 rdma를 사용 하는 rdma 서비스를 이더넷\-기반 RDMA 기술에 대해 rdma를 사용 하 여 호스트 프로세스에 노출 합니다.

>[!NOTE]
>수렴 형 NIC 기술을 사용 하려면 서버의 인증 된 네트워크 어댑터가 RDMA를 지원 해야 합니다.

이 가이드에서는 서버가 단일 네트워크 어댑터를 설치 하는 배포에 대 한 두 가지 지침 집합을 제공 하며,이는 수렴 NIC의 기본 배포입니다. 서버에 두 개 이상의 네트워크 어댑터가 설치 되어 있는 다른 지침 집합을 사용할 수 있습니다 .이는 스위치 포함 된 팀을 통해 수렴 형 NIC를 배포 \(설정\) RDMA\-지원 네트워크 어댑터를 팀으로 설정 합니다.


## <a name="prerequisites"></a>필수 조건

다음은 수렴 형 NIC의 기본 및 데이터 센터 배포를 위한 필수 구성 요소입니다.

>[!NOTE]
>제공 된 예제에서는 Connectx-3 Pro 40 g b 이더넷 어댑터를 사용 하지만이 기능을 지 원하는 Windows Server 인증 RDMA\-사용할 수 있는 네트워크 어댑터를 사용할 수 있습니다. 호환 되는 네트워크 어댑터에 대 한 자세한 내용은 Windows Server 카탈로그 항목 [LAN 카드](https://www.windowsservercatalog.com/results.aspx?&bCatID=1468&cpID=0&avc=85&ava=0&avt=0&avq=46&OR=1)를 참조 하십시오.

### <a name="basic-converged-nic-prerequisites"></a>기본 수렴 형 NIC 필수 조건

기본 수렴 형 NIC 구성에 대 한이 가이드의 단계를 수행 하려면 다음이 필요 합니다.

- Windows Server 2016 Datacenter edition 또는 Windows Server 2016 Standard edition을 실행 하는 두 대의 서버
- 각 서버에 설치 된 RDMA 지원, 인증 된 네트워크 어댑터 하나가 있습니다.
- 각 서버에 hyper-v 서버 역할이 설치 되어 있어야 합니다.

### <a name="datacenter-converged-nic-prerequisites"></a>데이터 센터 수렴 형 NIC 필수 조건

데이터 센터 수렴 형 NIC 구성에 대 한이 가이드의 단계를 수행 하려면 다음이 있어야 합니다.

- Windows Server 2016 Datacenter edition 또는 Windows Server 2016 Standard edition을 실행 하는 두 대의 서버
- 각 서버에 설치 된 RDMA 가능 인증 네트워크 어댑터 2 개
- 각 서버에 hyper-v 서버 역할이 설치 되어 있어야 합니다.
- Windows Server 2016에서 Hyper-v와 SDN (소프트웨어 방식 네트워킹) 스택을 포함 하는 환경에서 사용 되는 대체 NIC 팀 솔루션인 스위치 포함 된 팀 \(\)설정 하 여 잘 알고 있어야 합니다. 일부 NIC 팀 기능은 Hyper-v 가상 스위치에 통합 하는 설정 합니다. 자세한 내용은 [RDMA (원격 직접 메모리 액세스) 및 스위치 포함 된 팀 (SET)](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)을 참조 하세요.

## <a name="related-topics"></a>관련 항목
- [단일 네트워크 어댑터를 사용 하 여 수렴 형 NIC 구성](cnic-single.md)
- [수렴 형 NIC 팀 NIC 구성](cnic-datacenter.md)
- [수렴 형 NIC에 대 한 물리적 스위치 구성](cnic-app-switch-config.md)
- [수렴 형 NIC 구성 문제 해결](cnic-app-troubleshoot.md)

---