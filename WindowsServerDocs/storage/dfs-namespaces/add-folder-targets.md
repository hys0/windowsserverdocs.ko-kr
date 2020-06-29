---
title: 폴더 대상 추가
description: 이 항목에서는 폴더 대상을 추가 하는 방법에 대해 설명 합니다 (UNC 경로).
ms.prod: windows-server
ms.author: jgerend
manager: brianlic
ms.technology: storage
ms.topic: article
author: jasongerend
ms-date: 06/05/2017
ms.openlocfilehash: 2f4e0deb82f16c905f580c13115a5214556d4f5f
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475560"
---
# <a name="add-folder-targets"></a>폴더 대상 추가

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

폴더 대상은 공유 폴더의 UNC (범용 명명 규칙) 경로 이거나 네임 스페이스의 폴더와 연결 된 다른 네임 스페이스입니다. 여러 폴더 대상을 추가 하면 네임 스페이스에서 폴더의 가용성이 향상 됩니다.

## <a name="to-add-a-folder-target"></a>폴더 대상을 추가 하려면

DFS 관리를 사용 하 여 폴더 대상을 추가 하려면 다음 절차를 따르십시오.

1.  **시작**을 클릭하고 **관리 도구**를 가리킨 다음 **DFS 관리**를 클릭합니다.

2.  콘솔 트리의 **네임 스페이스** 노드에서 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **폴더 대상 추가**를 클릭 합니다.

3.  폴더 대상의 경로를 입력 하거나 **찾아보기** 를 클릭 하 여 폴더 대상을 찾습니다.

4.  DFS 복제를 사용 하 여 폴더를 복제 하는 경우 복제 그룹에 새 폴더 대상을 추가할지 여부를 지정할 수 있습니다.

> [!TIP]
> Windows PowerShell을 사용 하 여 폴더 대상을 추가 하려면 [DfsnFolderTarget](https://docs.microsoft.com/powershell/module/dfsn/new-dfsnfoldertarget) cmdlet을 사용 합니다. DFSN Windows PowerShell 모듈은 Windows Server 2012에서 도입 되었습니다.

> [!NOTE]
> 폴더는 폴더 계층의 같은 수준에서 폴더 대상 또는 다른 DFS 폴더를 포함할 수 있지만 둘 다 포함할 수는 없습니다.

## <a name="additional-references"></a>추가 참조

-   [DFS 네임스페이스 배포](deploying-dfs-namespaces.md)
-   [DFS 네임스페이스에 대한 관리 권한 위임](delegate-management-permissions-for-dfs-namespaces.md)
-   [DFS 복제를 사용 하 여 폴더 대상 복제](replicate-folder-targets-using-dfs-replication.md)