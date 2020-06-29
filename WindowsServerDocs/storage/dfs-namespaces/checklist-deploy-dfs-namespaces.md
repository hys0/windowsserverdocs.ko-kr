---
title: 검사 목록 DFS 네임 스페이스 배포
description: 이 문서에서는 DFS 네임 스페이스를 구성 하 고 배포 하는 방법을 설명 합니다.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: adae586c67a34912ea34dca5749d8c69856033d0
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85473510"
---
# <a name="checklist-deploy-dfs-namespaces"></a>검사 목록: DFS 네임스페이스 배포

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

분산 파일 시스템 (DFS) 네임 스페이스 및 DFS 복제를 사용 하 여 조직 전체의 사용자에 게 문서, 소프트웨어 및 기간 업무 (lob) 데이터를 게시할 수 있습니다. DFS 복제 만으로는 데이터를 분산 하는 데 충분 하지만, DFS 네임 스페이스를 사용 하 여 폴더의 업데이트 된 복사본을 포함 하는 여러 서버에서 폴더를 호스팅하도록 네임 스페이스를 구성할 수 있습니다. 이렇게 하면 데이터 가용성이 높아지고 클라이언트 로드가 서버에 분산 됩니다.

네임 스페이스의 폴더를 검색할 때 사용자는 폴더가 여러 서버에서 호스트 되는 것을 인식 하지 못합니다. 사용자가 폴더를 열면 클라이언트 컴퓨터가 자동으로 해당 사이트의 서버를 참조 합니다. 동일한 사이트 서버를 사용할 수 없는 경우 AD DS (Active Directory Directory Services)에 정의 된 대로 연결 비용이 가장 낮은 서버를 클라이언트에 참조 하도록 네임 스페이스를 구성할 수 있습니다.

DFS 네임 스페이스를 배포 하려면 다음 작업을 수행 합니다.

-   DFS 네임 스페이스의 개념 및 요구 사항을 검토 합니다.
[DFS 네임 스페이스 개요](dfs-overview.md)
-   [네임 스페이스 유형 선택](choose-a-namespace-type.md)
-   [DFS 네임 스페이스 만들기](create-a-dfs-namespace.md)
-   기존 도메인 기반 네임 스페이스를 Windows Server 2008 모드 도메인 기반 네임 스페이스로 마이그레이션합니다. [도메인 기반 네임 스페이스를 Windows Server 2008 모드로 마이그레이션](migrate-a-domain-based-namespace-to-windows-server-2008-mode.md)
-   도메인 기반 네임 스페이스에 네임 스페이스 서버를 추가 하 여 가용성을 높입니다. [도메인 기반 DFS 네임스페이스에 네임스페이스 서버 추가](add-namespace-servers-to-a-domain-based-dfs-namespace.md)
-   네임 스페이스에 폴더를 추가 합니다. [DFS 네임스페이스에 폴더 만들기](create-a-folder-in-a-dfs-namespace.md)
-   폴더 대상을 네임 스페이스의 폴더에 추가 합니다. [폴더 대상 추가](add-folder-targets.md)
-   DFS 복제를 사용 하 여 폴더 대상 간에 콘텐츠를 복제 합니다 (선택 사항). [DFS 복제를 사용 하 여 폴더 대상 복제](replicate-folder-targets-using-dfs-replication.md)


## <a name="additional-references"></a>추가 참조

-   [네임스페이스](https://technet.microsoft.com/library/cc771914(v=ws.11).aspx)
-   [검사 목록: DFS 네임스페이스 튜닝](checklist-tune-a-dfs-namespace.md)
-   [복제](https://technet.microsoft.com/library/cc770278(v=ws.11).aspx)


