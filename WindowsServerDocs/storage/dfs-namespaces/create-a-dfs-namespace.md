---
title: DFS 네임스페이스 만들기
description: 이 문서에서는 DFS 네임스페이스를 만드는 방법을 설명합니다.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: f4d4b86dd1a105576ac4d1749213696b319ba528
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402203"
---
# <a name="create-a-dfs-namespace"></a>DFS 네임스페이스 만들기

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

새 네임스페이스를 만들려면 DFS 네임스페이스 역할 서비스를 설치할 때 서버 관리자를 사용하여 네임스페이스를 만들 수 있습니다. Windows PowerShell 세션에서 [New-DfsnRoot cmdlet](https://docs.microsoft.com/powershell/module/dfsn/new-dfsnroot)을 사용할 수도 있습니다. 

DFSN Windows PowerShell 모듈은 Windows Server 2012에서 도입되었습니다. 

대신 역할 서비스 설치 후 다음 절차에 따라 네임스페이스를 만들 수 있습니다.

## <a name="to-create-a-namespace"></a>네임스페이스를 만들려면

1.  **시작**을 클릭하고 **관리 도구**를 가리킨 다음 **DFS 관리**를 클릭합니다.

2.  콘솔 트리에서 **네임스페이스** 노드를 마우스 오른쪽 단추로 클릭한 다음 **새 네임스페이스**를 클릭합니다.

3.  **새 네임스페이스 마법사**의 설명을 따릅니다.

    장애 조치(failover) 클러스터에 독립형 네임스페이스를 만들려면 **새 네임스페이스 마법사**의 **네임스페이스 서버** 페이지에서 클러스터된 파일 서버 인스턴스의 이름을 지정합니다.

> [!IMPORTANT]
> 포리스트 기능 수준이 Windows Server 2003 이상인 경우를 제외 하 고 Windows Server 2008 모드를 사용 하 여 도메인 기반 네임 스페이스를 만들지 마세요. 이렇게 하면 DFS 폴더를 삭제할 수 없는 네임 스페이스가 생성 되어 다음 오류 메시지가 표시 될 수 있습니다. "폴더를 삭제할 수 없습니다. 이 기능을 마칠 수 없습니다."라는 오류 메시지가 나타납니다.

## <a name="see-also"></a>참조

-   [DFS 네임스페이스 배포](deploying-dfs-namespaces.md)
-   [네임스페이스 형식 선택](choose-a-namespace-type.md)
-   [도메인 기반 DFS 네임스페이스에 네임스페이스 서버 추가](add-namespace-servers-to-a-domain-based-dfs-namespace.md)
-   [DFS 네임스페이스에 대한 관리 권한 위임](delegate-management-permissions-for-dfs-namespaces.md).


