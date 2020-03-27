---
title: DHCP 서브넷 선택 옵션
description: 이 항목에서는 Windows Server 2016에서 dhcp (Dynamic Host Configuration Protocol)에 대 한 DHCP 서브넷 선택 옵션에 대 한 정보를 제공 합니다.
manager: dougkim
ms.prod: windows-server
ms.technology: networking-dhcp
ms.topic: get-started-article
ms.assetid: ca19e7d1-e445-48fc-8cf5-e4c45f561607
ms.author: lizross
author: eross-msft
ms.date: 08/17/2018
ms.openlocfilehash: 4e83448e95f6a6f77deb9ff7997d715cbc7f13c6
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312543"
---
# <a name="dhcp-subnet-selection-options"></a>DHCP 서브넷 선택 옵션

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 새 DHCP 서브넷 선택 옵션에 대 한 정보를 확인할 수 있습니다.

이제 DHCP는 옵션 82 \(하위 옵션 5\)를 지원 합니다. 이러한 옵션을 사용 하 여 DHCP 프록시 클라이언트 및 릴레이 에이전트가 특정 서브넷에 대 한 IP 주소와 특정 IP 주소 범위 및 범위를 요청할 수 있습니다.  자세한 내용은 [DHCPv4의 릴레이 에이전트 정보 옵션에 대](https://tools.ietf.org/html/rfc3527)한 **옵션 82 하위 옵션 5**: RFC 3527 링크 선택 하위 옵션을 참조 하십시오.

DHCP 옵션 82, 하위 옵션 5로 구성 된 DHCP 릴레이 에이전트를 사용 하는 경우 릴레이 에이전트는 특정 IP 주소 범위에서 DHCP 클라이언트에 대 한 IP 주소 임대를 요청할 수 있습니다.


## <a name="option-82-sub-option-5-link-selection-sub-option"></a>옵션 82 하위 옵션 5: 링크 선택 하위 옵션

릴레이 에이전트 링크 선택 하위 옵션을 사용 하면 dhcp 릴레이 에이전트가 DHCP 서버에서 IP 주소 및 옵션을 할당 해야 하는 IP 서브넷을 지정할 수 있습니다.

일반적으로 DHCP 릴레이 에이전트는 게이트웨이 IP 주소 \(GID ADDR\) 필드를 사용 하 여 DHCP 서버와 통신 합니다. 그러나 두 가지 작동 함수는

1. DHCP 서버에 IP 주소 임대를 요청 하는 DHCP 클라이언트가 있는 서브넷에 대해 알리려면
2. 릴레이 에이전트와 통신 하는 데 사용할 IP 주소를 DHCP 서버에 알립니다.

경우에 따라 릴레이 에이전트가 DHCP 서버와 통신 하는 데 사용 하는 IP 주소가 DHCP 클라이언트 IP 주소를 할당 해야 하는 IP 주소 범위와 다를 수 있습니다. 

옵션 82의 링크 선택 하위 옵션은이 상황에서 유용 하며, 릴레이 에이전트가 DHCP v4 option 82 하위 옵션 5 형식으로 할당 된 IP 주소를 원하는 서브넷의 상태를 명시적으로 지정할 수 있도록 합니다.

> [!NOTE]
>
> 모든 릴레이 에이전트 IP 주소 (GID 주소)는 활성 DHCP 범위 IP 주소 범위의 일부 여야 합니다. DHCP 범위 IP 주소 범위 외부에 있는 모든 GID는 rogue 릴레이로 간주 되 고 Windows DHCP 서버는 해당 릴레이 에이전트의 DHCP 클라이언트 요청을 인식 하지 못합니다.
>
> "권한 부여" 릴레이 에이전트에 대 한 특수 범위를 만들 수 있습니다. GID 주소를 사용 하 여 범위를 만들고 (또는 GID 주소가 순차적인 IP 주소인 경우 여러 개) 분포에서 GID 주소 주소를 제외 하 고 범위를 활성화 합니다. 이렇게 하면 GID 주소 주소가 할당 되는 것을 방지 하는 동시에 릴레이 에이전트에 권한을 부여 합니다.


### <a name="use-case-scenario"></a>사용 사례 시나리오

이 시나리오에서 조직 네트워크에는 게스트 사용자를 위한 DHCP 서버 및 무선 액세스 지점 \(AP\) 모두 포함 됩니다. 게스트 클라이언트 IP 주소는 조직 DHCP 서버에서 할당 됩니다. 그러나 방화벽 정책 제한으로 인해 DHCP 서버는 broadcase 메시지를 사용 하 여 게스트 무선 네트워크 또는 무선 클라이언트에 액세스할 수 없습니다.

이 제한을 해결 하기 위해 AP는 링크 선택 하위 옵션 5를 사용 하 여 구성 되며,이 옵션을 선택 하 여 게스트 클라이언트에 할당 된 IP 주소를 원하는 서브넷을 지정할 수 있습니다. 회사 네트워크.
