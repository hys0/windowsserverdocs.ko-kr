---
title: '검사 목록: DFS 네임스페이스 배포'
description: 이 문서에서는 DFS 네임스페이스를 구성하고 배포하는 방법을 설명합니다.
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 7f7cca6b67ff6fa8d81e88323381866315f07f33
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842124"
---
# <a name="checklist-deploy-dfs-namespaces"></a>검사 목록: DFS 네임 스페이스를 배포 합니다.

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

분산된 파일 시스템 (DFS) 네임 스페이스 및 DFS 복제 조직 전체의 사용자에 게 문서, 소프트웨어 및 기간 업무 데이터를 게시할 수 있습니다. 단독으로 DFS 복제 데이터를 배포 하는 충분 한 경우에 폴더는 폴더의 업데이트 된 복사본을 보유 하는 각 여러 서버에서 호스트 되는 네임 스페이스를 구성 하려면 DFS 네임 스페이스를 사용할 수 있습니다. 그러면 데이터 가용성이 높아지고 여러 서버로 클라이언트 로드가 분산됩니다.

사용자는 네임스페이스에서 폴더를 찾을 때 여러 서버에서 폴더를 호스팅함을 알지 못합니다. 사용자가 폴더를 열 때 클라이언트가 자동으로 해당 사이트의 서버에 조회합니다. 동일한 사이트 서버가 있는 경우 클라이언트가 Active Directory Directory Services (AD DS)에 정의 된 대로 비용이 가장 낮은 연결 된 서버를 가리키도록 네임 스페이스를 구성할 수 있습니다.

DFS 네임스페이스를 배포하려면 다음 절차를 수행하세요.

-   DFS 네임스페이스의 기본 개념 및 요구 사항을 검토합니다.
[DFS 네임 스페이스 개요](dfs-overview.md)
-   [네임 스페이스 유형 선택](choose-a-namespace-type.md)
-   [DFS 네임 스페이스 만들기](create-a-dfs-namespace.md) 
-   기존의 도메인 기반 네임스페이스를 Windows Server 2008 모드 도메인 기반 네임스페이스로 마이그레이션합니다. [도메인 기반 Namespace 모드로 Windows Server 2008로 마이그레이션](migrate-a-domain-based-namespace-to-windows-server-2008-mode.md) 
-   도메인 기반 네임스페이스에 네임스페이스 서버를 추가하여 가용성을 높입니다. [도메인 기반 DFS Namespace Namespace 서버 추가](add-namespace-servers-to-a-domain-based-dfs-namespace.md)
-   네임스페이스에 폴더를 추가합니다. [DFS Namespace에 폴더를 만듭니다](create-a-folder-in-a-dfs-namespace.md)
-   네임스페이스의 폴더에 폴더 대상을 추가합니다. [대상 폴더를 추가 합니다.](add-folder-targets.md)
-   DFS 복제를 사용하여 폴더 대상 간에 콘텐츠를 복제합니다(옵션). [DFS 복제를 사용 하 여 폴더 대상에 복제](replicate-folder-targets-using-dfs-replication.md)


## <a name="see-also"></a>참조

-   [네임 스페이스](https://technet.microsoft.com/library/cc771914(v=ws.11).aspx)
-   [검사 목록: DFS Namespace 조정](checklist-tune-a-dfs-namespace.md)
-   [복제](https://technet.microsoft.com/library/cc770278(v=ws.11).aspx)


