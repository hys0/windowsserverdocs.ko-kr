---
title: qwinsta
description: Qwinsta 명령에 대 한 참조 항목으로, 원격 데스크톱 세션 호스트 서버에서 세션에 대 한 정보를 표시 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a793212a-7ecd-44cb-a77b-c5c2edb34979
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9122576cc0b972e01a7593fae918aed378297fc8
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85471878"
---
# <a name="qwinsta"></a>qwinsta

적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 데스크톱 세션 호스트 서버에서 세션에 대 한 정보를 표시 합니다. 목록에는 활성 세션에 대 한 뿐만 아니라 서버에서 실행 하는 다른 세션에 대 한 정보가 포함 됩니다.

> [!NOTE]
> 이 명령은 [query session 명령과](query-session.md)동일 합니다. 최신 버전의 새로운 기능을 확인 하려면 [Windows Server에서 원격 데스크톱 서비스의 새로운 기능](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn283323(v=ws.11))을 참조 하세요.

## <a name="syntax"></a>구문

```
qwinsta [<sessionname> | <username> | <sessionID>] [/server:<servername>] [/mode] [/flow] [/connect] [/counter]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|--|--|
| `<sessionname>` | 쿼리 하려는 세션의 이름을 지정 합니다. |
| `<username>` | 쿼리 하려는 세션이 사용자의 이름을 지정 합니다. |
| `<sessionID>` | 쿼리 하려는 세션의 ID를 지정 합니다. |
| /server:`<servername>` | 쿼리할 rd 세션 호스트 서버를 식별 합니다. 기본값은 현재 서버. |
| /mode | 현재 줄 설정을 표시합니다. |
| /flow | 현재 흐름 제어 설정을 표시합니다. |
| 연결 / | 현재의 연결 설정을 표시 합니다. |
| 카운터 / | 현재 카운터 정보를 표시, 만들어진 세션의 총 수를 포함 하 여 연결이 해제 및 다시 연결 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- 항상 사용자는 사용자가 현재 로그온 세션을 쿼리할 수 있습니다. 다른 세션을 쿼리하려면 사용자에 게 특별 한 액세스 권한이 있어야 합니다.

- <*username*>, <세션 *이름*> 또는 *sessionID* 매개 변수를 사용 하 여 세션을 지정 하지 않으면이 쿼리는 시스템의 모든 활성 세션에 대 한 정보를 표시 합니다.

- **Qwinsta** 가 정보를 반환 하는 경우 보다 큼 `(>)` 기호가 현재 세션 앞에 표시 됩니다. 예를 들면 다음과 같습니다.

    ```
    C:\>qwinsta
        SESSIONNAME     USERNAME        ID STATE    TYPE    DEVICE
        console         Administrator1  0 active    wdcon
        >rdp-tcp#1      User1           1 active    wdtshare
        rdp-tcp                         2 listen    wdtshare
                                        4 idle
                                        5 idle
    ```

    위치:
  - **세션 이름** 세션에 할당 된 이름을 지정 합니다.
  - **사용자 이름** 세션에 연결 된 사용자의 사용자 이름을 나타냅니다.
  - **상태** 는 세션의 현재 상태에 대 한 정보를 제공 합니다.
  - **유형** 은 세션 유형을 나타냅니다.
  - 콘솔 또는 네트워크에 연결 된 세션에 대해 존재 하지 않는 **장치**는 세션에 할당 된 장치 이름입니다.
  - 초기 상태가 사용 안 함으로 구성 된 세션은 사용 하도록 설정 될 때까지 **qwinsta** 목록에 표시 되지 않습니다.

### <a name="examples"></a>예제

*Server2*서버에서 모든 활성 세션에 대 한 정보를 표시 하려면 다음을 입력 합니다.

```
qwinsta /server:Server2
```

활성 세션 *modeM02*에 대 한 정보를 표시 하려면 다음을 입력 합니다.

```
qwinsta modeM02
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [쿼리 세션 명령](query-session.md)

- [원격 데스크톱 서비스(터미널 서비스) 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
