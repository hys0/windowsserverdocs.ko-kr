---
title: DNS 및 방화벽 설정 구성
description: 이 항목에서는 Always On VPN Windows Server 2016의 배포에 대 한 자세한 지침을 제공 합니다.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: d8cf3bae-45bf-4ffa-9205-290d555c59da
ms.localizationpriority: medium
ms.author: pashort
author: shortpatti
ms.date: 06/11/2018
ms.openlocfilehash: f57bfa005ef1af2556e4bd1cbb90ef8d3cfd22e3
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067321"
---
# 5단계. DNS 및 방화벽 설정 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

& #171;  [ **이전:** 4 단계. NPS 서버 설치 및 구성](vpn-deploy-nps.md)<br>
& #187;  [ **다음:** 6 단계입니다. VPN 연결에서 Windows 10 클라이언트를 항상 구성](vpn-deploy-client-vpn-connections.md)

DNS 및 방화벽 구성이 단계에서 VPN 연결에 대 한 설정 합니다.

## DNS 이름 확인 구성

원격 VPN 클라이언트에 연결할 때 사용 내부 클라이언트를 사용 하는 동일한 DNS 서버 이름을 내부 워크스테이션의 나머지 부분과 동일한 방식으로 확인할 수 있도록 합니다. 

이 인해 외부 클라이언트에서 사용할 VPN 서버에 연결 하는 컴퓨터 이름이 VPN 서버에 발급 된 인증서에 정의 된 주체 대체 이름 일치 하는지 확인 해야 합니다.

원격 클라이언트에 VPN 서버에 연결할 수 있도록 외부 DNS 영역에 DNS A (호스트) 레코드를 만들 수 있습니다. A 레코드에는 VPN 서버에 대 한 인증서 주체 대체 이름을 사용 해야 합니다.


### 호스트를 추가 하려면 \ 영역에 리소스 레코드 (A 또는 AAAA\)

1. 서버 관리자에서 DNS 서버의 **도구**클릭 하 고 **DNS**를 차례로 클릭 합니다. DNS 관리자가 열립니다.
2. DNS 관리자 콘솔 트리에서 관리할 서버를 클릭 합니다.
3. 세부 정보 창의 **이름**, double\ 클릭 **정방향 조회 영역** 보기를 확장 합니다.
4. 정방향 조회 영역 right\ 클릭 **정방향 조회 영역** 세부 정보에서를 레코드를 추가 하 여 클릭 **새 호스트 \(A or AAAA\)**. **새 호스트** 대화 상자가 열립니다.
5. **새 호스트** **이름**VPN 서버에 대 한 인증서 주체 대체 이름을 입력 합니다.
6. IP 주소에 VPN 서버의 IP 주소를 입력 합니다. Ip (IPv4) 버전 4 주소를 입력할 수도 있습니다 호스트 \(A\) 리소스 레코드를 추가 하는 형식 또는 IP 버전 6 \(IPv6\) 형식 호스트 \(AAAA\) 리소스 레코드를 추가 합니다.
7. IP 주소를 입력할 때를 포함 하 여 일정 범위의 IP 주소에 대 한 역방향 조회 영역을 만든 경우 **연결 된 포인터 (PTR) 레코드 만들기** 확인란을 선택 합니다.  이 옵션을 선택 하면 추가 포인터 \(PTR\) 리소스 레코드를 **이름** 및 **IP 주소**에서 입력 한 정보에 따라이 호스트에 대 한 역방향 영역에 만듭니다.
8. **호스트 추가**를 클릭합니다.

## Edge 방화벽 구성

Edge 방화벽 공용 인터넷에서 외부 경계 네트워크를 구분합니다. 시각적이 구분이 [항상에서 VPN 기술 개요](../always-on-vpn-technology-overview.md)항목에는 그림을 참조 하세요.

Edge 방화벽 허용 하 고 VPN 서버에 특정 포트 전달 해야 합니다. Network Address Translation \(NAT\) edge 방화벽을 사용 하는 경우 User Datagram Protocol \(UDP\) ports500 및 4500 포트 전달을 사용 하도록 필요할 수 있습니다. 이러한 포트 VPN 서버의 외부 인터페이스에 할당 된 IP 주소를 전달 합니다.

트래픽 라우팅 중인 인바운드 및 VPN 서버에서 공용 인터페이스에 적용 된 UDP ports500 허용 하도록 방화벽 규칙을 열어야 하 고 4500 인바운드 외부 IP 주소 또는 VPN 서버 뒤에 NAT를 수행 합니다.

두 경우 모두 방화벽 패킷 검사를 지원 하 고 클라이언트 연결을 설정 하는 데 문제가 있는 경우 해야 하거나 하려고 하면 완화 IKE 세션에 대 한 심층 패킷 검사를 사용 하지 않도록 설정 합니다.

이러한 구성을 변경 하는 방법에 대 한 정보를 방화벽 설명서를 참조 하세요.

## 내부 주변 네트워크 방화벽 구성

내부 주변 네트워크 방화벽 내부 경계 네트워크에서 조직/회사 네트워크를 구분합니다. 시각적이 구분이 [항상에서 VPN 기술 개요](../always-on-vpn-technology-overview.md)항목에는 그림을 참조 하세요.

이 배포에서는 경계 네트워크에서 원격 액세스 VPN 서버 RADIUS 클라이언트로 구성 됩니다.  VPN 서버 RADIUS 트래픽에 회사 네트워크에서 NPS 보내고 NPS에서 RADIUS 트래픽에 받습니다.

양방향 흐름 RADIUS 트래픽을 허용 하도록 방화벽을 구성 합니다.


>[!NOTE]
>RADIUS 클라이언트 VPN 서버에 대해 RADIUS 서버로 조직/회사 네트워크 기능에서 NPS 서버입니다. RADIUS 인프라에 대 한 자세한 내용은 [네트워크 정책 서버 (NPS)를](../../../../../networking/technologies/nps/nps-top.md)참조 하세요.

### VPN 서버와 NPS 서버에서 RADIUS 트래픽에 포트

기본적으로 NPS 및 VPN에 모든 설치 된 네트워크 어댑터에서 포트 1812, 1813, 1645 및 1646 RADIUS 트래픽에 대 한 수신 대기합니다. NPS를 설치할 때 고급 보안이 포함 된 Windows 방화벽을 사용 하면 이러한 포트에 대 한 방화벽 예외 가져오기 IPv6, IPv4 트래픽에 대 한 설치 과정에서 자동으로 만들어집니다.

>[!IMPORTANT]
>네트워크 액세스 서버 RADIUS 트래픽에 이러한 기본값 이외의 포트를 통해 보내도록 구성 된 경우 고급 보안이 포함 된 Windows 방화벽에서 NPS 설치 하는 동안 만든 예외를 제거 하 고 포트에 대 한 사용에 대 한 예외를 만듭니다 RADIUS 트래픽에 합니다.

### 내부 주변 네트워크 방화벽 구성에 대 한 동일한 RADIUS 포트를 사용 합니다.

기본 RADIUS 포트 구성을 사용 하 여 VPN 서버와 NPS 서버에서 하는 경우 내부 경계 네트워크 방화벽에서 다음 포트를 열고 있는지 확인 합니다.

- 포트 UDP1812, UDP1813, UDP1645, 및 UDP1646

NPS 배포에서 기본 RADIUS 포트를 사용 하지 않는 경우 사용 하는 포트에서 RADIUS 트래픽을 허용 하도록 방화벽을 구성 해야 합니다. 자세한 내용은 [RADIUS 트래픽에 대 한 방화벽 구성](../../../../../networking/technologies/nps/nps-firewalls-configure.md)을 참조 하세요.

## 다음 단계
6 단계를 [합니다. Windows 10 클라이언트 항상에서 VPN 연결 구성](vpn-deploy-client-vpn-connections.md):이 단계에서 VPN 연결을 사용 하 여 해당 인프라와 통신 하는 Windows 10 클라이언트 컴퓨터를 구성 합니다. Windows PowerShell, System Center Configuration Manager 및 Intune를 포함 하 여 Windows 10 VPN 클라이언트를 구성 하는 여러 가지 기술을 사용할 수 있습니다. 세 가지 모두 적절 한 VPN 설정을 구성 하는 XML VPN 프로필이 필요 합니다. 

---
