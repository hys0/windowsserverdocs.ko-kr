---
title: query termserver
description: 네트워크에 있는 모든 원격 데스크톱 세션 호스트 서버 목록을 표시 하는 query termserver 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3b89d3b4-236f-4376-90b6-939a0ec4b288
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c41ed824ee0b1e9dc2672646ef0af03e2593ec07
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85471978"
---
# <a name="query-termserver"></a>query termserver

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

네트워크에 있는 모든 원격 데스크톱 세션 호스트 서버 목록을 표시 합니다. 이 명령은 네트워크에서 연결 된 모든 원격 데스크톱 세션 호스트 서버를 검색 하 고 다음 정보를 반환 합니다.

- 서버의 이름

- 네트워크 (및/주소 옵션을 사용 하는 경우 노드 주소)

> [!NOTE]
> 최신 버전의 새로운 기능을 확인 하려면 [Windows Server에서 원격 데스크톱 서비스의 새로운 기능](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn283323(v=ws.11))을 참조 하세요.

## <a name="syntax"></a>구문

```
query termserver [<servername>] [/domain:<domain>] [/address] [/continue]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|--|--|
| `<servername>` | 원격 데스크톱 세션 호스트 서버를 식별 하는 이름을 지정 합니다. |
| /domain`<domain>` | 터미널 서버를 쿼리 하는 도메인을 지정합니다. 현재 작업 중인 도메인을 쿼리 하는 경우에는 도메인을 지정할 필요가 없습니다. |
| / 주소 | 각 서버에 대 한 네트워크 및 노드 주소를 표시합니다. |
| 계속 해 서 / | 각 정보 화면에 표시 되 면 일시 중지를 방지 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

### <a name="examples"></a>예제

네트워크에 있는 모든 원격 데스크톱 세션 호스트 서버에 대 한 정보를 표시 하려면 다음을 입력 합니다.

```
query termserver
```

*Server3*라는 원격 데스크톱 세션 호스트 서버에 대 한 정보를 표시 하려면 다음을 입력 합니다.

```
query termserver Server3
```

*CONTOSO*도메인의 모든 원격 데스크톱 세션 호스트 서버에 대 한 정보를 표시 하려면 다음을 입력 합니다.

```
query termserver /domain:CONTOSO
```

*Server3*라는 원격 데스크톱 세션 호스트 서버에 대 한 네트워크 및 노드 주소를 표시 하려면 다음을 입력 합니다.

```
query termserver Server3 /address
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [쿼리 명령](query.md)

- [원격 데스크톱 서비스(터미널 서비스) 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
