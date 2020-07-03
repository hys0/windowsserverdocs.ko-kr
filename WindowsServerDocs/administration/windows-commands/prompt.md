---
title: prompt
description: Cmd.exe 명령 프롬프트를 사용자 지정 하는 prompt 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3d98e965-02eb-46ad-9d0a-5dc44830373e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 72ed82c316faddba9486649497c8c48f88e6da81
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931141"
---
# <a name="prompt"></a>prompt

Cmd.exe 명령 프롬프트를 변경 합니다. 예를 들어 현재 디렉터리 이름, 시간 및 날짜, Microsoft Windows 버전 번호 등 원하는 텍스트를 표시할 수 있습니다. 매개 변수 없이 사용 하는 경우이 명령은 명령 프롬프트를 기본 설정으로 다시 설정 합니다 .이 설정에는 현재 드라이브 문자와 디렉터리 뒤에 보다 큼 기호 ()가 나옵니다 **>** .

## <a name="syntax"></a>구문

```
prompt [<text>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|--|--|
| `<text>` | 텍스트 및 명령 프롬프트에 포함 하려는 정보를 지정 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- *텍스트* 매개 변수에서 하나 이상의 문자열 대신 포함할 수 있는 문자 조합입니다.

    | 문자 | 설명 |
    |--|--|
    | $q | = (등호) |
    | $$ | $ (달러 기호) |
    | $t | 현재 시간 |
    | $d | 현재 날짜 |
    | $p | 현재 드라이브 및 경로 |
    | $v | Windows 버전 번호 |
    | $n | 현재 드라이브 |
    | $g | > (보다 큼 기호) |
    | $l | < (보다 작음 부호) |
    | $b | `|`(파이프 기호) |
    | $_ | 입력 줄 바꿈 |
    | $e | ANSI 이스케이프 코드 (27) |
    | $h | 백스페이스 (명령줄에 작성 된 문자) |
    | $는 | & (앰퍼샌드) |
    | $c | ((왼쪽 괄호) |
    | $f | ) (오른쪽 괄호) |
    | $s | Space |

- 명령 확장을 사용 하는 경우 **프롬프트** 명령은 다음과 같은 형식 지정 문자를 지원 합니다.

    | 문자 | 설명 |
    |--|--|
    | $+ | Pushd 디렉터리 스택의 깊이에 따라 0 개 이상의 더하기 기호 ( **+** ) 문자 ( **pushd** 푸시되는 각 수준에 대 한 문자 하나) |
    | $m | 현재 드라이브를 네트워크 드라이브로 없는 경우 현재 드라이브 문자 또는 빈 문자열와 연결 된 원격 이름입니다. |

- 포함 하는 경우는 **$p** 문자 텍스트 매개 변수에서 디스크를 각 명령 (현재 드라이브와 경로 결정)를 입력 한 후 읽습니다. 이 특히 플로피 디스크 드라이브에 대 한 시간이 걸릴 수 있습니다.

### <a name="examples"></a>예

첫 번째 줄 및 보다 큼 다음 줄에서 기호에 현재 날짜 및 시간으로 두 줄 명령 프롬프트를 설정 하려면 다음을 입력 합니다.

```
prompt $d$s$s$t$_$g
```

프롬프트는 날짜와 시간을 현재 다음과 같이 변경 합니다.

```
Fri 06/01/2007  13:53:28.91
```

화살표를 표시 하려면 명령 프롬프트를 설정 하려면 (`-->`), 유형:

```
prompt --$g
```

명령 프롬프트를 기본 설정 (현재 드라이브 및 경로 보다 큼 기호)를 수동으로 변경 하려면 다음을 입력 합니다.

```
prompt $p$g
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
