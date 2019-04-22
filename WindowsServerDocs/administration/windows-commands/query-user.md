---
title: 쿼리 사용자에 게
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a670fb78-c055-464a-b61d-3a85632c52c5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6e54d1b9701cc2f3a4f229a3910d5b325fee87c6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813944"
---
# <a name="query-user"></a>쿼리 사용자에 게

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 데스크톱 세션 호스트 (rd 세션 호스트) 서버에서 사용자 세션에 대 한 정보를 표시합니다.
이 명령을 사용 하는 방법의 예제를 참조 하세요 [예제](#BKMK_examples)합니다.
> [!NOTE]
> Windows Server 2008 R2에서는 터미널 서비스의 이름이 원격 데스크톱 서비스로 바뀌었습니다. 최신 버전의 새로운 기능을 참조 하세요 [어떤 새로운 Windows Server 2012의 원격 데스크톱 서비스](https://technet.microsoft.com/library/hh831527) 는 Windows Server TechNet 라이브러리에서.
## <a name="syntax"></a>구문
```
query user [<UserName> | <SessionName> | <SessionID>] [/server:<ServerName>]
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|<UserName>|쿼리 하려는 사용자의 로그온 이름을 지정 합니다.|
|<SessionName>|쿼리 하려는 세션의 이름을 지정 합니다.|
|<SessionID>|쿼리 하려는 세션의 ID를 지정 합니다.|
|/server:<ServerName>|쿼리 하려는 rd 세션 호스트 서버를 지정 합니다. 그렇지 않으면 현재 rd 세션 호스트 서버에서 사용 됩니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|
## <a name="remarks"></a>설명
-   알아보려면 경우 특정 사용자가 로그온을 특정 rd 세션 호스트 서버에이 명령을 사용할 수 있습니다. **쿼리 사용자에 게** 다음 정보를 반환 합니다.
    -   사용자의 이름
    -   Rd 세션 호스트 서버에서 세션의 이름
    -   세션 ID
    -   (활성 또는 연결 끊기) 세션의 상태
    -   유휴 시간 (세션에서 마지막 키 입력 이나 마우스 이동 이후 분 수)
    -   사용자 로그온 날짜 및 시간
-   사용 하도록 **쿼리 사용자에 게**, 모든 권한 또는 쿼리 정보 특별 한 액세스 권한이 있어야 합니다.
-   사용 하는 경우 **쿼리 사용자에 게** 지정 하지 않고 <*UserName*>, <*SessionName*>, 또는 <*SessionID*>, 모든 목록을 서버에 로그온 하는 사용자가 반환 됩니다. 또는 사용할 수도 있습니다 **세션 쿼리** 서버에서 모든 세션의 목록을 표시 합니다.
-   때 **쿼리 사용자에 게** 정보를 반환, 보다 큼 (>) 기호는 현재 세션 앞에 표시 됩니다.
-   **/server** 매개 변수는 사용 하는 경우에 필요 **쿼리 사용자에 게** 원격 서버에서.
## <a name="BKMK_examples"></a>예제
-   시스템에 로그온 한 모든 사용자에 대 한 정보를 표시 하려면 다음을 입력 합니다.
    ```
    query user
    ```
-   서버 서버 1에서 user1 계정 사용자에 대 한 정보를 표시 하려면 다음을 입력 합니다.
    ```
    query user USER1 /server:SERver1
    ```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[쿼리의](query.md)
[Remote Desktop Services &#40;터미널&#41; 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
