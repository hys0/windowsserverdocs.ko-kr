---
title: 편집
description: MS-DOS 편집기를 시작 하는 편집 명령에 대 한 참조 항목으로, ASCII 텍스트 파일을 만들고 변경할 수 있습니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4e0ff2e8-3518-47c1-8c69-5e93f895fa0e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a9f6c78889f466015d60149c27a87dcefe840133
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2020
ms.locfileid: "83436918"
---
# <a name="edit"></a>편집

ASCII 텍스트 파일을 만들고 변경 하는 MS-DOS 편집기를 시작 합니다.

## <a name="syntax"></a>구문

```
edit [/b] [/h] [/r] [/s] [/<nnn>] [[<drive>:][<path>]<filename> [<filename2> [...]]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `[<drive>:][<path>]<filename> [<filename2> [...]]` | 하나 이상의 ASCII 텍스트 파일의 이름과 위치를 지정합니다. 파일이 없으면 MS-DOS 편집기에서 해당 파일을 만듭니다. 파일이 있으면 MS-DOS 것 열리고 해당 내용을 화면에 표시 됩니다. *파일 이름* 옵션에는 와일드 카드 문자 (**&#42;** 및 **?**)를 사용할 수 있습니다. 여러 파일 이름을 공백으로 구분 합니다. |
| /b | 강제로 흑백 모드 흑백으로 해당 MS-DOS 편집기를 표시 합니다. |
| /h | 현재 모니터에 대 한 줄의 가능한 최대 수를 표시합니다. |
| /r | 읽기 전용 모드에서 파일을 로드합니다. |
| /s | 짧은 파일 이름 사용 하도록 강제 합니다. |
| `<nnn>` | 이진 파일을 로드 하 고, 줄을 *nnn* 문자 너비로 줄 바꿈 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- 자세한 도움말을 보려면 MS-DOS 편집기를 열고 F1 키를 누릅니다.

- 일부 모니터는 기본적으로 바로 가기 키 표시를 지원 하지 않습니다. 모니터에 바로 가기 키가 표시 되지 않으면 **/b**를 사용 합니다.

### <a name="examples"></a>예

MS-DOS 편집기를 열려면 다음을 입력 합니다.

```
edit
```

현재 디렉터리에 *newtextfile* 라는 파일을 만들고 편집 하려면 다음을 입력 합니다.

```
edit newtextfile.txt
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
