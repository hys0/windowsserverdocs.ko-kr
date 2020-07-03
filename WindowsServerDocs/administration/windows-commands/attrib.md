---
title: attrib
description: 파일 또는 디렉터리에 할당 된 특성을 표시, 설정 또는 제거 하는 attrib 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5e763ca5-21a2-45d2-b26d-a9c44c99091a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bc5d780ffd32976df306e2221987f24ec8553854
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923902"
---
# <a name="attrib"></a>attrib

표시 설정 하거나 파일 또는 디렉터리에 할당 된 특성을 제거 합니다. 매개 변수 없이 사용 하는 경우 **attrib** 현재 디렉터리에 있는 모든 파일의 속성을 표시 합니다.

## <a name="syntax"></a>구문

```
attrib [{+|-}r] [{+|-}a] [{+|-}s] [{+|-}h] [{+|-}i] [<drive>:][<path>][<filename>] [/s [/d] [/l]]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{+|-}r` | 집합 ( **+** )을 설정 하거나 취소 ( **-** ) 읽기 전용 파일 특성입니다. |
| `{+\|-}a` | 설정 ( **+** ) 하거나 취소 ( **-** ) 보관 파일 특성입니다. 이 특성 집합은 마지막으로 백업 된 이후에 변경 된 파일을 표시 합니다. **Xcopy** 명령은 보관 특성을 사용 합니다. |
| `{+\|-}s` | 설정 ( **+** ) 하거나 취소 ( **-** ) 시스템 파일 특성입니다. 파일이이 특성 집합을 사용 하는 경우에는 해당 파일에 대 한 다른 특성을 변경 하기 전에 특성을 지워야 합니다. |
| `{+\|-}h` | 집합 ( **+** )을 설정 하거나 취소 ( **-** ) 숨겨진 파일 특성입니다. 파일이이 특성 집합을 사용 하는 경우에는 해당 파일에 대 한 다른 특성을 변경 하기 전에 특성을 지워야 합니다. |
| `{+\|-}i` | 설정 ( **+** ) 하거나 취소 ( **-** ) 콘텐츠가 인덱싱되지 않은 파일 특성입니다. |
| `[<drive>:][<path>][<filename>]` | 디렉터리, 파일 또는 파일을 표시 하거나 특성을 변경 하려면 원하는 그룹의 이름과 위치를 지정 합니다.<p>사용할 수는 **?** 및는 파일 그룹에 대 한 특성을 표시 하거나 변경 하기 위해 *filename* 매개 변수에 와일드 카드 문자를 **&#42;** 합니다. |
| /s | 적용 대상 **attrib** 현재 디렉터리에 일치 하는 파일에 명령줄 옵션 및 모든 하위 디렉터리 및입니다. |
| /d | 적용 대상 **attrib** 와 디렉터리에 명령줄 옵션입니다. |
| /l | 적용 대상 **attrib** 와 기호화 된 링크의 대상이 아닌 기호화 된 링크에 명령줄 옵션입니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="examples"></a>예

현재 디렉터리에 있는 News86 라는 파일의 특성을 표시 하려면 다음을 입력 합니다.

```
attrib news86
```

report.txt 이라는 파일에 읽기 전용 특성을 할당 하려면 다음을 입력 합니다.

```
attrib +r report.txt
```

B: 드라이브의 디스크에서 공용 디렉터리와 해당 하위 디렉터리에 있는 파일의 읽기 전용 특성을 제거 하려면 다음을 입력 합니다.

```
attrib -r b:\public\*.* /s
```

드라이브 a의 모든 파일에 대 한 보관 특성을 설정 하려면:를 입력 한 다음 확장명이 .bak 인 파일에 대 한 Archive 특성을 지웁니다.

```
attrib +a a:*.* & attrib -a a:*.bak
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [xcopy 명령](xcopy.md)
