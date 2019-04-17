---
title: DHCP 서브넷 선택 옵션
description: 이 항목 대 한 DHCP(Dynamic Host Configuration Protocol) (DHCP) Windows Server 2016에 DHCP 서브넷 선택 옵션에 대 한 정보를 제공합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dhcp
ms.topic: get-started-article
ms.assetid: ca19e7d1-e445-48fc-8cf5-e4c45f561607
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 43bc3d165f895767ded921b41118ecaccf9734e8
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="dhcp-subnet-selection-options"></a>DHCP 서브넷 선택 옵션

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

새 DHCP 서브넷 선택 옵션에 대 한 내용은이 항목을 사용할 수 있습니다.

이제 DHCP \(sub-option 5\) 118 및 82 옵션을 지원합니다. DHCP 프록시 클라이언트 프로그램과 릴레이 상담원에 대 한 특정 서브넷 및 IP 주소 범위 특정 및 범위 IP 주소를 요청할 수 있도록 이러한 옵션을 사용할 수 있습니다.

DHCP 옵션 118으로 구성 된 DHCP 프록시 클라이언트를 사용 하는 경우 가상 개인 네트워크 등 Windows Server 2016 한 원격 액세스 거부 실행 하는 (VPN) 서버에 VPN 서버의 요청할 수 IP 주소 임대 특정 IP 주소 범위에서 VPN 클라이언트에 대 한 합니다.

옵션 5 일 하위는 로컬 구성 된 DHCP 82 옵션을 사용 하는 경우 릴레이 에이전트 IP 주소 임대 DHCP 클라이언트에서 특정 IP 주소 범위를 요청할 수 있습니다.

다음은 이러한 옵션에 대 한 의견 항목에 대 한 요청에 대 한 링크입니다.

- **옵션 118**: [dhcp RFC 3011 IPv4 서브넷 선택 옵션](http://www.rfc-base.org/rfc-3011.html)
- **옵션 82 하위 옵션 5**: [DHCPv4에 대 한 릴레이 에이전트 정보 옵션에 대 한 RFC 3527 링크 선택 하위 옵션](https://tools.ietf.org/html/rfc3527)


## <a name="dhcp-option-118-client-subnet-and-relay-agent-link-selection"></a>DHCP 옵션 118: 클라이언트 서브넷 및 릴레이 에이전트 링크 선택

DHCP 서브넷 선택 옵션에는 IP 주소 및 옵션 DHCP 서버 지정 해야 IP 서브넷 지정 하려면 DHCP 프록시 메커니즘을 제공 합니다.

### <a name="use-case-scenario"></a>사례 시나리오를 사용 하 여

이 경우 가상 개인 네트워크 \(VPN\) 서버 VPN 클라이언트를 IP 주소를 할당합니다. 

이 경우에 VPN 서버의에 연결 되어 모두 인트라넷 DHCP 서버가 설치 되어 있고 인터넷에 VPN 클라이언트 원격 위치에서 VPN 서버에 연결할 수 있도록 합니다.

에 VPN 서버의 IP 주소 임대 VPN 클라이언트를 제공할 수를 전에 서버 내부 서브넷 DHCP 서버에 연결 하 고 블록 IP 주소를 예약 합니다. 다음에 VPN 서버의 DHCP 서버에서 얻은 IP 주소를 관리 합니다. 에 VPN 서버의 VPN 클라이언트를 모두 임대에서 예약 된 IP 주소를 제공, 하는 경우에 VPN 서버의 DHCP 서버에서 추가 IP 주소를 얻습니다.

DHCP 옵션 118에 VPN 서버의 구성, IP 주소 범위 및 VPN 클라이언트를 사용 하 여 원하는 범위를 지정할 수 있습니다. 옵션 118 구성 하 고 나면 VPN 서버의 특정 IP 주소 범위 및 범위 DHCP 서버에서 IP 주소를 요청 합니다.

### <a name="the-dhcp-subnet-selection-option-field"></a>DHCP 서브넷 선택 옵션 필드

DHCP 서브넷 선택 옵션 필드에 단일 IPv4 주소 DHCP 임대 요청에 대 한 원래 서브넷 주소를 나타내는 데 포함 되어 있습니다.  이 옵션에 응답 하도록 구성 된 DHCP를 중 하나에서 주소를 할당 합니다.

1. 서브넷 선택 옵션에 지정 된 서브넷 합니다.
2. 서브넷 선택 옵션에 지정 된 서브넷와 같은 네트워크 세그먼트 켜져 있는 서브넷 합니다.

## <a name="option-82-sub-option-5-link-selection-sub-option"></a>옵션 82 하위 옵션 5: 링크 선택 하위 옵션

릴레이 에이전트 링크를 선택 하위 옵션에는 로컬 있는 IP 주소 및 옵션 DHCP 서버 지정 해야 IP 서브넷 지정할 수 있습니다.

일반적으로 DHCP 릴레이 에이전트 DHCP 서버와 통신 하도록 게이트웨이 IP 주소 \(GIADDR\) 필드에 의존 합니다. 그러나 GIADDR 하 여 두 운영 기능 제한 됩니다.

1. 서버에 알리는 DHCP 서브넷 요청 하는 IP 주소 임대 DHCP 클라이언트 상주 하는 정보입니다.
2. IP 주소 릴레이 에이전트와 통신 하는 데 DHCP 서버 알리는 합니다.

경우에 따라 릴레이 에이전트 DHCP 서버와의 커뮤니케이션을 사용 하 여 IP 주소 DHCP 클라이언트 IP 주소를 할당 필요한 IP 주소 범위 보다 다를 수 있습니다. 

해당 기능을 제한 된 대로, 118 옵션을 사용 하 고 GIADDR 필드 또는 릴레이 에이전트 정보 옵션 \(option 82\) 쓰기만 수 DHCP 릴레이 에이전트 만들 수 없습니다. 

옵션 82 링크 선택 하위 옵션이 릴레이 에이전트 82 하위 옵션 5 DHCP v4 옵션의 형태로 IP 주소 원하는 서브넷 할당을 명시적으로 지정할 수 있도록이 경우에 유용 합니다.

### <a name="use-case-scenario"></a>사례 시나리오를 사용 하 여

이 경우 조직의 네트워크 포함 DHCP 서버와 무선 액세스 포인트 게스트 사용자에 대해 \(AP\) 합니다. 하지만 조직 DHCP 서버에서-정책 제한 방화벽으로 인해 게스트 클라이언트 IP 주소를 할당, DHCP 서버 게스트 무선 네트워크 또는 무선 클라이언트 broadcase 메시지에 액세스할 수 없습니다.

이 제한은 해결 하려면 AP 게스트 클라이언트도 회사 네트워크에 연결 하는 내부 인터페이스의 IP 주소를 지정 GIADDR에 있는 동안에 할당 된 IP 주소 원하는 서브넷 지정 하려면 링크 선택 하위 옵션 5로 구성 됩니다.
