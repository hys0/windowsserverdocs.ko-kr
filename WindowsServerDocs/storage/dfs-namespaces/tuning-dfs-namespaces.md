---
title: DFS 네임스페이스 조정
description: 이 문서에서는 DFS 네임스페이스를 조정하거나 최적화하는 방법을 설명합니다.
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: c11bbf65c3baebebe1e5143a5e694ca752500aca
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844634"
---
# <a name="tuning-dfs-namespaces"></a>DFS 네임스페이스 조정

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

네임 스페이스를 만들고 폴더 및 대상 추가 후 튜닝 하거나 조회를 처리 방식으로 DFS Namespace 및 설문 조사 Active Directory Domain Services (AD DS) 네임 스페이스 업데이트 된 데이터에 대 한 최적화는 다음 섹션을 참조 하세요.

-   [Namespace에 액세스 기반 열거를 사용 하도록 설정](enable-access-based-enumeration-on-a-namespace.md)
-   [사용 하도록 설정 하거나 조회 하 고 클라이언트 장애 복구를 사용 하지 않도록](enable-or-disable-referrals-and-client-failback.md)
-   [변경 클라이언트 조회를 캐시 하는 기간](change-the-amount-of-time-that-clients-cache-referrals.md)
-   [순서 지정 방법을 조회의 대상에 대 한 설정](set-the-ordering-method-for-targets-in-referrals.md)
-   [조회 순서 지정을 재정의 하려면 대상 우선 순위를 설정 합니다.](set-target-priority-to-override-referral-ordering.md)
-   [Namespace 폴링 최적화](optimize-namespace-polling.md)
-   [상속 된 사용 권한을 액세스 기반 열거 사용](using-inherited-permissions-with-access-based-enumeration.md)

> [!NOTE]
> 폴더나 폴더 대상을 검색하려면 네임스페이스를 선택하고 **검색** 탭을 클릭한 다음 텍스트 상자에 검색 문자열을 입력하고 **검색**을 클릭합니다.