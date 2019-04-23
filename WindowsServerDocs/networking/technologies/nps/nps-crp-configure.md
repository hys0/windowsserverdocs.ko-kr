---
title: 연결 요청 정책 구성
description: 이 항목에서는 Windows Server 2016에서 네트워크 정책 서버에 연결 요청 정책 구성 하는 방법을 설명 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: f62c6a67-4dda-47f8-8bdf-9b76c37953e6
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4f80f9fb8be0c44cfb5685e5b9cc489282e4961d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884514"
---
# <a name="configure-connection-request-policies"></a>연결 요청 정책 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 로컬 NPS 연결 요청을 처리 하거나 처리를 위해 원격 RADIUS 서버에 전달 하는지 여부를 지정 하는 연결 요청 정책을 만들고 구성에 사용할 수 있습니다.

인증을 수행 하는 네트워크 관리자는 전화 접속 사용자 서비스 RADIUS (Remote Authentication) 서버를 지정할 수 있도록 설정 및 연결 권한 부여를 요청 하는 연결 요청 정책 되는 조건 집합을 네트워크 정책 서버를 실행 하는 서버 \(NPS\) RADIUS 클라이언트에서 수신 합니다.

기본 연결 요청 정책을 NPS를 RADIUS 서버로 사용 하 고 로컬로 모든 인증 요청을 처리 합니다.

NPS를 RADIUS 프록시로 및 연결 요청 전달 다른 NPS 또는 RADIUS 서버 역할을 실행 하는 서버를 구성 하려면 조건 및 설정을 지정 하는 새 연결 요청 정책을 추가 하는 것 외에도 원격 RADIUS 서버 그룹을 구성 해야 하는 연결 요청 일치 해야 합니다.

새 연결 요청 정책 마법사를 사용 하 여 새 연결 요청 정책을 만드는 동안 새 원격 RADIUS 서버 그룹을 만들 수 있습니다.

NPS를 RADIUS 서버 및 프로세스 연결 로컬로 요청 하지 않으려면 기본 연결 요청 정책을 삭제할 수 있습니다.

NPS 역할을 모두 RADIUS 서버에 로컬로 연결 요청을 처리 하 고 원격 RADIUS 서버 그룹에 일부 연결 요청을 전달 하는 RADIUS 프록시로 다음 절차를 사용 하 여 새 정책 추가 되어 있는지를 확인 하는 기본을 하려는 경우 연결 요청 정책에는 정책 목록에서 마지막으로 배치 하 여 처리 하는 마지막 정책이입니다.

## <a name="add-a-connection-request-policy"></a>연결 요청 정책 추가

**Domain Admins**의 구성원이거나 이에 준하는 자격이 있어야 이 절차를 완료할 수 있습니다.

### <a name="to-add-a-new-connection-request-policy"></a>새 연결 요청 정책을 추가 하려면 

1. 서버 관리자에서 클릭 **도구**를 클릭 하 고 **네트워크 정책 서버** NPS 콘솔을 엽니다. 
2. 콘솔 트리에서 **정책을**합니다.
3. 마우스 오른쪽 단추로 클릭 **연결 요청 정책**를 클릭 하 고 **새 연결 요청 정책**합니다.
4. 사용 하 여 연결을 구성 하려면 새 연결 요청 정책 마법사 정책을 요청 하 고, 그렇지 않은 경우 이전에 구성 된, 원격 RADIUS 서버 그룹입니다.


NPS를 관리 하는 방법에 대 한 자세한 내용은 참조 하세요. [네트워크 정책 서버 관리](nps-manage-top.md)합니다.

NPS에 대 한 자세한 내용은 참조 하세요. [네트워크 정책 (NPS 서버)](nps-top.md)합니다.

