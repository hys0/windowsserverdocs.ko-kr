---
title: RADIUS 클라이언트
description: 이 항목에서는 Windows Server 2016에서 네트워크 정책 서버에 대 한 RADIUS 클라이언트의 개요를 제공 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: d3a09ac9-75f8-4f57-aab4-b0fdfe110118
ms.author: pashort
author: shortpatti
ms.openlocfilehash: fdca45237d971c1b2e08443112b63d3ce77e4a2d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59874314"
---
# <a name="radius-clients"></a>RADIUS 클라이언트

>적용 대상: Windows Server (반기 채널), Windows Server 2016

네트워크 액세스 서버 \(NAS\) 일정 수준의 더 큰 네트워크에 대 한 액세스를 제공 하는 장치입니다. RADIUS 인프라를 사용 하 여 NAS RADIUS 클라이언트를 인증, 권한 부여에 대 한 RADIUS 서버로 연결 요청 및 계정 메시지를 전송 및 계정 이기도 합니다.

>[!NOTE]
>랩톱 컴퓨터 및 클라이언트 운영 체제를 실행 하는 다른 컴퓨터 등의 클라이언트 컴퓨터는 RADIUS 클라이언트가 아닙니다. RADIUS 클라이언트는 네트워크 액세스 서버-무선 액세스 지점, 802.1x 인증 스위치, 가상 사설망 \(VPN\) 서버 및 전화 접속 서버-RADIUS를 사용 하 여 통신 하는 RADIUS 프로토콜을 사용 하기 때문에 네트워크 정책 서버와 같은 서버 \(NPS\) 서버.

NPS를 RADIUS 서버로 또는 RADIUS 프록시를 배포 하려면 NPS에서 RADIUS 클라이언트를 구성 해야 합니다.

## <a name="radius-client-examples"></a>RADIUS 클라이언트 예제

네트워크 액세스 서버는 예제입니다.

- 조직 네트워크 또는 인터넷에 대 한 원격 액세스 연결을 제공 하는 네트워크 액세스 서버입니다. 예로 조직 인트라넷에 Windows Server 2016 운영 체제 및 원격 액세스 제공 하는 서비스 중 일반적인 전화 접속 또는 가상 사설망 (VPN) 원격 액세스 서비스를 실행 하는 컴퓨터입니다.
- 물리적 계층 무선 기반 전송 및 수신 기술을 사용 하 여 조직 네트워크에 대 한 액세스를 제공 하는 무선 액세스 지점입니다.
- 물리적 계층 이더넷과 같은 기존 LAN 기술을 사용 하 여 조직의 네트워크에 대 한 액세스를 제공 하는 스위치입니다.
- RADIUS 프록시에 구성 되어 있는 원격 RADIUS 서버 그룹의 구성원 인 RADIUS 서버로 연결 요청을 전달 하는 RADIUS 프록시

## <a name="radius-access-request-messages"></a>RADIUS 액세스 요청 메시지

RADIUS 클라이언트 중 RADIUS 액세스 요청 메시지 만들기 및 RADIUS 프록시 또는 RADIUS 서버에 전달할 또는 다른 RADIUS 클라이언트에서 받은 있지만 자체를 만든 RADIUS 서버에 대 한 액세스 요청 메시지를 전달 하는 합니다.

RADIUS 클라이언트 인증, 권한 부여를 수행 하 고 고려 하 여 액세스 요청 메시지를 처리 하지 않습니다. RADIUS 서버 에서만 이러한 함수를 수행 합니다.

NPS는 구성할 수 있습니다 RADIUS 프록시 및 RADIUS 서버 모두 동시에 일부 액세스 요청 메시지를 처리 하 고 다른 메시지를 전달할 수 있도록 합니다.

## <a name="nps-as-a-radius-client"></a>NPS를 RADIUS 클라이언트로

액세스 요청 메시지 처리를 위해 다른 RADIUS 서버를 전달 하는 RADIUS 프록시로 구성 하는 경우 NPS를 RADIUS 클라이언트로 작동 합니다. RADIUS 프록시로 NPS를 사용 하는 경우는 다음과 같은 일반 구성 단계가 필요 합니다.

1. 무선 액세스 지점 및 VPN 서버와 같은 네트워크 액세스 서버를 지정 된 RADIUS 서버 또는 인증 서버로 NPS 프록시의 IP 주소를 사용 하 여 구성 됩니다. 이렇게 하면 NPS 프록시로 메시지를 전달할 액세스 클라이언트에서 받은 정보에 따라 액세스 요청 메시지를 작성 하는 네트워크 액세스 서버를 수 있습니다.

2. NPS 프록시는 각 네트워크 액세스 서버를 RADIUS 클라이언트로 추가 하 여 구성 됩니다. 이 구성 단계에는 NPS 프록시를 네트워크 액세스 서버에서 메시지를 수신 하는 데 전체 인증에서 통신할 수 있습니다. 또한 NPS 프록시에 연결 요청 정책은 하나 이상의 RADIUS 서버로 전달 하는 액세스 요청 메시지를 지정 하도록 구성 됩니다. 이러한 정책은 NPS 네트워크 액세스 서버에서 수신한 메시지를 보낼 위치를 지시 하는 원격 RADIUS 서버 그룹을 사용 하 여 구성 됩니다.

3. NPS 또는 NPS 프록시에서 원격 RADIUS 서버 그룹의 구성원 인 다른 RADIUS 서버에서 NPS 프록시 메시지를 수신 하도록 구성 됩니다. 이렇게 하려면 NPS 프록시를 RADIUS 클라이언트로 구성 하 여 합니다.

## <a name="radius-client-properties"></a>RADIUS 클라이언트 속성

네트워크 액세스 서버에서 RADIUS 액세스 요청 메시지를 수신 하는 NPS를 구성 하는 RADIUS 클라이언트를 NPS 콘솔을 통해 또는 NPS 용 netsh 명령 또는 Windows PowerShell 명령을 사용 하 여 NPS 구성에 추가할 때 또는 RADIUS 프록시입니다.

NPS에서 RADIUS 클라이언트를 구성 하는 경우에 다음 속성을 지정할 수 있습니다.

### <a name="client-name"></a>클라이언트 이름

 NPS 스냅인 또는 netsh 명령을 사용 하 여 NPS에 대 한 때 쉽게 식별할 수 있도록 RADIUS 클라이언트에 대 한 이름입니다.

### <a name="ip-address"></a>IP 주소

인터넷 프로토콜 버전 4 \(IPv4\) 주소나 Domain Name System \(DNS\) RADIUS 클라이언트의 이름입니다.

### <a name="client-vendor"></a>클라이언트-공급 업체

RADIUS 클라이언트의 공급 업체입니다. 그렇지 않으면 클라이언트 공급 업체에 대 한 RADIUS 표준 값을 사용할 수 있습니다.

### <a name="shared-secret"></a>공유 암호

RADIUS 클라이언트, RADIUS 서버 및 RADIUS 프록시 간의 암호로 사용 되는 텍스트 문자열입니다. 메시지 인증자 특성을 사용 하는 경우 공유 암호도 사용 됩니다 키로 RADIUS 메시지를 암호화 하기. NPS 스냅인에서 RADIUS 클라이언트에이 문자열을 설정 해야 합니다.

### <a name="message-authenticator-attribute"></a>메시지 인증자 특성

RFC 2869, RADIUS "Extensions", 메시지 다이제스트 5에에서 설명 된 \(MD5\) 전체 RADIUS 메시지의 해시입니다. RADIUS 메시지 인증자 특성이 있는 경우 확인 됩니다. 확인 실패 한 경우에 RADIUS 메시지가 무시 됩니다. 클라이언트 설정 메시지 인증자 특성 하며 없는, 하는 경우에 RADIUS 메시지가 삭제 됩니다. 메시지 인증자 특성을 사용 하는 것이 좋습니다.

>[!NOTE]
>메시지 인증자 특성은 필수 이며 Extensible Authentication Protocol을 사용 하는 경우 기본적으로 사용 하도록 설정 \(EAP\) 인증 합니다. 

NPS에 대 한 자세한 내용은 참조 하세요. [네트워크 정책 (NPS 서버)](nps-top.md)합니다.

