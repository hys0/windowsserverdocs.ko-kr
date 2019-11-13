---
title: DFS 네임스페이스에 대한 관리 권한 위임
description: 이 문서에서는 DFS 네임스페이스에 대한 관리 권한을 위임하는 방법과 기본적으로 어느 그룹이 네임스페이스 작업을 실행할 수 있는지 설명합니다.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 5bf23498c95d4b44d5c17aecd216921dc70819a3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402212"
---
# <a name="delegate-management-permissions-for-dfs-namespaces"></a>DFS 네임스페이스에 대한 관리 권한 위임

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

다음 표에서는 기초적인 네임스페이스 작업을 기본적으로 수행할 수 있는 그룹과 이러한 작업을 수행할 수 있는 권한을 위임하는 방법을 설명합니다.

|태스크 | 기본적으로 이 작업을 수행할 수 있는 그룹 | 위임 방법 |
|---|---|---|
|도메인 기반 네임스페이스 만들기|네임스페이스가 구성된 도메인의 도메인 관리자 그룹|콘솔 트리에서 **네임스페이스** 노드를 마우스 오른쪽 단추로 클릭하고 **관리 권한 위임**을 클릭합니다. 또는 [Set-DfsnRoot GrantAdminAccounts](https://technet.microsoft.com/itpro/powershell/windows/dfsn/set-dfsnroot)와 [Set-DfsnRoot RevokeAdminAccounts](https://technet.microsoft.com/itpro/powershell/windows/dfsn/set-dfsnroot)를 사용합니다. Windows PowerShell cmdlet(Windows Server 2012에서 도입됨). 또한 네임스페이스 서버의 로컬 관리자 그룹에 사용자를 추가해야 합니다.|
|도메인 기반 네임스페이스에 네임스페이스 서버 추가|네임스페이스가 구성된 도메인의 도메인 관리자 그룹| 콘솔 트리에서 도메인 기반 네임스페이스를 마우스 오른쪽 단추로 클릭하고 **관리 권한 위임**을 클릭합니다. 또는 [Set-DfsnRoot GrantAdminAccounts](https://technet.microsoft.com/itpro/powershell/windows/dfsn/set-dfsnroot)와 [Set-DfsnRoot RevokeAdminAccounts](https://technet.microsoft.com/itpro/powershell/windows/dfsn/set-dfsnroot)를 사용합니다. Windows PowerShell cmdlet(Windows Server 2012에서 도입됨). 또한 추가할 네임스페이스 서버의 로컬 관리자 그룹에 사용자를 추가해야 합니다.|
|도메인 기반 네임스페이스 관리|각 네임스페이스 서버의 로컬 관리자 그룹| 콘솔 트리에서 도메인 기반 네임스페이스를 마우스 오른쪽 단추로 클릭하고 **관리 권한 위임**을 클릭합니다. |
|독립형 네임스페이스 만들기|네임스페이스 서버의 로컬 관리자 그룹| 네임스페이스 서버의 로컬 관리자 그룹에 사용자를 추가합니다. |
|독립형 네임스페이스 관리*|네임스페이스 서버의 로컬 관리자 그룹| 콘솔 트리에서 독립형 네임스페이스를 마우스 오른쪽 단추로 클릭하고 **관리 권한 위임**을 클릭합니다. 또는 [Set-DfsnRoot GrantAdminAccounts](https://technet.microsoft.com/itpro/powershell/windows/dfsn/set-dfsnroot)와 [Set-DfsnRoot RevokeAdminAccounts](https://technet.microsoft.com/itpro/powershell/windows/dfsn/set-dfsnroot)를 사용합니다. Windows PowerShell cmdlet(Windows Server 2012에서 도입됨).|
|복제 그룹 만들기 또는 폴더에서 DFS 복제 사용|네임스페이스가 구성된 도메인의 도메인 관리자 그룹| 콘솔 트리에서 복제 노드를 마우스 오른쪽 단추로 클릭하고 **관리 권한 위임**을 클릭합니다. |

<br />

독립 실행형 네임 스페이스를 관리 하는 관리 권한을 위임 하는 \*사용자가 네임 스페이스 서버에서 로컬 관리자 그룹의 멤버가 아닌 경우 **위임** 탭을 사용 하 여 보안을 확인 하 고 관리할 수 있는 기능을 사용자에 게 부여 하지 않습니다. 이는 DFS 관리 스냅인이 레지스트리에서 독립형 네임스페이스에 대한 DACL(임의 액세스 제어 목록)을 검색할 수 없기 때문입니다. 스냅인에서 위임 정보를 표시할 수 있게 하려면 Microsoft<sup>®</sup> 기술 자료 문서: [KB314837: 레지스트리에 대한 원격 액세스를 관리하는 방법](https://go.microsoft.com/fwlink?linkid=46803)의 단계를 수행해야 합니다.