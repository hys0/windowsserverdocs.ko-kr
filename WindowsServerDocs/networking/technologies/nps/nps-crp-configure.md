---
title: 구성 연결 요청 정책
description: 이 항목의 Windows Server 2016 네트워크 정책 서버에 연결 요청 정책 구성 하는 방법에 대해 설명 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: f62c6a67-4dda-47f8-8bdf-9b76c37953e6
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9677e147bdaea4de71a054cd6c52d81126e005d1
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="configure-connection-request-policies"></a>구성 연결 요청 정책

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목을 만들고를 지정 로컬 NPS 서버 연결 요청을 처리 하거나 처리에 대 한 원격 RADIUS 서버를 전달 연결 요청 정책 구성 사용할 수 있습니다.

연결 요청 정책은 집합 조건 및 네트워크 관리자가 어떤 RADIUS(Remote Authentication Dial-In User Service) (RADIUS) 서버 네트워크 정책 서버 \(NPS\) 실행 하는 서버 RADIUS 클라이언트에서 수신 하는 연결 요청 인증과 수행 하 여 지정 하도록 허용 하는 설정입니다.

기본 연결 요청 정책 NPS RADIUS 서버도 사용 및 로컬 모든 인증 요청을 처리 합니다.

구성 하려면 NPS RADIUS 프록시 및 기타 NPS RADIUS 서버에 연결 앞으로 요청 역할을 실행 하는 서버, 새 연결 요청 정책 조건과 연결 요청 일치 하는 설정을 지정 하는 추가 뿐 아니라 원격 RADIUS 서버 그룹을 구성 해야 합니다.

새 연결 요청 정책을 새 연결 요청 정책 마법사 만들 때 원격 새로운 RADIUS 서버 그룹을 만들 수 있습니다.

NPS RADIUS 서버와 프로세스 연결 로컬로 요청 작동 하도록 서버를 하지 않을 경우 기본 연결 요청 정책을 삭제할 수 있습니다.

NPS RADIUS 서버 역할을 서버의 하려는 경우 연결 요청을 처리, 로컬 및 일부 연결 요청 원격 RADIUS 서버 그룹 전달 RADIUS 프록시 다음 절차에 따라 새 정책을 추가 기본 연결 요청 정책을 정책 목록에서 마지막 배치 하 여 처리 마지막 정책을 확인 합니다.

## <a name="add-a-connection-request-policy"></a>연결 요청 정책 추가

회원 **도메인 관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.

### <a name="to-add-a-new-connection-request-policy"></a>새 연결 요청 정책을 추가 하려면 

1. 서버 관리자 클릭 **도구**을 차례로 클릭 하 고 **네트워크 정책 서버** NPS 콘솔을 엽니다. 
2. 두 번 클릭 콘솔 트리에서 **정책**합니다.
3. 마우스 오른쪽 단추로 클릭 **연결 요청 정책**을 차례로 클릭 하 고 **새 연결 요청 정책**합니다.
4. 사용 하 여 연결 구성에 새 연결 요청 정책 마법사 요청 정책 및, 그렇지 않은 경우 이전 구성, 원격 RADIUS 서버 그룹입니다.


NPS 관리에 대 한 자세한 내용은 참조 [네트워크 정책 서버 관리](nps-manage-top.md)합니다.

NPS에 대 한 자세한 내용은 참조 [네트워크 NPS 정책 서버 ()](nps-top.md)합니다.

