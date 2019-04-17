---
title: NAS NPS의 알림 전달 사용 안 함
description: 이 항목 Windows Server 2016에 네트워크 정책 서버 동시 인증 구성에 대해 설명 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: a09bfb03-95fc-4534-bf3c-97078ef6b07e
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c25f3b5a94624a35099e84ede3296f7ab860da7c
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="disable-nas-notification-forwarding-in-nps"></a>NAS NPS의 알림 전달 사용 안 함

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 절차를 시작 전달 사용 하지 않고 중지 네트워크 Nas 액세스 서버 () 메시지 NPS 구성 원격 RADIUS 서버 그룹의 회원 사용할 수 있습니다.

구성 원격 RADIUS 서버 그룹 하 고, NPS에서 **연결 요청 정책**, 선택을 취소 하면는 **계정 요청이 원격 RADIUS 서버 그룹 앞으로** 확인란을 이러한 그룹 NAS 전송 여전히은 시작 및 중지 알림 메시지. 

불필요 한 네트워크 교통을 만듭니다. 이 교통을 제거 하려면 NAS 알림 전달 원격 RADIUS 서버 그룹 각각의 개별 서버에 대 한 사용 하지 않도록 설정 합니다.

이 절차를 완료 하려면의 회원 있어야는 **관리자** 그룹입니다.

### <a name="to-disable-nas-notification-forwarding"></a>NAS 알림 전달 사용 하지 않도록 설정 하려면

1. 서버 관리자 클릭 **도구**을 차례로 클릭 하 고 **네트워크 정책 서버**합니다. NPS console을 엽니다.

2. 두 번 클릭 NPS 콘솔에서 **RADIUS 클라이언트 및 서버**, 클릭 **원격 RADIUS 서버 그룹**, 원격 RADIUS 서버 그룹 구성할을 두 번 클릭 합니다. 원격 RADIUS 서버 그룹 **속성** 대화 상자를 엽니다.

3. 그룹 구성원을 구성 하 고 클릭 한 다음 두 번 클릭 하 고 **인증/계정** 탭 합니다.

4. **계정**취소는 **앞으로 네트워크 액세스 서버 시작 및 중지이 서버에 알림에** 확인란을 선택한 다음 클릭 **확인**합니다.

5. 구성 하려면 모든 그룹 구성원 3-4 단계를 반복 합니다.

NPS 관리에 대 한 자세한 내용은 참조 [네트워크 정책 서버 관리](nps-manage-top.md)합니다.

NPS에 대 한 자세한 내용은 참조 [네트워크 NPS 정책 서버 ()](nps-top.md)합니다.
