---
title: 요청을 처리 연결
description: 이 항목에서는 네트워크 정책 서버 연결 요청 처리 Windows Server 2016에 대 한 개요입니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 849d661a-42c1-4f93-b669-6009d52aad39
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6756c89dadbd01998ffef6a6d785c079076f2532
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="connection-request-processing"></a>요청을 처리 연결

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

Windows Server 2016에 네트워크 정책 서버에서 처리 연결 요청에 대 한 자세한 내용은이 항목을 사용할 수 있습니다.

>[!NOTE]
>이 항목 외에 다음 연결 요청을 처리 설명서를 사용할 수 있습니다.
> - [연결 요청 정책](nps-crp-crpolicies.md)
> - [영역 이름](nps-crp-realm-names.md)
> - [원격 RADIUS 서버 그룹](nps-crp-rrsg.md)

연결 요청 인증을 수행-원격 RADIUS 서버 그룹 구성원 원격 RADIUS 서버 또는 로컬 컴퓨터에서 위치를 지정 하려면 요청을 처리 연결을 사용할 수 있습니다. 

네트워크 NPS 정책 서버 () 인증을 수행 연결 요청을 실행 하는 로컬 서버 하려는 경우 기본 연결 요청 정책을 추가 구성 하지 않고 사용할 수 있습니다. 기본 정책에 따라, NPS 사용자와 기다렸다가 및 신뢰할 수 있는 도메인에 있는 계정이 컴퓨터를 인증 합니다.

원격 NPS 또는 기타 RADIUS 서버에 연결 요청을 전송 하도록 원격 RADIUS 서버 그룹 만들고 요청 원격 해당 RADIUS 서버 그룹을 전달 하는 연결 요청 정책의 구성 합니다. 이 구성 NPS RADIUS 서버에 요청 인증 전달할 수 및 사용자가 신뢰할 수 없는 도메인에 있는 계정 인증 될 수 있습니다.

다음 그림 원격 RADIUS 서버 그룹에 액세스 요청 메시지의 네트워크 액세스 서버에서 RADIUS 프록시도 이동한 다음 RADIUS 서버에 로그온 할 경로 보여 줍니다. 네트워크 액세스 서버 구성 RADIUS 클라이언트로 RADIUS 프록시에서 및 각 RADIUS 서버에서 RADIUS 프록시 RADIUS 클라이언트도 구성 됩니다.


![요청을 처리 NPS 연결](../../media/Nps-Connection-Request-Processing/Nps-Connection-Request-Processing.jpg)


>[!NOTE]
>802.1 X 무선 액세스 포인트 및 인증 스위치, VPN으로 구성 된 원격 액세스를 실행 하는 서버 또는 전화 접속 서버 등 RADIUS 프로토콜와 호환 되는 게이트웨이 디바이스 또는 다른 RADIUS 호환 되는 장치가 NPS와 함께 사용 하는 네트워크 액세스 서버 수 있습니다.

NPS RADIUS 서버 원격 그룹에 다른 요청을 전달 하는 동안 로컬로 일부 인증 요청을 처리 하기를 원하는 경우 둘 이상의 연결 요청 정책을 구성 합니다.

인증 요청을 처리 하는 어떤 NPS 또는 RADIUS 서버 그룹 지정 하는 연결 요청 정책을 연결 요청 정책 참조 하십시오.

NPS 또는 기타 RADIUS 서버 인증을 요청은 전달를 지정 하려면 원격 RADIUS 서버 그룹 참조 하십시오.

## <a name="nps-as-a-radius-server-connection-request-processing"></a>NPS RADIUS 서버 연결 요청 처리도

NPS RADIUS 서버를 사용 하면 RADIUS 메시지, 인증, 인증과 계정 액세스 네트워크 연결을 위해 다음과 같은 방법으로 제공 합니다.

1. 전화 접속 네트워킹 액세스 서버, VPN 서버의 무선 액세스 포인트 등 액세스 서버 액세스 하는 클라이언트에서 연결 요청을 받습니다. 

2. 인증, 권한 및 계정 프로토콜 RADIUS 사용 하도록 구성 액세스 서버 액세스 요청 메시지 만들고 NPS 서버에 전송 합니다. 

3. NPS 서버 액세스 요청 메시지를 확인합니다. 

4. 필요한 경우 NPS 서버 액세스 서버에 액세스 과제 메시지를 보냅니다. 액세스 서버 하는 문제를 처리 하 고 NPS 서버에 업데이트 액세스 요청을 보냅니다. 

5. 사용자 자격 증명 확인 되 고 사용자 계정의 전화 속성 도메인 컨트롤러에 보안 연결을 사용 하 여 가져옵니다. 

6. 사용자 계정 및 네트워크 정책 둘 다 전화 접속 속성와 연결 시도 권한이 부여 됩니다. 

7. 연결 시도 인증 되 고 권한이, NPS 서버 액세스 허용 메시지를 액세스 서버를 보냅니다. 연결 시도 인증 되지 않거나 권한이 없는, NPS 서버 액세스 거부 메시지를 액세스 서버를 보냅니다. 

8. 액세스 서버 액세스 고객과 연결 프로세스를 완료 하 고 메시지 기록 됩니다 NPS 서버에 계정 요청 메시지를 보냅니다. 

9. NPS 서버 계정 응답 액세스 서버에 전송 합니다. 

>[!NOTE]
>또한 액세스 서버에 연결 되는, 액세스 클라이언트 연결을 닫을 때 액세스 서버 시작 및 중지 하는 동안 계정 요청 메시지를 보냅니다.

## <a name="nps-as-a-radius-proxy-connection-request-processing"></a>NPS RADIUS 프록시 연결 요청 처리도

NPS RADIUS 서버 RADIUS 클라이언트 사이의 RADIUS 프록시도 사용 되 면 RADIUS 메시지 네트워크에 대 한 액세스 연결 시도 다음과 같은 방법으로 전달 됩니다.

1. 전화 접속 네트워킹 액세스 서버, 가상 개인 네트워크 (VPN) 서버, 무선 액세스 포인트 등 액세스 서버 액세스 클라이언트의 연결이 요청을 받습니다.

2. 인증, 권한 및 계정 프로토콜 RADIUS 사용 하도록 구성 액세스 서버 액세스 요청 메시지 만들고 NPS RADIUS 프록시도 사용 되는 NPS 서버에 전송 합니다.

3. NPS RADIUS 프록시 액세스 요청 메시지를 받고을 로컬로 구성 된 연결 요청 정책에 따라, 액세스 요청 메시지를 전달 하는 위치를 결정 합니다.

4. NPS RADIUS 프록시 적절 한 RADIUS 서버에 요청 액세스 메시지를 전달합니다.

5. RADIUS 서버 액세스 요청 메시지를 확인합니다.

6. 필요한 경우 RADIUS 서버는 액세스 과제 메시지를 보냅니다 NPS RADIUS 프록시 액세스 서버에 전달 됩니다. 액세스 서버 액세스 클라이언트에서 도전 과제를 처리 하 고 RADIUS 서버에 게 전달 NPS RADIUS 프록시 업데이트 액세스 요청을 보냅니다.

7. RADIUS 서버 인증 하 고 연결 시도 권한을 부여 합니다.

8. 연결 시도 인증 되 고 권한이, 경우 RADIUS 서버 있는 액세스 허용 메시지를 보냅니다 NPS RADIUS 프록시 액세스 서버에 전달 됩니다. 연결 시도 인증 되지 않거나 권한이 없는, 경우 RADIUS 서버 액세스 거부 메시지를 보냅니다 NPS RADIUS 프록시 액세스 서버에 전달 합니다.

9. 액세스 서버 액세스 고객과 연결 프로세스를 완료 하 고 계정 요청 메시지 NPS RADIUS 프록시를 보냅니다. NPS RADIUS 프록시 계정 데이터를 기록 하 고 RADIUS 서버에 게 메시지를 전달 합니다.

10. RADIUS 서버에 전송 NPS RADIUS 프록시에 액세스 서버에 전달 계정 응답 합니다.

NPS에 대 한 자세한 내용은 참조 [네트워크 NPS 정책 서버 ()](nps-top.md)합니다.
