---
title: NPS UDP 포트 정보 구성
description: 전화 접속 사용자 서비스 RADIUS (Remote Authentication) 인증 및 Windows Server 2016에서 계정 관리 트래픽의 네트워크 정책 (NPS 서버)를 사용 하는 포트를 구성 하려면이 항목에서는 사용할 수 있습니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 70569958-d7a7-474e-a817-6b7b5134784a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 44c20092180c47e97f1505271203f4491606bbcf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851974"
---
# <a name="configure-nps-udp-port-information"></a>NPS UDP 포트 정보 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016

다음 절차를 사용 하 여 원격 인증 전화 접속 사용자 서비스에 대 한 서버 NPS (네트워크 정책)를 사용 하는 포트를 구성 하기 \(RADIUS\) 인증 및 계정 관리 트래픽의 합니다.

기본적으로 NPS RADIUS에서 트래픽을 수신 대기 포트 1812, 1813, 1645 및 1646 인터넷 프로토콜 버전 6에 대 한 \(IPv6\) 및 모든 설치 된 네트워크 어댑터에 대 한 IPv4 합니다.

>[!NOTE]
>네트워크 어댑터에 IPv4 또는 IPv6 중 하나를 제거 하는 경우 NPS RADIUS 트래픽을 제거 된 프로토콜에 대 한 모니터링 하지 않습니다.

인증용 1812 및 계정에 대해 1813 포트 값은 Internet Engineering Task Force에서 정의한 RADIUS 표준 포트 \(IETF\) Rfc 2865 및 2866에에서 있습니다. 그러나 기본적으로 많은 액세스 서버 포트 인증 요청에 대 한 1645 및 1646 요청에 사용할 계정입니다. 포트 번호에 관계 없이 사용 하 여, NPS 및 액세스 서버와 동일한 것을 사용 하도록 구성 되어 있는지 확인 하기로 합니다.

>[중요] RADIUS 기본 포트 번호를 사용 하지 않는 경우에 새 포트에서 RADIUS 트래픽을 허용 하도록 로컬 컴퓨터에 대 한 방화벽 예외를 구성 해야 합니다. 자세한 내용은 [RADIUS 트래픽에 대 한 방화벽 구성](nps-firewalls-configure.md)합니다.

**Domain Admins**의 구성원이거나 이에 준하는 자격이 있어야 이 절차를 완료할 수 있습니다.

## <a name="to-configure-nps-udp-port-information"></a>NPS UDP 포트 정보를 구성 하려면 

1. NPS 콘솔을 엽니다.
2. 마우스 오른쪽 단추로 클릭 **네트워크 정책 서버**를 클릭 하 고 **속성**합니다.
3. 클릭 합니다 **포트** 탭을 클릭 한 다음 포트에 대 한 설정을 검토 합니다. RADIUS 인증 및 RADIUS 계정 UDP 포트가 제공 되는 기본값 (1812 및 인증용 1645 및 1813 및 1646)에서 다를 경우 입력에서 포트 설정을 **Authentication** 고  **회계**합니다.
4. 인증 또는 계정 요청에 대 한 여러 포트 설정을 사용 하려면 포트 번호를 쉼표로 구분 합니다.

NPS를 관리 하는 방법에 대 한 자세한 내용은 참조 하세요. [네트워크 정책 서버 관리](nps-manage-top.md)합니다.

NPS에 대 한 자세한 내용은 참조 하세요. [네트워크 정책 (NPS 서버)](nps-top.md)합니다.
