---
title: 네임스페이스 폴링 최적화
description: 이 문서에서는 네임 스페이스 서버 간에 일관 된 도메인 기반 네임 스페이스를 유지 하기 위해 네임 스페이스 폴링을 최적화 하는 방법을 설명 합니다.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: ea867cbb36286297ff3c5274d11c36b5815ab9ac
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475460"
---
# <a name="optimize-namespace-polling"></a>네임스페이스 폴링 최적화

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

네임스페이스 서버 간에 일관된 도메인 기반 네임스페이스를 유지 관리하려면 네임스페이스 서버가 AD DS(Active Directory Domain Services)를 정기적으로 폴링하여 최신 네임스페이스 데이터를 얻어야 합니다.

## <a name="to-optimize-namespace-polling"></a>네임스페이스 폴링을 최적화하려면

다음 절차를 사용 하 여 네임 스페이스 폴링을 수행 하는 방법을 최적화 합니다.

1.  **시작**을 클릭하고 **관리 도구**를 가리킨 다음 **DFS 관리**를 클릭합니다.

2.  콘솔 트리의 **네임 스페이스** 노드에서 도메인 기반 네임 스페이스를 마우스 오른쪽 단추로 클릭 한 다음 **속성** 을 클릭 합니다.

3.  **고급** 탭에서 네임 스페이스의 일관성 또는 확장성을 최적화 하려는 지 여부를 선택 합니다.

    -   네임 스페이스를 호스팅하는 네임 스페이스 서버가 16 개 이하인 경우 **일관성을 위해 최적화를** 선택 합니다.
    -   네임 스페이스 서버가 16 개 이상인 경우 **확장성을 위해 최적화를** 선택 합니다. 이렇게 하면 주 도메인 컨트롤러 (PDC) 에뮬레이터의 로드가 줄어들지만 네임 스페이스를 변경 하 여 모든 네임 스페이스 서버에 복제 하는 데 필요한 시간이 늘어납니다. 변경 내용이 모든 서버에 복제될 때까지 사용자에게 표시되는 네임스페이스 내용이 다를 수 있습니다.

> [!NOTE]
> Windows PowerShell을 사용 하 여 네임 스페이스 폴링 모드를 설정 하려면 Windows Server 2012에 도입 된 [DfsnRoot EnableRootScalability](https://technet.microsoft.com/library/jj884281.aspx) cmdlet을 사용 합니다.

## <a name="additional-references"></a>추가 참조

-   [DFS 네임스페이스 튜닝](tuning-dfs-namespaces.md)
-   [DFS 네임스페이스에 대한 관리 권한 위임](delegate-management-permissions-for-dfs-namespaces.md)