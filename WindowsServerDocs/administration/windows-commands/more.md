---
title: 시각화
description: 한 번에 하나의 출력 화면을 표시 하는 more 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ded14f6a-d82f-4aeb-a2d8-7ec1c94dfb8f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/26/2019
ms.openlocfilehash: fec0ffbd7f2ce5d1efe1953cb4ab283d33f06ec8
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935735"
---
# <a name="more"></a>시각화

한 번에 한 화면씩 출력을 표시합니다.

> [!NOTE]
> 다른 매개 변수를 사용 하는 **더 많은** 명령을 복구 콘솔에서 사용할 수도 있습니다.

## <a name="syntax"></a>구문

```
<command> | more [/c] [/p] [/s] [/t<n>] [+<n>]
more [[/c] [/p] [/s] [/t<n>] [+<n>]] < [<drive>:][<path>]<filename>
more [/c] [/p] [/s] [/t<n>] [+<n>] [<files>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<command>` | 출력을 표시 하려는 명령을 지정 합니다. |
| /C | 페이지를 표시 하기 전에 화면을 지웁니다. |
| /p | 용지 공급 문자를 확장 합니다. |
| /s | 비어 있는 단일 선으로 여러 개의 빈 줄을 표시합니다. |
| /t`<n>` | 탭을 *n*으로 지정 된 공백 수로 표시 합니다. |
| +`<n>` | *N*에 지정 된 줄에서 시작 하 여 첫 번째 파일을 표시 합니다. |
| `[<drive>:][<path>]<filename>` | 표시할 파일의 이름과 위치를 지정 합니다. |
| `<files>` | 표시할 파일의 목록을 지정 합니다. 파일은 공백을 사용 하 여 구분 해야 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- 다음 하위 명령은 다음을 포함 하 여 **더 많은** 프롬프트 ()에서 허용 됩니다 `-- More --` .

    | 키 | 작업 |
    | --- | ------ |
    | 스페이스바 | **스페이스바** 를 눌러 다음 화면을 표시 합니다. |
    | Enter 키 | **Enter** 키를 눌러 파일을 한 번에 한 줄씩 표시 합니다. |
    | f | **F** 를 눌러 명령줄에 나열 된 다음 파일을 표시 합니다. |
    | q | **Q** 키를 눌러 **더 많은** 명령을 종료 합니다. |
    | = | 줄 번호를 보여 줍니다. |
    | ®`<n>` | **P** 키를 눌러 다음 *n* 줄을 표시 합니다. |
    | 삭제`<n>` | 다음 *n* 줄을 건너뛰려면 **S** 를 누릅니다. |
    | ? | 키 **를** 누르세요. **추가** 프롬프트에서 사용할 수 있는 명령을 표시 합니다.|

- 리디렉션 문자 ()를 사용 하는 경우에는 `<` 파일 이름도 원본으로 지정 해야 합니다.

- 파이프 ()를 사용 하는 경우 `|` **dir**, **sort**및 **type**과 같은 명령을 사용할 수 있습니다.

### <a name="examples"></a>예

이름이 *Clients*인 파일의 첫 번째 화면 정보를 보려면 다음 명령 중 하나를 입력 합니다.

```
more < clients.new
type clients.new | more
```

**추가** 명령은 클라이언트의 첫 번째 정보 화면을 표시 하 고, 스페이스바를 눌러 다음 정보 화면을 볼 수 있습니다.

화면을 지우고 파일 *클라이언트*를 표시 하기 전에 빈 줄을 모두 제거 하려면 다음 명령 중 하나를 입력 합니다.

```
more /c /s < clients.new
type clients.new | more /c /s
```

**자세히** 프롬프트에서 현재 줄 번호를 표시 하려면 다음을 입력 합니다.

```
more =
```

현재 줄 번호는와 같이 **더 많은** 프롬프트에 추가 됩니다.`-- More [Line: 24] --`

**더 많은** 프롬프트에서 특정 줄 수를 표시 하려면 다음을 입력 합니다.

```
more p
```

**더 많은** 프롬프트가 표시 되 면 다음과 같이 표시할 줄 수를 묻는 메시지가 표시 `-- More -- Lines:` 됩니다. 표시할 줄 번호를 입력 하 고 enter 키를 누릅니다. 화면은 해당 줄 수만 표시 하도록 변경 됩니다.

**프롬프트에서** 특정 줄 수를 건너뛰려면 다음과 같이 입력 합니다.

```
more s
```

**더 많은** 프롬프트가 표시 되 면 다음과 같이 건너뛸 줄 수를 묻는 메시지가 표시 `-- More -- Lines:` 됩니다. 건너뛸, 줄 번호를 입력 하 고 enter 키를 누릅니다. 화면은 해당 줄을 건너뛰도록 표시 하도록 변경 됩니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [Windows 복구 환경 (WinRE)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference)
