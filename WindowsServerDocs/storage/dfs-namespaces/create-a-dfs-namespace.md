---
title: DFS 네임스페이스 만들기
description: 이 문서에서는 DFS 네임 스페이스를 만드는 방법을 설명 합니다.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 90a6c0f72fc1a11d9070fa7866c0b64044131a07
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85469718"
---
# <a name="create-a-dfs-namespace"></a>DFS 네임 스페이스 만들기

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

새 네임 스페이스를 만들려면 DFS 네임 스페이스 역할 서비스를 설치할 때 서버 관리자를 사용 하 여 네임 스페이스를 만들 수 있습니다. Windows PowerShell 세션에서 [DfsnRoot cmdlet](https://docs.microsoft.com/powershell/module/dfsn/new-dfsnroot) 을 사용할 수도 있습니다.

DFSN Windows PowerShell 모듈은 Windows Server 2012에서 도입 되었습니다.

Alernatively 역할 서비스를 설치한 후 다음 절차를 사용 하 여 네임 스페이스를 만들 수 있습니다.

## <a name="to-create-a-namespace"></a>네임 스페이스를 만들려면

1.  **시작**을 클릭하고 **관리 도구**를 가리킨 다음 **DFS 관리**를 클릭합니다.

2.  콘솔 트리에서 **네임 스페이스** 노드를 마우스 오른쪽 단추로 클릭 한 다음 **새 네임 스페이스**를 클릭 합니다.

3.  **새 네임 스페이스 마법사**의 지시를 따릅니다.

    장애 조치 (failover) 클러스터에서 독립 실행형 네임 스페이스를 만들려면 **새 네임 스페이스 마법사** 의 **네임 스페이스 서버** 페이지에서 클러스터 된 파일 서버 인스턴스의 이름을 지정 합니다.

> [!IMPORTANT]
> 포리스트 기능 수준이 Windows Server 2003 이상인 경우를 제외 하 고 Windows Server 2008 모드를 사용 하 여 도메인 기반 네임 스페이스를 만들지 마세요. 이렇게 하면 DFS 폴더를 삭제할 수 없는 네임 스페이스가 생성 될 수 있습니다. "폴더를 삭제할 수 없습니다. 이 함수를 완료할 수 없습니다. "

## <a name="additional-references"></a>추가 참조

-   [DFS 네임스페이스 배포](deploying-dfs-namespaces.md)
-   [네임스페이스 형식 선택](choose-a-namespace-type.md)
-   [도메인 기반 DFS 네임스페이스에 네임스페이스 서버 추가](add-namespace-servers-to-a-domain-based-dfs-namespace.md)
-   [DFS 네임 스페이스에 대 한 관리 권한을 위임](delegate-management-permissions-for-dfs-namespaces.md)합니다.


