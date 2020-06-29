---
title: 조회 대상의 순서를 지정하는 방법 설정
description: 이 문서에서는 조회의 대상에 대 한 순서 지정 메서드를 설정 하는 방법을 설명 합니다.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 9b420e311c98477d369c81f10eca274e665dae3a
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475160"
---
# <a name="set-the-ordering-method-for-targets-in-referrals"></a>조회 대상의 순서를 지정하는 방법 설정

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

조회는 사용자가 대상이 있는 네임 스페이스 루트 또는 폴더에 액세스할 때 클라이언트 컴퓨터가 도메인 컨트롤러나 네임 스페이스 서버에서 받는 대상의 정렬 된 목록입니다. 클라이언트는 조회를 받은 후 목록의 첫 번째 대상에 액세스를 시도 합니다. 대상을 사용할 수 없는 경우 클라이언트는 다음 대상에 액세스 하려고 시도 합니다.
클라이언트 사이트의 대상은 항상 조회에 먼저 나열 됩니다. 클라이언트 사이트 외부의 대상은 순서 지정 메서드에 따라 나열 됩니다.

다음 섹션을 사용 하 여 클라이언트에 참조 해야 하는 순서를 지정 하 고 대상 조회 순서를 지정 하는 다양 한 방법을 파악 합니다.

## <a name="to-set-the-ordering-method-for-targets-in-namespace-root-referrals"></a>네임 스페이스 루트 조회에서 대상에 대 한 순서 지정 메서드를 설정 하려면

다음 절차를 사용 하 여 네임 스페이스 루트에 순서 지정 메서드를 설정 합니다.

1.  **시작**을 클릭하고 **관리 도구**를 가리킨 다음 **DFS 관리**를 클릭합니다.

2.  콘솔 트리의 **네임스페이스** 노드에서 네임스페이스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.

3.  **조회** 탭에서 순서 지정 방법을 선택 합니다.

> [!NOTE]
> Windows PowerShell을 사용 하 여 네임 스페이스 루트 조회의 대상에 대 한 순서 지정 방법을 설정 하려면 다음 매개 변수 중 하 나와 함께 [DfsnRoot](https://technet.microsoft.com/library/jj884281.aspx) cmdlet을 사용 합니다.
>    -   **EnableSiteCosting** 는 **최저 비용 주문** 방법을 지정 합니다.
>    -   **EnableInsiteReferrals** 는 **클라이언트의 사이트 순서 메서드 외부에서 제외 대상을** 지정 합니다.
>    -   매개 변수 중 하나를 생략 하면 **무작위 주문** 조회 순서 지정 방법이 지정 됩니다.

DFSN Windows PowerShell 모듈은 Windows Server 2012에서 도입 되었습니다.

## <a name="to-set-the-ordering-method-for-targets-in-folder-referrals"></a>폴더 조회의 대상에 대 한 순서 지정 방법을 설정 하려면

대상이 있는 폴더는 네임 스페이스 루트의 순서 지정 메서드를 상속 합니다. 다음 절차를 사용 하 여 순서 지정 메서드를 재정의할 수 있습니다.

1.  **시작**을 클릭하고 **관리 도구**를 가리킨 다음 **DFS 관리**를 클릭합니다.

2.  콘솔 트리의 **네임스페이스** 노드에서 대상이 있는 폴더를 마우스 오른쪽 단추를 클릭한 다음 **속성**을 클릭합니다.

3.  **조회** 탭에서 **클라이언트 사이트 외부의 대상 제외** 확인란을 선택 합니다.

> [!NOTE]
> Windows PowerShell을 사용 하 여 클라이언트 사이트 외부에서 폴더 대상을 제외 하려면 [DfsnFolder – EnableInsiteReferrals](https://technet.microsoft.com/library/jj884283.aspx) cmdlet을 사용 합니다.

## <a name="target-referral-ordering-methods"></a>대상 조회 순서 지정 방법

세 가지 정렬 메서드는 다음과 같습니다.

-   임의 순서
-   가장 저렴 한 비용
-   클라이언트 사이트 외부에서 대상 제외

## <a name="random-order"></a>임의 순서

이 메서드에서 대상은 다음과 같이 정렬 됩니다.

1.  클라이언트와 동일한 AD DS (Active Directory Directory Services) 사이트의 대상은 조회 맨 위에 임의의 순서로 나열 됩니다.
2.  클라이언트 사이트 외부의 대상은 임의 순서로 나열 됩니다.

동일한 사이트 대상 서버를 사용할 수 없는 경우 연결의 비용이 나 대상의 거리에 관계 없이 클라이언트 컴퓨터를 임의 대상 서버 라고 합니다.

## <a name="lowest-cost"></a>가장 저렴 한 비용

이 메서드에서 대상은 다음과 같이 정렬 됩니다.

1.  클라이언트와 동일한 사이트의 대상은 조회 맨 위에 임의의 순서로 나열 됩니다.
2.  클라이언트 사이트 외부의 대상은 가장 저렴 한 비용으로 가장 저렴 한 비용 순으로 나열 됩니다. 순위가 같은 조회는 함께 그룹화 되 고 대상은 각 그룹 내에서 임의 순서로 나열 됩니다.

> [!NOTE]
> 사이트 링크 비용은 DFS 관리 스냅인에 표시 되지 않습니다. 사이트 링크 비용을 보려면 Active Directory 사이트 및 서비스 스냅인을 사용 합니다.

## <a name="exclude-targets-outside-of-the-clients-site"></a>클라이언트 사이트 외부에서 대상 제외

이 메서드에서 조회는 클라이언트와 동일한 사이트에 있는 대상만 포함 합니다. 이러한 동일한 사이트 대상은 임의 순서로 나열 됩니다. 동일한 사이트 대상이 없으면 클라이언트는 조회를 수신 하지 않고 네임 스페이스의 해당 부분에 액세스할 수 없습니다.

> [!NOTE]
> 대상 우선 순위가 "모든 대상 중 첫 번째" 또는 "모든 대상 중 마지막"으로 설정 된 대상은 주문 메서드가 **클라이언트 사이트 외부에서 대상을 제외**하도록 설정 된 경우에도 조회에 계속 나열 됩니다.

## <a name="additional-references"></a>추가 참조

-   [DFS 네임스페이스 튜닝](tuning-dfs-namespaces.md)
-   [DFS 네임스페이스에 대한 관리 권한 위임](delegate-management-permissions-for-dfs-namespaces.md)