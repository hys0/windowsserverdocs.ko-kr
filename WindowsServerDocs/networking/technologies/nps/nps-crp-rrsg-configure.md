---
title: 원격 RADIUS 서버 그룹 구성
description: 이 항목의 Windows Server 2016 네트워크 정책 서버에서 원격 RADIUS 서버 그룹을 구성 하는 방법에 대해 설명 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: ca125e57-249c-4d97-85d1-2929cbf871f1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f293fd18176115365e5e243a90a034676b3262f9
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="configure-remote-radius-server-groups"></a>원격 RADIUS 서버 그룹 구성

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

프록시 서버 및 앞으로 연결 요청을 처리 하기 위해 다른 NPS 서버 역할을 NPS 구성할 때 원격 RADIUS 서버 그룹 구성 하려면이 항목을 사용할 수 있습니다.

## <a name="add-a-remote-radius-server-group"></a>원격 RADIUS 서버 그룹 추가

이 절차 그룹을 새로 추가 원격 RADIUS 서버 스냅인 네트워크 NPS 정책 서버 ()을 사용할 수 있습니다.

NPS RADIUS 프록시도를 구성할 때 NPS RADIUS 서버 다른에 전달 하도록 요청 하는 연결 확인 하기 위해 사용 하는 새 연결 요청 정책을 만듭니다. 또한 연결 요청 정책은 원격 RADIUS 서버 포함 하는 그룹 하나 또는 여러 개의 RADIUS 서버, NPS 연결 요청 정책을 일치 하는 연결 요청을 보낼 수 있는 위치에 알려주는 지정 하 여 구성 됩니다.

>[!NOTE]
>또한 새로운 원격 RADIUS 서버 그룹 새 연결 요청 정책을 만드는 과정 구성할 수 있습니다.

회원 **도메인 관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.

### <a name="to-add-a-remote-radius-server-group"></a>원격 RADIUS 서버 그룹을 추가 하려면 

1. 서버 관리자 클릭 **도구**을 차례로 클릭 하 고 **네트워크 정책 서버** NPS 콘솔을 엽니다.
2. 콘솔 트리에서 두 번 클릭 **RADIUS 클라이언트 및 서버**를 마우스 오른쪽 단추로 클릭 **원격 RADIUS 서버 그룹**을 차례로 클릭 하 고 **새로**합니다.
3. **원격 새로운 RADIUS 서버 그룹** 대화 상자를 엽니다. **그룹 이름을**, 원격 RADIUS 서버 그룹 이름을 입력 합니다.
4. **RADIUS 서버에서**, 클릭 **추가**합니다. **RADIUS 서버 추가** 대화 상자를 엽니다. 그룹에 추가 하거나 정식 도메인 이름 \(FQDN\) RADIUS 서버를 입력 한 다음 원하는 RADIUS 서버의 IP 주소를 입력 **확인**합니다.
5. **RADIUS 서버 추가**를 클릭 하는 **인증/계정** 탭 합니다. **공유 암호** 및 **공유 암호 확인**, 공유 암호를 입력 합니다. 로컬 컴퓨터에서 원격 RADIUS 서버 RADIUS 클라이언트로 구성 하는 경우 동일한 공유 암호를 사용 해야 합니다.
6. 인증에 대 한 Extensible 인증 (EAP 프로토콜)를 사용 하지 않는 경우 클릭 **요청 메시지 인증 특성 있어야**합니다. EAP은 메시지 인증자 특성 기본적으로 사용 됩니다.
7. 배포에 대 한 포트 번호를 인증 및 계정 올바른지 확인 합니다.
8. 계정에 대 한에서 공유 서로 다른 암호를 사용 하는 경우 **계정**취소는 **공유 동일한 암호를 사용 하 여 인증과 계정에 대 한** 확인란을 선택한 다음에서 계정 공유 암호를 입력 **공유 암호** 및 **공유 암호 확인**합니다.
9. 앞으로 네트워크 액세스 서버 시작 및 중지 원격 RADIUS 서버, 메시지 확인란의 선택을 취소 하 고 원하지 않는 경우는 **앞으로 네트워크 액세스 서버 시작 및 중지이 서버에 알림에** 확인란을 선택 합니다.

NPS 관리에 대 한 자세한 내용은 참조 [네트워크 정책 서버 관리](nps-manage-top.md)합니다.

NPS에 대 한 자세한 내용은 참조 [네트워크 NPS 정책 서버 ()](nps-top.md)합니다.

