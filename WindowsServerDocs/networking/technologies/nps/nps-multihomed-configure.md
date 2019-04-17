---
title: 다중 홈 컴퓨터 NPS 구성
description: 이 항목 서버를 실행 하는 네트워크 정책 Windows Server 2016에 여러 네트워크 어댑터와 구성에 대해 설명 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: d9d9e9ac-4859-4522-89ed-a23092c9e12a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f80e83a4d79036729b6b442e6362d52fbda12edd
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="configure-nps-on-a-multihomed-computer"></a>다중 홈 컴퓨터 NPS 구성

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

네트워크 어댑터가 여러 NPS 서버 구성 하려면이 항목을 사용할 수 있습니다.

네트워크 NPS 정책 서버 ()를 실행 하는 서버에 여러 네트워크 어댑터를 사용 하면 다음 구성할 수 있습니다.

- 네트워크 어댑터를 수행 하 고 수행 하지 보내고 받는 RADIUS(Remote Authentication Dial-In User Service) \(RADIUS\) 교통 합니다.
- 여부-네트워크 어댑터 별로 NPS이 인터넷 프로토콜 버전 4 \(IPv4\), IPv6 또는 둘 다 IPv4 및에서 IPv6 RADIUS 교통량을 모니터링합니다.
- 어떤 RADIUS 통해 교통은에서 보내고 받은 프로토콜에 따라 UDP 포트 번호 \-네트워크 어댑터 별로 (IPv4 또는 IPv6\).

기본적으로 NPS 수신 1812, 1813 1645 1646 및 포트의 RADIUS 교통 IPv6와 IPv4에 대 한 모든 설치 된 네트워크 어댑터에 대 한 합니다. 자동으로 NPS RADIUS 교통 모든 네트워크 어댑터 사용을 하기 때문에 NPS 특정 네트워크 어댑터를 사용 하지 못하도록 하려는 경우 네트워크 어댑터 NPS RADIUS에 대 한 사용 하 여 원하는 교통를 지정 하기만 하면 됩니다.

>[!NOTE]
>네트워크 어댑터에 IPv4 또는 IPv6 제거, NPS RADIUS 교통 제거 프로토콜에 대 한을 모니터링 하지 않습니다.

네트워크 어댑터가 있는 여러 설치 NPS 서버, NPS RADIUS 교통 사용자가 지정 어댑터에 대해서만 송수신를 구성할 좋습니다.

예를 들어, NPS 서버에 설치 된 네트워크 어댑터가 RADIUS 클라이언트 포함 되지 않는 네트워크 분할을 이어질 수, 네트워크 어댑터를 추가로 제공 하는 동안에 네트워크 경로로 NPS RADIUS 클라이언트를 구성 했으므로 합니다. 이이 시나리오 nps RADIUS 교통량 모든 두 번째 네트워크 어댑터를 사용 하 여 중요 합니다.

NPS 서버 설치 세 네트워크 어댑터에 있지만 NPS RADIUS 교통량 어댑터 중 두 사용 하 여 원하는 경우 다른 예에서 두 어댑터에 대 한 포트 정보를 구성할 수 있습니다. 세 번째 어댑터에 대 한 포트 구성 제외 하 고, NPS RADIUS 교통량 어댑터를 사용 하 여 방지할.

## <a name="using-a-network-adapter"></a>네트워크 어댑터를 사용 하 여

수신 하 고 네트워크 어댑터에 RADIUS 교통 전송 NPS 구성, NPS 콘솔에서 네트워크 정책 서버의 속성 대화 상자에서 다음 구문을 사용 합니다.

- IPv4 교통 구문을: IPAddress:UDPport 여기서 ip 주소 IPv4 주소 RADIUS 교통 있는 보내려는 네트워크 어댑터에서 구성 된 이며 UDPport RADIUS 포트 번호를 인증 RADIUS 또는 계정 교통에 사용 하려는 합니다.
- IPv6 교통 구문을: [IPv6Address]: UDPport 되는 IPv6Address 대괄호, IPv6Address IPv6 주소 RADIUS 교통 있는 보내려는 네트워크 어댑터에서 구성 된 이며 UDPport RADIUS 포트 번호를 인증 RADIUS 또는 계정 교통에 사용 하려는 합니다.

다음 문자 IP 주소와 UDP 포트 정보 구성 구분으로 사용할 수 있습니다.

- 주소/구분 포트:으로 (:)
- 포트 구분: 쉼표 (,)
- 구분 인터페이스: 세미콜론 (;)

## <a name="configuring-network-access-servers"></a>네트워크 액세스 서버 구성

네트워크 액세스 서버 NPS 서버에서 구성 하는 동일한 UDP RADIUS 포트 번호 구성 되어 있는지 확인 합니다. 2865와 2866 Rfc에 정의 된 RADIUS 표준 UDP 포트가 인증을 위한 1812 및 1813입니다. 그러나 일부 액세스 서버 인증 요청을 UDP 포트 1645 및 UDP 포트 1646 계정 요청에 대 한 사용 하는 기본적으로 구성 됩니다.

>[!IMPORTANT]
>RADIUS 기본 포트 번호를 사용 하지 않는 경우 방화벽 RADIUS 트래픽을 새로운 포트에서 허용 하는 로컬 컴퓨터에 대 한 예외 구성 해야 합니다. 자세한 내용은 참조 [RADIUS 교통에 대 한 구성 방화벽](nps-firewalls-configure.md)합니다.

## <a name="configure-the-multihomed-nps-server"></a>다중 홈 NPS 서버 구성

다음 절차 구성 다중 홈 NPS 서버를 사용할 수 있습니다.

회원 **도메인 관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.

### <a name="to-specify-the-network-adapter-and-udp-ports-that-nps-uses-for-radius-traffic"></a>네트워크 어댑터와 NPS RADIUS 교통에 사용 하는 UDP 포트를 지정 하려면

1. 서버 관리자 클릭 **도구**을 차례로 클릭 하 고 **네트워크 정책 서버** NPS 콘솔을 엽니다.

2. 마우스 오른쪽 단추로 클릭 **네트워크 정책 서버**을 차례로 클릭 하 고 **속성**합니다.

3. 클릭는 **포트** 탭 하 고 앞에 IP 주소 RADIUS 교통량 기존 포트 번호를 사용 하 여 네트워크 어댑터에 대 한 추가 합니다. 예를 들어, 인증 요청 192.168.1.2 IP 주소와 1812 및 1645 RADIUS 포트 사용 하려는 경우에서 포트 설정을 변경 **1812,1645** 에 **192.168.1.2:1812,1645**합니다. RADIUS 인증과 계정 UDP RADIUS 포트가 기본값 다른 경우 포트 설정을 변경 적절 하 게 됩니다.

4. 인증 또는 계정 요청에 대 한 여러 포트 설정을 사용 하려면 포트 번호 쉼표로 구분 합니다.

포트 NPS UDP에 대 한 자세한 내용은 참조 [구성 NPS UDP 포트 정보](nps-udp-ports-configure.md)


NPS에 대 한 자세한 내용은 참조 [네트워크 정책 서버](nps-top.md)

