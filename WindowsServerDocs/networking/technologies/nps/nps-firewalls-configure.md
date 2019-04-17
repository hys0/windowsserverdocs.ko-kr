---
title: 방화벽 RADIUS 교통에 대 한 구성
description: 이 항목에서는 Windows Server 2016에 네트워크 정책 서버에 대 한 교통량 RADIUS 수 있도록 방화벽을 구성 하는 방법 소개 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 58cca2b2-4ef3-4a09-a614-8bdc08d24f15
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 140111e10eabbece098ae9b7c36746cc663c9cce
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="configure-firewalls-for-radius-traffic"></a>방화벽 RADIUS 교통에 대 한 구성

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

방화벽을 허용 하거나 차단 하 고 컴퓨터 또는 방화벽 실행 되는 디바이스에서 IP 교통 유형의 구성할 수 있습니다. 방화벽 RADIUS 클라이언트 간의 RADIUS 교통 수 있도록 올바르게 구성 되지 않은 경우 네트워크 액세스 인증 RADIUS 프록시 및 RADIUS 서버, 사용자가 네트워크 리소스에 액세스 하지 못하도록 실패할 수 있습니다. 

방화벽 RADIUS 교통 수 있도록 두 가지 유형의 구성 해야 할 수 있습니다.

- 고급 보안 네트워크 NPS 정책 서버 ()를 실행 하는 로컬 서버에 포함 된 Windows Defender 방화벽.
- 다른 컴퓨터 또는 하드웨어 디바이스에서 실행 되는 방화벽.

## <a name="windows-firewall-on-the-local-nps-server"></a>Windows 방화벽 로컬 NPS 서버에서

기본적으로 NPS 송수신 RADIUS 교통 1812, 1813 1645 1646 및 사용자 데이터 그램 프로토콜 \(UDP\) 포트를 사용 하 여 합니다. Windows Defender 방화벽 NPS 서버에 NPS RADIUS 트래픽을이 보내고 받을 수 있도록 설치 하는 동안 예외에 자동으로 구성 됩니다.

따라서 기본 UDP 포트를 사용 하는 하지 필요 RADIUS 교통 NPS 서버에서 고를 수 있도록 Windows Defender 방화벽 구성을 변경 합니다.

경우에 따라 NPS RADIUS 교통에 사용 되 고 포트 변경 하려는 수 있습니다. NPS 및 네트워크 액세스 서버를 보내고 받을 RADIUS 트래픽을 기본값으로 이외의 포트에서 구성 하는 경우 다음을 수행 해야 합니다.

- RADIUS 트래픽을 기본 포트에서 허용 하는 예외를 제거 하세요.
- RADIUS 트래픽을 새로운 포트에서 허용 하는 새로운 예외를 만듭니다.

자세한 내용은 참조 [구성 NPS UDP 포트 정보](nps-udp-ports-configure.md)합니다.

## <a name="other-firewalls"></a>다른 방화벽

가장 일반적인 구성 방화벽은 인터넷에 연결 되 고 NPS 서버 주변 네트워크에 연결 되어 있는 인트라넷 리소스가 합니다.

도메인 컨트롤러 인트라넷 연결할 NPS 서버 있을 수 있습니다.

- 주변 네트워크 인터페이스에 있는 인트라넷 켜고 인터페이스 (IP 경로 사용할 수 없음). 
- 주변 네트워크의 단일 인터페이스 합니다. 이 구성 NPS 도메인 컨트롤러를 인트라넷 주변 네트워크에 연결 하는 다른 방화벽을 통해 통신할 합니다.

## <a name="configuring-the-internet-firewall"></a>인터넷 방화벽 구성

인터넷에 연결 되어 있는 방화벽 인터넷 인터페이스에 입출력 필터 구성 해야 \ (그리고, 원하는 경우 해당 네트워크 주변 interface\), 인터넷 서버 NPS와 RADIUS 클라이언트 또는 프록시 간의 RADIUS 메시지를 전달 수 있도록 합니다. 추가 필터 주변 네트워크의 웹 서버, VPN 서버 또는 다른 종류의 서버로 교통 전달 사용할 수 있습니다.

구분 입출력 패킷 인터넷 인터페이스 및 주변 네트워크 인터페이스 필터를 구성할 수 있습니다.

### <a name="configure-input-filters-on-the-internet-interface"></a>인터넷에 입력된 필터를 구성 합니다.

다음과 같은 유형의 교통 수 있도록 방화벽의 인터넷에 다음과 같은 입력된 패킷 필터를 구성 합니다.

- IP 주소 주변 네트워크 인터페이스 및 NPS 서버 (0x714) 1812 UDP 목적지 포트 대상 합니다.  이 필터 NPS 서버에 인터넷 기반 RADIUS 클라이언트의 RADIUS 인증 교통 수 있게합니다. 이 RFC 2865에 정의 된 대로 NPS에서 사용 되는 기본 UDP 포트 합니다. 다른 포트를 사용 하는 경우 1812에 대 한 포트 번호를 대체 합니다.
- IP 주소 주변 네트워크 인터페이스 및 NPS 서버 (0x715) 1813 UDP 목적지 포트 대상 합니다. 이 필터 NPS 서버에 인터넷 기반 RADIUS 클라이언트의 RADIUS 계정 교통 수 있게합니다. 이 2866 RFC에에서 정의 된 대로 NPS에서 사용 되는 기본 UDP 포트 합니다. 다른 포트를 사용 하는 경우 1813에 대 한 포트 번호를 대체 합니다.
- 주변 네트워크 인터페이스 대상 IP 주소 및 NPS 서버 1645 \(0x66D\) UDP 목적지 포트 \(Optional\) 합니다. 이 필터 NPS 서버에 인터넷 기반 RADIUS 클라이언트의 RADIUS 인증 교통 수 있게합니다. 이 이전 RADIUS 클라이언트에서 사용 되는 UDP 포트 합니다.
- 주변 네트워크 인터페이스 대상 IP 주소 및 NPS 서버 1646 \(0x66E\) UDP 목적지 포트 \(Optional\) 합니다. 이 필터 NPS 서버에 인터넷 기반 RADIUS 클라이언트의 RADIUS 계정 교통 수 있게합니다. 이 이전 RADIUS 클라이언트에서 사용 되는 UDP 포트 합니다.

### <a name="configure-output-filters-on-the-internet-interface"></a>인터넷에 출력 필터를 구성 합니다.

다음과 같은 유형의 교통 수 있도록 방화벽의 인터넷에 다음과 같은 출력 필터를 구성 합니다.

- IP 주소 주변 네트워크 인터페이스 및 NPS 서버 (0x714) 1812 UDP 소스 포트 소스입니다. 이 필터 인터넷 기반 RADIUS 클라이언트 NPS 서버에서 RADIUS 인증 트래픽을 수 있게합니다. 이 RFC 2865에 정의 된 대로 NPS에서 사용 되는 기본 UDP 포트 합니다. 다른 포트를 사용 하는 경우 1812에 대 한 포트 번호를 대체 합니다.
- IP 주소 주변 네트워크 인터페이스 및 NPS 서버 (0x715) 1813 UDP 소스 포트 소스입니다. 이 필터 인터넷 기반 RADIUS 클라이언트 NPS 서버에서 RADIUS 계정 트래픽을 수 있게합니다. 이 2866 RFC에에서 정의 된 대로 NPS에서 사용 되는 기본 UDP 포트 합니다. 다른 포트를 사용 하는 경우 1813에 대 한 포트 번호를 대체 합니다.
- 주변 네트워크 인터페이스 원본 IP 주소 및 NPS 서버 1645 \(0x66D\) UDP 소스 포트 \(Optional\) 합니다. 이 필터 인터넷 기반 RADIUS 클라이언트 NPS 서버에서 RADIUS 인증 트래픽을 수 있게합니다. 이 이전 RADIUS 클라이언트에서 사용 되는 UDP 포트 합니다.
- 주변 네트워크 인터페이스 원본 IP 주소 및 NPS 서버 1646 \(0x66E\) UDP 소스 포트 \(Optional\) 합니다. 이 필터 인터넷 기반 RADIUS 클라이언트 NPS 서버에서 RADIUS 계정 트래픽을 수 있게합니다. 이 이전 RADIUS 클라이언트에서 사용 되는 UDP 포트 합니다.

### <a name="configure-input-filters-on-the-perimeter-network-interface"></a>주변 네트워크에 입력된 필터가 구성

다음과 같은 유형의 교통 수 있도록 방화벽 주변 네트워크에 다음과 같은 입력된 필터를 구성 합니다.

- IP 주소 주변 네트워크 인터페이스 및 NPS 서버 (0x714) 1812 UDP 소스 포트 소스입니다. 이 필터 인터넷 기반 RADIUS 클라이언트 NPS 서버에서 RADIUS 인증 트래픽을 수 있게합니다. 이 RFC 2865에 정의 된 대로 NPS에서 사용 되는 기본 UDP 포트 합니다. 다른 포트를 사용 하는 경우 1812에 대 한 포트 번호를 대체 합니다.
- IP 주소 주변 네트워크 인터페이스 및 NPS 서버 (0x715) 1813 UDP 소스 포트 소스입니다. 이 필터 인터넷 기반 RADIUS 클라이언트 NPS 서버에서 RADIUS 계정 트래픽을 수 있게합니다. 이 2866 RFC에에서 정의 된 대로 NPS에서 사용 되는 기본 UDP 포트 합니다. 다른 포트를 사용 하는 경우 1813에 대 한 포트 번호를 대체 합니다.
- 주변 네트워크 인터페이스 원본 IP 주소 및 NPS 서버 1645 \(0x66D\) UDP 소스 포트 \(Optional\) 합니다. 이 필터 인터넷 기반 RADIUS 클라이언트 NPS 서버에서 RADIUS 인증 트래픽을 수 있게합니다. 이 이전 RADIUS 클라이언트에서 사용 되는 UDP 포트 합니다.
- 주변 네트워크 인터페이스 원본 IP 주소 및 NPS 서버 1646 \(0x66E\) UDP 소스 포트 \(Optional\) 합니다. 이 필터 인터넷 기반 RADIUS 클라이언트 NPS 서버에서 RADIUS 계정 트래픽을 수 있게합니다. 이 이전 RADIUS 클라이언트에서 사용 되는 UDP 포트 합니다.

### <a name="configure-output-filters-on-the-perimeter-network-interface"></a>주변 네트워크에 출력 필터가 구성

다음과 같은 유형의 교통 수 있도록 방화벽 주변 네트워크에 다음과 같은 출력 패킷 필터를 구성 합니다.

- IP 주소 주변 네트워크 인터페이스 및 NPS 서버 (0x714) 1812 UDP 목적지 포트 대상 합니다. 이 필터 NPS 서버에 인터넷 기반 RADIUS 클라이언트의 RADIUS 인증 교통 수 있게합니다. 이 RFC 2865에 정의 된 대로 NPS에서 사용 되는 기본 UDP 포트 합니다. 다른 포트를 사용 하는 경우 1812에 대 한 포트 번호를 대체 합니다.
- IP 주소 주변 네트워크 인터페이스 및 NPS 서버 (0x715) 1813 UDP 목적지 포트 대상 합니다. 이 필터 NPS 서버에 인터넷 기반 RADIUS 클라이언트의 RADIUS 계정 교통 수 있게합니다. 이 2866 RFC에에서 정의 된 대로 NPS에서 사용 되는 기본 UDP 포트 합니다. 다른 포트를 사용 하는 경우 1813에 대 한 포트 번호를 대체 합니다.
- 주변 네트워크 인터페이스 대상 IP 주소 및 NPS 서버 1645 \(0x66D\) UDP 목적지 포트 \(Optional\) 합니다. 이 필터 NPS 서버에 인터넷 기반 RADIUS 클라이언트의 RADIUS 인증 교통 수 있게합니다. 이 이전 RADIUS 클라이언트에서 사용 되는 UDP 포트 합니다.
- 주변 네트워크 인터페이스 대상 IP 주소 및 NPS 서버 1646 \(0x66E\) UDP 목적지 포트 \(Optional\) 합니다. 이 필터 NPS 서버에 인터넷 기반 RADIUS 클라이언트의 RADIUS 계정 교통 수 있게합니다. 이 이전 RADIUS 클라이언트에서 사용 되는 UDP 포트 합니다.

보안을 강화 보내는 클라이언트 NPS 서버의 IP 주소와 교통량 필터 주변 네트워크의 정의를 방화벽을 통해 패킷이 각 RADIUS 클라이언트의 IP 주소를 사용할 수 있습니다.

### <a name="filters-on-the-perimeter-network-interface"></a>주변 네트워크에 필터

다음과 같은 유형의 교통 수 있도록 인트라넷 방화벽 주변 네트워크에 다음과 같은 입력된 패킷 필터를 구성 합니다.

- IP 주소 NPS 서버 주변 네트워크 인터페이스 소스입니다. 이 필터 주변 네트워크에 있는 NPS 서버에서 교통량을 허용합니다.

다음과 같은 유형의 교통 수 있도록 인트라넷 방화벽 주변 네트워크에 다음과 같은 출력 필터를 구성 합니다.

- IP 주소 NPS 서버 주변 네트워크 인터페이스 대상 합니다. 이 필터 주변 네트워크 NPS 서버에 대 한 교통량을 허용합니다.

### <a name="filters-on-the-intranet-interface"></a>필터 인트라넷 인터페이스에서

다음과 같은 유형의 교통 수 있도록 방화벽 인트라넷 인터페이스에서 다음과 같은 입력된 필터를 구성 합니다.

- IP 주소 NPS 서버 주변 네트워크 인터페이스 대상 합니다. 이 필터 주변 네트워크 NPS 서버에 대 한 교통량을 허용합니다.

다음과 같은 유형의 교통 수 있도록 방화벽 인트라넷 인터페이스에서 다음과 같은 출력 패킷 필터를 구성 합니다.

- IP 주소 NPS 서버 주변 네트워크 인터페이스 소스입니다. 이 필터 주변 네트워크에 있는 NPS 서버에서 교통량을 허용합니다.


NPS 관리에 대 한 자세한 내용은 참조 [네트워크 정책 서버 관리](nps-manage-top.md)합니다.

NPS에 대 한 자세한 내용은 참조 [네트워크 NPS 정책 서버 ()](nps-top.md)합니다.




