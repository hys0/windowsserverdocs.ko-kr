---
title: "DFS 네임스페이스 조정"
description: "이 문서에서는 DFS 네임스페이스를 조정하거나 최적화하는 방법을 설명합니다."
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 4614441fc54913ba5a8b547bbf1ad3e8ce7ee69b
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="tuning-dfs-namespaces"></a>DFS 네임스페이스 조정

> 적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

네임스페이스를 만들고 폴더와 대상을 추가한 후 다음 섹션을 참조하여 DFS 네임스페이스가 조회를 처리하고 AD DS(Active Directory Domain Services)를 폴링하여 업데이트된 네임스페이스 데이터를 가져오는 방식을 조정하거나 최적화하세요.

-   [네임스페이스에 액세스 기반 열거 사용](enable-access-based-enumeration-on-a-namespace.md)
-   [조회 및 클라이언트 장애 복구(failback) 사용 또는 사용 안 함](enable-or-disable-referrals-and-client-failback.md)
-   [클라이언트가 조회를 캐시하는 기간 변경](change-the-amount-of-time-that-clients-cache-referrals.md)
-   [조회 대상 순서 지정 방법 설정](set-the-ordering-method-for-targets-in-referrals.md)
-   [대상 우선 순위를 설정하여 조회 순서 지정 무시](set-target-priority-to-override-referral-ordering.md)
-   [네임스페이스 폴링 최적화](optimize-namespace-polling.md)
-   [액세스 기반 열거에 상속된 사용 권한 사용](using-inherited-permissions-with-access-based-enumeration.md)

> [!NOTE]
> 폴더나 폴더 대상을 검색하려면 네임스페이스를 선택하고 **검색** 탭을 클릭한 다음 텍스트 상자에 검색 문자열을 입력하고 **검색**을 클릭합니다.