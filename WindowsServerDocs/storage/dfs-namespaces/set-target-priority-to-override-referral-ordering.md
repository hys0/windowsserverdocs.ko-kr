---
title: "대상 우선 순위를 설정하여 조회 순서 지정 무시"
description: "이 문서에서는 대상 우선 순위를 설정하여 조회 순서 지정을 무시하는 방법을 설명합니다."
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 10f5e8979ae2f6390da76276dfa193226019e5d3
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="set-target-priority-to-override-referral-ordering"></a>대상 우선 순위를 설정하여 조회 순서 지정 무시

> 적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

조회는 사용자가 네임스페이스에 대상을 가진 네임스페이스 루트나 폴더에 액세스할 때 클라이언트 컴퓨터가 도메인 컨트롤러나 네임스페이스 서버에서 받는 대상의 정렬된 목록입니다. 조회에 있는 각 대상은 네임스페이스 루트 또는 폴더의 순서 지정 방법에 따라 순서가 지정됩니다. 

대상 순서 지정 방법을 구체화하려면 개별 대상에 우선 순위를 설정합니다. 예를 들어 모든 대상 중 첫 번째, 모든 대상 중 마지막 또는 같은 비용의 모든 대상 중 첫 번째(또는 마지막)로 대상을 지정할 수 있습니다.

## <a name="to-set-target-priority-on-a-root-target-for-a-domain-based-namespace"></a>도메인 기반 네임스페이스의 루트 대상에 대상 우선 순위를 설정하려면

도메인 기반 네임스페이스의 루트 대상에 대상 우선 순위를 설정하려면 다음 절차를 수행합니다.

1.  **시작**을 클릭하고 **관리 도구**를 가리킨 다음 **DFS 관리**를 클릭합니다.

2.  콘솔 트리의 **네임스페이스** 노드에서 루트 대상에 우선 순위를 설정할 도메인 기반 네임스페이스를 클릭합니다.

3.  **세부 정보** 창의 **네임스페이스 서버** 탭에서 우선 순위를 변경할 루트 대상을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.

4.  **고급** 탭에서 **조회 순서 지정 무시**를 클릭한 다음 원하는 우선 순위를 클릭합니다.

    -   **모든 대상 중 첫 번째**  대상을 사용할 수 있는 경우 사용자가 항상 이 대상에 조회해야 함을 지정합니다.
    -   **모든 대상 중 마지막**  기타 모든 대상을 사용할 수 없는 경우가 아니면 사용자가 이 대상에 조회하면 안 됨을 지정합니다.
    -   **같은 비용의 대상 중 첫 번째**  같은 비용의 다른 대상(일반적으로 같은 사이트에 있는 다른 대상) 전에 사용자가 이 대상에 조회해야 함을 지정합니다.
    -   **같은 비용의 대상 중 마지막**  같은 비용의 다른 대상(일반적으로 같은 사이트에 있는 다른 대상을 말함)을 사용할 수 있는 경우 사용자가 이 대상에 조회하면 안 됨을 지정합니다.

## <a name="to-set-target-priority-on-a-folder-target"></a>폴더 대상에 대상 우선 순위를 설정하려면

폴더 대상에 대상 우선 순위를 설정하려면 다음 절차를 수행합니다.

1.  **시작**을 클릭하고 **관리 도구**를 가리킨 다음 **DFS 관리**를 클릭합니다.

2.  콘솔 트리의 **네임스페이스** 노드에서 대상에 우선 순위를 설정할 폴더를 클릭합니다.

3.  **세부 정보** 창의 **폴더 대상** 탭에서 우선 순위를 변경할 폴더 대상을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.

4.  **고급** 탭에서 **조회 순서 지정 무시**를 클릭한 다음 원하는 우선 순위를 클릭합니다.

> [!NOTE]
> Windows PowerShell을 사용하여 대상 우선 순위를 설정하려면 [Set-DfsnRootTarget](https://technet.microsoft.com/library/jj884266.aspx) 및 [Set-DfsnFolderTarget](https://technet.microsoft.com/library/jj884264.aspx) cmdlet을 **ReferralPriorityClass** 및 **ReferralPriorityRank** 매개 변수와 함께 사용합니다. 이 cmdlet은 Windows Server 2012에서 도입되었습니다.

## <a name="see-also"></a>참고 항목

-   [DFS 네임스페이스 조정](tuning-dfs-namespaces.md)
-   [DFS 네임스페이스에 대한 관리 권한 위임](delegate-management-permissions-for-dfs-namespaces.md)