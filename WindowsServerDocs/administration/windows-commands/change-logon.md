---
title: change logon
description: 클라이언트 세션에서 로그온을 사용 하거나 사용 하지 않도록 설정 하거나 현재 로그온 상태를 표시 하는 변경 로그온 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 41466260-aee9-4333-bcb6-178112c22afd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4a2ebe75f6efa8c3bcfc0018d1f4e6051bb9ebb7
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82716128"
---
# <a name="change-logon"></a>change logon

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

또는 클라이언트 세션에서 로그온을 사용 하지 않도록 설정 하거나 현재 로그온 상태를 표시 합니다. 이 유틸리티는 시스템 유지 관리에 유용 합니다. 이 명령을 실행 하려면 관리자 여야 합니다.

> [!NOTE]
> Windows Server 2008 R2에서는 터미널 서비스의 이름이 원격 데스크톱 서비스로 바뀌었습니다. 최신 버전의 새로운 기능을 확인 하려면 [Windows Server에서 원격 데스크톱 서비스의 새로운 기능](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn283323(v=ws.11))을 참조 하세요.

## <a name="syntax"></a>구문

```
change logon {/query | /enable | /disable | /drain | /drainuntilrestart}
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| / 쿼리 | 사용 여부는 현재 로그온 상태를 표시 합니다. |
| 같습니다. | 콘솔에서가 아니라 하지만 클라이언트 세션에서 로그온 수 있습니다. |
| /disable | 이후에 로그온을 콘솔 있지만 클라이언트 세션에서 사용할 수 없습니다. 현재 로그온된 사용자가 영향을 주지 않습니다. |
| /drain | 새 클라이언트 세션에서 로그온 할 수 없게 하 하지만 기존 세션에 다시 연결을 허용 합니다. |
| /drainuntilrestart | 컴퓨터 다시 시작 되 면 기존 세션에 다시 연결을 허용 될 때까지 새 클라이언트 세션에서 로그온을 사용 하지 않도록 설정 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- 시스템 다시 시작 하는 경우에 다시 로그온이 설정 됩니다.

- 클라이언트 세션에서 원격 데스크톱 세션 호스트 서버에 연결 되어 있는 상태에서 로그온을 사용 하지 않도록 설정 하 고 로그 오프 한 후 로그온을 다시 사용 하도록 설정 하면 세션에 다시 연결할 수 없습니다. 클라이언트 세션에서 로그온을 다시 활성화 하려면 콘솔에 로그온 합니다.

### <a name="examples"></a>예

- 현재 로그온 상태를 표시 하려면 다음을 입력 합니다.
  
  ```
  change logon /query
  ```

- 클라이언트 세션에서 로그온을 사용 하려면 다음을 입력 합니다.

  ```
  change logon /enable
  ```

- 클라이언트 로그온을 사용 하지 않으려면 다음을 입력 합니다.

  ```
  change logon /disable
  ```
  
## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [명령 변경](change.md)

- [원격 데스크톱 서비스(터미널 서비스) 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
