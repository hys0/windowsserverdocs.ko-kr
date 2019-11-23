---
title: Windows Server 2008 모드로 도메인 기반 네임스페이스 마이그레이션
description: 이 문서에서는 Windows Server 2008 모드로 도메인 기반 네임스페이스 마이그레이션하는 방법을 설명합니다.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 75e366d6b72e9f08ece77558cff253239474777c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386213"
---
# <a name="migrate-a-domain-based-namespace-to-windows-server-2008-mode"></a>Windows Server 2008 모드로 도메인 기반 네임스페이스 마이그레이션

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

도메인 기반 네임스페이스에 대한 Windows Server 2008 모드에는 액세스 기반 열거와 향상된 확장성 지원이 포함됩니다.

## <a name="to-migrate-a-domain-based-namespace-to-windows-server-2008-mode"></a>Windows Server 2008 모드로 도메인 기반 네임스페이스를 마이그레이션하려면

Windows 2000 Server 모드에서 Windows Server 2008 모드로 도메인 기반 네임스페이스를 마이그레이션하려면 파일로 네임스페이스를 내보내고, 네임스페이스를 삭제하고, Windows Server 2008 모드에서 네임스페이스를 다시 만든 다음, 네임스페이스 설정을 가져옵니다. 그렇게 하려면 다음 절차를 따르세요.

1.  명령 프롬프트 창을 열고 다음 명령을 입력 하 여 네임 스페이스를 파일로 내보냅니다. 여기서 \\\\*도메인*\\*네임 스페이스* 는 적절 한 도메인의 이름이 고, 네임 스페이스 및 *경로\\filename* 은 내보낼 파일의 경로 및 파일 이름입니다.
     ```
     Dfsutil root export \\domain\namespace path\filename.xml 
     ```
2.  각 네임 스페이스 서버에 대 한 경로 (\\\\*서버* \\*공유* )를 기록 합니다. Dfsutil은 네임스페이스 서버를 가져올 수 없기 때문에 다시 만든 네임스페이스에 네임스페이스 서버를 직접 추가해야 합니다.
3.  DFS 관리에서 네임스페이스를 마우스 오른쪽 단추로 클릭하고 **삭제**를 클릭하거나 명령 프롬프트에서 다음 명령을 입력합니다. <br /> 여기서 \\\\*도메인*\\*네임 스페이스* 는 적절 한 도메인 및 네임 스페이스의 이름입니다.
     ```
     Dfsutil root remove \\domain\namespace
     ```
4.  DFS 관리에서 동일한 이름의 네임스페이스를 다시 만듭니다. 그러나 Windows Server 2008 모드를 사용하거나 명령 프롬프트에서 다음 명령을 입력합니다. <br /> \\\\*server*\\*네임 스페이스* 는 네임 스페이스 루트에 대 한 적절 한 서버 및 공유의 이름입니다.
     ```
     Dfsutil root adddom \\server\namespace v2
     ```
5.  내보내기 파일에서 네임스페이스를 가져오려면 명령 프롬프트에서 다음 명령을 입력합니다. <br /> \\\\*도메인*\\*네임 스페이스* 는 적절 한 도메인의 이름과 네임 스페이스 및 *경로\\filename* 은 가져올 파일의 경로 및 파일 이름입니다.
     ```
     Dfsutil root import merge path\filename.xml \\domain\namespace
     ```

    > [!NOTE]
    > 큰 네임스페이스를 가져오는 데 필요한 시간을 최소화하려면 네임스페이스 서버에서 로컬로 **Dfsutil** 루트 가져오기 명령을 실행합니다.
6.  DFS 관리에서 네임스페이스를 마우스 오른쪽 단추로 클릭하고 **네임스페이스 서버 추가**를 클릭하거나, 명령 프롬프트에서 다음 명령을 입력하여 남은 네임스페이스 서버를 다시 만든 네임스페이스에 추가합니다. <br /> \\\\*서버*\\*공유* 는 네임 스페이스 루트에 대 한 적절 한 서버 및 공유의 이름입니다.
     ```
     Dfsutil target add \\server\share 
     ```

    > [!NOTE]
    > 네임스페이스를 가져오기 전에 네임스페이스 서버를 추가할 수 있지만 그렇게 하면 네임스페이스 서버로 추가된 직후 전체 네임스페이스를 다운로드하는 대신 네임스페이스 서버가 네임스페이스에 대한 메타데이터를 증분 다운로드합니다.

## <a name="see-also"></a>참고 항목
-   [DFS 네임스페이스 배포](deploying-dfs-namespaces.md)
-   [네임스페이스 형식 선택](choose-a-namespace-type.md)