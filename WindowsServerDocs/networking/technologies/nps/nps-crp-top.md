---
title: 연결 요청 처리
description: 이 항목에서는 Windows Server 2016의 네트워크 정책 서버 연결 요청 처리에 대 한 개요를 제공 합니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 849d661a-42c1-4f93-b669-6009d52aad39
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 268a307336d9a4fae1be5621eec7c32a06a6204e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405401"
---
# <a name="connection-request-processing"></a>연결 요청 처리

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목을 사용 하 여 Windows Server 2016의 네트워크 정책 서버에서 연결 요청 처리에 대해 알아볼 수 있습니다.

>[!NOTE]
>이 항목 외에 다음 연결 요청 처리 설명서를 사용할 수 있습니다.
> - [연결 요청 정책](nps-crp-crpolicies.md)
> - [영역 이름](nps-crp-realm-names.md)
> - [원격 RADIUS 서버 그룹](nps-crp-rrsg.md)

연결 요청 처리를 사용 하 여 로컬 컴퓨터 또는 원격 RADIUS 서버 그룹의 구성원 인 원격 RADIUS 서버에서 연결 요청 인증을 수행할 위치를 지정할 수 있습니다. 

NPS (네트워크 정책 서버)를 실행 하는 로컬 서버에서 연결 요청에 대 한 인증을 수행 하려는 경우 추가 구성 없이 기본 연결 요청 정책을 사용할 수 있습니다. 기본 정책에 따라 NPS는 로컬 도메인 및 트러스트 된 도메인에 계정이 있는 사용자와 컴퓨터를 인증 합니다.

원격 NPS 또는 다른 RADIUS 서버에 대 한 연결 요청을 전달 하려면 원격 RADIUS 서버 그룹을 만든 다음 해당 원격 RADIUS 서버 그룹에 요청을 전달 하는 연결 요청 정책을 구성 합니다. 이 구성을 사용 하면 NPS는 모든 RADIUS 서버에 인증 요청을 전달할 수 있으며, 트러스트 되지 않은 도메인의 계정이 있는 사용자는 인증할 수 있습니다.

다음 그림에서는 네트워크 액세스 서버에서 RADIUS 프록시로의 액세스 요청 메시지 경로를 표시 한 다음 원격 RADIUS 서버 그룹의 RADIUS 서버로 경로를 표시 합니다. RADIUS 프록시에서 네트워크 액세스 서버는 RADIUS 클라이언트로 구성 됩니다. 각 RADIUS 서버에서 radius 프록시는 RADIUS 클라이언트로 구성 됩니다.


![NPS 연결 요청 처리](../../media/Nps-Connection-Request-Processing/Nps-Connection-Request-Processing.jpg)


>[!NOTE]
>NPS와 함께 사용 하는 네트워크 액세스 서버는 RADIUS 프로토콜과 호환 되는 게이트웨이 장치 (예: 802.1 X 무선 액세스 지점과 인증 스위치, VPN 또는 전화 접속 서버로 구성 된 원격 액세스를 실행 하는 서버)가 될 수 있습니다. 기타 RADIUS 호환 장치.

NPS가 원격 RADIUS 서버 그룹에 다른 요청을 전달 하는 동안 일부 인증 요청을 로컬로 처리 하도록 하려면 둘 이상의 연결 요청 정책을 구성 합니다.

인증 요청을 처리 하는 NPS 또는 RADIUS 서버 그룹을 지정 하는 연결 요청 정책을 구성 하려면 연결 요청 정책을 참조 하세요.

인증 요청을 전달할 NPS 또는 다른 RADIUS 서버를 지정 하려면 원격 RADIUS 서버 그룹을 참조 하세요.

## <a name="nps-as-a-radius-server-connection-request-processing"></a>RADIUS 서버 연결 요청을 처리 하는 NPS

RADIUS 서버로 NPS를 사용 하는 경우 RADIUS 메시지는 다음과 같은 방식으로 네트워크 액세스 연결에 대 한 인증, 권한 부여 및 계정을 제공 합니다.

1. 액세스 서버 (예: 전화 접속 네트워크 액세스 서버, VPN 서버 및 무선 액세스 지점과 같은 액세스 서버)는 액세스 클라이언트에서 연결 요청을 수신 합니다. 

2. RADIUS를 인증, 권한 부여 및 계정 프로토콜로 사용 하도록 구성 된 액세스 서버는 액세스 요청 메시지를 만들어 NPS에 보냅니다. 

3. NPS는 액세스 요청 메시지를 평가 합니다. 

4. 필요한 경우 NPS는 액세스 챌린지 메시지를 액세스 서버에 보냅니다. 액세스 서버에서 챌린지를 처리 하 고 NPS에 업데이트 된 액세스 요청을 보냅니다. 

5. 사용자 자격 증명을 확인 하 고 도메인 컨트롤러에 대 한 보안 연결을 사용 하 여 사용자 계정의 전화 접속 속성을 가져옵니다. 

6. 연결 시도에는 사용자 계정 및 네트워크 정책의 전화 접속 속성을 모두 사용 하 여 권한이 부여 됩니다. 

7. 연결 시도가 인증 되 고 권한이 부여 된 경우 NPS는 액세스 허용 메시지를 액세스 서버에 보냅니다. 연결 시도가 인증 되지 않았거나 인증 되지 않은 경우 NPS는 액세스 거부 메시지를 액세스 서버에 보냅니다. 

8. 액세스 서버는 액세스 클라이언트를 사용 하 여 연결 프로세스를 완료 하 고 메시지가 기록 되는 계정 요청 메시지를 NPS에 보냅니다. 

9. NPS는 액세스 서버에 대 한 계정 응답을 보냅니다. 

>[!NOTE]
>또한 액세스 서버는 연결이 설정 된 시간, 액세스 클라이언트 연결이 닫힐 때 및 액세스 서버가 시작 및 중지 된 시간 동안 계정 요청 메시지를 보냅니다.

## <a name="nps-as-a-radius-proxy-connection-request-processing"></a>RADIUS 프록시 연결 요청 처리로 서의 NPS

RADIUS 클라이언트와 RADIUS 서버 간에 NPS를 RADIUS 프록시로 사용 하는 경우 네트워크 액세스 연결 시도에 대 한 RADIUS 메시지는 다음과 같은 방식으로 전달 됩니다.

1. 액세스 서버 (예: 전화 접속 네트워크 액세스 서버, VPN (가상 사설망) 서버 및 무선 액세스 지점과 같은 액세스 서버)는 액세스 클라이언트에서 연결 요청을 수신 합니다.

2. RADIUS를 인증, 권한 부여 및 계정 프로토콜로 사용 하도록 구성 된 액세스 서버는 액세스 요청 메시지를 만들고 NPS RADIUS 프록시로 사용 되는 NPS로 보냅니다.

3. NPS RADIUS 프록시는 액세스 요청 메시지를 수신 하 고 로컬로 구성 된 연결 요청 정책에 따라 액세스 요청 메시지를 전달할 위치를 결정 합니다.

4. NPS RADIUS 프록시는 액세스 요청 메시지를 적절 한 RADIUS 서버에 전달 합니다.

5. RADIUS 서버는 액세스 요청 메시지를 평가 합니다.

6. 필요한 경우 RADIUS 서버는 액세스 챌린지 메시지를 NPS RADIUS 프록시로 보냅니다. 그러면 액세스 서버에 전달 됩니다. 액세스 서버는 액세스 클라이언트를 사용 하 여 챌린지를 처리 하 고 NPS RADIUS 프록시로 업데이트 된 액세스 요청을 보냅니다. 여기에서 RADIUS 서버로 전달 됩니다.

7. RADIUS 서버는 연결 시도를 인증 하 고 권한을 부여 합니다.

8. 연결 시도가 인증 되 고 권한이 부여 된 경우 RADIUS 서버는 액세스 서버에 전달 되는 NPS RADIUS 프록시로 액세스 허용 메시지를 보냅니다. 연결 시도가 인증 되지 않았거나 인증 되지 않은 경우에는 RADIUS 서버에서 액세스 거부 메시지를 NPS RADIUS 프록시로 전송 합니다. 여기서 액세스 거부 메시지는 액세스 서버에 전달 됩니다.

9. 액세스 서버는 액세스 클라이언트를 사용 하 여 연결 프로세스를 완료 하 고 NPS RADIUS 프록시로 계정 요청 메시지를 보냅니다. NPS RADIUS 프록시는 계정 데이터를 기록 하 고 메시지를 RADIUS 서버로 전달 합니다.

10. RADIUS 서버는 액세스 서버에 전달 되는 NPS RADIUS 프록시에 대 한 계정 응답을 보냅니다.

NPS에 대 한 자세한 내용은 [nps (네트워크 정책 서버)](nps-top.md)를 참조 하세요.
