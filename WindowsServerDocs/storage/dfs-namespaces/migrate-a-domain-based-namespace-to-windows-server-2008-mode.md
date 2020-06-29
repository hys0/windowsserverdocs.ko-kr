---
title: 도메인 기반 네임스페이스를 Windows Server 2008 모드로 마이그레이션
description: 이 문서에서는 도메인 기반 네임 스페이스를 Windows Server 2008 모드로 마이그레이션하는 방법에 대해 설명 합니다.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 3aa7743773a8a6e9ed22c0f626c2c6a0dbafce56
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475470"
---
# <a name="migrate-a-domain-based-namespace-to-windows-server-2008-mode"></a>도메인 기반 네임 스페이스를 Windows Server 2008 모드로 마이그레이션

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

도메인 기반 네임 스페이스에 대 한 Windows Server 2008 모드에는 액세스 기반 열거 및 향상 된 확장성에 대 한 지원이 포함 됩니다.

## <a name="to-migrate-a-domain-based-namespace-to-windows-server-2008-mode"></a>도메인 기반 네임 스페이스를 Windows Server 2008 모드로 마이그레이션하려면

Windows 2000 서버 모드에서 Windows Server 2008 모드로 도메인 기반 네임 스페이스를 마이그레이션하려면 네임 스페이스를 파일로 내보내고, 네임 스페이스를 삭제 하 고, Windows Server 2008 모드에서 네임 스페이스를 다시 만든 후 네임 스페이스 설정을 가져와야 합니다. 이렇게 하려면 다음 절차를 따르십시오.

1.  명령 프롬프트 창을 열고 다음 명령을 입력 하 여 네임 스페이스를 파일로 내보냅니다. 여기서 \\ \\ *도메인* \\ *네임 스페이스* 는 적절 한 도메인의 이름이 고, 네임 스페이스 및 *경로 \\ 파일* 이름은 내보낼 파일의 경로 및 파일 이름입니다.
     ```
     Dfsutil root export \\domain\namespace path\filename.xml
     ```
2.  \\ \\ *server* \\ 각 네임 스페이스 서버에 대 한 경로 (서버 *공유* )를 기록 합니다. Dfsutil에서 네임 스페이스 서버를 가져올 수 없기 때문에 네임 스페이스 서버를 다시 생성 된 네임 스페이스에 수동으로 추가 해야 합니다.
3.  DFS 관리에서 네임 스페이스를 마우스 오른쪽 단추로 클릭 한 다음 **삭제**를 클릭 하거나 명령 프롬프트에서 다음 명령을 입력 합니다. <br /> 여기서 \\ \\ *domain* \\ *namespace* 는 적절 한 도메인 및 네임 스페이스의 이름입니다.
     ```
     Dfsutil root remove \\domain\namespace
     ```
4.  DFS 관리에서 이름이 같은 네임 스페이스를 다시 만든 다음 Windows Server 2008 모드를 사용 하거나 명령 프롬프트에서 다음 명령을 입력 합니다. <br /> \\\\*서버* \\ *namespace* 는 네임 스페이스 루트에 대 한 적절 한 서버 및 공유의 이름입니다.
     ```
     Dfsutil root adddom \\server\namespace v2
     ```
5.  내보내기 파일에서 네임 스페이스를 가져오려면 명령 프롬프트에서 다음 명령을 입력 합니다. <br /> \\\\*도메인* \\ *namespace* 는 적절 한 도메인 및 네임 스페이스의 이름이 고 *경로 \\ filename* 은 가져올 파일의 경로 및 파일 이름입니다.
     ```
     Dfsutil root import merge path\filename.xml \\domain\namespace
     ```

    > [!NOTE]
    > 많은 네임 스페이스를 가져오는 데 필요한 시간을 최소화 하려면 네임 스페이스 서버에서 **Dfsutil** root import 명령을 로컬로 실행 합니다.
6.  DFS 관리에서 네임 스페이스를 마우스 오른쪽 단추로 클릭 한 다음 **네임 스페이스 서버 추가**를 클릭 하거나 명령 프롬프트에서 다음 명령을 입력 하 여 다시 생성 된 네임 스페이스에 나머지 네임 스페이스 서버를 추가 합니다. <br /> \\\\*서버* \\ *share* 는 네임 스페이스 루트에 대 한 적절 한 서버 및 공유의 이름입니다.
     ```
     Dfsutil target add \\server\share
     ```

    > [!NOTE]
    > 네임 스페이스를 가져오기 전에 네임 스페이스 서버를 추가할 수 있지만 이렇게 하면 네임 스페이스 서버가 네임 스페이스 서버로 추가 된 후에 전체 네임 스페이스를 즉시 다운로드 하는 대신 네임 스페이스에 대 한 메타 데이터를 증분 다운로드 합니다.

## <a name="additional-references"></a>추가 참조
-   [DFS 네임스페이스 배포](deploying-dfs-namespaces.md)
-   [네임스페이스 형식 선택](choose-a-namespace-type.md)