---
title: echo
description: 메시지를 표시 하거나 명령 에코 기능을 설정 하거나 해제 하는 echo 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fb9fcd0f-5e73-4504-aa95-78204e1a79d3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ca2a10a5d52c9d175d453a164f3ab4f47ca0841d
ms.sourcegitcommit: 430c6564c18f89eecb5bbc39cfee1a6f1d8ff85b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/26/2020
ms.locfileid: "83855667"
---
# <a name="echo"></a>echo

메시지를 표시 하거나 명령 에코 기능의 해제 하거나 설정 합니다. 매개 변수 없이 사용 하는 경우 **echo** 현재 에코 설정을 표시 합니다.

## <a name="syntax"></a>구문

```
echo [<message>]
echo [on | off]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| --------- | ----------- |
| [ \| 꺼짐] | 또는 명령 에코 기능의 해제를 설정 합니다. 기본적으로 켜져 명령 에코 합니다. |
| `<message>` | 화면에 표시할 텍스트를 지정 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- `echo <message>`명령은 **echo** 가 꺼져 있을 때 특히 유용 합니다. 명령을 표시 하지 않고 몇 줄의 긴 메시지를 표시 하려면 `echo <message>` 배치 프로그램에서 **echo off** 명령 뒤에 여러 명령을 포함 하면 됩니다.

- **Echo** 가 해제 되 면 명령 프롬프트 창에 명령 프롬프트가 표시 되지 않습니다. 명령 프롬프트를 표시 하려면 입력 **화면 표시 합니다.**

- 배치 파일에서 사용 하는 경우 **echo on** 및 **echo off** 는 명령 프롬프트의 설정에 영향을 주지 않습니다.

- 배치 파일에서 특정 명령이 반향을 방지 하려면 `@` 명령 앞에 기호를 삽입 합니다. 배치 파일에서 모든 명령 에코를 방지 하려면 포함는 **오프 에코** 파일의 시작 부분에 명령 합니다.

- `|`Echo를 사용할 때 파이프 () 또는 리디렉션 문자 (또는)를 표시 하려면 `<` `>` **echo** `^` 파이프 또는 리디렉션 문자 바로 앞에 캐럿 ()을 사용 합니다. 예:, `^|` `^>` 또는 `^<` ). 캐럿을 표시 하려면 두 캐럿 연속으로 입력 합니다 (`^^`).

### <a name="examples"></a>예

현재 표시 하려면 **echo** 설정에 입력 합니다.

```
echo
```

화면에 빈 줄을 에코를 하려면 다음을 입력 합니다.

```
echo.
```

> [!NOTE]
> 마침표 앞에 공백을 포함 하지 않습니다. 그렇지 않으면 빈 줄 대신 마침표를 표시 합니다.

방지 하기 위해 명령 프롬프트에서 명령을 에코를 입력 합니다.

```
echo off
```

> [!NOTE]
> **Echo** 가 꺼져 있으면 명령 프롬프트 창에 명령 프롬프트가 나타나지 않습니다. 명령 프롬프트를 다시 표시 하려면 다음을 입력 **화면 표시**합니다.

배치 파일에서 모든 명령을 방지 하기 위해 (포함 하는 **오프 에코** 명령)에서 일괄 처리 파일 형식의 첫 번째 줄에서 화면에 표시:

```
@echo off
```

사용할 수는 **echo** 의 일부분으로 명령은 **경우** 문입니다. 예를 들어를 이러한 파일을 찾지 못하면 에코 메시지 및.rpt 파일 이름 확장명과 파일에 대 한 현재 디렉터리를 검색 하려면 다음을 입력 합니다.

```
if exist *.rpt echo The report has arrived.
```

다음 배치 파일.txt 파일 이름 확장명을 사용 하 여 파일에 대 한 현재 디렉터리를 검색 하 고 검색 결과 나타내는 메시지를 표시 합니다.

```
@echo off
if not exist *.txt (
echo This directory contains no text files.
) else (
   echo This directory contains the following text files:
   echo.
   dir /b *.txt
   )
```

배치 파일을 실행할 때.txt 파일이 발견 되 면 다음 메시지가 표시 됩니다.

```
This directory contains no text files.
```

.Txt 파일은 배치 파일을 실행 하는 경우 발견 되 면 다음과 같은 출력이 표시 됩니다 (이 예에서는 File1.txt, File2.txt, 및 존재 File3.txt 파일 가정):

```
This directory contains the following text files:
File1.txt
File2.txt
File3.txt
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
