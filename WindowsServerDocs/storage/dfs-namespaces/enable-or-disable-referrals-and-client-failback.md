---
title: 조회 및 클라이언트 장애 복구(failback) 사용 또는 사용 안 함
description: 이 문서에서는 조회와 클라이언트 장애 복구(failback)를 사용하거나 사용하지 않도록 설정하는 방법을 설명합니다.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: e7dd11b530c61e2536db425d3e85e0fbe458d349
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386224"
---
# <a name="enable-or-disable-referrals-and-client-failback"></a>조회 및 클라이언트 장애 복구(failback) 사용 또는 사용 안 함

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

조회는 사용자가 대상을 가진 네임스페이스 루트나 DFS 폴더에 액세스할 때 클라이언트 컴퓨터가 도메인 컨트롤러나 네임스페이스 서버에서 받는 서버의 정렬된 목록입니다. 컴퓨터는 조회를 받은 후 목록에서 첫 번째 서버에 액세스하려고 합니다. 서버가 사용 가능하지 않으면 클라이언트 컴퓨터는 다음 서버에 액세스를 시도합니다. 서버를 사용할 수 없는 경우 대상이 복원된 후 기본 설정 서버로 장애 복구하도록 클라이언트를 구성할 수 있습니다.

다음 섹션에서는 조회를 사용하거나 사용하지 않도록 설정하거나 클라이언트 장애 복구(failback)를 사용하도록 설정하는 방법에 대한 정보를 제공합니다.

## <a name="enable-or-disable-referrals"></a>조회 사용 또는 사용 안 함

네임스페이스 서버 또는 폴더 대상의 조회를 사용하지 않도록 설정하면 사용자가 해당 네임스페이스 서버나 폴더 대상으로 연결되는 것을 방지할 수 있습니다. 이는 유지 관리를 위해 일시적으로 서버를 오프라인 상태로 만들어야 할 경우 유용합니다.

-   폴더 대상에 대한 조회를 사용하거나 사용하지 않도록 설정하려면 다음 단계를 사용합니다.

    1.  DFS 관리 콘솔 트리의 **네임스페이스** 노드에서 대상을 가진 폴더를 클릭한 다음 **세부 정보** 창에서 **폴더 대상** 탭을 클릭합니다.
    2.  폴더 대상을 마우스 오른쪽 단추로 클릭한 다음 **폴더 대상 사용 안 함** 또는 **폴더 대상 사용**을 클릭합니다.

-   네임스페이스 서버에 대한 조회를 사용하거나 사용하지 않도록 설정하려면 다음 단계를 사용합니다.

    1.  DFS 관리 콘솔 트리에서 적절한 네임스페이스를 선택한 다음 **네임스페이스 서버** 탭을 클릭합니다.
    2.  적절한 네임스페이스 서버를 마우스 오른쪽 단추로 클릭한 다음 **네임스페이스 서버 사용 안 함** 또는 **네임스페이스 서버 사용**을 클릭합니다.


> [!TIP]
> Windows PowerShell을 사용 하 여 조회를 사용 하거나 사용 하지 않도록 설정 하려면 [DfsnRootTarget – State](https://technet.microsoft.com/library/jj884266.aspx) 또는 [DfsnServerConfiguration](https://technet.microsoft.com/library/jj884277.aspx) cmdlet을 사용 합니다 .이 cmdlet은 windows Server 2012에 도입 되었습니다.

## <a name="enable-client-failback"></a>클라이언트 장애 복구를 사용하도록 설정

대상을 사용할 수 없는 경우 대상이 복원된 후 대상으로 장애 복구하도록 클라이언트를 구성할 수 있습니다. 장애 복구 (failback)가 작동 하려면 클라이언트 컴퓨터가 다음 항목에 나열 된 요구 사항을 충족 해야 합니다. [DFS 네임 스페이스 클라이언트 요구 사항을 검토](https://technet.microsoft.com/library/cc771913(v=ws.11).aspx)합니다.


> [!NOTE]
> Windows PowerShell을 사용하여 네임스페이스 루트에서 클라이언트 장애 복구(failback)를 사용하도록 설정하려면 [Set-DfsnRoot](https://technet.microsoft.com/library/jj884281.aspx) cmdlet을 사용합니다. Windows PowerShell을 사용하여 네임스페이스 루트에서 클라이언트 장애 복구(failback)를 사용하도록 설정하려면 [Set-DfsnRoot](https://technet.microsoft.com/library/jj884283.aspx) cmdlet을 사용합니다.


## <a name="to-enable-client-failback-for-a-namespace-root"></a>네임스페이스 루트에 클라이언트 장애 복구를 사용하려면

1.  **시작**을 클릭하고 **관리 도구**를 가리킨 다음 **DFS 관리**를 클릭합니다.

2.  콘솔 트리의 **네임스페이스** 노드에서 네임스페이스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.

3.  **조회** 탭에서 **기본 설정 대상으로 클라이언트 장애 복구** 확인란을 선택합니다.

대상을 가진 폴더는 네임스페이스 루트에서 클라이언트 장애 복구 설정을 상속받습니다. 클라이언트 장애 복구(failback)를 네임스페이스 루트에서 사용할 수 없는 경우 다음 절차를 사용하여 클라이언트가 대상을 가진 폴더에서 장애 복구되도록 설정할 수 있습니다.

## <a name="to-enable-client-failback-for-a-folder-with-targets"></a>대상이 있는 폴더에 대해 클라이언트 장애 복구를 사용하도록 설정하려면

1.  **시작**을 클릭하고 **관리 도구**를 가리킨 다음 **DFS 관리**를 클릭합니다.

2.  콘솔 트리의 **네임스페이스** 노드에서 대상이 있는 폴더를 마우스 오른쪽 단추를 클릭한 다음 **속성**을 클릭합니다.

3.  **조회** 탭에서 **기본 설정 대상으로 클라이언트 장애 복구** 확인란을 클릭합니다.

## <a name="see-also"></a>참조 

-   [DFS 네임스페이스 튜닝](tuning-dfs-namespaces.md)
-   [DFS 네임 스페이스 클라이언트 요구 사항 검토](https://technet.microsoft.com/library/cc771913(v=ws.11).aspx)
-   [DFS 네임스페이스에 대한 관리 권한 위임](delegate-management-permissions-for-dfs-namespaces.md)