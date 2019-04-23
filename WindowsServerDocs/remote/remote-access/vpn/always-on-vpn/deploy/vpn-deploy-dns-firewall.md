---
title: DNS 및 방화벽 설정 구성
description: 이 항목에서는 Always On VPN Windows Server 2016에 배포 하기 위한 자세한 지침을 제공 합니다.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: d8cf3bae-45bf-4ffa-9205-290d555c59da
ms.localizationpriority: medium
ms.author: pashort
author: shortpatti
ms.date: 06/11/2018
ms.openlocfilehash: f57bfa005ef1af2556e4bd1cbb90ef8d3cfd22e3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886254"
---
# <a name="step-5-configure-dns-and-firewall-settings"></a>5단계. DNS 및 방화벽 설정 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

&#171;  [**이전:** 4단계. NPS 서버 설치 및 구성](vpn-deploy-nps.md)<br>
&#187;  [**Next:** 6단계. Windows 10 클라이언트를 VPN 연결에 always On 구성](vpn-deploy-client-vpn-connections.md)

이 단계에서는 DNS 및 방화벽 구성 VPN 연결에 대 한 설정입니다.

## <a name="configure-dns-name-resolution"></a>DNS 이름 확인 구성

원격 VPN 클라이언트 연결, 사용 내부 클라이언트를 사용 하는 동일한 DNS 서버 이름을 내부 워크스테이션의 나머지와 동일한 방식으로 확인할 수 있도록 합니다. 

이 인해 VPN 서버에 연결 하는 데 사용할 외부 클라이언트가 있는 컴퓨터 이름을 VPN 서버에 발급 된 인증서에 정의 된 주체 대체 이름과 일치 하는지 확인 해야 합니다.

원격 클라이언트가 VPN 서버에 연결할 수 있는지을 보장 하려면 외부 DNS 영역에는 DNS A (호스트) 레코드를 만들 수 있습니다. A 레코드에는 VPN 서버에 대 한 인증서 주체 대체 이름을 사용 해야 합니다.


### <a name="to-add-a-host-a-or-aaaa-resource-record-to-a-zone"></a>호스트를 추가 하려면 \(A 또는 AAAA\) 영역에 리소스 레코드

1. DNS 서버를 서버 관리자에서 클릭 **도구**를 클릭 하 고 **DNS**합니다. DNS 관리자가 열립니다.
2. DNS 관리자 콘솔 트리에서 서버를 관리 하려면를 클릭 합니다.
3. 세부 정보 창에서의 **이름을**, 이중\-클릭 **정방향 조회 영역** 보기를 확장 합니다.
4. **정방향 조회 영역** 세부 정보를 오른쪽\-레코드를를 추가 하 고 클릭 한 다음 원하는 정방향 조회 영역을 클릭 **새 호스트 \(A 또는 AAAA\)** 합니다. 합니다 **새 호스트** 대화 상자가 열립니다.
5. **새 호스트**의 **이름**, VPN 서버에 대 한 인증서 주체 대체 이름을 입력 합니다.
6. IP 주소를 VPN 서버에 대 한 IP 주소를 입력 합니다. Ip 버전 4 (IPv4) 주소를 입력할 수 있습니다 호스트를 추가 하는 형식을 \(A\) 리소스 레코드 또는 IP 버전 6 \(IPv6\) 호스트를 추가 하는 형식 \(AAAA\) 리소스 레코드입니다.
7. 만든 경우 다음 입력 하는 IP 주소를 포함 하는 범위의 IP 주소에 대 한 역방향 조회 영역을 선택 합니다 **연결 된 포인터 (PTR) 레코드 만들기** 확인란 합니다.  이 옵션을 선택 하면 추가 포인터를 만듭니다 \(PTR\) 에 입력 한 정보를 기반으로 하는이 호스트에 대 한 리소스 레코드는 역방향에서 영역 **이름** 하 고 **IP 주소**합니다.
8. **호스트 추가**를 클릭합니다.

## <a name="configure-the-edge-firewall"></a>에 지 방화벽 구성

에 지 방화벽 공용 인터넷을 통해 외부 경계 네트워크를 구분합니다. 이 분리와 시각적 표시가 항목의 그림을 참조 하세요 [항상의 VPN 기술 개요](../always-on-vpn-technology-overview.md)합니다.

에 지 방화벽을 허용 하 고 VPN 서버에 특정 포트를 전달 해야 합니다. 네트워크 주소 변환을 사용 하는 경우 \(NAT\) edge 방화벽에서 사용자 데이터 그램 프로토콜에 대 한 포트 전달을 사용 하도록 설정 해야 \(UDP\) 포트 500과 4500 합니다. 이러한 포트를 VPN 서버는 외부 인터페이스에 할당 된 IP 주소를 전달 합니다.

트래픽을 라우팅하는 경우 인바운드 및 VPN 서버에서 공용 인터페이스에 적용 된 외부 IP 주소로 포트 500과 4500 인바운드 UDP를 허용 하도록 방화벽 규칙을 열어야 하는 다음 이나 뒤, VPN 서버의 NAT를 수행 합니다.

두 경우 모두 방화벽 심층 패킷 검사를 지원 하 고 클라이언트 연결을 설정 하는 데 문제가 있는 경우 해야 하려는 완화 하거나 IKE 세션에 대 한 심층 패킷 검사를 사용 하지 않도록 설정 합니다.

이러한 구성을 변경 하는 방법에 대 한 자세한 내용은 해당 방화벽 설명서를 참조 하세요.

## <a name="configure-the-internal-perimeter-network-firewall"></a>내부 경계 네트워크 방화벽 구성

내부 경계 네트워크 방화벽 내부 경계 네트워크에서 조직/회사 네트워크를 구분합니다. 이 분리와 시각적 표시가 항목의 그림을 참조 하세요 [항상의 VPN 기술 개요](../always-on-vpn-technology-overview.md)합니다.

이 배포에서는 경계 네트워크에 원격 액세스 VPN 서버를 RADIUS 클라이언트로 구성 됩니다.  VPN 서버 회사 네트워크의 NPS로 RADIUS 트래픽을 전송 하 고 NPS에서 RADIUS 트래픽을 수신 합니다.

양방향에서 흐름에 RADIUS 트래픽을 허용 하도록 방화벽을 구성 합니다.


>[!NOTE]
>RADIUS 클라이언트는 VPN 서버에 대 한 RADIUS 서버로 조직/회사 네트워크 기능에서 NPS 서버. RADIUS 인프라에 대 한 자세한 내용은 참조 하세요. [네트워크 정책 (NPS 서버)](../../../../../networking/technologies/nps/nps-top.md)합니다.

### <a name="radius-traffic-ports-on-the-vpn-server-and-nps-server"></a>VPN 서버와 NPS 서버에서 RADIUS 트래픽을 포트

기본적으로 NPS 및 VPN에 대 한 모든 설치 된 네트워크 어댑터의 포트 1812, 1813, 1645 및 1646에서 RADIUS 트래픽을 수신합니다. NPS를 설치할 때 고급 보안이 포함 된 Windows 방화벽을 사용 하면, IPv6 및 IPv4 트래픽 모두에 대 한 설치 과정에서 이러한 포트에 대 한 방화벽 예외 자동으로 생성 합니다.

>[!IMPORTANT]
>네트워크 액세스 서버가 이러한 기본값 이외의 포트를 통해 RADIUS 트래픽을 보내도록 구성 된 경우 NPS 설치 중 Windows Firewall with Advanced Security에서에서 생성 된 예외를 제거 하 고 예외를 사용 하 여는 포트를 만들려면 RADIUS 트래픽을 합니다.

### <a name="use-the-same-radius-ports-for-the-internal-perimeter-network-firewall-configuration"></a>내부 경계 네트워크 방화벽 구성에 대 한 동일한 RADIUS 포트를 사용 합니다.

VPN 서버와 NPS 서버에서 기본 RADIUS 포트 구성을 사용 하면 내부 경계 네트워크 방화벽에서 다음 포트를 열어야 있는지 확인 합니다.

- 포트 UDP1812, UDP1813, UDP1645, 및 UDP1646

NPS 배포에서 기본 RADIUS 포트를 사용 하지 않는 경우 사용 중인 포트에서 RADIUS 트래픽을 허용 하도록 방화벽을 구성 해야 합니다. 자세한 내용은 [RADIUS 트래픽에 대 한 방화벽 구성](../../../../../networking/technologies/nps/nps-firewalls-configure.md)합니다.

## <a name="next-step"></a>다음 단계
[6 단계입니다. Always On VPN 연결에 Windows 10 클라이언트를 구성](vpn-deploy-client-vpn-connections.md): 이 단계에서는 VPN 연결을 사용 하 여 해당 인프라와 통신 하는 Windows 10 클라이언트 컴퓨터를 구성 합니다. Windows PowerShell, System Center Configuration Manager 및 Intune 등의 Windows 10 VPN 클라이언트를 구성 하려면 여러 가지 기술을 사용할 수 있습니다. 세 가지 모두 적절 한 VPN 설정을 구성 하는 XML VPN 프로필을 필요 합니다. 

---
