---
title: 멀티홈 컴퓨터에서 NPS 구성
description: 이 항목에서는 Windows Server 2016에서 네트워크 정책 서버를 실행 하는 여러 네트워크 어댑터를 사용 하 여 서버를 구성 하는 지침을 제공 합니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: d9d9e9ac-4859-4522-89ed-a23092c9e12a
ms.author: lizross
author: eross-msft
ms.openlocfilehash: a937e151954629f7e8775ec68ba8ab5f2b63ee1a
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80315816"
---
# <a name="configure-nps-on-a-multihomed-computer"></a>멀티홈 컴퓨터에서 NPS 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2016

여러 네트워크 어댑터를 사용 하 여 NPS를 구성 하려면이 항목을 사용할 수 있습니다.

NPS (네트워크 정책 서버)를 실행 하는 서버에서 여러 네트워크 어댑터를 사용 하는 경우 다음을 구성할 수 있습니다.

- RADIUS(Remote Authentication Dial-In User Service) \(RADIUS\) 트래픽을 전송 및 수신 하지 않는 네트워크 어댑터입니다.
- 네트워크 어댑터를 기준으로 NPS는 인터넷 프로토콜 버전 4 \(IPv4\), IPv6 또는 IPv4 및 IPv6 모두에서 RADIUS 트래픽을 모니터링 하는지 여부를 지정 합니다.
- IPv4 또는 IPv6\)네트워크 어댑터를 기준으로 하는 프로토콜에 따라 RADIUS 트래픽이 전송 및 수신 되는 UDP 포트 번호를 \(합니다.

기본적으로 NPS는 설치 된 모든 네트워크 어댑터에 대해 IPv6 및 IPv4의 포트 1812, 1813, 1645 및 1646에 대 한 RADIUS 트래픽을 수신 대기 합니다. NPS는 RADIUS 트래픽에 대해 모든 네트워크 어댑터를 자동으로 사용 하므로 nps가 특정 네트워크 어댑터를 사용 하지 못하도록 하려면 NPS에서 RADIUS 트래픽에 사용할 네트워크 어댑터만 지정 해야 합니다.

>[!NOTE]
>네트워크 어댑터에서 IPv4 또는 IPv6을 제거 하는 경우 NPS는 제거 된 프로토콜에 대 한 RADIUS 트래픽을 모니터링 하지 않습니다.

네트워크 어댑터가 여러 개 설치 된 NPS에서 지정 된 어댑터 에서만 RADIUS 트래픽을 보내고 받도록 NPS를 구성 해야 할 수 있습니다.

예를 들어 NPS에 설치 된 네트워크 어댑터 하나는 RADIUS 클라이언트를 포함 하지 않는 네트워크 세그먼트로 이어질 수 있으며, 두 번째 네트워크 어댑터는 NPS에 구성 된 RADIUS 클라이언트에 대 한 네트워크 경로를 제공 합니다. 이 시나리오에서는 NPS가 모든 RADIUS 트래픽에 대해 두 번째 네트워크 어댑터를 사용 하도록 지시 하는 것이 중요 합니다.

또 다른 예로 NPS에 세 개의 네트워크 어댑터가 설치 되어 있지만 NPS에서 RADIUS 트래픽에 대해 두 개의 어댑터를 사용 하려는 경우에만 두 어댑터에 대 한 포트 정보를 구성할 수 있습니다. 세 번째 어댑터에 대 한 포트 구성을 제외 하 여 NPS에서 RADIUS 트래픽에 대해 어댑터를 사용 하지 못하도록 합니다.

## <a name="using-a-network-adapter"></a>네트워크 어댑터 사용

네트워크 어댑터에서 RADIUS 트래픽을 수신 하 고 보내도록 NPS를 구성 하려면 NPS 콘솔의 네트워크 정책 서버에 대 한 속성 대화 상자에서 다음 구문을 사용 합니다.

- IPv4 트래픽 구문: IPAddress: UDPport. 여기서 IPAddress는 RADIUS 트래픽을 보내려는 네트워크 어댑터에서 구성 된 IPv4 주소이 고, UDPport는 RADIUS 인증 또는 계정에 사용 하려는 RADIUS 포트 번호입니다. 교통.
- IPv6 트래픽 구문: [IPv6Address]: UDPport (IPv6Address 주위의 대괄호가 필요 함), IPv6Address는 RADIUS 트래픽을 보내려는 네트워크 어댑터에서 구성 된 IPv6 주소, UDPport는 원하는 RADIUS 포트 번호입니다. RADIUS 인증 또는 계정 트래픽에 사용 하는입니다.

IP 주소와 UDP 포트 정보를 구성 하는 데 다음 문자를 구분 기호로 사용할 수 있습니다.

- 주소/포트 구분 기호: 콜론 (:)
- 포트 구분 기호: 쉼표 (,)
- 인터페이스 구분 기호: 세미콜론 (;)

## <a name="configuring-network-access-servers"></a>네트워크 액세스 서버 구성

네트워크 액세스 서버가 NPSs에서 구성 하는 것과 동일한 RADIUS UDP 포트 번호를 사용 하 여 구성 되었는지 확인 합니다. Rfc 2865 및 2866에 정의 된 RADIUS 표준 UDP 포트는 인증을 위한 1812와 계정에 대 한 1813입니다. 그러나 일부 액세스 서버는 기본적으로 인증 요청에 UDP 포트 1645을 사용 하 고, 계정 요청에는 UDP 포트 1646을 사용 하도록 구성 됩니다.

>[!IMPORTANT]
>RADIUS 기본 포트 번호를 사용 하지 않는 경우 새 포트에서 RADIUS 트래픽을 허용 하도록 로컬 컴퓨터의 방화벽에 대 한 예외를 구성 해야 합니다. 자세한 내용은 [RADIUS 트래픽에 대 한 방화벽 구성](nps-firewalls-configure.md)을 참조 하세요.

## <a name="configure-the-multihomed-nps"></a>멀티홈 NPS 구성

멀티홈 NPS를 구성 하려면 다음 절차를 사용할 수 있습니다.

이 절차를 완료하려면 적어도 **Domain Admins** 그룹 구성원이거나 이에 해당하는 권한이 있어야 합니다.

### <a name="to-specify-the-network-adapter-and-udp-ports-that-nps-uses-for-radius-traffic"></a>NPS에서 RADIUS 트래픽에 사용 하는 네트워크 어댑터 및 UDP 포트를 지정 하려면

1. 서버 관리자에서 **도구**를 클릭 한 다음 **네트워크 정책 서버** 를 클릭 하 여 NPS 콘솔을 엽니다.

2. **네트워크 정책 서버**를 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다.

3. **포트** 탭을 클릭 하 고 RADIUS 트래픽에 사용 하려는 네트워크 어댑터의 IP 주소를 기존 포트 번호 앞에 추가 합니다. 예를 들어 인증 요청에 IP 주소 192.168.1.2 및 RADIUS 포트 1812 및 1645을 사용 하려면 포트 설정을 **1812, 1645** 에서 **192.168.1.2:1812, 1645**로 변경 합니다. RADIUS 인증 및 RADIUS 계정 UDP 포트가 기본값과 다른 경우 포트 설정을 적절 하 게 변경 합니다.

4. 인증 또는 계정 요청에 여러 포트 설정을 사용 하려면 포트 번호를 쉼표로 구분 합니다.

NPS UDP 포트에 대 한 자세한 내용은 [NPS Udp 포트 정보 구성](nps-udp-ports-configure.md) 을 참조 하세요.


NPS에 대 한 자세한 내용은 [네트워크 정책 서버](nps-top.md) 를 참조 하세요.

