---
title: if
description: 일괄 처리 프로그램에서 조건부 처리를 수행 하는 if 명령의 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 698b3fb9-532b-4c2b-af7f-179f8dc57131
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d6f73e784d6fb394db258a056f38045b6a545469
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83818553"
---
# <a name="if"></a>if

배치 프로그램에서 조건부 처리를 수행 합니다.

## <a name="syntax"></a>구문

```
if [not] ERRORLEVEL <number> <command> [else <expression>]
if [not] <string1>==<string2> <command> [else <expression>]
if [not] exist <filename> <command> [else <expression>]
```

명령 확장을 사용 하는 경우에 다음 구문을 사용 합니다.

```
if [/i] <string1> <compareop> <string2> <command> [else <expression>]
if cmdextversion <number> <command> [else <expression>]
if defined <variable> <command> [else <expression>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- |------------ |
| not | 명령이 실행 되도록 조건이 false 인 경우에 지정 합니다. |
| 수준은`<number>` | Cmd.exe에서 이전 프로그램이 실행 한 경우에만 true 조건을 지정 하 여 종료 코드를 *number*보다 크거나 같은 값으로 반환 합니다. |
| `<command>` | 앞의 조건을 충족 하는 경우 실행 되도록 하는 명령을 지정 합니다. |
| `<string1>==<string2>` | *문자열* 1과 *문자열 2* 가 동일한 경우에만 true 조건을 지정 합니다. 이러한 값은 리터럴 문자열 또는 일괄 처리 변수 일 수 있습니다 (예: `%1` ). 리터럴 문자열을 따옴표로 묶습니다 필요가 없습니다. |
| 있지만`<filename>` | 지정 된 파일 이름이 있는 경우 참인 조건을 지정 합니다. |
| `<compareop>` | 다음을 포함 하 여 세 문자로 된 비교 연산자를 지정 합니다.<ul><li>**같음** -같음</li><li>**Neq** -같지 않음</li><li>**Lss** -보다 작음</li><li>**Leq** -작거나 같음</li><li>**Gtr** -보다 큼</li><li>**Geq** -크거나 같음</li></ul> |
| /i | 강제로 문자열 대/소문자를 비교 합니다. If 형식의 **/i** 를 사용할 수 있습니다 `string1==string2` . **if** 이러한 비교는 제네릭이 며, *string1* 과 *문자열 2* 가 모두 숫자로만 구성 된 경우 문자열은 숫자로 변환 되 고 숫자 비교가 수행 됩니다. |
| cmdextversion`<number>` | 내부 버전 번호를 지정 된 숫자 보다 크거나 연결 Cmd.exe의 기능은 같은 명령 확장 된 경우에만 참이 지정 합니다. 첫 번째 버전은 1입니다. 명령 확장에 중요 한 향상 된 기능을 추가할 때 1 씩 증가 합니다. **cmdextversion** 조건부가 true 되지 명령을 경우 (기본적으로 확장을 사용 하는 명령) 확장을 사용할 수 있습니다. |
| defined `<variable>` | *변수가* 정의 되어 있는 경우 true 조건을 지정 합니다. |
| `<expression>` | 명령에 전달 되는 명령줄 명령 및 매개 변수를 지정 된 **다른** 절. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- **If** 절에 지정 된 조건이 true 이면 조건 다음에 오는 명령이 수행 됩니다. 조건이 false 이면 **if** 절의 명령이 무시 되 고 명령이 **else** 절에 지정 된 명령을 실행 합니다.

- 프로그램이 중지 되 면 종료 코드를 반환 합니다. 종료 코드를 조건으로 사용 하려면 **errorlevel** 매개 변수를 사용 합니다.

- 사용 하는 경우 **정의**, 다음과 같은 세 개의 변수는 환경에 추가 됩니다: **%errorlevel%**, **%cmdcmdline%**, 및 **%cmdextversion%** 합니다.

  - **% errorlevel%**: errorlevel 환경 변수의 현재 값에 대 한 문자열 표현으로 확장 됩니다. 이 변수는 이름이 ERRORLEVEL 인 기존 환경 변수가 없는 것으로 가정 합니다. 있는 경우 해당 ERRORLEVEL 값을 대신 가져옵니다.

  - **% cmdcmdline%**: cmd.exe에 의해 처리 되기 전에 cmd.exe에 전달 된 원래 명령줄로 확장 됩니다. 여기서는 이름이 CMDCMDLINE 인 기존 환경 변수가 없는 것으로 가정 합니다. 있는 경우 해당 CMDCMDLINE 값을 대신 가져옵니다.

  - **% cmdextversion%**: **cmdextversion**의 현재 값에 대 한 문자열 표현으로 확장 됩니다. 여기서는 이름이 CMDEXTVERSION 인 기존 환경 변수가 없는 것으로 가정 합니다. 있는 경우 해당 CMDEXTVERSION 값을 대신 가져옵니다.

- 사용 해야는 **다른** 절 뒤의 명령과 동일한 줄에는 **경우**합니다.

### <a name="examples"></a>예

**데이터 파일을 찾을 수 없습니다. .dat 파일을 찾을**수 없는 경우 메시지를 표시 하려면 다음을 입력 합니다.

```
if not exist product.dat echo Cannot find data file
```

A: 드라이브의 디스크를 포맷 하 고 포맷 프로세스 동안 오류가 발생 하는 경우에 오류 메시지를 표시 하려면 배치 파일에서 다음 줄을 입력 합니다.

```
:begin
@echo off
format a: /s
if not errorlevel 1 goto end
echo An error occurred during formatting.
:end
echo End of batch program.
```

를 현재 디렉터리에서 Product.dat 파일을 삭제 하거나 Product.dat을 찾을 수 없는 경우 메시지를 표시 하려면 배치 파일에서 다음 줄을 입력 합니다.

```
IF EXIST Product.dat (
del Product.dat
) ELSE (
echo The Product.dat file is missing.
)
```

> [!NOTE]
> 이 줄을 한 줄으로 다음과 같이 결합할 수 있습니다.
> ```
> IF EXIST Product.dat (del Product.dat) ELSE (echo The Product.dat file is missing.)
> ```

배치 파일을 실행 한 후 ERRORLEVEL 환경 변수의 값을 에코 하려면 배치 파일에서 다음 줄을 입력 합니다.

```
goto answer%errorlevel%
:answer1
echo The program returned error level 1
goto end
:answer0
echo The program returned error level 0
goto end
:end
echo Done!
```

ERRORLEVEL 환경 변수의 값이 1 보다 작거나 같으면 확인 레이블로 이동 하려면 다음을 입력 합니다.

```
if %errorlevel% LEQ 1 goto okay
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [goto 명령](goto.md)
