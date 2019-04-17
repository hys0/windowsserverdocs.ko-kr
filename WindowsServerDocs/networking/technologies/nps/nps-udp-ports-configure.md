---
title: 구성 NPS UDP 포트 정보
description: 네트워크 NPS 정책 서버 () RADIUS(Remote Authentication Dial-In User Service) (RADIUS) 인증과 계정 교통 Windows Server 2016에 사용 하 여 포트 구성 하려면이 항목을 사용할 수 있습니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 70569958-d7a7-474e-a817-6b7b5134784a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f0e703dc6f9083f1e79091a6cee6d1ac58753d12
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="configure-nps-udp-port-information"></a>구성 NPS UDP 포트 정보

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

다음 절차 RADIUS(Remote Authentication Dial-In User Service) \(RADIUS\) 인증과 계정 교통 네트워크 NPS 정책 서버 () 사용 하 여 포트 구성을 사용할 수 있습니다.

기본적으로 NPS RADIUS 트래픽을 모든 설치 된 네트워크 어댑터에 대 한 1812, 1813 1645 및 인터넷 프로토콜 버전 6 \(IPv6\) 및 IPv4 1646 포트에서 수신합니다.

>[!NOTE]
>네트워크 어댑터에 IPv4 또는 IPv6 제거, NPS RADIUS 교통 제거 프로토콜에 대 한을 모니터링 하지 않습니다.

인증에 대 한 1812 및 1813 계정에 대 한 포트 값은 RADIUS 표준 포트에 정의 된 대로만 2865 Rfc 및 2866 인터넷 엔지니어링 작업 힘 \(IETF\)입니다. 그러나 기본적으로 많은 액세스 서버 포트를 사용 1645 인증 요청을와 1646 계정 요청에 있습니다. 포트 번호를 사용 하려는 어떤에 관계 없이 NPS 액세스 서버 같은 기능을 사용 하 여 구성 되어 있는지 확인 합니다.

>[중요 한] RADIUS 기본 포트 번호를 사용 하지 않는 경우 방화벽 RADIUS 트래픽을 새로운 포트에서 허용 하는 로컬 컴퓨터에 대 한 예외 구성 해야 합니다. 자세한 내용은 참조 [RADIUS 교통에 대 한 구성 방화벽](nps-firewalls-configure.md)합니다.

회원 **도메인 관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.

## <a name="to-configure-nps-udp-port-information"></a>포트 정보 NPS UDP 구성 하려면 

1. NPS console을 엽니다.
2. 마우스 오른쪽 단추로 클릭 **네트워크 정책 서버**을 차례로 클릭 하 고 **속성**합니다.
3. 클릭 하 고 **포트** 탭 한 다음 포트에 대 한 설정을 검토 합니다. 기본 제공 (1812 및 인증을 위한 1645 및 1813 및 값 1646)에서 RADIUS 인증과 계정 UDP RADIUS 포트가 다를에서 포트 설정을 입력 **인증** 및 **계정**합니다.
4. 인증 또는 계정 요청에 대 한 여러 포트 설정을 사용 하려면 포트 번호 쉼표로 구분 합니다.

NPS 관리에 대 한 자세한 내용은 참조 [네트워크 정책 서버 관리](nps-manage-top.md)합니다.

NPS에 대 한 자세한 내용은 참조 [네트워크 NPS 정책 서버 ()](nps-top.md)합니다.
