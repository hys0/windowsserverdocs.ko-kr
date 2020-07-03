---
title: 쿼리 프로세스
description: 원격 데스크톱 세션 호스트 서버에서 실행 중인 프로세스에 대 한 정보를 표시 하는 쿼리 프로세스 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 36ce3ffc-0092-4eb1-a374-28e6616ca946
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a11177ad62e83efd9dbe5da844b159b40266837d
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936992"
---
# <a name="query-process"></a>쿼리 프로세스

적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 데스크톱 세션 호스트 서버에서 실행 중인 프로세스에 대 한 정보를 표시 합니다. 이 명령을 사용 하 여 특정 사용자를 실행 하는 프로그램을 찾으려면 및 또한 어떤 사용자가 특정 프로그램을 실행 합니다. 이 명령은 다음 정보를 반환합니다.

- 프로세스를 소유 하는 사용자

- 프로세스를 소유 하는 세션

- 세션의 ID입니다.

- 프로세스 이름

- 프로세스의 ID입니다.

> [!NOTE]
> 최신 버전의 새로운 기능을 확인 하려면 [Windows Server에서 원격 데스크톱 서비스의 새로운 기능](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn283323(v=ws.11))을 참조 하세요.

## <a name="syntax"></a>구문

```
query process [*|<processID>|<username>|<sessionname>|/id:<nn>|<programname>] [/server:<servername>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|--|--|
| * | 모든 세션에 대 한 프로세스를 나열합니다. |
| `<processID>` | 쿼리 하려는 프로세스를 식별 하는 숫자 ID를 지정 합니다. |
| `<username>` | 표시 하려는 프로세스의 사용자 이름을 지정 합니다. |
| `<sessionname>` | 나열할 프로세스가 포함 된 활성 세션의 이름을 지정 합니다. |
| 더불어`<nn>` | 표시 하려는 프로세스의 세션의 ID를 지정 합니다. |
| `<programname>` | 쿼리 하려는 프로세스의 프로그램의 이름을 지정 합니다. .Exe 확장명은 필수입니다. |
| /server:`<servername>` | 나열 하려는 프로세스의 원격 데스크톱 세션 호스트 서버를 지정 합니다. 지정 하지 않으면 서버에 현재 로그온이 사용 됩니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- 관리자 권한을 갖기 때문에 모든 **쿼리 프로세스** 함수입니다.

- <*username*>, <*세션 이름*>, */id `<nn>` :*, <*programname*> 또는 *&#42;* 매개 변수를 지정 하지 않으면이 쿼리는 현재 사용자에 속한 프로세스만 표시 합니다.

- **쿼리 프로세스** 에서 정보를 반환 하는 경우 `(>)` 현재 세션에 속하는 각 프로세스 앞에 보다 큼 기호가 표시 됩니다.

## <a name="examples"></a>예

모든 세션에서 사용 중인 프로세스에 대 한 정보를 표시 하려면 다음을 입력 합니다.

```
query process *
```

*세션 ID 2*에서 사용 중인 프로세스에 대 한 정보를 표시 하려면 다음을 입력 합니다.

```
query process /ID:2
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [쿼리 명령](query.md)

- [원격 데스크톱 서비스(터미널 서비스) 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
