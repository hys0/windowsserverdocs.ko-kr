---
title: 검사 목록 DFS 네임 스페이스 튜닝
description: 이 문서에서는 DFS 네임 스페이스가 업데이트 된 네임 스페이스 데이터에 대 한 조회를 처리 하 고 AD DS를 폴링하는 방법을 최적화 하는 방법을 설명
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: a6632e363b933ff0bce2fd59999e0a1dcffbe665
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475620"
---
# <a name="checklist-tune-a-dfs-namespace"></a>검사 목록: DFS 네임 스페이스 튜닝

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

네임 스페이스를 만들고 폴더 및 대상을 추가한 후에는 다음 검사 목록을 사용 하 여 DFS 네임 스페이스에서 조회를 처리 하 고 업데이트 된 네임 스페이스 데이터에 대 한 Active Directory Domain Services (AD DS)를 폴링합니다.

-   사용자가 액세스할 수 있는 권한이 없는 네임 스페이스의 폴더를 보지 못하도록 합니다. [네임 스페이스에 대 한 액세스 기반 열거 사용](enable-access-based-enumeration-on-a-namespace.md)
-   네임 스페이스의 폴더에 액세스 하는 경우 사용자가 네임 스페이스 또는 폴더 대상으로 참조 되는 것을 허용 하거나 금지 합니다. [조회 및 클라이언트 장애 복구 사용 또는 사용 안 함](enable-or-disable-referrals-and-client-failback.md)
-   클라이언트가 새 조회를 요청 하기 전에 조회를 캐시 하는 기간을 조정 합니다. [클라이언트에서 조회를 캐시 하는 시간 변경](change-the-amount-of-time-that-clients-cache-referrals.md)
-   네임 스페이스 서버가 최신 네임 스페이스 데이터를 가져오는 AD DS를 폴링하는 방법을 최적화 합니다. [네임스페이스 폴링 최적화](optimize-namespace-polling.md)
-   상속 된 사용 권한을 사용 하 여 액세스 기반 열거를 사용 하는 네임 스페이스의 폴더를 볼 수 있는 사용자를 제어할 수 있습니다. [액세스 기반 열거와 함께 상속 된 권한 사용](using-inherited-permissions-with-access-based-enumeration.md)

또한 대상 우선 순위 라고 하는 DFS 네임 스페이스 기능을 사용 하면 특정 서버가 항상 먼저 배치 되도록 서버 우선 순위를 지정 하 여 네임 스페이스의 대상이 있는 폴더에 액세스할 때 클라이언트가 수신 하는 서버 목록 (조회 라고 함)의 우선 순위를 지정할 수 있습니다.

-   사용자가 폴더 대상으로 참조 해야 하는 순서를 지정 합니다. [조회 대상의 순서를 지정하는 방법 설정](set-the-ordering-method-for-targets-in-referrals.md)
-   특정 네임 스페이스 서버나 폴더 대상에 대 한 조회 순서를 재정의 합니다. [대상 우선 순위를 설정하여 조회 순서 지정 재정의](set-target-priority-to-override-referral-ordering.md)

## <a name="additional-references"></a>추가 참조

-   [네임스페이스](https://technet.microsoft.com/library/cc771914(v=ws.11).aspx)
-   [검사 목록: DFS 네임스페이스 배포](checklist-deploy-dfs-namespaces.md)
-   [DFS 네임스페이스 튜닝](tuning-dfs-namespaces.md)


