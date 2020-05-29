---
title: DHCP (Dynamic Host Configuration Protocol)에 대 한 문제 해결 가이드
description: 이 artilce는 DHCP 문제에 대 한 문제 해결 가이드를 소개 합니다.
ms.prod: windows-server
ms.service: na
manager: dcscontentpm
ms.technology: server-general
ms.date: 5/26/2020
ms.topic: article
author: Deland-Han
ms.author: delhan
ms.openlocfilehash: 4bded9f879061903b1e925632a3cb4c83dfaac08
ms.sourcegitcommit: ef089864980a1d4793a35cbf4cbdd02ce1962054
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/28/2020
ms.locfileid: "84150321"
---
# <a name="troubleshooting-guide-for-dynamic-host-configuration-protocol-dhcp"></a>DHCP (Dynamic Host Configuration Protocol)에 대 한 문제 해결 가이드

네트워크에서 작동할 수 있는 모든 장치 (예: 컴퓨터 또는 전화)의 경우 IP 주소를 할당 해야 합니다. 수동으로 또는 자동으로 IP 주소를 할당할 수 있습니다. 자동 할당은 DHCP 서비스 (Microsoft 또는 타사 서버)에 의해 처리 됩니다.

이 문서에서는 Microsoft IPv4 DHCP 클라이언트 및 서버에 대 한 일반적인 문제 해결 단계에 대해 설명 합니다.

## <a name="more-information"></a>자세한 정보

IPv4 주소 할당 절차에는 일반적으로 다음 세 가지 주요 구성 요소가 포함 됩니다.

- IP 주소를 가져와야 하는 DHCP 클라이언트 장치

- 특정 설정에 따라 클라이언트에 IP 주소를 제공 하는 DHCP 서비스입니다.

- 다른 네트워크 세그먼트로 DHCP 브로드캐스트 요청을 보내기 위한 DHCP 릴레이 에이전트/IP 도우미

DHCP 클라이언트와 서버 간 통신은 두 피어 간에 세 가지 종류의 상호 작용으로 구성 됩니다.

- **브로드캐스트 기반 DORA** (검색, 제안, 요청, 승인). 이 프로세스는 다음 단계로 구성됩니다.
  
    - DHCP 클라이언트는 범위 내의 모든 사용 가능한 DHCP 서버에 DHCP 검색 브로드캐스트 요청을 보냅니다.
  
    - Dhcp 제품 브로드캐스트 응답이 DHCP 서버에서 수신 되어 사용 가능한 IP 주소 임대를 제공 합니다.
  
    - DHCP 클라이언트 브로드캐스트 요청은 제공 된 IP 주소 임대 및 DHCP 브로드캐스트 승인을 끝에 요청 합니다.
  
    - DHCP 클라이언트와 서버가 서로 다른 논리 네트워크 세그먼트에 있는 경우 DHCP 릴레이 에이전트는 전달자를 작동 하 여 피어 간에 DHCP 브로드캐스트 패킷을 보내고 주고 보냅니다.

- **유니캐스트 Dhcp 갱신 요청**: ip 주소 임대 시간 50% 후 ip 주소 할당을 갱신 하기 위해 dhcp 클라이언트에서 dhcp 서버로 직접 전송 됩니다.

- **Dhcp 브로드캐스트 요청 다시 바인딩**: 클라이언트 범위 내의 모든 dhcp 서버에 적용 됩니다. IP 주소 임대 기간의 87.5% 이후에 전송 된 유니캐스트 요청이 작동 하지 않음을 나타냅니다. DORA 프로세스의 경우이 프로세스에는 DHCP 릴레이 에이전트 통신이 포함 됩니다.

Microsoft DHCP 클라이언트가 유효한 DHCP IPv4 주소를 수신 하지 않는 경우 클라이언트는 APIPA 주소를 사용 하도록 구성 될 수 있습니다. 자세한 내용은 다음 기술 자료 문서를 참조 하십시오.  
[220874](https://support.microsoft.com/help/220874) DHCP 서버 없이 tcp/ip 주소 자동 지정을 사용 하는 방법

모든 통신은 UDP 포트 67 및 68에서 수행 됩니다. 자세한 내용은 다음 기술 자료 문서를 참조 하십시오.  
[169289](https://support.microsoft.com/help/169289) DHCP (동적 호스트 구성 프로토콜) 기본 사항입니다.