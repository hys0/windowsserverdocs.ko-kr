---
title: 원격 RADIUS 서버 그룹 구성
description: 이 항목에서는 Windows Server 2016의 네트워크 정책 서버에서 원격 RADIUS 서버 그룹을 구성 하는 방법에 대 한 정보를 제공 합니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: ca125e57-249c-4d97-85d1-2929cbf871f1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: fe34d25d2b54b02bb56fcad99c433054a309f60b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405453"
---
# <a name="configure-remote-radius-server-groups"></a>원격 RADIUS 서버 그룹 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목을 사용 하 여 NPS에서 프록시 서버 역할을 하도록 구성 하 고 처리를 위해 다른 NPSs로 연결 요청을 전달 하려는 경우 원격 RADIUS 서버 그룹을 구성할 수 있습니다.

## <a name="add-a-remote-radius-server-group"></a>원격 RADIUS 서버 그룹 추가

이 절차를 사용 하 여 NPS (네트워크 정책 서버) 스냅인에서 새 원격 RADIUS 서버 그룹을 추가할 수 있습니다.

NPS를 RADIUS 프록시로 구성 하는 경우 NPS에서 다른 RADIUS 서버로 전달할 연결 요청을 결정 하는 데 사용 하는 새 연결 요청 정책을 만듭니다. 또한 연결 요청 정책은 하나 이상의 RADIUS 서버를 포함 하는 원격 RADIUS 서버 그룹을 지정 하 여 구성 됩니다 .이 그룹은 NPS가 연결 요청 정책과 일치 하는 연결 요청을 보낼 위치를 알려 줍니다.

>[!NOTE]
>새 연결 요청 정책을 만드는 과정에서 새 원격 RADIUS 서버 그룹을 구성할 수도 있습니다.

**Domain Admins**의 구성원이거나 이에 준하는 자격이 있어야 이 절차를 완료할 수 있습니다.

### <a name="to-add-a-remote-radius-server-group"></a>원격 RADIUS 서버 그룹을 추가 하려면 

1. 서버 관리자에서 **도구**를 클릭 한 다음 **네트워크 정책 서버** 를 클릭 하 여 NPS 콘솔을 엽니다.
2. 콘솔 트리에서 **RADIUS 클라이언트 및 서버**를 두 번 클릭 하 고 **원격 radius 서버 그룹**을 마우스 오른쪽 단추로 클릭 한 다음 **새로 만들기**를 클릭 합니다.
3. **새 원격 RADIUS 서버 그룹** 대화 상자가 열립니다. **그룹 이름**에 원격 RADIUS 서버 그룹의 이름을 입력 합니다.
4. **RADIUS 서버에서** **추가**를 클릭 합니다. **RADIUS 서버 추가** 대화 상자가 열립니다. 그룹에 추가할 RADIUS 서버의 IP 주소를 입력 하거나, RADIUS 서버의 정규화 된 도메인 이름 \(FQDN @ no__t-1을 입력 하 고 **확인**을 클릭 합니다.
5. **RADIUS 서버 추가**에서 **인증/계정** 탭을 클릭 합니다. 공유 **암호** 및 공유 **암호 확인**에 공유 암호를 입력 합니다. 로컬 컴퓨터를 원격 RADIUS 서버에서 RADIUS 클라이언트로 구성할 때 동일한 공유 암호를 사용 해야 합니다.
6. 인증을 위해 EAP (확장할 수 있는 인증 프로토콜)를 사용 하지 않는 경우 **요청은 메시지 인증자 특성을 포함 해야 합니다**.를 클릭 합니다. EAP는 기본적으로 메시지 인증자 특성을 사용 합니다.
7. 배포에 대 한 인증 및 계정 포트 번호가 올바른지 확인 합니다.
8. 계정에 다른 공유 암호를 사용 하는 경우 **계정**에서 **인증 및 계정에 동일한 공유 암호 사용** 확인란의 선택을 취소 하 고 **공유 암호** 에 계정 공유 암호를 입력 하 고 공유를 **확인 합니다. 비밀**.
9. 네트워크 액세스 서버 시작 및 중지 메시지를 원격 RADIUS 서버에 전달 하지 않으려면 **네트워크 액세스 서버에서이 서버에 대 한 알림 시작 및 중지** 확인란의 선택을 취소 합니다.

NPS를 관리 하는 방법에 대 한 자세한 내용은 [네트워크 정책 서버 관리](nps-manage-top.md)를 참조 하세요.

NPS에 대 한 자세한 내용은 [nps (네트워크 정책 서버)](nps-top.md)를 참조 하세요.

