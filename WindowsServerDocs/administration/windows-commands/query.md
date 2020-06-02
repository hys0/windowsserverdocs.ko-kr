---
title: Query
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 675c5128-f3cf-4e8f-8a3f-b29ab2a8b6de
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1dcea0fa4ea91de56e81c51bf9fe87ec7e3a49fa
ms.sourcegitcommit: 4894649cc47dfa535306cc334871f81155198f76
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/01/2020
ms.locfileid: "84254716"
---
# <a name="query"></a>Query

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

프로세스, 세션 및 원격 데스크톱 세션 호스트 (RD 세션 호스트) 서버에 대 한 정보를 표시합니다.

> [!NOTE]
> Windows Server 2008 R2에서는 터미널 서비스의 이름이 원격 데스크톱 서비스로 바뀌었습니다. 최신 버전의 새로운 기능에 대 한 자세한 내용은 windows server 라이브러리 Microsoft Docs에서 [원격 데스크톱 서비스의 새로운 기능](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn283323(v=ws.11)) 을 참조 하십시오.

## <a name="syntax"></a>구문

```
query process
query session
query termserver
query user
```

### <a name="parameters"></a>매개 변수

|매개 변수|Description|
|-------|--------|
|[쿼리 프로세스](query-process.md)|Rd 세션 호스트 서버에서 실행 중인 프로세스에 대 한 정보를 표시 합니다.|
|[세션 쿼리](query-session.md)|Rd 세션 호스트 서버에서 세션에 대 한 정보를 표시 합니다.|
|[termserver 쿼리](query-termserver.md)|네트워크에 있는 모든 rd 세션 호스트 서버 목록을 표시 합니다.|
|[사용자 쿼리](query-user.md)|Rd 세션 호스트 서버에서 사용자 세션에 대 한 정보를 표시 합니다.|

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
- [원격 데스크톱 서비스(터미널 서비스) 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
