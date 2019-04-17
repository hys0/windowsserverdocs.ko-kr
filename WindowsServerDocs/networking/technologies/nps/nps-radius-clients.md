---
title: RADIUS 클라이언트
description: 이 항목에서는 Windows Server 2016에 네트워크 정책 서버에 대 한 RADIUS 클라이언트 개요를 제공 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: d3a09ac9-75f8-4f57-aab4-b0fdfe110118
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a970dabcc6f3f4fc4d8ed5a0dedd01b5a7dee71a
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="radius-clients"></a>RADIUS 클라이언트

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

네트워크 액세스 서버 \(NAS\)는 어느 정도 더 큰 네트워크에 대 한 액세스를 제공 하는 디바이스입니다. 사용 하 여 radius NAS RADIUS 클라이언트, 인증, 인증, RADIUS 서버에 연결 요청 하 고 계정 메시지를 보내는 및 계정 이기도 합니다.

>[!NOTE]
>클라이언트 운영 체제를 실행 하는 다른 컴퓨터, 랩톱 컴퓨터 등 클라이언트 컴퓨터 RADIUS 클라이언트 되지 않습니다. 네트워크 정책 서버 \(NPS\) 서버 등 RADIUS 서버와 통신 하는 RADIUS 프로토콜을 사용 하기 때문에 RADIUS 클라이언트는 무선 액세스 포인트 등 네트워크 액세스 서버-, 802.1 X 인증 스위치, 가상 개인 네트워크 \(VPN\) 서버 및 전화 접속 서버-합니다.

NPS RADIUS 서버 또는 RADIUS 프록시 배포를 NPS RADIUS 클라이언트 구성 해야 합니다.

## <a name="radius-client-examples"></a>클라이언트 예 RADIUS

네트워크 액세스 서버의 예는 다음과 같습니다.

- 조직의 네트워크 또는 인터넷에 액세스 원격 연결을 제공 하는 네트워크 액세스 서버 합니다. 예를 들어 Windows Server 2016 운영 체제 중 하나 일반적인 전화 접속 제공 하는 원격 액세스 서비스 또는 가상 개인 네트워크 (VPN) 원격 액세스 서비스와 회사 인트라넷을 실행 하는 컴퓨터입니다.
- 실제 계층 무선 기반 송수신 기술을 사용 하 여 회사 네트워크에 대 한 액세스를 제공 하는 무선 액세스 포인트 합니다.
- 실제 계층 이더넷 같은 기존 LAN 기술을 사용 하 여 조직의 네트워크에 대 한 액세스를 제공 하는 전환 합니다.
- RADIUS 프록시 RADIUS 프록시에서 구성 된 원격 RADIUS 서버 그룹의 회원 RADIUS 서버에 연결 요청을 전달입니다.

## <a name="radius-access-request-messages"></a>RADIUS 액세스 요청 메시지

RADIUS 클라이언트 하거나 RADIUS 액세스 요청 메시지를 작성 및 RADIUS 프록시 또는 RADIUS 서버에 게 전달할 수 하거나 다른 RADIUS 클라이언트에서 받은 된 자체 만들지 않은 RADIUS 서버에 요청 액세스 메시지를 전달 합니다.

RADIUS 클라이언트 계정 및 인증 인증을 수행 하 여 메시지 액세스 요청을 처리 하지 않습니다. 만 RADIUS 서버 이러한 기능을 수행 합니다.

그러나 NPS 구성할 수 있습니다 RADIUS 프록시와 RADIUS 서버 동시에 처리 하는 일부 액세스 요청 메시지 및 기타 메시지를 전달 되도록 합니다.

## <a name="nps-as-a-radius-client"></a>NPS RADIUS 클라이언트로

다른 RADIUS 서버 처리에 대 한 액세스 요청 메시지를 전달 하는 RADIUS 프록시 구성 NPS RADIUS 클라이언트로 작동 합니다. NPS RADIUS 프록시도를 사용 하면 다음 일반 구성 단계가 필요 합니다.

1. 네트워크 액세스 서버 무선 액세스 포인트 및 VPN 서버의 NPS RADIUS 서버 지정된 또는 인증 서버 프록시 IP 주소를 가진 구성 됩니다. 따라서 NPS 프록시 메시지를 전달 하기 위해 액세스 클라이언트에서 수신 액세스 요청 메시지 정보에 따라 만들 되 네트워크 액세스 서버가 있습니다.

2. 프록시 NPS RADIUS 클라이언트로 각 네트워크 액세스 서버를 추가 하 여 구성 됩니다. 이 구성 단계 NPS 프록시를 인증 전반에서 통신 하도록 하 고 네트워크 액세스 서버에서 메시지를 받을 수 있습니다. 또한 연결 요청 정책 NPS 프록시에 하나 이상의 RADIUS 서버에 전달 하도록 액세스 요청 메시지를 지정 구성 됩니다. 이 정책 그룹과 원격 RADIUS 서버, NPS 네트워크 액세스 서버에서 수신 메시지를 보낼 수 있는 위치에 알려주는 구성 됩니다.

3. NPS 또는 NPS 프록시에서 원격 RADIUS 서버 그룹의 회원 다른 RADIUS 서버 NPS 프록시에서 메시지를 받는 구성 됩니다. 프록시 NPS RADIUS 클라이언트로 구성으로 수행 됩니다.

## <a name="radius-client-properties"></a>RADIUS 클라이언트 속성

RADIUS 클라이언트 NPS 구성 NPS 콘솔을 통해 또는 NPS netsh 명령을 또는 Windows PowerShell 명령을 사용 하 여에 추가 하면를 구성 하는 NPS RADIUS 프록시 또는 네트워크 액세스 서버에서 RADIUS 액세스 요청 메시지를 받을 수 있습니다.

NPS RADIUS 클라이언트를 구성 다음 속성 지정할 수 있습니다.

### <a name="client-name"></a>클라이언트 이름

 쉽게 nps NPS 또는 netsh 스냅인 명령을 사용 하는 경우 사용자의 신원을 확인 RADIUS 클라이언트 이름입니다.

### <a name="ip-address"></a>IP 주소

인터넷 프로토콜 버전 4 \(IPv4\) 주소 또는 RADIUS 클라이언트의 Domain Name System \(DNS\) 이름입니다.

### <a name="client-vendor"></a>공급 업체 클라이언트

공급 업체 RADIUS 클라이언트의 합니다. 그렇지 않은 경우에 대 한 클라이언트 공급 업체 RADIUS 표준 값을 사용할 수 있습니다.

### <a name="shared-secret"></a>공유 암호

암호 RADIUS 고객과 RADIUS 서버, RADIUS 프록시 사이의으로 사용 되는 텍스트 문자열 합니다. 메시지 인증 특성을 사용 하는 경우 공유 암호는 또한 사용 키로 RADIUS 메시지를 암호화 하 합니다. 이 문자열 스냅인 NPS RADIUS 클라이언트 켜고 구성 되어야 합니다.

### <a name="message-authenticator-attribute"></a>메시지 인증 특성

한번 RADIUS "확장"을 전체 RADIUS 메시지 메시지 요약 5 \(MD5\) 콘텐츠의 해시 설명합니다. 메시지 인증자 특성 있으면 확인 합니다. 인증, 실패 RADIUS 메시지를 무시 합니다. 클라이언트 설정을 메시지 인증자 특성 필요 없는 RADIUS 메시지 삭제 됩니다. 메시지 인증 특성을 사용 하는 것이 좋습니다.

>[!NOTE]
>메시지 인증자 특성 필요 이며 Extensible 인증 프로토콜 \(EAP\) 인증을 사용 하면 기본적으로 활성화 됩니다. 

NPS에 대 한 자세한 내용은 참조 [네트워크 NPS 정책 서버 ()](nps-top.md)합니다.

