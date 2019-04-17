---
title: "도메인 기반 DFS 네임스페이스에 네임스페이스 서버 추가"
description: "이 문서에서는 DFS 관리를 사용하여 네임스페이스 호스팅을 위한 추가 네임스페이스 서버를 지정하는 방법을 설명합니다."
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 70ab3cac71f5766bc572015c6b23c0937e5252f0
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="add-namespace-servers-to-a-domain-based-dfs-namespace"></a>도메인 기반 DFS 네임스페이스에 네임스페이스 서버 추가

> 적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

네임스페이스 호스팅을 위한 추가 네임스페이스 서버를 지정하여 도메인 기반 네임스페이스의 가용성을 높일 수 있습니다.

## <a name="to-add-a-namespace-server-to-a-domain-based-namespace"></a>도메인 기반 네임스페이스에 네임스페이스 서버를 추가하려면

DFS 관리를 사용하여 도메인 기반 네임스페이스에 네임스페이스 서버를 추가하려면 다음 절차를 따르세요.

1.  **시작**을 클릭하고 **관리 도구**를 가리킨 다음 **DFS 관리**를 클릭합니다.

2.  콘솔 트리의 **네임스페이스** 노드에서 도메인 기반 네임스페이스를 마우스 오른쪽 단추로 클릭한 다음 **네임스페이스 서버 추가**를 클릭합니다.

3.  다른 서버의 경로를 입력하거나 **찾아보기**를 클릭하여 서버를 찾습니다.

> [!NOTE]
> 단일 네임스페이스 서버만 지원하는 독립형 네임스페이스에는 이 절차를 사용할 수 없습니다. 독립형 네임스페이스의 가용성을 높이려면 새 네임스페이스 마법사에서 장애 조치(failover) 클러스터를 네임스페이스 서버로 지정합니다.


> [!TIP]
> Windows PowerShell을 사용하여 네임스페이스 서버를 추가하려면 [New-DfsnRootTarget cmdlet](https://docs.microsoft.com/powershell/module/dfsn/set-dfsnroottarget)을 사용합니다. DFSN Windows PowerShell 모듈은 Windows Server 2012에서 도입되었습니다.

## <a name="see-also"></a>참고 항목

-   [DFS 네임스페이스 배포](deploying-dfs-namespaces.md)
-   [DFS 네임스페이스 서버 요구 사항 검토](https://technet.microsoft.com/library/cc753448(v=ws.11).aspx)
-   [DFS 네임스페이스 만들기](create-a-dfs-namespace.md)
-   [DFS 네임스페이스에 대한 관리 권한 위임](delegate-management-permissions-for-dfs-namespaces.md)

