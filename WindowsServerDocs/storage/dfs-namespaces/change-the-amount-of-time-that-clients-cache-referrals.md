---
title: 클라이언트가 조회를 캐시하는 기간 변경
description: 이 문서에서는 클라이언트가 조회를 캐시하는 기간을 변경하는 방법을 설명합니다.
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 08a1212c983de6e2492609330c1be222286e9e8f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888774"
---
# <a name="change-the-amount-of-time-that-clients-cache-referrals"></a>클라이언트가 조회를 캐시하는 기간 변경

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

조회는 사용자가 네임스페이스에 대상이 있는 네임스페이스 루트나 폴더에 액세스할 때 클라이언트 컴퓨터가 도메인 컨트롤러나 네임스페이스 서버에서 받는 대상의 정렬된 목록입니다. 새 조회를 요청하기 전에 클라이언트가 조회를 캐시하는 기간을 조정할 수 있습니다.

## <a name="to-change-the-amount-of-time-that-clients-cache-namespace-root-referrals"></a>클라이언트가 네임스페이스 루트 조회를 캐시하는 기간을 변경하려면

1.  **시작**을 클릭하고 **관리 도구**를 가리킨 다음 **DFS 관리**를 클릭합니다.

2.  콘솔 트리의 **네임스페이스** 노드에서 네임스페이스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.

3.  **조회** 탭의 **캐시 기간(초)** 텍스트 상자에 클라이언트가 네임스페이스 루트 조회를 캐시하는 기간(초)을 입력합니다. 기본 설정은 300초(5분)입니다.

> [!TIP]
> Windows PowerShell을 사용하여 클라이언트가 네임스페이스 루트 조회를 캐시하는 기간을 변경하려면 [Set-DfsnRoot TimeToLiveSec](https://technet.microsoft.com/library/jj884281.aspx) cmdlet을 사용하세요. 이러한 cmdlet은 Windows Server 2012에서 도입 되었습니다.

## <a name="to-change-the-amount-of-time-that-clients-cache-folder-referrals"></a>클라이언트가 폴더 조회를 캐시하는 기간을 변경하려면

1.  **시작**을 클릭하고 **관리 도구**를 가리킨 다음 **DFS 관리**를 클릭합니다.

2.  콘솔 트리의 **네임스페이스** 노드에서 대상이 있는 폴더를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.

3.  **조회** 탭의 **캐시 기간(초)** 텍스트 상자에 클라이언트가 폴더 조회를 캐시하는 기간(초)을 입력합니다. 기본 설정은 1800초(30분)입니다.

## <a name="see-also"></a>참조

-   [DFS 네임 스페이스를 튜닝합니다.](tuning-dfs-namespaces.md)
-   [DFS 네임 스페이스에 대 한 관리 권한 위임](delegate-management-permissions-for-dfs-namespaces.md)


