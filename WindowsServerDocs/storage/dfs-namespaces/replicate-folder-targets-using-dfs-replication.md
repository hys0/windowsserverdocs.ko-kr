---
title: "DFS 복제를 사용하여 폴더 대상 복제"
description: "이 문서에서는 DFS 복제를 사용하여 폴더 대상을 복제하는 방법을 설명합니다."
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: ef13c338d8b13c24a02efb0468f06d5fef803cea
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="replicate-folder-targets-using-dfs-replication"></a>DFS 복제를 사용하여 폴더 대상 복제

> 적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 및 Windows Server 2008

클라이언트 컴퓨터가 어느 폴더 대상에 조회하는지에 관계없이 사용자가 동일한 파일을 보도록 DFS 복제를 사용하여 폴더 내용을 동기화된 상태로 유지할 수 있습니다.

## <a name="to-replicate-folder-targets-using-dfs-replication"></a>DFS 복제를 사용하여 폴더 대상을 복제하려면

1.  **시작**을 클릭하고 **관리 도구**를 가리킨 다음 **DFS 관리**를 클릭합니다.

2.  콘솔 트리의 **네임스페이스** 노드에서 여러 폴더 대상을 가진 폴더를 마우스 오른쪽 단추로 클릭한 다음 **폴더 복제**를 클릭합니다.

3.  폴더 복제 마법사의 지침을 따릅니다.

> [!NOTE]
> [Suspend-DfsReplicationGroup](https://technet.microsoft.com/itpro/powershell/windows/dfsr/suspend-dfsreplicationgroup) 및 [Sync-DfsReplicationGroup](https://technet.microsoft.com/itpro/powershell/windows/dfsr/sync-dfsreplicationgroup) cmdlet을 사용할 때 이외에는 구성 변경 사항이 모든 구성원에게 즉시 적용되지 않습니다. 새 구성은 모든 도메인 컨트롤러에 복제되어야 하며 복제 그룹의 각 구성원은 가장 가까운 도메인 컨트롤러를 폴링하여 변경 사항을 가져와야 합니다. 이 작업에 걸리는 시간은 각 구성원에 대한 AD DS(Active Directory Directory Services) 복제 대기 시간 및 긴 폴링 간격(60분)에 따라 다릅니다. 구성 변경 사항을 즉시 폴링하려면 명령 프롬프트 창을 열고 복제 그룹의 각 구성원에 대해 다음 명령을 한 번씩 입력합니다. <br /> dfsrdiag.exe PollAD /Member:DOMAIN\Server1
<br />
Windows PowerShell 세션에서 이렇게 하려면 Windows Server 2012 R2에서 도입된 [Update-DfsrConfigurationFromAD](https://technet.microsoft.com/itpro/powershell/windows/dfsr/update-dfsrconfigurationfromad) cmdlet을 사용합니다.

## <a name="see-also"></a>참고 항목

-   [DFS 네임스페이스 배포](deploying-dfs-namespaces.md)
-   [DFS 네임스페이스에 대한 관리 권한 위임](delegate-management-permissions-for-dfs-namespaces.md)
-   [복제](https://technet.microsoft.com/library/cc770278(v=ws.11).aspx)