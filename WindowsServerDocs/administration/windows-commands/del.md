---
title: del
description: 하나 이상의 파일을 삭제 하는 del 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 346eede2-2085-44f5-9936-6877b5d5a833
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f32efd6e29a715cdc67b5a1ddcb166922d1cfcc9
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2020
ms.locfileid: "82993133"
---
# <a name="del"></a>del

하나 이상의 파일을 삭제합니다. 이 명령은 **erase** 명령과 동일한 작업을 수행 합니다.

**Del** 명령은 Windows 복구 콘솔에서 다른 매개 변수를 사용 하 여 실행할 수도 있습니다. 자세한 내용은 [WinRE (Windows 복구 환경)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference)를 참조 하세요.

> [!WARNING]
> **Del** 을 사용 하 여 디스크에서 파일을 삭제 하면 해당 파일을 검색할 수 없습니다.

## <a name="syntax"></a>구문

```
del [/p] [/f] [/s] [/q] [/a[:]<attributes>] <names>
erase [/p] [/f] [/s] [/q] [/a[:]<attributes>] <names>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| --------- | ----------- |
| `<names>` | 하나 이상의 파일 또는 디렉터리 목록을 지정합니다. 여러 파일을 삭제 하려면 와일드 카드를 사용할 수 있습니다. 디렉터리를 지정 하는 경우 디렉터리 내의 모든 파일이 삭제 됩니다. |
| /p | 지정된 된 파일을 삭제 하기 전에 확인 메시지를 표시 합니다. |
| /f | 읽기 전용 파일을 강제로 삭제 합니다. |
| /s | 지정 된 현재 디렉터리와 모든 하위 디렉터리에서 파일을 삭제 합니다. 삭제 될 파일의 이름을 표시 됩니다. |
| /q | 자동 모드를 지정합니다. 삭제 확인 필요 하지 않습니다. |
| /a [:]`<attributes>` | 다음과 같은 파일 특성에 따라 파일을 삭제 합니다.<ul><li>**r** 읽기 전용 파일</li><li>**h** 숨김 파일</li><li>**i** 하지 인덱싱된 파일의 내용</li><li>**s** 시스템 파일</li><li>**** 기록 파일</li><li>**l** 재분석 지점</li><li>**-** 접두사로 사용 됩니다 (' not ' 의미).</li></ul>. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- 명령을 사용 하는 `del /p` 경우 다음과 같은 메시지가 표시 됩니다.

    `FileName, Delete (Y/N)?`

    삭제를 확인 하려면 **Y**를 누릅니다. 삭제를 취소 하 고 파일 그룹을 지정한 경우 다음 파일 이름을 표시 하려면 **N**을 누릅니다. **Del** 명령을 중지 하려면 Ctrl + C를 누릅니다.

- 명령 확장을 사용 하지 않도록 설정 하면 삭제 되는 파일의 이름을 표시 하는 대신 **/s** 매개 변수를 통해 찾지 못한 파일의 이름이 표시 됩니다.

- `<names>` 매개 변수에 특정 폴더를 지정 하면 포함 된 파일도 모두 삭제 됩니다. 예를 들어 *\work* 폴더의 모든 파일을 삭제 하려면 다음을 입력 합니다.

  ```
  del \work
  ```

- 와일드 카드 (**&#42;** 및 **?**)를 사용 하 여 한 번에 두 개 이상의 파일을 삭제할 수 있습니다. 그러나 실수로 파일을 삭제 하지 않으려면 와일드 카드를 사용 해야 합니다. 예를 들어, 다음 명령을 입력 합니다.

  ```
  del *.*
  ```

  **Del** 명령은 다음 프롬프트를 표시 합니다.

  `Are you sure (Y/N)?`

  현재 디렉터리에 있는 모든 파일을 삭제 하려면 **Y** 를 누르고 enter 키를 누릅니다. 삭제를 취소 하려면 **N** 을 누르고 enter 키를 누릅니다.

  > [!NOTE]
  > 와일드 카드 문자를 사용 하기 전에 **del** 명령와 같은 와일드 카드 문자를 사용 하 여는 **dir** 명령을 삭제 하 여 모든 파일을 나열 합니다.

## <a name="examples"></a>예

C 드라이브에 Test 라는 폴더에 있는 모든 파일을 삭제 하려면 다음 중 하나를 입력 합니다.

```
del c:\test
del c:\test\*.*
```

현재 디렉터리에서.bat 파일 이름 확장명을 사용 하 여 모든 파일을 삭제 하려면 다음을 입력 합니다.

```
del *.bat
```

현재 디렉터리의 모든 읽기 전용 파일을 삭제 하려면 다음을 입력 합니다.

```
del /a:r *.*
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [Windows 복구 환경 (WinRE)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference)
