---
title: DHCP(동적 호스트 구성 프로토콜)
description: 이 항목의 동적 호스트 구성 프로토콜 (DHCP) Windows Server 2016에 대 한 간략 한 개요를 제공합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dhcp
ms.topic: article
ms.assetid: 0ff29ef3-c458-4432-9065-e50a7de5b4b9
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 08b07e902486ae633b30949270e15f8bf94afaaf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857494"
---
# <a name="dynamic-host-configuration-protocol-dhcp"></a>DHCP(동적 호스트 구성 프로토콜)

>적용 대상: Windows Server (반기 채널), Windows Server 2016

Windows Server 2016에서 DHCP의 간략 한 개요는이 항목을 사용할 수 있습니다.

>[!NOTE]
>이 항목 외에 다음 DHCP 설명서는 사용할 수 있습니다.
>
>- [DHCP의 새로운 기능](What-s-New-in-DHCP.md)
>- [Windows PowerShell을 사용 하 여 DHCP 배포](dhcp-deploy-wps.md)

동적 호스트 구성 프로토콜 (DHCP)는 자동으로 IP (인터넷 프로토콜)를 호스트 하는 IP 주소 및 서브넷 마스크 및 기본 게이트웨이 등의 기타 관련된 구성 정보를 제공 하는 클라이언트/서버 프로토콜입니다. Rfc 2131 및 2132 DHCP로는 IETF Internet Engineering Task Force () 표준에 BOOTP (부트스트랩 프로토콜), DHCP를 사용 하는 많은 구현 세부 사항의 공유 하는 프로토콜 기반을 정의 합니다. DHCP 호스트를 DHCP 서버에서 필요한 TCP/IP 구성 정보를 가져올 수 있습니다.

Windows Server 2016 DHCP 서버는 IP 주소를 임대 하 여 네트워크 및 기타 정보를 DHCP 클라이언트에 배포할 수 있는 선택적 네트워킹 서버 역할을 포함 합니다. TCP/IP의 일환으로 DHCP 클라이언트를 포함 하는 모든 Windows 기반 클라이언트 운영 체제 및 DHCP 클라이언트는 기본적으로 사용 합니다.

## <a name="why-use-dhcp"></a>DHCP를 사용 하는 이유는?

모든 장치는 TCP 기반 네트워크에서 네트워크 및 해당 리소스에 액세스 하는 고유한 유니캐스트 IP 주소가 있어야 합니다. DHCP를 하지 않고 새 컴퓨터 또는 하나의 서브넷에서 다른 위치로 이동 하는 컴퓨터에 대 한 IP 주소 수동으로 구성 해야 합니다. 네트워크에서 제거 된 컴퓨터에 대 한 IP 주소를 수동으로 회수할 수 해야 합니다.

Dhcp를이 전체 프로세스 자동화 하 고 중앙에서 관리 됩니다. DHCP 서버는 IP 주소 풀을 유지 관리 하 고 네트워크에서 시작 될 때 모든 DHCP 사용 클라이언트에 주소를 임대할 합니다. IP 주소는 정적 (영구적으로 할당) 하는 대신 (임대) 동적 이기 때문에 더 이상 사용 중인 주소 재할당에 대 한 풀에 자동으로 반환 됩니다.

네트워크 관리자는 TCP/IP 구성 정보를 유지 관리 하 고 임대 제공의 형태로 DHCP 사용 클라이언트에 주소 구성을 제공 하는 DHCP 서버를 설정 합니다. DHCP 서버는 포함 하는 데이터베이스에 구성 정보를 저장 합니다.

- 네트워크에 있는 모든 클라이언트에 대 한 TCP/IP 구성 매개 유효 합니다.

- 유효한 IP 주소를 클라이언트에 게 할당에 대 한 풀에서 유지 관리 뿐만 아니라 주소를 제외 합니다.

- 특정 DHCP 클라이언트와 관련 된 예약 된 IP 주소입니다. 따라서 일관 된 단일 DHCP 클라이언트에 단일 IP 주소를 할당할 수 있습니다.

- 임대 기간 또는 시간을 IP 주소 전에 사용할 수 있는 임대 갱신을 반드시 입력 해야 합니다.

임대 제공을 수락 하면 DHCP 사용 클라이언트를 받습니다.

- 연결 있는 서브넷에 대 한 유효한 IP 주소입니다.  
  
- DHCP 옵션에는 DHCP 서버가 구성 되어 있는 추가 매개 변수는 요청 된 클라이언트에 할당 합니다. DHCP 옵션의 예는 라우터 (기본 게이트웨이), DNS 서버 및 DNS 도메인 이름에 속합니다.

## <a name="benefits-of-dhcp"></a>DHCP의 이점

DHCP는 다음과 같은 이점을 제공합니다.

- **신뢰할 수 있는 IP 주소 구성을**합니다. DHCP 철자 오류와 같은 수동 IP 주소 구성에 의해 발생 하는 구성 오류를 최소화 하거나 동시에 둘 이상의 컴퓨터에 IP 주소를 할당 하 여 발생 한 충돌을 해결 합니다.

- **네트워크 관리 감소**합니다. DHCP는 네트워크 관리를 줄이는 데 다음과 같은 기능이 포함 되어 있습니다.

    - 중앙에서 자동화 된 TCP/IP 구성 합니다.

    - 중앙 위치에서 TCP/IP 구성을 정의할 수 있습니다.

    - DHCP 옵션을 사용 하 여 추가 TCP/IP 구성 값의 전체 범위를 지정할 수 있습니다.

    - 무선 네트워크에서 다른 위치로 이동 하는 휴대용 장치에 대 한 것과 같은 자주 업데이트 해야 하는 클라이언트에 대 한 IP 주소를 효과적으로 처리 변경 합니다.

    - 모든 서브넷에서 DHCP 서버에 대 한 필요성을 없애 주는 DHCP 릴레이 에이전트를 사용 하 여 초기 DHCP 메시지를 전달 합니다.

