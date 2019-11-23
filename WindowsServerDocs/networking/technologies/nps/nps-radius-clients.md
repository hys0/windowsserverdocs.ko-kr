---
title: RADIUS 클라이언트
description: 이 항목에서는 Windows Server 2016의 네트워크 정책 서버에 대 한 RADIUS 클라이언트에 대 한 개요를 제공 합니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: d3a09ac9-75f8-4f57-aab4-b0fdfe110118
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1dfc1bb71d2800a8a9587e54147950dfd7fb371f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71396002"
---
# <a name="radius-clients"></a>RADIUS 클라이언트

>적용 대상: Windows Server(반기 채널), Windows Server 2016

NAS\) \(네트워크 액세스 서버는 더 큰 네트워크에 대 한 특정 수준의 액세스를 제공 하는 장치입니다. RADIUS 인프라를 사용 하는 NAS는 인증, 권한 부여 및 계정에 대해 연결 요청 및 계정 메시지를 RADIUS 서버로 보내는 RADIUS 클라이언트 이기도 합니다.

>[!NOTE]
>랩톱 컴퓨터 및 클라이언트 운영 체제를 실행 하는 다른 컴퓨터와 같은 클라이언트 컴퓨터는 RADIUS 클라이언트가 아닙니다. RADIUS 클라이언트는 radius 프로토콜을 사용 하 여 NPS\) 서버 \(네트워크 정책 서버와 같은 RADIUS 서버와 통신 하기 때문에 무선 액세스 지점의 802.1 X 인증 스위치, 가상 사설망 \(VPN\) 서버 및 전화 접속 서버와 같은 네트워크 액세스 서버입니다.

Radius 서버 또는 RADIUS 프록시로 NPS를 배포 하려면 NPS에서 RADIUS 클라이언트를 구성 해야 합니다.

## <a name="radius-client-examples"></a>RADIUS 클라이언트 예제

네트워크 액세스 서버의 예는 다음과 같습니다.

- 조직 네트워크 또는 인터넷에 대 한 원격 액세스 연결을 제공 하는 네트워크 액세스 서버입니다. 예를 들어 Windows Server 2016 운영 체제 및 원격 액세스 서비스를 실행 하는 컴퓨터에서 조직 인트라넷에 기존 전화 접속 또는 VPN (가상 사설망) 원격 액세스 서비스를 제공 하는 경우를 예로 들 수 있습니다.
- 무선 기반 전송 및 수신 기술을 사용 하 여 조직 네트워크에 대 한 물리적 계층 액세스를 제공 하는 무선 액세스 지점이 제공 됩니다.
- 이더넷과 같은 기존 LAN 기술을 사용 하 여 조직의 네트워크에 대 한 물리적 계층 액세스를 제공 하는 스위치입니다.
- Radius 프록시에 구성 된 원격 RADIUS 서버 그룹의 구성원 인 RADIUS 서버에 대 한 연결 요청을 전달 하는 RADIUS 프록시입니다.

## <a name="radius-access-request-messages"></a>RADIUS 액세스-요청 메시지

Radius 클라이언트는 radius 액세스 요청 메시지를 만들어 RADIUS 프록시 또는 RADIUS 서버에 전달 하거나, 다른 RADIUS 클라이언트에서 받았지만 직접 만들지 않은 RADIUS 서버에 액세스 요청 메시지를 전달 합니다.

RADIUS 클라이언트는 인증, 권한 부여 및 계정을 수행 하 여 액세스 요청 메시지를 처리 하지 않습니다. RADIUS 서버만 이러한 기능을 수행 합니다.

그러나 NPS는 RADIUS 프록시와 RADIUS 서버로 동시에 구성 될 수 있으므로 일부 액세스 요청 메시지를 처리 하 고 다른 메시지를 전달 합니다.

## <a name="nps-as-a-radius-client"></a>RADIUS 클라이언트로 서의 NPS

NPS는 radius 프록시로 구성 하 여 액세스 요청 메시지를 다른 RADIUS 서버에 전달 하 여 처리할 수 있습니다. NPS를 RADIUS 프록시로 사용 하는 경우 다음과 같은 일반 구성 단계가 필요 합니다.

1. 무선 액세스 지점이 나 VPN 서버와 같은 네트워크 액세스 서버는 NPS 프록시의 IP 주소를 지정 된 RADIUS 서버 또는 인증 서버로 구성 됩니다. 이렇게 하면 액세스 클라이언트에서 받은 정보를 기반으로 액세스 요청 메시지를 만들어 NPS 프록시로 메시지를 전달 하는 네트워크 액세스 서버를 사용할 수 있습니다.

2. NPS 프록시는 각 네트워크 액세스 서버를 RADIUS 클라이언트로 추가 하 여 구성 됩니다. 이 구성 단계를 통해 NPS 프록시는 네트워크 액세스 서버에서 메시지를 수신 하 고 인증을 통해 통신할 수 있습니다. 또한 NPS 프록시의 연결 요청 정책은 하나 이상의 RADIUS 서버에 전달할 액세스 요청 메시지를 지정 하도록 구성 됩니다. 이러한 정책은 네트워크 액세스 서버에서 수신 하는 메시지를 보낼 위치를 NPS에 알려 주는 원격 RADIUS 서버 그룹을 사용 하 여 구성 됩니다.

3. Nps 또는 nps 프록시에서 원격 RADIUS 서버 그룹의 구성원 인 NPS 또는 기타 RADIUS 서버는 NPS 프록시에서 메시지를 받도록 구성 됩니다. 이는 RADIUS 클라이언트로 NPS 프록시를 구성 하 여 수행 됩니다.

## <a name="radius-client-properties"></a>RADIUS 클라이언트 속성

Nps 콘솔을 사용 하거나 nps 또는 Windows PowerShell 용 netsh 명령을 사용 하 여 nps 구성에 RADIUS 클라이언트를 추가 하는 경우 네트워크 액세스 서버 또는에서 RADIUS 액세스 요청 메시지를 받도록 NPS를 구성 하는 중입니다. RADIUS 프록시.

NPS에서 RADIUS 클라이언트를 구성 하는 경우 다음 속성을 지정할 수 있습니다.

### <a name="client-name"></a>클라이언트 이름

 Nps 스냅인 또는 NPS 용 netsh 명령을 사용 하는 경우 쉽게 식별할 수 있도록 하는 RADIUS 클라이언트의 이름입니다.

### <a name="ip-address"></a>IP 주소

인터넷 프로토콜 버전 4 \(IPv4\) 주소 또는 도메인 이름 시스템 \(DNS\) 이름 RADIUS 클라이언트입니다.

### <a name="client-vendor"></a>클라이언트-공급 업체

RADIUS 클라이언트의 공급 업체입니다. 그렇지 않으면 클라이언트 공급 업체에 대 한 RADIUS 표준 값을 사용할 수 있습니다.

### <a name="shared-secret"></a>공유 암호

RADIUS 클라이언트, RADIUS 서버 및 RADIUS 프록시 사이의 암호로 사용 되는 텍스트 문자열입니다. 메시지 인증자 특성을 사용 하는 경우 공유 암호는 RADIUS 메시지를 암호화 하는 키로도 사용 됩니다. 이 문자열은 RADIUS 클라이언트와 NPS 스냅인에서 구성 해야 합니다.

### <a name="message-authenticator-attribute"></a>메시지 인증자 특성

RFC 2869, "RADIUS 확장"에 설명 된 메시지 다이제스트 5 \(전체 RADIUS 메시지의 해시를\) 합니다. RADIUS 메시지 인증자 특성이 있으면 확인 됩니다. 확인이 실패 하면 RADIUS 메시지가 무시 됩니다. 클라이언트 설정에 메시지 인증자 특성이 필요 하 고 존재 하지 않는 경우에는 RADIUS 메시지가 무시 됩니다. 메시지 인증자 특성을 사용 하는 것이 좋습니다.

>[!NOTE]
>EAP\) 인증 \(확장할 수 있는 인증 프로토콜을 사용 하는 경우 메시지 인증자 특성이 필요 하며 기본적으로 사용 하도록 설정 되어 있습니다. 

NPS에 대 한 자세한 내용은 [nps (네트워크 정책 서버)](nps-top.md)를 참조 하세요.

