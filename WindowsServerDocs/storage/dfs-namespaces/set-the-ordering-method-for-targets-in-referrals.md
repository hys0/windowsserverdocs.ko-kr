---
title: 조회 대상 순서 지정 방법 설정
description: 이 문서에서는 어떻게 조회 대상 순서 지정 방법을 설정하는지 설명합니다.
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 06e7aa1309b453da649537d5ae9b22acce830530
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816864"
---
# <a name="set-the-ordering-method-for-targets-in-referrals"></a>조회 대상 순서 지정 방법 설정

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

조회는 사용자가 대상을 가진 네임스페이스 루트나 폴더에 액세스할 때 클라이언트 컴퓨터가 도메인 컨트롤러나 네임스페이스 서버에서 받는 대상의 정렬된 목록입니다. 클라이언트는 조회를 받은 후 목록에서 첫 번째 대상에 액세스하려고 합니다. 대상을 사용할 수 없는 경우 클라이언트는 다음 대상에 액세스를 시도합니다.
클라이언트 사이트의 대상이 조회에서 항상 먼저 나열됩니다. 클라이언트 사이트 밖의 대상은 순서 지정 방법에 따라 나열됩니다.

다음 섹션을 사용하여 대상이 클라이언트에 조회해야 하는 순서를 지정하고 여러 가지 대상 조회 순서 지정 방법을 알아봅니다.

## <a name="to-set-the-ordering-method-for-targets-in-namespace-root-referrals"></a>네임스페이스 루트 조회 대상 순서 지정 방법을 설정하려면

다음 절차에 따라 네임스페이스 루트 조회 대상 순서 지정 방법을 설정합니다.

1.  **시작**을 클릭하고 **관리 도구**를 가리킨 다음 **DFS 관리**를 클릭합니다.

2.  콘솔 트리의 **네임스페이스** 노드에서 네임스페이스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.

3.  **조회** 탭에서 순서 지정 방법을 선택합니다.

> [!NOTE]
> Windows PowerShell을 사용하여 네임스페이스 루트 조회 대상 순서 지정 방법을 설정하려면 다음 매개 변수 중 하나와 함께 [Set-DfsnRoot](https://technet.microsoft.com/library/jj884281.aspx) cmdlet을 사용합니다.
   -   **EnableSiteCosting**은 **최저 비용 순서 지정** 방법을 지정합니다.
   -   **EnableInsiteReferrals**는 **클라이언트 사이트의 외부 대상 제외** 순서 지정 방법을 지정합니다.
   -   **순서 없음** 조회 순서 지정 방법을 지정하려면 매개 변수를 생략합니다. 

DFSN Windows PowerShell 모듈은 Windows Server 2012에서 도입 되었습니다.
   
## <a name="to-set-the-ordering-method-for-targets-in-folder-referrals"></a>폴더 조회 대상 순서 지정 방법을 설정하려면

대상을 가진 폴더는 네임스페이스 루트에서 순서 지정 방법을 상속받습니다. 다음 절차에 따라 순서 지정 방법을 무시할 수 있습니다.

1.  **시작**을 클릭하고 **관리 도구**를 가리킨 다음 **DFS 관리**를 클릭합니다.

2.  콘솔 트리의 **네임스페이스** 노드에서 대상이 있는 폴더를 마우스 오른쪽 단추를 클릭한 다음 **속성**을 클릭합니다.

3.  **조회** 탭에서 **클라이언트 사이트의 외부 대상 제외** 확인란을 선택합니다.

> [!NOTE]
> Windows PowerShell을 사용하여 클라이언트 사이트의 외부 대상을 제외하려면 [Set-DfsnFolder –EnableInsiteReferrals](https://technet.microsoft.com/library/jj884283.aspx) cmdlet을 사용합니다.

## <a name="target-referral-ordering-methods"></a>대상 조회 순서 지정 방법

다음과 같은 세 가지 순서 지정 방법이 있습니다.

-   순서 없음
-   최저 비용
-   클라이언트 사이트의 외부 대상 제외

## <a name="random-order"></a>순서 없음

이 방법을 사용하면 다음과 같이 대상 순서가 지정됩니다.

1.  클라이언트와 동일한 Active Directory Directory Services (AD DS) 사이트에 대상 조회의 맨 위에 있는 임의의 순서로 나열 됩니다.
2.  클라이언트 사이트의 외부 대상은 임의의 순서로 나열됩니다.

동일한 사이트의 대상 서버를 사용할 수 없는 경우 클라이언트 컴퓨터는 연결 비용이나 대상과의 거리에 관계없이 임의의 대상 서버에 조회합니다.

## <a name="lowest-cost"></a>최저 비용

이 방법을 사용하면 다음과 같이 대상 순서가 지정됩니다.

1.  클라이언트와 동일한 사이트의 대상이 조회 위쪽에 임의의 순서로 나열됩니다.
2.  클라이언트 사이트의 외부 대상이 최저 비용에서 최고 비용의 순서로 나열됩니다. 같은 비용의 조회가 함께 그룹화되고 대상은 각 그룹 내에 임의의 순서로 나열됩니다.

> [!NOTE]
> 사이트 링크 비용은 DFS 관리 스냅인에 표시되지 않습니다. 사이트 링크 비용을 보려면 Active Directory 사이트 및 서비스 스냅인을 사용합니다.

## <a name="exclude-targets-outside-of-the-clients-site"></a>클라이언트 사이트의 외부 대상 제외

이 방법을 사용하면 클라이언트와 동일한 사이트의 대상만 조회에 포함됩니다. 이러한 동일한 사이트의 대상이 임의의 순서로 나열됩니다. 동일한 사이트의 대상이 없는 경우 클라이언트가 조회를 받지 않으며 네임스페이스의 해당 부분에 액세스할 수 없습니다.

> [!NOTE]
> 순서 지정 방법이 **클라이언트 사이트의 외부 대상 제외**로 설정되어도 우선 순위가 "모든 대상 중 첫 번째"나 "모든 대상 중 마지막"으로 설정된 대상은 조회에 계속 나열됩니다.

## <a name="see-also"></a>참조 

-   [DFS 네임 스페이스를 튜닝합니다.](tuning-dfs-namespaces.md)
-   [DFS 네임 스페이스에 대 한 관리 권한 위임](delegate-management-permissions-for-dfs-namespaces.md)