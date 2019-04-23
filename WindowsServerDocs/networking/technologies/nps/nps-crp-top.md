---
title: 연결 요청 처리
description: 이 항목에서는 Windows Server 2016에서 처리 하는 네트워크 정책 서버 연결 요청에 대 한 개요를 제공 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 849d661a-42c1-4f93-b669-6009d52aad39
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6ab08dced15cfadd5a0fc773efc2ddaa2da24c08
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829114"
---
# <a name="connection-request-processing"></a>연결 요청 처리

>적용 대상: Windows Server (반기 채널), Windows Server 2016

Windows Server 2016에서 네트워크 정책 서버에서 처리 하는 연결 요청에 대해 자세히 알아보려면이 항목에서는 사용할 수 있습니다.

>[!NOTE]
>이 항목 외에 문서를 처리 하는 다음 연결 요청은 사용할 수 있습니다.
> - [연결 요청 정책](nps-crp-crpolicies.md)
> - [영역 이름](nps-crp-realm-names.md)
> - [원격 RADIUS 서버 그룹](nps-crp-rrsg.md)

연결 요청 인증을 수행-원격 RADIUS 서버 그룹의 구성원 인 원격 RADIUS 서버 또는 로컬 컴퓨터의 위치를 지정 하려면 연결 요청 처리를 사용할 수 있습니다. 

정책 서버 NPS (네트워크) 연결 요청에 대 한 인증을 수행 하도록를 실행 하는 로컬 서버를 하려는 경우에 추가 구성 없이 기본 연결 요청 정책을 사용할 수 있습니다. 기본 정책에 따라 NPS 로컬 도메인 및 신뢰할 수 있는 도메인에 계정이 있는 사용자와 컴퓨터를 인증 합니다.

다른 RADIUS 서버 또는 원격 NPS 연결 요청을 전달 하려는 경우 원격 RADIUS 서버 그룹을 만들고 해당 원격 RADIUS 서버 그룹에 요청을 전달 하는 연결 요청 정책을 구성한 합니다. 이 구성을 사용 하 여 NPS RADIUS 서버에 인증 요청을 전달할 수 있습니다 하 고 신뢰할 수 없는 도메인에 계정이 있는 사용자를 인증할 수 있습니다.

다음 그림에서는 원격 RADIUS 서버 그룹의 액세스 요청 메시지의 네트워크 액세스 서버에서 RADIUS 프록시를 및 RADIUS 서버에 로그온 한 다음 경로 보여 줍니다. RADIUS 프록시에서 네트워크 액세스 서버를 RADIUS 클라이언트로 구성 됩니다. 및 각 RADIUS 서버에서 RADIUS 프록시의 RADIUS 클라이언트로 구성 됩니다.


![NPS 연결 요청 처리](../../media/Nps-Connection-Request-Processing/Nps-Connection-Request-Processing.jpg)


>[!NOTE]
>NPS와 함께 사용 하는 네트워크 액세스 서버는 802.1x 무선 액세스 지점 및 인증 스위치, VPN으로 구성 된 원격 액세스를 실행 하는 서버 또는 전화 접속 서버와 같은 RADIUS 프로토콜과 호환 되는 게이트웨이 장치 수 또는 다른 RADIUS 호환 장치입니다.

원격 RADIUS 서버 그룹에 다른 요청을 전달 하는 동안 일부 인증 요청을 로컬로 처리 하는 NPS를 하려는 경우에 둘 이상의 연결 요청 정책을 구성 합니다.

인증 요청을 처리 하는 NPS 또는 RADIUS 서버 그룹을 지정 하는 연결 요청 정책을 연결 요청 정책을 참조 하십시오.

NPS 또는 다른 RADIUS 서버는 인증 요청이 전달 되도록 원격 RADIUS 서버 그룹을 참조 하세요.

## <a name="nps-as-a-radius-server-connection-request-processing"></a>NPS를 RADIUS 서버 연결 요청 처리

NPS를 RADIUS 서버로 사용 하면 RADIUS 메시지 인증, 권한 부여 및 계정을 네트워크 액세스 연결에 대 한 다음과 같은 방법으로 제공 합니다.

1. 전화 접속 네트워크 액세스 서버, VPN 서버 및 무선 액세스 지점과 같은 액세스 서버를 액세스 클라이언트에서 연결 요청을 받습니다. 

2. RADIUS 인증, 권한 부여 및 계정 프로토콜을 사용 하도록 구성 된 액세스 서버에서 액세스 요청 메시지를 만들고를 NPS로 보냅니다. 

3. NPS는 액세스 요청 메시지를 평가합니다. 

4. 필요한 경우 NPS 액세스 서버에 액세스 챌린지 메시지를 보냅니다. 액세스 서버는 문제를 처리 하 고 NPS로 업데이트 된 액세스 요청을 보냅니다. 

5. 사용자 자격 증명이 확인 되 고 도메인 컨트롤러 보안 연결을 사용 하 여 사용자 계정 전화 접속 속성을 가져옵니다. 

6. 연결 시도가 모두 전화 접속 속성으로 사용자 계정 및 네트워크 정책 권한이 부여 됩니다. 

7. 연결 시도가 인증 되 고 권한이 부여, 하는 경우 NPS는 액세스 서버에 액세스 허용 메시지를 보냅니다. 연결 시도가 인증 되지 않거나 권한이 없는, 하는 경우 NPS 액세스 서버에는 액세스 거부 메시지를 보냅니다. 

8. 액세스 서버는 액세스 클라이언트를 사용 하 여 연결 프로세스를 완료 하 고 메시지가 기록 되는 위치를 NPS로는 계정 요청 메시지를 보냅니다. 

9. NPS는 액세스 서버에는 계정 응답을 보냅니다. 

>[!NOTE]
>또한 액세스 서버에 연결 되는, 액세스 클라이언트 연결이 닫힐 때 액세스 서버를 시작 및 중지 시간 동안 계정 요청 메시지를 보냅니다.

## <a name="nps-as-a-radius-proxy-connection-request-processing"></a>NPS를 RADIUS 프록시 연결 요청 처리

RADIUS 클라이언트와 RADIUS 서버 사이의 RADIUS 프록시로 NPS를 사용 하면 네트워크에 대 한 RADIUS 메시지 액세스 연결 시도 다음과 같은 방법으로 전달 됩니다.

1. 전화 접속 네트워크 액세스 서버, 가상 사설망 (VPN) 서버 및 무선 액세스 지점과 같은 액세스 서버를 액세스 클라이언트에서 연결 요청을 받습니다.

2. RADIUS 인증, 권한 부여 및 계정 프로토콜을 사용 하도록 구성 된 액세스 서버에서 액세스 요청 메시지를 만들고 NPS RADIUS 프록시로 사용 되는 NPS로 보냅니다.

3. NPS RADIUS 프록시에 액세스 요청 메시지를 받는 로컬로 구성 된 연결 요청 정책에 따라, 액세스 요청 메시지를 전달할 위치를 결정 합니다.

4. NPS RADIUS 프록시에서 액세스 요청 메시지를 적절 한 RADIUS 서버로 전달합니다.

5. RADIUS 서버는 액세스 요청 메시지를 평가합니다.

6. 필요한 경우 RADIUS 서버의 메시지를 보냅니다 액세스 챌린지 NPS RADIUS 프록시에 액세스 서버에 전달 됩니다. 액세스 서버는 액세스 클라이언트를 사용 하 여 문제를 처리 하 고 RADIUS 서버로 전달 됩니다 NPS RADIUS 프록시에 업데이트 된 액세스 요청을 보냅니다.

7. RADIUS 서버 인증 및 연결 시도 인증 합니다.

8. 연결 시도가 인증 되 고 권한이 부여, 하는 경우 RADIUS 서버는 액세스 허용 메시지를 보냅니다 NPS RADIUS 프록시 액세스 서버에 전달 됩니다. 연결 시도가 인증 되지 않거나 권한이 없는, 하는 경우 RADIUS 서버는 액세스 거부 메시지를 보냅니다 NPS RADIUS 프록시 액세스 서버에 전달 됩니다.

9. 액세스 서버는 액세스 클라이언트를 사용 하 여 연결 프로세스를 완료 하 고 NPS RADIUS 프록시 계정 요청 메시지를 보냅니다. NPS RADIUS 프록시 계정 데이터를 기록 하 고 RADIUS 서버에 메시지를 전달 합니다.

10. RADIUS 서버 응답을 보냅니다는 회계-NPS RADIUS 프록시에 액세스 서버에 전달 됩니다.

NPS에 대 한 자세한 내용은 참조 하세요. [네트워크 정책 (NPS 서버)](nps-top.md)합니다.
