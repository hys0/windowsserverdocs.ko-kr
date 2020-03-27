---
title: NPS에서 NAS 알림 전달 사용 안 함
description: 이 항목에서는 Windows Server 2016에서 네트워크 정책 서버 동시 인증을 구성 하는 방법에 대 한 지침을 제공 합니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: a09bfb03-95fc-4534-bf3c-97078ef6b07e
ms.author: lizross
author: eross-msft
ms.openlocfilehash: dd56dfd4db9dd41c98141e2239efcca544a364fe
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80316165"
---
# <a name="disable-nas-notification-forwarding-in-nps"></a>NPS에서 NAS 알림 전달 사용 안 함

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 절차를 사용 하 여 네트워크 액세스 서버 (Nas)에서 NPS에 구성 된 원격 RADIUS 서버 그룹의 구성원으로 시작 및 중지 메시지 전달을 사용 하지 않도록 설정할 수 있습니다.

원격 RADIUS 서버 그룹을 구성 하 고 NPS **연결 요청 정책**에서 **이 원격 radius 서버 그룹에 대 한 계정 요청 전달** 확인란의 선택을 취소 하면 이러한 그룹은 계속 해 서 NAS가 시작 및 중지 알림 메시지를 보냅니다. 

이렇게 하면 불필요 한 네트워크 트래픽이 생성 됩니다. 이 트래픽을 제거 하려면 각 원격 RADIUS 서버 그룹의 개별 서버에 대 한 NAS 알림 전달을 사용 하지 않도록 설정 합니다.

이 절차를 완료하려면 **Administrators** 그룹의 구성원이어야 합니다.

### <a name="to-disable-nas-notification-forwarding"></a>NAS 알림 전달을 사용 하지 않도록 설정 하려면

1. 서버 관리자에서 클릭 **도구**, 를 클릭 하 고 **네트워크 정책 서버**합니다. NPS 콘솔이 열립니다.

2. NPS 콘솔에서 **Radius 클라이언트 및 서버**를 두 번 클릭 하 고 **원격 radius 서버 그룹**을 클릭 한 다음 구성 하려는 원격 radius 서버 그룹을 두 번 클릭 합니다. 원격 RADIUS 서버 그룹 **속성** 대화 상자가 열립니다.

3. 구성 하려는 그룹 구성원을 두 번 클릭 한 다음 **인증/계정** 탭을 클릭 합니다.

4. **계정**에서 **네트워크 액세스 서버에서이 서버에 대 한 알림 시작 및 중지** 확인란의 선택을 취소 하 고 **확인**을 클릭 합니다.

5. 구성 하려는 모든 그룹 구성원에 대해 3 단계와 4 단계를 반복 합니다.

NPS를 관리 하는 방법에 대 한 자세한 내용은 [네트워크 정책 서버 관리](nps-manage-top.md)를 참조 하세요.

NPS에 대 한 자세한 내용은 [nps (네트워크 정책 서버)](nps-top.md)를 참조 하세요.
