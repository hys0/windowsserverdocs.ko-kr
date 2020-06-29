---
title: DFS 네임스페이스에 폴더 만들기
description: 이 문서에서는 DFS 네임 스페이스에서 폴더를 만드는 방법을 설명 합니다.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 18e0f1ad19e8c6ce2b6dbffe0d25c940c4f8f985
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474280"
---
# <a name="create-a-folder-in-a-dfs-namespace"></a>DFS 네임 스페이스에 폴더 만들기

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

폴더를 사용 하 여 네임 스페이스에서 계층의 추가 수준을 만들 수 있습니다. 폴더 대상을 사용 하 여 폴더를 만들어 네임 스페이스에 공유 폴더를 추가할 수도 있습니다. 폴더 대상이 있는 DFS 폴더는 다른 DFS 폴더를 포함할 수 없으므로 계층의 수준을 네임 스페이스에 추가 하려는 경우 폴더 대상을 폴더에 추가 하지 마십시오.

DFS 관리를 사용 하 여 네임 스페이스에서 폴더를 만들려면 다음 절차를 따르십시오.

## <a name="to-create-a-folder-in-a-dfs-namespace"></a>DFS 네임 스페이스에서 폴더를 만들려면

1.  **시작**을 클릭하고 **관리 도구**를 가리킨 다음 **DFS 관리**를 클릭합니다.

2.  콘솔 **트리의 네임 스페이스 노드에서 네임** 스페이스 또는 네임 스페이스 내의 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **새 폴더**를 클릭 합니다.

3.  **이름** 텍스트 상자에 새 폴더의 이름을 입력 합니다.

4.  폴더에 폴더 대상을 하나 이상 추가 하려면 **추가** 를 클릭 하 고 폴더 대상의 UNC (범용 명명 규칙) 경로를 지정한 다음 **확인** 을 클릭 합니다.


> [!TIP]
> Windows PowerShell을 사용 하 여 네임 스페이스에서 폴더를 만들려면 [DfsnFolder](https://docs.microsoft.com/powershell/module/dfsn/new-dfsnfolder) cmdlet을 사용 합니다. DFSN Windows PowerShell 모듈은 Windows Server 2012에서 도입 되었습니다.


## <a name="additional-references"></a>추가 참조

-   [DFS 네임스페이스 배포](deploying-dfs-namespaces.md)
-   [DFS 네임스페이스에 대한 관리 권한 위임](delegate-management-permissions-for-dfs-namespaces.md)


