---
title: 도메인 기반 DFS 네임스페이스에 네임스페이스 서버 추가
description: 이 문서에서는 DFS 관리를 사용 하 여 네임 스페이스를 호스팅하는 추가 네임 스페이스 서버를 지정 하는 방법을 설명 합니다.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: ee2ae5ddf40c6d8b49b9fbd40505f4e8c70fd92c
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85473500"
---
# <a name="add-namespace-servers-to-a-domain-based-dfs-namespace"></a>도메인 기반 DFS 네임 스페이스에 네임 스페이스 서버 추가

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

네임 스페이스를 호스팅할 추가 네임 스페이스 서버를 지정 하 여 도메인 기반 네임 스페이스의 가용성을 높일 수 있습니다.

## <a name="to-add-a-namespace-server-to-a-domain-based-namespace"></a>도메인 기반 네임 스페이스에 네임 스페이스 서버를 추가 하려면

DFS 관리를 사용 하 여 도메인 기반 네임 스페이스에 네임 스페이스 서버를 추가 하려면 다음 절차를 따르십시오.

1.  **시작**을 클릭하고 **관리 도구**를 가리킨 다음 **DFS 관리**를 클릭합니다.

2.  콘솔 트리의 **네임** 스페이스 노드에서 도메인 기반 네임 스페이스를 마우스 오른쪽 단추로 클릭 한 다음 **네임 스페이스 서버 추가**를 클릭 합니다.

3.  다른 서버에 대 한 경로를 입력 하거나 **찾아보기** 를 클릭 하 여 서버를 찾습니다.

> [!NOTE]
> 이 프로시저는 단일 네임 스페이스 서버만 지원 하기 때문에 독립 실행형 네임 스페이스에는 적용 되지 않습니다. 독립 실행형 네임 스페이스의 가용성을 높이려면 새 네임 스페이스 마법사에서 장애 조치 (failover) 클러스터를 네임 스페이스 서버로 지정 합니다.


> [!TIP]
> Windows PowerShell을 사용 하 여 네임 스페이스 서버를 추가 하려면 [DfsnRootTarget cmdlet](https://docs.microsoft.com/powershell/module/dfsn/new-dfsnroottarget)을 사용 합니다. DFSN Windows PowerShell 모듈은 Windows Server 2012에서 도입 되었습니다.

## <a name="additional-references"></a>추가 참조

-   [DFS 네임스페이스 배포](deploying-dfs-namespaces.md)
-   [DFS 네임 스페이스 서버 요구 사항 검토](https://technet.microsoft.com/library/cc753448(v=ws.11).aspx)
-   [DFS 네임스페이스 만들기](create-a-dfs-namespace.md)
-   [DFS 네임스페이스에 대한 관리 권한 위임](delegate-management-permissions-for-dfs-namespaces.md)

