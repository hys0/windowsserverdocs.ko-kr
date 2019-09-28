---
title: DFS 네임스페이스 조정
description: 이 문서에서는 DFS 네임스페이스를 조정하거나 최적화하는 방법을 설명합니다.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 011512deaeb99ded7d0bfc32a48f19ab3b622475
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386146"
---
# <a name="tuning-dfs-namespaces"></a>DFS 네임스페이스 조정

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

네임 스페이스를 만들고 폴더 및 대상을 추가한 후에는 다음 섹션을 참조 하 여 DFS 네임 스페이스가 업데이트 된 네임 스페이스 데이터에 대 한 조회 및 폴링 Active Directory Domain Services (AD DS)를 처리 하는 방법을 조정 하거나 최적화 합니다.

-   [네임 스페이스에 대 한 액세스 기반 열거 사용](enable-access-based-enumeration-on-a-namespace.md)
-   [조회 및 클라이언트 장애 복구 사용 또는 사용 안 함](enable-or-disable-referrals-and-client-failback.md)
-   [클라이언트에서 조회를 캐시 하는 시간 변경](change-the-amount-of-time-that-clients-cache-referrals.md)
-   [조회 대상의 순서를 지정하는 방법 설정](set-the-ordering-method-for-targets-in-referrals.md)
-   [대상 우선 순위를 설정하여 조회 순서 지정 재정의](set-target-priority-to-override-referral-ordering.md)
-   [네임스페이스 폴링 최적화](optimize-namespace-polling.md)
-   [액세스 기반 열거와 함께 상속 된 권한 사용](using-inherited-permissions-with-access-based-enumeration.md)

> [!NOTE]
> 폴더나 폴더 대상을 검색하려면 네임스페이스를 선택하고 **검색** 탭을 클릭한 다음 텍스트 상자에 검색 문자열을 입력하고 **검색**을 클릭합니다.