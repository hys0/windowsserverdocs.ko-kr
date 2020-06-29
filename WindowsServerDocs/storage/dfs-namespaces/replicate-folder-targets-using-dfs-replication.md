---
title: DFS 복제를 사용하여 폴더 대상 복제
description: 이 문서에서는 DFS 복제를 사용 하 여 폴더 대상을 복제 하는 방법을 설명 합니다.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 3a4f76e43c2dbf5296afd163055adeafb36a5576
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474400"
---
# <a name="replicate-folder-targets-using-dfs-replication"></a>DFS 복제를 사용 하 여 폴더 대상 복제

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 및 Windows Server 2008

DFS 복제를 사용 하 여 클라이언트 컴퓨터를 참조 하는 폴더 대상에 관계 없이 사용자가 동일한 파일을 볼 수 있도록 폴더 대상의 내용을 동기화 상태로 유지할 수 있습니다.

## <a name="to-replicate-folder-targets-using-dfs-replication"></a>DFS 복제를 사용 하 여 폴더 대상을 복제 하려면

1.  **시작**을 클릭하고 **관리 도구**를 가리킨 다음 **DFS 관리**를 클릭합니다.

2.  콘솔 트리의 **네임 스페이스** 노드에서 둘 이상의 폴더 대상이 있는 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **폴더 복제**를 클릭 합니다.

3.  폴더 복제 마법사의 지침을 따릅니다.

> [!NOTE]
> [DfsReplicationGroup](https://technet.microsoft.com/itpro/powershell/windows/dfsr/suspend-dfsreplicationgroup) 및 [DfsReplicationGroup](https://technet.microsoft.com/itpro/powershell/windows/dfsr/sync-dfsreplicationgroup) cmdlet을 사용 하는 경우를 제외 하 고는 구성 변경 내용이 모든 멤버에 즉시 적용 되지 않습니다. 새 구성은 모든 도메인 컨트롤러에 복제되어야 하며 복제 그룹의 각 구성원은 가장 가까운 도메인 컨트롤러를 폴링하여 변경 사항을 가져와야 합니다. 이 작업에 걸리는 시간은 각 구성원에 대 한 AD DS (Active Directory Directory Services) 복제 대기 시간 및 긴 폴링 간격 (60 분)에 따라 달라 집니다. 구성 변경 내용에 대해 즉시 폴링 하려면 명령 프롬프트 창을 열고 복제 그룹의 각 구성원에 대해 다음 명령을 입력 합니다. <br /> dfsrdiag.exe PollAD /Member:DOMAIN\Server1
<br />
Windows PowerShell 세션에서이 작업을 수행 하려면 Windows Server 2012 r 2에 도입 된 [DfsrConfigurationFromAD](https://technet.microsoft.com/itpro/powershell/windows/dfsr/update-dfsrconfigurationfromad) cmdlet을 사용 합니다.

## <a name="additional-references"></a>추가 참조

-   [DFS 네임스페이스 배포](deploying-dfs-namespaces.md)
-   [DFS 네임스페이스에 대한 관리 권한 위임](delegate-management-permissions-for-dfs-namespaces.md)
-   [DFS 복제](../dfs-replication/dfsr-overview.md)