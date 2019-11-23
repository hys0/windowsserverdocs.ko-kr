---
title: NPS UDP 포트 정보 구성
description: 이 항목을 사용 하 여 NPS (네트워크 정책 서버)에서 Windows Server 2016의 RADIUS(Remote Authentication Dial-In User Service) (RADIUS) 인증 및 계정 트래픽에 사용 하는 포트를 구성할 수 있습니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 70569958-d7a7-474e-a817-6b7b5134784a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1ba6c059639b9ae7e77a9e103e7ed84f6a2032df
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405308"
---
# <a name="configure-nps-udp-port-information"></a>NPS UDP 포트 정보 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2016

다음 절차를 사용 하 여 NPS (네트워크 정책 서버)에서 \(RADIUS\) 인증 및 계정 트래픽을 RADIUS(Remote Authentication Dial-In User Service) 하는 데 사용 하는 포트를 구성할 수 있습니다.

기본적으로 NPS는 1812, 1813, 1645 및 1646 포트에서,, 및\) \(포트에서 RADIUS 트래픽을 수신 합니다.

>[!NOTE]
>네트워크 어댑터에서 IPv4 또는 IPv6을 제거 하는 경우 NPS는 제거 된 프로토콜에 대 한 RADIUS 트래픽을 모니터링 하지 않습니다.

1812의 포트 값은 인증을 위해 1813, Rfc 2865 및 2866에서는 IETF\) Internet 공학적 작업 Force \(에서 정의한 RADIUS 표준 포트입니다. 그러나 기본적으로 많은 액세스 서버는 인증 요청에 포트 1645을 사용 하 고 계정 요청에는 1646을 사용 합니다. 사용할 포트 번호에 관계 없이 NPS 및 액세스 서버는 동일한 포트 번호를 사용 하도록 구성 되어 있는지 확인 합니다.

>중요 한 RADIUS 기본 포트 번호를 사용 하지 않는 경우 새 포트에서 RADIUS 트래픽을 허용 하도록 로컬 컴퓨터의 방화벽에 대 한 예외를 구성 해야 합니다. 자세한 내용은 [RADIUS 트래픽에 대 한 방화벽 구성](nps-firewalls-configure.md)을 참조 하세요.

**Domain Admins**의 구성원이거나 이에 준하는 자격이 있어야 이 절차를 완료할 수 있습니다.

## <a name="to-configure-nps-udp-port-information"></a>NPS UDP 포트 정보를 구성 하려면 

1. NPS 콘솔을 엽니다.
2. **네트워크 정책 서버**를 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다.
3. **포트** 탭을 클릭 한 다음 포트에 대 한 설정을 검사 합니다. RADIUS 인증 및 RADIUS 계정 UDP 포트가 제공 된 기본값 (인증의 경우 1812 및 1645, 계정에 대 한 1813 및 1646)과 다를 경우 **인증** 및 **계정**에 포트 설정을 입력 합니다.
4. 인증 또는 계정 요청에 여러 포트 설정을 사용 하려면 포트 번호를 쉼표로 구분 합니다.

NPS를 관리 하는 방법에 대 한 자세한 내용은 [네트워크 정책 서버 관리](nps-manage-top.md)를 참조 하세요.

NPS에 대 한 자세한 내용은 [nps (네트워크 정책 서버)](nps-top.md)를 참조 하세요.
