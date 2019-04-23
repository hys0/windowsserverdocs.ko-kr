---
title: NPS의 알림 전달 NAS를 사용 하지 않도록 설정
description: 이 항목에서는 Windows Server 2016의 동시 인증이 네트워크 정책 서버를 구성 하는 방법에 지침을 제공 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: a09bfb03-95fc-4534-bf3c-97078ef6b07e
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bc4c6afdcb02eb2bbab1f0373a5b3a28236269bf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882264"
---
# <a name="disable-nas-notification-forwarding-in-nps"></a>NPS의 알림 전달 NAS를 사용 하지 않도록 설정

>적용 대상: Windows Server (반기 채널), Windows Server 2016

시작의 전달을 사용 하지 않도록 설정 하 여 NPS에 구성 하는 원격 RADIUS 서버 그룹의 구성원에 네트워크 액세스 서버 (Nas)에서 메시지를 중지이 절차를 사용할 수 있습니다.

원격 RADIUS 서버 그룹을 구성 해야 하는 경우 및 NPS **연결 요청 정책**의 선택을 취소 하면 합니다 **이 원격 RADIUS 서버 그룹에 계정 요청을 전달** 확인란, 이러한 그룹은 여전히 보낸된 NAS 시작 하 고 알림 메시지를 중지 합니다. 

이렇게 하면 불필요 한 네트워크 트래픽을 만들어집니다. 이 트래픽을 제거 하려면 각 원격 RADIUS 서버 그룹의 개별 서버에 대 한 전달 하는 NAS 알림 사용 하지 않도록 설정 합니다.

이 절차를 완료 하려면의 구성원 이어야는 **관리자** 그룹입니다.

### <a name="to-disable-nas-notification-forwarding"></a>NAS 알림 전달을 사용 하지 않도록 설정

1. 서버 관리자에서 클릭 **도구**, 를 클릭 하 고 **네트워크 정책 서버**합니다. NPS 콘솔이 열립니다.

2. NPS 콘솔을 두 번 클릭 **RADIUS 클라이언트 및 서버**, 클릭 **원격 RADIUS 서버 그룹**, 구성 하려는 원격 RADIUS 서버 그룹을 두 번 클릭 합니다. 원격 RADIUS 서버 그룹 **속성** 대화 상자가 열립니다.

3. 구성 하 고 클릭 하려는 그룹 멤버를 두 번 클릭 합니다 **인증/계정** 탭 합니다.

4. **Accounting**의 선택을 취소 합니다 **전달 네트워크 액세스 서버 시작 및 중지이 서버에 알림을** 확인란을 선택한 다음 클릭 **확인**합니다.

5. 구성 하려는 모든 그룹 멤버에 대해 3 및 4 단계를 반복 합니다.

NPS를 관리 하는 방법에 대 한 자세한 내용은 참조 하세요. [네트워크 정책 서버 관리](nps-manage-top.md)합니다.

NPS에 대 한 자세한 내용은 참조 하세요. [네트워크 정책 (NPS 서버)](nps-top.md)합니다.
