---
title: 연결 요청 정책 구성
description: 이 항목에서는 Windows Server 2016의 네트워크 정책 서버에서 연결 요청 정책을 구성 하는 방법에 대 한 정보를 제공 합니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: f62c6a67-4dda-47f8-8bdf-9b76c37953e6
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d62beb3106141d4683c957020bc96e4a7dfb306f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405472"
---
# <a name="configure-connection-request-policies"></a>연결 요청 정책 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목을 사용 하 여 로컬 NPS가 연결 요청을 처리 하거나 처리를 위해 원격 RADIUS 서버에 전달 하는지 여부를 지정 하는 연결 요청 정책을 만들고 구성할 수 있습니다.

연결 요청 정책은 네트워크 관리자가 연결 요청에 대 한 인증 및 권한 부여를 수행 하는 RADIUS(Remote Authentication Dial-In User Service) (RADIUS) 서버를 지정 하는 데 사용할 수 있는 조건 및 설정 집합입니다. 네트워크 정책 서버를 실행 하는 서버 \(NPS @ no__t-1은 RADIUS 클라이언트에서 수신 합니다.

기본 연결 요청 정책은 NPS를 RADIUS 서버로 사용 하 고 모든 인증 요청을 로컬로 처리 합니다.

RADIUS 프록시로 작동 하 고 다른 NPS 또는 RADIUS 서버에 연결 요청을 전달 하도록 NPS를 실행 하는 서버를 구성 하려면 다음 조건을 지정 하는 새 연결 요청 정책을 추가 하는 것 외에 원격 RADIUS 서버 그룹을 구성 해야 합니다. 연결 요청이 일치 해야 합니다.

새 연결 요청 정책 마법사를 사용 하 여 새 연결 요청 정책을 만드는 동안 새 원격 RADIUS 서버 그룹을 만들 수 있습니다.

NPS를 RADIUS 서버로 작동 하 고 연결 요청을 로컬로 처리 하지 않으려는 경우 기본 연결 요청 정책을 삭제할 수 있습니다.

NPS가 RADIUS 서버 역할을 하 고, 연결 요청을 로컬로 처리 하 고, RADIUS 프록시로 사용 하 여 일부 연결 요청을 원격 RADIUS 서버 그룹으로 전달 하려면 다음 절차를 사용 하 여 새 정책을 추가 하 고 기본값을 확인 합니다. 연결 요청 정책은 마지막으로 정책 목록에 배치 하 여 처리 된 정책입니다.

## <a name="add-a-connection-request-policy"></a>연결 요청 정책 추가

**Domain Admins**의 구성원이거나 이에 준하는 자격이 있어야 이 절차를 완료할 수 있습니다.

### <a name="to-add-a-new-connection-request-policy"></a>새 연결 요청 정책을 추가 하려면 

1. 서버 관리자에서 **도구**를 클릭 한 다음 **네트워크 정책 서버** 를 클릭 하 여 NPS 콘솔을 엽니다. 
2. 콘솔 트리에서 **정책**을 두 번 클릭 합니다.
3. **연결 요청 정책**을 마우스 오른쪽 단추로 클릭 한 다음 **새 연결 요청 정책**을 클릭 합니다.
4. 새 연결 요청 정책 마법사를 사용 하 여 연결 요청 정책을 구성 하 고, 이전에 구성 하지 않은 경우 원격 RADIUS 서버 그룹을 구성 합니다.


NPS를 관리 하는 방법에 대 한 자세한 내용은 [네트워크 정책 서버 관리](nps-manage-top.md)를 참조 하세요.

NPS에 대 한 자세한 내용은 [nps (네트워크 정책 서버)](nps-top.md)를 참조 하세요.

