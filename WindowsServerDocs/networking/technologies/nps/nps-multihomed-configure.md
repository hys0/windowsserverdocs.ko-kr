---
title: 멀티홈 컴퓨터에서 NPS 구성
description: 이 항목에서는 Windows Server 2016에서 네트워크 정책 서버를 실행 중인 여러 네트워크 어댑터를 사용 하 여 서버를 구성 하는 방법에 지침을 제공 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: d9d9e9ac-4859-4522-89ed-a23092c9e12a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 55eccf3afc649e84c5b6f5ce7932ed97617ddca9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856804"
---
# <a name="configure-nps-on-a-multihomed-computer"></a>멀티홈 컴퓨터에서 NPS 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016

여러 네트워크 어댑터를 사용 하 여 NPS를 구성 하려면이 항목에서는 사용할 수 있습니다.

네트워크 정책 (NPS 서버)를 실행 하는 서버에서 여러 네트워크 어댑터를 사용 하는 경우 다음을 구성할 수 있습니다.

- 수행 하 고 수행 하지 송신 및 수신 원격 인증 전화 접속 사용자 서비스는 네트워크 어댑터 \(RADIUS\) 트래픽입니다.
- 각 네트워크 어댑터 별로 여부 NPS RADIUS 트래픽을 모니터링 인터넷 프로토콜 버전 4 \(IPv4\), IPv6 또는 IPv4 및 IPv6입니다.
- UDP 포트 번호는 RADIUS를 통한 트래픽을 전달 하 고 개별 프로토콜에서 받은 \(IPv4 또는 IPv6\), 당 네트워크 어댑터를 기반으로 합니다.

기본적으로 NPS 수신 대기 포트 1812, 1813, 1645 및 1646에서 RADIUS 트래픽에 대 한 IPv6 및 IPv4 둘 다에 대 한 모든 네트워크 어댑터를 설치 합니다. NPS RADIUS 트래픽에 대 한 모든 네트워크 어댑터를 자동으로 사용, 때문에 NPS를 RADIUS를 사용 하 여 원하는 네트워크 어댑터 트래픽이 특정 네트워크 어댑터를 사용 하 여 NPS를 방지 하려는 경우 지정 해야 합니다.

>[!NOTE]
>네트워크 어댑터에 IPv4 또는 IPv6 중 하나를 제거 하는 경우 NPS RADIUS 트래픽을 제거 된 프로토콜에 대 한 모니터링 하지 않습니다.

여러 네트워크 어댑터가 설치 되어 있는 NPS에서 RADIUS 트래픽을 지정 하는 어댑터를 수신 하는 NPS를 구성 하는 것이 좋습니다.

예를 들어 NPS에 설치 된 하나의 네트워크 어댑터는 두 번째 네트워크 어댑터를 NPS의 네트워크 경로 사용 하 여 구성 된 RADIUS 클라이언트에 제공 하는 동안 RADIUS 클라이언트를 포함 하지 않는 네트워크 세그먼트에 발생할 수 있습니다. 이 시나리오에서 모든 RADIUS 트래픽에 대해 두 번째 네트워크 어댑터를 사용 하도록 NPS를 반드시 합니다.

에 NPS에 세 개의 네트워크 어댑터가 설치 되어 있지만 NPS를 RADIUS 트래픽에 대 한 두 가지 어댑터를 사용 하려는 경우 또 다른 예로, 두 어댑터에 대 한 포트 정보를 구성할 수 있습니다. 세 번째 어댑터의 포트 구성을 제외 하 고, RADIUS 트래픽에 대 한 어댑터를 사용 하 여 NPS 방지할 수 있습니다.

## <a name="using-a-network-adapter"></a>네트워크 어댑터를 사용 하 여

수신 대기할 네트워크 어댑터에서 RADIUS 트래픽을 전송 하는 NPS를 구성 하려면 NPS 콘솔에서 네트워크 정책 서버 속성 대화 상자에서 다음 구문을 사용 합니다.

- IPv4 트래픽 구문: IPAddress:UDPport, 여기서 IPAddress가 RADIUS 트래픽을 보내도록 원하는는 네트워크 어댑터에 구성 되어 있는 IPv4 주소 및 UDPport 계정 관리 트래픽의 RADIUS 인증에 사용 하려는 RADIUS 포트 번호입니다.
- IPv6 트래픽 구문: [IPv6Address]: UDPport, 여기서 IPv6Address 묶는 대괄호가 필요, IPv6Address RADIUS 트래픽을 보내도록 원하는는 네트워크 어댑터에 구성 된 IPv6 주소 이며 UDPport는 RADIUS 인증을 위해 사용 하려는 RADIUS 포트 번호 또는 계정 관리 트래픽의 합니다.

IP 주소 및 UDP 포트 정보 구성에 대 한 문자를 구분 기호로 사용할 수 있습니다.

- 구분 기호에 대 한 주소/포트: 콜론 (:)
- 포트 구분 기호: 쉼표 (,)
- 인터페이스 구분 기호: 세미콜론 (;)

## <a name="configuring-network-access-servers"></a>네트워크 액세스 서버를 구성합니다.

네트워크 액세스 서버에 NPSs에서 구성 하는 동일한 RADIUS UDP 포트 번호를 사용 하 여 구성 되었는지 확인 합니다. Rfc 2865 및 2866에에서 정의 된 RADIUS 표준 UDP 포트 1812 인증 되며 1813입니다. 그러나 일부 액세스 서버는 계정 요청에 대 한 인증 요청에 대 한 UDP 포트 1645 및 1646 UDP 포트를 사용 하 여 구성 됩니다.

>[!IMPORTANT]
>RADIUS 기본 포트 번호를 사용 하지 않는 경우에 새 포트에서 RADIUS 트래픽을 허용 하도록 로컬 컴퓨터에 대 한 방화벽 예외를 구성 해야 합니다. 자세한 내용은 [RADIUS 트래픽에 대 한 방화벽 구성](nps-firewalls-configure.md)합니다.

## <a name="configure-the-multihomed-nps"></a>멀티홈 NPS 구성

프로그램 멀티홈 NPS를 구성 하려면 다음 절차를 사용할 수 있습니다.

**Domain Admins**의 구성원이거나 이에 준하는 자격이 있어야 이 절차를 완료할 수 있습니다.

### <a name="to-specify-the-network-adapter-and-udp-ports-that-nps-uses-for-radius-traffic"></a>네트워크 어댑터와 NPS RADIUS 트래픽에 사용 되는 UDP 포트를 지정 하려면

1. 서버 관리자에서 클릭 **도구**를 클릭 하 고 **네트워크 정책 서버** NPS 콘솔을 엽니다.

2. 마우스 오른쪽 단추로 클릭 **네트워크 정책 서버**를 클릭 하 고 **속성**합니다.

3. 클릭 합니다 **포트** 탭 및 기존 포트 번호에 RADIUS 트래픽에 사용 하려는 네트워크 어댑터에 대 한 IP 주소 앞에 추가 합니다. 예를 들어, 인증 요청에 대 한 IP 주소 192.168.1.2 및 1645와 1812 RADIUS 포트를 사용 하려는 경우는에서 포트 설정을 변경 **1812,1645** 하 **192.168.1.2:1812,1645**합니다. RADIUS 인증 및 RADIUS 계정 UDP 포트가 다른 경우 기본값에서 변경 포트 설정을 적절 하 게 합니다.

4. 인증 또는 계정 요청에 대 한 여러 포트 설정을 사용 하려면 포트 번호를 쉼표로 구분 합니다.

NPS UDP 포트에 대 한 자세한 내용은 참조 하세요. [NPS UDP 포트 정보 구성](nps-udp-ports-configure.md)


NPS에 대 한 자세한 내용은 참조 하세요. [네트워크 정책 서버](nps-top.md)

