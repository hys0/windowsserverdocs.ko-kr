---
title: DHCP(Dynamic Host Configuration Protocol) DHCP)
description: 이 항목에서는 DHCP(Dynamic Host Configuration Protocol) (DHCP) Windows Server 2016에 대 한 간략 한 소개 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dhcp
ms.topic: article
ms.assetid: 0ff29ef3-c458-4432-9065-e50a7de5b4b9
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 770cfd78c7b9a0e122bd9f9936623a73b56af808
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="dynamic-host-configuration-protocol-dhcp"></a>DHCP(Dynamic Host Configuration Protocol) DHCP)

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목에 대 한 개요 dhcp Windows Server 2016에 사용할 수 있습니다.

>[!NOTE]
>이 항목 외에 다음과 같은 DHCP 문서를 사용할 수 있습니다.
>
>- [DHCP의 새로운 기능](What-s-New-in-DHCP.md)
>- [DHCP를 사용 하 여 Windows PowerShell 배포](dhcp-deploy-wps.md)

DHCP(Dynamic Host Configuration Protocol) DHCP ()는 자동으로 IP (인터넷 프로토콜) 호스트 IP 주소와 같은 서브넷 마스크와 기본 게이트웨이 기타 관련된 구성 정보를 제공 하는 클라이언트/서버 프로토콜 합니다. 2131 및 2132 Rfc 정의 DHCP으로 인터넷 엔지니어링 작업 포스 (IETF) 표준에 부트스트랩 (BOOTP 프로토콜), DHCP 사용 하는 많은 구현 세부 정보를 공유 하는 프로토콜을 기반으로 합니다. DHCP 호스트를 DHCP 서버에서 필요한 TCP/IP 구성 정보를 얻을 수 있습니다.

Windows Server 2016에는 IP 주소를 임대 네트워크가 및 기타 정보 DHCP 클라이언트를에 배포할 수 있는 선택적 네트워킹 서버 역할 DHCP 서버에 포함 되어 있습니다. DHCP 클라이언트 기본적으로 활성화 되어 및 모든 Windows 기반 클라이언트 운영 체제는 클라이언트에서 DHCP TCP/IP의 일부로 포함 됩니다.

## <a name="why-use-dhcp"></a>DHCP를 사용 하는 이유는?

IP 기반 네트워크의 모든 디바이스에는 네트워크 및 리소스에 액세스 하려면 고유한 유니캐스트 IP 주소가 있어야 합니다. DHCP를 않고도 새 컴퓨터 또는 한 서브넷에서 다른 위치로 이동는 컴퓨터의 IP 주소 수동으로 구성 해야 합니다. 네트워크에서 제거 하는 컴퓨터의 IP 주소 수동으로 회수 합니다.

Dhcp를이 전체 프로세스는 자동으로 및 중앙 관리 합니다. DHCP 서버 풀의 IP 주소를 유지 하 고 네트워크에은 시작 시 클라이언트 DHCP를 사용 하는 주소 임대 합니다. IP 주소는 동적 (임대) 정적 (영구적으로 지정 됨) 하는 대신, 더 이상 사용 하 여 주소 자동으로 다시 할당 풀으로 돌아갑니다.

네트워크 관리자 TCP/IP 구성 정보를 유지 하 고 주소 구성 임대 제안의 형태로 DHCP 사용 하는 클라이언트를 제공 하는 DHCP 서버 설정 합니다. DHCP 서버 구성 정보를 포함 하는 데이터베이스에 저장 됩니다.

- 네트워크의 모든 클라이언트에 대 한 TCP/IP 구성 매개 유효 합니다.

- 유효한 IP 주소가 클라이언트의 경우 지정 하기 위해 풀에 유지 뿐만 아니라 주소 제외 합니다.

- 예약 된 IP 주소 특정 DHCP는 클라이언트와 관련 된 합니다. 이 통해 일관성 있는 단일 DHCP 클라이언트 단일 IP 주소를 지정 합니다.

- 임대 기간 하거나 기간에는 IP 주소 사용할 수 있는 임대 갱신이 필요 합니다.

임대 제안을 수락 시 DHCP를 사용 하도록 클라이언트를 받을 수 있습니다.

- 연결 된 서브넷 유효한 IP 주소가 합니다.  
  
- DHCP를 하도록 구성 된 추가 매개 DHCP 옵션을 요청 하는 클라이언트를 할당 합니다. DHCP 옵션의 몇 가지 예는 라우터에 (기본 게이트웨이), DNS 서버, 및 DNS 도메인 이름입니다.

## <a name="benefits-of-dhcp"></a>DHCP의 이점

DHCP는 다음과 같은 이점을 제공합니다.

- **신뢰할 수 있는 IP 주소 구성**합니다. DHCP 최소화 입력 오류와 같은 수동 IP 주소 구성으로 인 한 구성 오류 또는 동시에 여러 개 컴퓨터에 IP 주소 할당으로 인 한 충돌을 해결 합니다.

- **네트워크 관리를 줄였습니다**합니다. DHCP은 네트워크 관리를 줄이기 위해 다음과 같은 기능이 포함 됩니다.

    - 중앙 집중식된 자동된 TCP/IP 구성 합니다.

    - TCP/IP 구성을 한곳에서 정의 수 있습니다.

    - DHCP 옵션을 사용 하 여 추가 TCP/IP 구성 값 여러 지정할 수 있습니다.

    - 무선 네트워크의 다른 위치로 이동 휴대용 장치에 대 한 등과 같이 자주를 업데이트 해야 하는 클라이언트 효율적으로 처리 IP 주소를 변경 합니다.

    - 모든 서브넷 DHCP 서버에 대 한 하지 않아도 DHCP 전달할 에이전트를 사용 하 여 초기 DHCP 메시지를 전달 됩니다.

