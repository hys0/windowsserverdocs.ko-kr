---
title: 대상 우선 순위를 설정하여 조회 순서 지정 재정의
description: 이 문서에서는 조회 순서를 재정의 하도록 대상 우선 순위를 설정 하는 방법을 설명 합니다.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 401e15c248687c7585cb85172b1d4d57125cdc86
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475180"
---
# <a name="set-target-priority-to-override-referral-ordering"></a>대상 우선 순위를 조회 순서 재정의로 설정

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

조회는 사용자가 네임스페이스에 대상이 있는 네임스페이스 루트나 폴더에 액세스할 때 클라이언트 컴퓨터가 도메인 컨트롤러나 네임스페이스 서버에서 받는 대상의 정렬된 목록입니다. 조회에 있는 각 대상은 네임스페이스 루트 또는 폴더의 순서 지정 방법에 따라 순서가 지정됩니다.

대상의 순서를 조정 하려면 개별 대상에 우선 순위를 설정할 수 있습니다. 예를 들어 대상이 모든 대상 중 먼저, 모든 대상 중 마지막 또는 동일한 비용의 모든 대상 중 첫 번째 또는 마지막으로 지정 되도록 지정할 수 있습니다.

## <a name="to-set-target-priority-on-a-root-target-for-a-domain-based-namespace"></a>도메인 기반 네임스페이스의 루트 대상에 대상 우선 순위를 설정하려면

도메인 기반 네임 스페이스의 루트 대상에 대상 우선 순위를 설정 하려면 다음 절차를 따르십시오.

1.  **시작**을 클릭하고 **관리 도구**를 가리킨 다음 **DFS 관리**를 클릭합니다.

2.  콘솔 트리의 **네임 스페이스** 노드에서 우선 순위를 설정 하려는 루트 대상의 도메인 기반 네임 스페이스를 클릭 합니다.

3.  **세부 정보** 창의 **네임 스페이스 서버** 탭에서 우선 순위가 변경 하려는 루트 대상을 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다.

4.  **고급** 탭에서 **조회 순서 재정의**를 클릭 하 고 원하는 우선 순위를 클릭 합니다.

    -   **모든 대상 중 첫 번째**  대상을 사용할 수 있는 경우 사용자에 게 항상이 대상을 참조 하도록 지정 합니다.
    -   **모든 대상 중 마지막** 다른 모든 대상을 사용할 수 없는 경우를 제외 하 고 사용자가이 대상으로 참조 되어서는 안 됨을 지정 합니다.
    -   **동일한 비용의 대상 중 첫 번째**  동일한 비용의 다른 대상 (일반적으로 동일한 사이트의 다른 대상을 의미 함)에 대해 사용자가이 대상으로 참조 되어야 함을 지정 합니다.
    -   **동일한 비용의 대상 중 마지막**  사용 가능한 동일한 비용의 다른 대상이 있는 경우 (일반적으로 동일한 사이트의 다른 대상을 의미 함) 사용자를이 대상으로 참조 하지 않도록 지정 합니다.

## <a name="to-set-target-priority-on-a-folder-target"></a>폴더 대상에 대상 우선 순위를 설정하려면

폴더 대상에 대상 우선 순위를 설정 하려면 다음 절차를 따르십시오.

1.  **시작**을 클릭하고 **관리 도구**를 가리킨 다음 **DFS 관리**를 클릭합니다.

2.  콘솔 트리의 **네임 스페이스** 노드에서 우선 순위를 설정 하려는 대상의 폴더를 클릭 합니다.

3.  **세부 정보** 창의 **폴더 대상** 탭에서 우선 순위가 변경 하려는 폴더 대상을 마우스 오른쪽 단추로 클릭 한 다음 **속성** 을 클릭 합니다.

4.  **고급** 탭에서 **조회 순서 재정의** 를 클릭 한 다음 원하는 우선 순위를 클릭 합니다.

> [!NOTE]
> Windows PowerShell을 사용 하 여 대상 우선 순위를 설정 하려면 **ReferralPriorityClass** 및 **ReferralPriorityRank** 매개 변수를 사용 하 여 [DfsnRootTarget](https://technet.microsoft.com/library/jj884266.aspx) 및 [DfsnFolderTarget](https://technet.microsoft.com/library/jj884264.aspx) cmdlet을 사용 합니다. 이러한 cmdlet은 Windows Server 2012에서 도입 되었습니다.

## <a name="additional-references"></a>추가 참조

-   [DFS 네임스페이스 튜닝](tuning-dfs-namespaces.md)
-   [DFS 네임스페이스에 대한 관리 권한 위임](delegate-management-permissions-for-dfs-namespaces.md)