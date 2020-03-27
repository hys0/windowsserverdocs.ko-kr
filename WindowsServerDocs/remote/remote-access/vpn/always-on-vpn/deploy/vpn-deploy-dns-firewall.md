---
title: DNS 및 방화벽 설정 구성
description: 이 항목에서는 Windows Server 2016에 Always On VPN을 배포 하는 방법에 대 한 자세한 지침을 제공 합니다.
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: d8cf3bae-45bf-4ffa-9205-290d555c59da
ms.localizationpriority: medium
ms.author: lizross
author: eross-msft
ms.date: 06/11/2018
ms.openlocfilehash: 394e589028d9d3d22851ea970346b0f150fee393
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80309402"
---
# <a name="step-5-configure-dns-and-firewall-settings"></a>5단계. DNS 및 방화벽 설정 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**이전:** 4 단계. NPS 서버 설치 및 구성](vpn-deploy-nps.md)
- [**다음:** 6 단계. Windows 10 클라이언트 Always On VPN 연결 구성](vpn-deploy-client-vpn-connections.md)

이 단계에서는 VPN 연결에 대 한 DNS 및 방화벽 설정을 구성 합니다.

## <a name="configure-dns-name-resolution"></a>DNS 이름 확인 구성

원격 VPN 클라이언트는 연결 될 때 내부 클라이언트에서 사용 하는 것과 동일한 DNS 서버를 사용 하 여 내부 워크스테이션의 나머지 부분과 동일한 방식으로 이름을 확인할 수 있도록 합니다.

따라서 외부 클라이언트에서 VPN 서버에 연결 하는 데 사용 하는 컴퓨터 이름이 VPN 서버에 발급 된 인증서에 정의 된 주체 대체 이름과 일치 하는지 확인 해야 합니다.

원격 클라이언트가 VPN 서버에 연결할 수 있도록 하려면 외부 DNS 영역에서 DNS A (호스트) 레코드를 만들 수 있습니다. A 레코드는 VPN 서버에 대 한 인증서 주체 대체 이름을 사용 해야 합니다.

### <a name="to-add-a-host-a-or-aaaa-resource-record-to-a-zone"></a>영역에 호스트 (A 또는 AAAA) 리소스 레코드를 추가 하려면

1. DNS 서버의 서버 관리자에서 **도구**를 선택 하 고 **dns**를 선택 합니다. DNS 관리자가 열립니다.
2. DNS 관리자 콘솔 트리에서 관리 하려는 서버를 선택 합니다.
3. 세부 정보 창의 **이름**에서 **전방 조회 영역** 을 두 번 클릭 하 여 보기를 확장 합니다.
4. **전방 조회 영역** 세부 정보에서 레코드를 추가 하려는 전방 조회 영역을 마우스 오른쪽 단추로 클릭 한 다음 **새 호스트 (a 또는 AAAA)** 를 선택 합니다. **새 호스트** 대화 상자가 열립니다.
5. **새 호스트**의 **이름**에 VPN 서버의 인증서 주체 대체 이름을 입력 합니다.
6. IP 주소에서 VPN 서버에 대 한 IP 주소를 입력 합니다. IPv4 (IP 버전 4) 형식으로 주소를 입력 하 여 호스트 (A) 리소스 레코드 또는 IPv6 (IP 버전 6) 형식을 추가 하 여 호스트 (AAAA) 리소스 레코드를 추가할 수 있습니다.
7. 입력 한 IP 주소를 포함 하 여 IP 주소 범위에 대 한 역방향 조회 영역을 만든 경우에는 **연결 된 포인터 (PTR) 레코드 만들기** 확인란을 선택 합니다.  이 옵션을 선택 하면 **이름** 및 **IP 주소**에 입력 한 정보에 따라이 호스트의 역방향 영역에 PTR (추가 포인터) 리소스 레코드가 만들어집니다.
8. **호스트 추가**를 선택 합니다.

## <a name="configure-the-edge-firewall"></a>에 지 방화벽 구성

에 지 방화벽은 공용 인터넷에서 외부 경계 네트워크를 분리 합니다. 이러한 분리를 시각적으로 표시 하려면 [VPN 기술 개요 Always On](../always-on-vpn-technology-overview.md)항목의 그림을 참조 하세요.

에 지 방화벽은 특정 포트를 허용 하 고 VPN 서버로 전달 해야 합니다. 에 지 방화벽에서 NAT (네트워크 주소 변환)를 사용 하는 경우 UDP (사용자 데이터 그램 프로토콜) 포트 500 및 4500에 대 한 포트 전달을 사용 하도록 설정 해야 할 수 있습니다. VPN 서버의 외부 인터페이스에 할당 된 IP 주소로 이러한 포트를 전달 합니다.

트래픽 인바운드를 라우팅 하 고 VPN 서버에서 NAT를 수행 하는 경우 VPN 서버의 공용 인터페이스에 적용 되는 외부 IP 주소에 대 한 UDP 포트 500 및 4500 인바운드를 허용 하는 방화벽 규칙을 열어야 합니다.

두 경우 모두 방화벽에서 심층 패킷 검사를 지원 하 고 클라이언트 연결을 설정 하는 데 어려움이 있는 경우 IKE 세션의 심층 패킷 검사를 완화 하거나 사용 하지 않도록 설정 해야 합니다.

이러한 구성 변경을 수행 하는 방법에 대 한 자세한 내용은 방화벽 설명서를 참조 하세요.

## <a name="configure-the-internal-perimeter-network-firewall"></a>내부 경계 네트워크 방화벽 구성

내부 경계 네트워크 방화벽은 조직/회사 네트워크를 내부 경계 네트워크와 분리 합니다. 이러한 분리를 시각적으로 표시 하려면 [VPN 기술 개요 Always On](../always-on-vpn-technology-overview.md)항목의 그림을 참조 하세요.

이 배포에서 경계 네트워크의 원격 액세스 VPN 서버는 RADIUS 클라이언트로 구성 됩니다.  VPN 서버는 회사 네트워크의 NPS에 RADIUS 트래픽을 보내고 NPS에서 RADIUS 트래픽도 수신 합니다.

양방향으로 RADIUS 트래픽이 흐를 수 있도록 방화벽을 구성 합니다.

>[!NOTE]
>조직/회사 네트워크의 NPS 서버는 VPN 서버에 대 한 RADIUS 서버 (RADIUS 클라이언트)로 작동 합니다. RADIUS 인프라에 대 한 자세한 내용은 [NPS (네트워크 정책 서버)](../../../../../networking/technologies/nps/nps-top.md)를 참조 하세요.

### <a name="radius-traffic-ports-on-the-vpn-server-and-nps-server"></a>VPN 서버 및 NPS 서버의 RADIUS 트래픽 포트

기본적으로 NPS 및 VPN은 설치 된 모든 네트워크 어댑터에서 포트 1812, 1813, 1645 및 1646에 대 한 RADIUS 트래픽을 수신 대기 합니다. NPS를 설치할 때 고급 보안이 포함 된 Windows 방화벽을 사용 하도록 설정 하면 IPv6 및 IPv4 트래픽 모두에 대해 설치 프로세스 중에 이러한 포트에 대 한 방화벽 예외가 자동으로 생성 됩니다.

>[!IMPORTANT]
>네트워크 액세스 서버가 이러한 기본값 이외의 포트를 통해 RADIUS 트래픽을 보내도록 구성 된 경우에는 NPS 설치 중에 고급 보안이 설정 된 Windows 방화벽에서 생성 된 예외를 제거 하 고에서 사용 하는 포트에 대 한 예외를 만듭니다. RADIUS 트래픽

### <a name="use-the-same-radius-ports-for-the-internal-perimeter-network-firewall-configuration"></a>내부 경계 네트워크 방화벽 구성에 동일한 RADIUS 포트 사용

VPN 서버와 NPS 서버에서 기본 RADIUS 포트 구성을 사용 하는 경우 내부 경계 네트워크 방화벽에서 다음 포트를 열어야 합니다.

- UDP1812, UDP1813, UDP1645 및 UDP1646 포트

NPS 배포에서 기본 RADIUS 포트를 사용 하지 않는 경우 사용 중인 포트에서 RADIUS 트래픽을 허용 하도록 방화벽을 구성 해야 합니다. 자세한 내용은 [RADIUS 트래픽에 대 한 방화벽 구성](../../../../../networking/technologies/nps/nps-firewalls-configure.md)을 참조 하세요.

## <a name="next-steps"></a>다음 단계

[6 단계. Windows 10 클라이언트 Always On VPN 연결 구성](vpn-deploy-client-vpn-connections.md):이 단계에서는 vpn 연결을 사용 하 여 해당 인프라와 통신 하도록 windows 10 클라이언트 컴퓨터를 구성 합니다. 여러 기술을 사용 하 여 Windows PowerShell, Microsoft 끝점 Configuration Manager 및 Intune을 비롯 한 Windows 10 VPN 클라이언트를 구성할 수 있습니다. 세 가지 모두 적절 한 VPN 설정을 구성 하려면 XML VPN 프로필이 필요 합니다.