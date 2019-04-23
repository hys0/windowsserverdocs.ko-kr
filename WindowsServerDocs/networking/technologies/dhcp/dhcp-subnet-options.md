---
title: DHCP 서브넷 선택 옵션
description: 이 항목에 대 한 동적 호스트 구성 프로토콜 (DHCP) Windows Server 2016에서 DHCP 서브넷 선택 옵션에 대 한 정보를 제공합니다.
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-dhcp
ms.topic: get-started-article
ms.assetid: ca19e7d1-e445-48fc-8cf5-e4c45f561607
ms.author: pashort
author: shortpatti
ms.date: 08/17/2018
ms.openlocfilehash: 034ca48ef13a6bdac63ca99ac753fc9826460922
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870814"
---
# <a name="dhcp-subnet-selection-options"></a>DHCP 서브넷 선택 옵션

>적용 대상: Windows Server (반기 채널), Windows Server 2016

새 DHCP 서브넷 선택 옵션에 대 한 내용은이 항목에서는 사용할 수 있습니다.

지원 옵션 82 이제 DHCP \(하위 5 옵션\)합니다. DHCP 프록시 클라이언트와 릴레이 에이전트에서 특정 IP 주소 범위와 범위를 특정 서브넷을 IP 주소를 요청할 수 있도록 이러한 옵션을 사용할 수 있습니다.  자세한 내용은 참조 하세요. **옵션 82 하위 옵션 5**: [DHCPv4에 대 한 릴레이 에이전트 정보 옵션에 대 한 RFC 3527 링크 선택 하위 옵션](https://tools.ietf.org/html/rfc3527)합니다.

옵션 5 하위 82 DHCP 옵션을 사용 하 여 구성 된 DHCP 릴레이 에이전트를 사용 하는 경우 릴레이 에이전트가 특정 IP 주소 범위에서 DHCP 클라이언트에 대 한 IP 주소 임대를 요청할 수 있습니다.


## <a name="option-82-sub-option-5-link-selection-sub-option"></a>82 option 하위 옵션 5: 링크 선택 하위 옵션

릴레이 에이전트 링크 선택 하위 옵션에는 DHCP 릴레이 에이전트는 DHCP 서버 IP 주소 및 옵션 할당 해야 하는 IP 서브넷을 지정할 수 있습니다.

일반적으로, DHCP 릴레이 에이전트 게이트웨이 IP 주소에 의존 \(GIADDR\) DHCP 서버와 통신 하는 필드입니다. 그러나 GIADDR 해당 두 작업 함수에 의해 제한 됩니다.

1. 서버에 알리는 DHCP IP 주소 임대를 요청 하는 DHCP 클라이언트는 서브넷에 대 한 합니다.
2. 릴레이 에이전트와 통신 하는 데 IP 주소의 DHCP 서버에 알림을 보내야 합니다.

경우에 따라 DHCP 서버와 통신 하는 릴레이 에이전트가 사용 하는 IP 주소는 DHCP 클라이언트 IP 주소를 할당 해야 하는 IP 주소 범위 보다 달라질 수 있습니다. 

82 옵션의 링크 선택 하위 옵션이 릴레이 에이전트 82 하위 옵션 5 DHCP v4 옵션의 형태로 할당 된 IP 주소는 원하는 서브넷을 명시적으로 지정할 수 있습니다.이 이런 경우에 유용 합니다.

> [!NOTE]
>
> 모든 릴레이 에이전트 IP 주소 (GIADDR)는 활성 DHCP 범위 IP 주소 범위에 속해야 합니다. DHCP 범위 IP 주소 범위를 벗어난 모든 GIADDR rogue 릴레이 것으로 간주 됩니다 및 Windows DHCP 서버 해당 릴레이 에이전트에서 DHCP 클라이언트 요청을 승인 하지 않습니다.
>
> 특별 한 범위를 "권한 부여" 릴레이 에이전트를 만들 수 있습니다. GIADDR (또는 여러 IP 주소를 순차적 GIADDR의 경우)를 사용 하 여 범위를 만들고 GIADDR 주소 배포에서 제외 범위를 활성화 합니다. 이 때 GIADDR 주소를 할당 하지 않도록 릴레이 에이전트를 인증 합니다.


### <a name="use-case-scenario"></a>사용 사례 시나리오

이 시나리오에서는 조직 네트워크 포함 DHCP 서버 및 무선 액세스 지점 \(AP\) 게스트 사용자에 대 한 합니다. 그러나 조직의 DHCP 서버에서-방화벽 정책 제한으로 인해 게스트 클라이언트 IP 주소를 할당, DHCP 서버에는 게스트 무선 네트워크 또는 무선 클라이언트 broadcase 메시지를 사용 하 여 액세스할 수 없습니다.

이 제한은 해결 하려면 AP 구성과 링크 선택 하위 옵션 5로 이어지는 내부 인터페이스의 IP 주소 지정 GIADDR에서 게스트 클라이언트에 할당 된 IP 주소는 원하는 서브넷을 지정 하는 회사 네트워크입니다.
