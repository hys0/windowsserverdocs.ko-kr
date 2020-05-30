---
title: manage-bde wipefreespace
description: Manage-bde wipefreespace command에 대 한 참조 항목으로, 공간에 있을 수 있는 데이터 조각을 제거 하는 볼륨의 사용 가능한 공간을 제거 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b8d83a2a-c5c8-4019-9041-23d1d6abf282
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 09bc59ab631dd1fa2177b50aa4187b30239571bd
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222130"
---
# <a name="manage-bde-wipefreespace"></a>manage-bde wipefreespace

볼륨의 사용 가능한 공간을 초기화 하 여 공간에 존재 했을 수 있는 모든 데이터 조각을 제거 합니다. **사용 된 공간만** 암호화 방법을 사용 하 여 암호화 된 볼륨에서이 명령을 실행 하면 **전체 볼륨 암호화** 암호화 방법과 동일한 수준의 보호 기능이 제공 됩니다.

## <a name="syntax"></a>구문

```
manage-bde -wipefreespace|-w [<drive>] [-cancel] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<drive>` | 드라이브 문자를 뒤에 콜론을 나타냅니다. |
| -취소 | 프로세스에 있는 빈 공간의 초기화를 취소 합니다. |
| -computername | 다른 컴퓨터에서 BitLocker 보호를 수정 하는 데 manage-bde.exe를 사용 하도록 지정 합니다. 사용할 수도 있습니다 **-cn** 이 명령의 축약된 버전으로 합니다. |
| `<name>` | BitLocker 보호를 수정할 수 있는 컴퓨터의 이름을 나타냅니다. 사용 가능한 값에는 컴퓨터의 NetBIOS 이름 및 컴퓨터의 IP 주소 포함 됩니다. |
| -? 또는 /? | 도움말에 대 한 간단한 명령 프롬프트에 표시 됩니다. |
| -help 또는-h | 명령 프롬프트에서 전체 도움말을 표시 합니다. |

### <a name="examples"></a>예

C 드라이브의 사용 가능한 공간을 초기화 하려면 다음을 입력 합니다.

```
manage-bde -w C:
```

```
manage-bde -wipefreespace C:
```

C 드라이브에서 사용 가능한 공간의 초기화를 취소 하려면 다음을 입력 합니다.

```
manage-bde -w -cancel C:
```

```
manage-bde -wipefreespace -cancel C:
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [manage-bde 명령](manage-bde.md)
