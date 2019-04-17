---
title: "검사 목록: DFS 네임스페이스 조정"
description: "이 문서에서는 DFS 네임스페이스가 조회를 처리하고 AD DS를 폴링하여 업데이트된 네임스페이스 데이터를 가져오는 방식을 최적화하는 방법을 설명합니다."
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 827484c2ffcbb2617626129011a8b510473fe669
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="checklist-tune-a-dfs-namespace"></a>검사 목록: DFS 네임스페이스 조정

> 적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

네임스페이스를 만들고 폴더와 대상을 추가한 후 다음 검사 목록을 사용하여 DFS 네임스페이스가 조회를 처리하고 AD DS(Active Directory Domain Services)를 폴링하여 업데이트된 네임스페이스 데이터를 가져오는 방식을 조정하거나 최적화하세요.

-   사용자가 액세스 권한이 없는 네임스페이스의 폴더를 보지 못하게 합니다. [네임스페이스에 액세스 기반 열거 사용](enable-access-based-enumeration-on-a-namespace.md) 
-   사용자가 네임스페이스의 폴더에 액세스할 때 네임스페이스나 폴더 대상에 조회하게 하거나 조회하지 못하게 합니다. [조회 및 클라이언트 장애 복구(failback) 사용 또는 사용 안 함](enable-or-disable-referrals-and-client-failback.md) 
-   새 조회를 요청하기 전에 클라이언트가 조회를 캐시하는 기간을 조정합니다. [클라이언트가 조회를 캐시하는 기간 변경](change-the-amount-of-time-that-clients-cache-referrals.md)
-   네임스페이스 서버가 AD DS를 폴링하여 최신 네임스페이스 데이터를 가져오는 방식을 최적화합니다. [네임스페이스 폴링 최적화](optimize-namespace-polling.md)
-   상속된 사용 권한을 사용하여 액세스 기반 열거가 사용되는 네임스페이스의 폴더를 볼 수 있는 사용자를 제어합니다. [액세스 기반 열거에 상속된 사용 권한 사용](using-inherited-permissions-with-access-based-enumeration.md)

또한 대상 우선 순위라는 향상된 DFS 네임스페이스 기능을 사용하여 클라이언트가 네임스페이스에서 대상을 가진 폴더에 액세스할 때 받는 서버 목록(조회)에 특정 서버가 첫 번째나 마지막으로 배치되도록 서버의 우선 순위를 지정할 수 있습니다.

-   사용자가 폴더 대상에 조회해야 하는 순서를 지정합니다. [조회 대상 순서 지정 방법 설정](set-the-ordering-method-for-targets-in-referrals.md)
-   특정 네임스페이스 서버나 폴더 대상에 대한 조회 순서를 무시합니다. [대상 우선 순위를 설정하여 조회 순서 지정 무시](set-target-priority-to-override-referral-ordering.md)

## <a name="see-also"></a>참고 항목

-   [네임스페이스](https://technet.microsoft.com/library/cc771914(v=ws.11).aspx)
-   [검사 목록: DFS 네임스페이스 배포](checklist-deploy-dfs-namespaces.md)
-   [DFS 네임스페이스 조정](tuning-dfs-namespaces.md)


