---
title: DHCP 문제 해결을 위한 일반적인 지침
description: 이 artilce DHCP 문제를 해결 하는 일반적인 지침을 소개 합니다.
ms.prod: windows-server
ms.service: na
manager: dcscontentpm
ms.technology: server-general
ms.date: 5/26/2020
ms.topic: article
author: Deland-Han
ms.author: delhan
ms.openlocfilehash: c0460791fef2451722af09e8bbe08b51a605f01b
ms.sourcegitcommit: ef089864980a1d4793a35cbf4cbdd02ce1962054
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/28/2020
ms.locfileid: "84150161"
---
# <a name="general-guidance-to-troubleshoot-dhcp"></a>DHCP 문제 해결을 위한 일반적인 지침

문제 해결을 시작 하기 전에 다음 항목을 확인 하십시오. 이를 통해 문제의 근본 원인을 찾을 수 있습니다.

## <a name="checklist"></a>검사 목록

  - 문제가 언제 시작되었나요?

  - 오류 메시지가 있나요?

  - DHCP 서버가 이전에 작동 했거나 작동 하지 않나요?  
    이전에 작동 한 경우 문제가 시작 되기 전에 무엇이 변경 되었습니까? 예를 들어 업데이트를 설치 했습니까? 인프라에 변경 사항이 있나요?

  - 문제가 지속 되 고 간헐적 입니까? 간헐적으로 발생 하는 경우 마지막으로 발생 한 경우

  - 모든 클라이언트 또는 단일 범위 서브넷과 같은 특정 클라이언트에 대해서만 주소 임대 오류가 발생 하나요?

  - DHCP 서버와 동일한 네트워크 서브넷에 클라이언트가 있나요?

  - 클라이언트가 동일한 네트워크 서브넷에 있는 경우 IP 주소를 얻을 수 있나요?

  - 클라이언트가 동일한 네트워크 서브넷에 있지 않은 경우에는 라우터 또는 VLAN 스위치가 DHCP 릴레이 에이전트 (IP 도우미 라고도 함)를 포함 하도록 올바르게 구성 되어 있나요?

  - DHCP 서버가 독립 실행형 이거나 분할 범위 또는 DHCP 장애 조치 (Failover)와 같은 고가용성을 위해 구성 되어 있습니까?

  - 중간 장치에서 문제를 일으키는 것으로 알려진 VRRP/HSRP, 동적 ARP 검사 또는 DHCP 스누핑 등의 기능을 확인 합니다.
