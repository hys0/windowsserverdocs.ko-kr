---
title: 폴더 대상 추가
description: 이 항목에서는 폴더 대상(UNC 경로)을 추가하는 방법을 설명합니다.
ms.prod: windows-server
ms.author: jgerend
manager: brianlic
ms.technology: storage
ms.topic: article
author: jasongerend
ms-date: 06/05/2017
ms.openlocfilehash: d2f3845a612556a51692aaf51d256bbedd518e7a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854106"
---
# <a name="add-folder-targets"></a>폴더 대상 추가

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

폴더 대상은 공유 폴더의 UNC(범용 명명 규칙) 경로이거나 네임스페이스의 폴더와 연결된 다른 네임스페이스입니다. 여러 폴더 대상을 추가하면 네임스페이스에서 폴더의 가용성이 향상됩니다.

## <a name="to-add-a-folder-target"></a>폴더 대상을 추가하려면

DFS 관리를 사용하여 폴더 대상을 추가하려면 다음 절차를 따르세요.

1.  **시작**을 클릭하고 **관리 도구**를 가리킨 다음 **DFS 관리**를 클릭합니다.

2.  콘솔 트리의 **네임스페이스** 노드에서 폴더를 마우스 오른쪽 단추를 클릭한 다음 **폴더 대상 추가**를 클릭합니다.

3.  폴더 대상의 경로를 입력하거나 **찾아보기**를 클릭하여 폴더 대상을 찾습니다.

4.  폴더가 DFS 복제를 사용하여 복제되는 경우 복제 그룹에 새 폴더 대상을 추가할지 여부를 지정할 수 있습니다.

> [!TIP]
> Windows PowerShell을 사용하여 폴더 대상을 추가하려면 [New-DfsnFolderTarget](https://docs.microsoft.com/powershell/module/dfsn/new-dfsnfoldertarget) cmdlet을 사용합니다. DFSN Windows PowerShell 모듈은 Windows Server 2012에서 도입되었습니다.

> [!NOTE]
> 폴더 계층 구조의 동일한 수준에 폴더 대상과 다른 DFS 폴더 중 하나만 있을 수 있습니다.

## <a name="see-also"></a>참고 항목

-   [DFS 네임스페이스 배포](deploying-dfs-namespaces.md)
-   [DFS 네임스페이스에 대한 관리 권한 위임](delegate-management-permissions-for-dfs-namespaces.md)
-   [DFS 복제를 사용 하 여 폴더 대상 복제](replicate-folder-targets-using-dfs-replication.md)