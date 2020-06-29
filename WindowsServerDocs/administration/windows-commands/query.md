---
title: Query
description: 프로세스, 세션 및 원격 데스크톱 세션 호스트 서버에 대 한 정보를 표시 하는 쿼리 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 675c5128-f3cf-4e8f-8a3f-b29ab2a8b6de
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ba5785fb37821848f98383da5b972333dfc8a9cc
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85471938"
---
# <a name="query"></a>Query

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

프로세스, 세션 및 원격 데스크톱 세션 호스트 서버에 대 한 정보를 표시 합니다. 최신 버전의 새로운 기능을 확인 하려면 [Windows Server에서 원격 데스크톱 서비스의 새로운 기능](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn283323(v=ws.11))을 참조 하세요.

## <a name="syntax"></a>구문

```
query process
query session
query termserver
query user
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|--|--|
| [query process](query-process.md) | 원격 데스크톱 세션 호스트 서버에서 실행 중인 프로세스에 대 한 정보를 표시 합니다. |
| [query session](query-session.md) | 원격 데스크톱 세션 호스트 서버에서 세션에 대 한 정보를 표시 합니다. |
| [query termserver](query-termserver.md) | 네트워크에 있는 모든 원격 데스크톱 세션 호스트 서버 목록을 표시 합니다. |
| [query user](query-user.md) | 원격 데스크톱 세션 호스트 서버의 사용자 세션에 대 한 정보를 표시 합니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [원격 데스크톱 서비스(터미널 서비스) 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
