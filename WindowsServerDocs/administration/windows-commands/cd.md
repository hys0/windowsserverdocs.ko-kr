---
title: CD
description: Cd 명령에 대 한 참조 항목으로, 이름을 표시 하거나 현재 디렉터리를 변경 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 932d9cc1-3dff-40da-835c-1cb0894874f1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7c9ee57590cf165ba46f394cab06817c7c13f0a9
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719654"
---
# <a name="cd"></a>CD

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

현재 디렉터리의 이름을 표시 하거나 현재 디렉터리를 변경 합니다. 드라이브 문자로 사용 하는 경우 (예를 들어 `cd C:`), **cd** 지정된 된 드라이브의 현재 디렉터리의 이름을 표시 합니다. 매개 변수 없이 사용 하는 경우 **cd** 디렉터리와 현재 드라이브를 표시 합니다.

> [!NOTE]
> 이 명령은 [chdir 명령과](chdir.md)같습니다.

## <a name="syntax"></a>구문

```
cd [/d] [<drive>:][<path>]
cd [..]
chdir [/d] [<drive>:][<path>]
chdir [..]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| /d | 드라이브에 대 한 현재 디렉터리와 현재 드라이브를 변경합니다. |
| `<drive>:` | 표시 하거나 (다른 경우 현재 드라이브)를 변경 하려면 드라이브를 지정 합니다. |
| `<path>` | 표시 하거나 변경 하려는 디렉터리의 경로를 지정 합니다. |
| [..] | 상위 폴더를 변경 하려면 지정 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="remarks"></a>설명

다음과 같은 명령 확장을 사용 하는 경우에 적용 된 **cd** 명령:

- 디스크의 이름으로는 대/소문자를 사용 하 여 현재 디렉터리 문자열 변환 됩니다. 예를 들어 `cd c:\temp` 되어 디스크의 경우에는 현재 디렉터리를 C:\Temp로 설정 합니다.

- 공백은 구분 기호로 처리 되지 않으므로 `<path>` 따옴표 없이 공백을 포함할 수 있습니다. 다음은 그 예입니다. 

  ```
  cd username\programs\start menu
  ```

  이 코드는 다음과 같습니다.  
  
  ```
  cd "username\programs\start menu"
  ```

  확장을 사용 하지 않도록 설정한 경우에는 따옴표가 필요 합니다.

- 명령 확장을 사용 하지 않으려면 다음을 입력 합니다.

  ```
  cmd /e:off
  ```

## <a name="examples"></a>예

루트 디렉터리로 돌아가려면 드라이브의 디렉터리 계층 구조 맨 위:

```
cd\
```

사용자가 있는 것과 다른 드라이브의 기본 디렉터리를 변경 하려면 다음을 수행 합니다.

```
cd [<drive>:[<directory>]]
```

디렉터리 변경을 확인 하려면 다음을 입력 합니다.

```
cd [<drive>:]
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [chdir 명령](chdir.md)
