---
title: quser
description: 원격 데스크톱 세션 호스트 서버의 사용자 세션에 대 한 정보를 표시 하는 quser 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8056204f-ed11-4c91-bb1d-c799283a48a4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e51abe030ca0f473246cdc85fd01d89fddf8b056
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85471928"
---
# <a name="quser"></a>quser

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 데스크톱 세션 호스트 서버의 사용자 세션에 대 한 정보를 표시 합니다. 특정 사용자가 특정 원격 데스크톱 세션 호스트 서버에 로그온 했는지 여부를 확인 하려면이 명령을 사용할 수 있습니다. 이 명령은 다음 정보를 반환합니다.

- 사용자의 이름

- 원격 데스크톱 세션 호스트 서버의 세션 이름

- 세션 ID

- 세션의 상태 (활성 또는 연결 끊김)

- 유휴 시간 (세션에서 마지막 키 입력 또는 마우스 이동 이후 경과 된 시간 (분))

- 사용자가 로그온 한 날짜 및 시간

> [!NOTE]
> 이 명령은 [쿼리 사용자 명령과](query-user.md)동일 합니다. 최신 버전의 새로운 기능을 확인 하려면 [Windows Server에서 원격 데스크톱 서비스의 새로운 기능](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn283323(v=ws.11))을 참조 하세요.

## <a name="syntax"></a>구문

```
quser [<username> | <sessionname> | <sessionID>] [/server:<servername>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|--|--|
| `<username>` | 쿼리 하려는 사용자의 로그온 이름을 지정 합니다. |
| `<sessionname>` | 쿼리 하려는 세션의 이름을 지정 합니다. |
| `<sessionID>` | 쿼리 하려는 세션의 ID를 지정 합니다. |
| /server:`<servername>` | 쿼리 하려는 원격 데스크톱 세션 호스트 서버를 지정 합니다. 그렇지 않으면 현재 원격 데스크톱 세션 호스트 서버가 사용 됩니다. 이 매개 변수는 원격 서버에서이 명령을 사용 하는 경우에만 필요 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- 이 명령을 사용 하려면 모든 권한 또는 특별 한 액세스 권한이 있어야 합니다.

- <*username*>, <*세션 이름*> 또는 *sessionID* 매개 변수를 사용 하 여 사용자를 지정 하지 않으면 서버에 로그온 한 모든 사용자의 목록이 반환 됩니다. 또는 **쿼리 세션** 명령을 사용 하 여 서버에 있는 모든 세션의 목록을 표시할 수도 있습니다.

- **Quser** 가 정보를 반환 하면 보다 큼 `(>)` 기호가 현재 세션 앞에 표시 됩니다.

### <a name="examples"></a>예제

시스템에 로그온 한 모든 사용자에 대 한 정보를 표시 하려면 다음을 입력 합니다.

```
quser
```

서버 *Server1*의 사용자 *USER1* 에 대 한 정보를 표시 하려면 다음을 입력 합니다.

```
quser USER1 /server:Server1
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [사용자 쿼리 명령](query-user.md)

- [원격 데스크톱 서비스(터미널 서비스) 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
