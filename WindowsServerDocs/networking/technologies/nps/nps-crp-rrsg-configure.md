---
title: 원격 RADIUS 서버 그룹 구성
description: 이 항목에서는 Windows Server 2016에서 네트워크 정책 서버에서 원격 RADIUS 서버 그룹을 구성 하는 방법을 설명 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: ca125e57-249c-4d97-85d1-2929cbf871f1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 02088a35196c0bfadeb65e8971a47fdcc741258d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818764"
---
# <a name="configure-remote-radius-server-groups"></a>원격 RADIUS 서버 그룹 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016

NPS 연결 요청 전달 처리를 위해 다른 NPSs 및 프록시 서버 역할을 구성 하려는 경우 원격 RADIUS 서버 그룹을 구성 하려면이 항목에서는 사용할 수 있습니다.

## <a name="add-a-remote-radius-server-group"></a>원격 RADIUS 서버 그룹 추가

네트워크 정책 (NPS 서버) 스냅인에서 새 원격 RADIUS 서버 그룹을 추가 하려면이 절차를 사용할 수 있습니다.

NPS를 RADIUS 프록시로 구성 하는 경우 NPS 연결 요청을 다른 RADIUS 서버로 전달 하도록 결정 하는 새 연결 요청 정책을 만듭니다. 또한 원격 RADIUS 서버 그룹 하나 이상의 RADIUS 서버를 포함 하는 NPS 연결 요청 정책과 일치 하는 연결 요청을 보낼 위치를 알려 주는 지정 하 여 연결 요청 정책 구성 됩니다.

>[!NOTE]
>또한 새 연결 요청 정책을 만드는 동안 새 원격 RADIUS 서버 그룹을 구성할 수 있습니다.

**Domain Admins**의 구성원이거나 이에 준하는 자격이 있어야 이 절차를 완료할 수 있습니다.

### <a name="to-add-a-remote-radius-server-group"></a>원격 RADIUS 서버 그룹을 추가 하려면 

1. 서버 관리자에서 클릭 **도구**를 클릭 하 고 **네트워크 정책 서버** NPS 콘솔을 엽니다.
2. 콘솔 트리에서 **RADIUS 클라이언트 및 서버**를 마우스 오른쪽 단추로 클릭 **원격 RADIUS 서버 그룹**를 클릭 하 고 **새**합니다.
3. 합니다 **새 원격 RADIUS 서버 그룹** 대화 상자가 열립니다. **그룹 이름**, 원격 RADIUS 서버 그룹의 이름을 입력 합니다.
4. **RADIUS 서버에서**, 클릭 **추가**합니다. 합니다 **RADIUS 서버 추가** 대화 상자가 열립니다. 그룹에 추가 하려는 RADIUS 서버의 IP 주소를 입력 하거나 정규화 된 도메인 이름을 입력 \(FQDN\) RADIUS 서버 및 클릭 **확인**합니다.
5. **RADIUS 서버 추가**를 클릭 합니다 **인증/계정** 탭 합니다. **공유 비밀** 하 고 **공유 비밀 확인**, 공유 암호를 입력 합니다. 원격 RADIUS 서버에서 RADIUS 클라이언트로 로컬 컴퓨터를 구성한 경우 동일한 공유 암호를 사용 해야 합니다.
6. 인증에 대 한 Extensible Authentication Protocol (EAP)를 사용 하지 않는 경우 클릭 **요청 메시지 인증자 특성을 포함 해야 합니다**합니다. EAP는 기본적으로 메시지 인증자 특성을 사용 합니다.
7. 배포에 대 한 인증 및 계정 포트 번호가 올바른지 확인 합니다.
8. 계정에 대 한 다른 공유 암호를 사용 하는 경우 **Accounting**의 선택을 취소 합니다 **인증 및 계정에 대 한 동일한 공유 암호를 사용 하 여** 확인란을 선택한 다음 계정공유암호를입력 **공유 비밀** 하 고 **공유 비밀 확인**합니다.
9. 전달 네트워크 액세스 서버 시작 및 중지 원격 RADIUS 서버에 메시지의 선택을 취소 하지 않을 경우 합니다 **전달 네트워크 액세스 서버 시작 및 중지이 서버에 알림을** 확인란 합니다.

NPS를 관리 하는 방법에 대 한 자세한 내용은 참조 하세요. [네트워크 정책 서버 관리](nps-manage-top.md)합니다.

NPS에 대 한 자세한 내용은 참조 하세요. [네트워크 정책 (NPS 서버)](nps-top.md)합니다.

