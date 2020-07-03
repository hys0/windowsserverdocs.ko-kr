---
title: 로그오프
description: 원격 데스크톱 세션 호스트 서버의 세션에서 사용자를 로그 오프 하 고 세션을 삭제 하는 logoff 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 939f09cc-de8c-436c-a05d-aca5f2a06371
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d154b767302f5c536e0a7efb30d99ac0a8e087d5
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927161"
---
# <a name="logoff"></a>로그오프

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 데스크톱 세션 호스트 서버의 세션에서 사용자를 로그 오프 하 고 세션을 삭제 합니다.

## <a name="syntax"></a>구문
```
logoff [<sessionname> | <sessionID>] [/server:<servername>] [/v]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<sessionname>` | 세션의 이름을 지정합니다. 활성 세션 이어야 합니다.|
| `<sessionID>` | 서버에 세션을 식별 하는 숫자 ID를 지정 합니다. |
| /server:`<servername>` | 로그 오프 하려는 사용자의 세션을 포함 하는 원격 데스크톱 세션 호스트 서버를 지정 합니다. 지정 하지 않으면 현재 활성화 되어 있는 서버에 사용 됩니다. |
| /v | 수행 중인 작업에 대 한 정보를 표시 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- 현재 로그온 한 세션에서 항상 로그 오프 할 수 있습니다. 그러나 다른 세션에서 사용자를 로그 오프 하려면 **모든** 권한이 있어야 합니다.

- 경고 없이 세션에서 사용자를 로그 오프 사용자의 세션에서 데이터의 손실 될 수 있습니다. 사용 하 여 사용자에 게 메시지를 전송 해야는 **msg** 이 작업을 수행 하기 전에 경고를 표시 하는 명령입니다.

- `<sessionID>`또는 `<sessionname>` 를 지정 하지 않으면 **logoff** 현재 세션에서 사용자가 로그 오프 됩니다.

- 사용자를 로그 오프 하면 모든 프로세스가 종료 되 고 세션이 서버에서 삭제 됩니다.

- 콘솔 세션에서 사용자를 로그 오프 할 수는 없습니다.

### <a name="examples"></a>예

현재 세션에서 사용자를 기록 하려면 다음을 입력 합니다.

```
logoff
```

세션의 ID (예: 세션 *12*)를 사용 하 여 세션에서 사용자를 로그 오프 하려면 다음을 입력 합니다.

```
logoff 12
```

세션 및 서버의 이름 (예: *Server1*의 session *TERM04* )을 사용 하 여 세션에서 사용자를 로그 오프 하려면 다음을 입력 합니다.

```
logoff TERM04 /server:Server1
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [원격 데스크톱 서비스(터미널 서비스) 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
