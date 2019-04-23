---
title: if
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 698b3fb9-532b-4c2b-af7f-179f8dc57131
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2fafd14b0b620a8b5630c869e33c5dbc7cd902f1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869234"
---
# <a name="if"></a>if



배치 프로그램에서 조건부 처리를 수행 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
if [not] ERRORLEVEL <Number> <Command> [else <Expression>]
if [not] <String1>==<String2> <Command> [else <Expression>]
if [not] exist <FileName> <Command> [else <Expression>]
```
명령 확장을 사용 하는 경우에 다음 구문을 사용 합니다.
```
if [/i] <String1> <CompareOp> <String2> <Command> [else <Expression>]
if cmdextversion <Number> <Command> [else <Expression>]
if defined <Variable> <Command> [else <Expression>]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|not|명령이 실행 되도록 조건이 false 인 경우에 지정 합니다.|
|errorlevel \<번호 >|보다 크거나 같은 Cmd.exe 실행 이전 프로그램에서 종료 코드를 반환 하는 경우에 참인 조건을 지정 *번호*합니다.|
|\<명령 >|앞의 조건을 충족 하는 경우 실행 되도록 하는 명령을 지정 합니다.|
|\<String1>==<String2>|경우에만 true 조건 지정 *String1* 및 *String2* 동일 합니다. 이러한 값은 리터럴 문자열이 나 일괄 처리 변수 (예: %1) 수 있습니다. 리터럴 문자열을 따옴표로 묶습니다 필요가 없습니다.|
|exist \<FileName>|지정 된 파일 이름이 있는 경우 참인 조건을 지정 합니다.|
|\<CompareOp>|세 문자로 비교 연산자를 지정합니다. 다음은 유효한 값을 나타내는 *CompareOp*:</br>**EQU** 같음</br>**NEQ** 같지 않음</br>**LSS** 미만</br>**LEQ** 값 보다 작거나 같음</br>**GTR** 보다 큼</br>**GEQ** 보다 크거나 같은 경우|
|/i|강제로 문자열 대/소문자를 비교 합니다.  사용할 수 있습니다 **/i** 에 *String1***==*** String2* 형태의 **경우**합니다. 이러한 비교는 일반, 있는 경우 두 *String1* 및 *String2* 자리 숫자 이루어져 있습니다만, 문자열을 숫자로 변환 됩니다 및 숫자 비교를 수행 합니다.|
|cmdextversion \<번호 >|내부 버전 번호를 지정 된 숫자 보다 크거나 연결 Cmd.exe의 기능은 같은 명령 확장 된 경우에만 참이 지정 합니다. 첫 번째 버전은 1입니다. 명령 확장에 중요 한 향상 된 기능을 추가할 때 1 씩 증가 합니다. **cmdextversion** 조건부가 true 되지 명령을 경우 (기본적으로 확장을 사용 하는 명령) 확장을 사용할 수 있습니다.|
|정의 \<변수 >|경우에 true 조건을 지정 *변수* 정의 됩니다.|
|\<Expression>|명령에 전달 되는 명령줄 명령 및 매개 변수를 지정 된 **다른** 절.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   조건에 지정 된 경우는 **경우** 절 true 이면 조건이 다음에 나오는 명령이 실행 됩니다. 조건이 false 인 경우 명령에는 경우 절이 무시 되 고 명령에 지정 된 모든 명령이 실행는 **다른** 절.
-   프로그램이 중지 되 면 종료 코드를 반환 합니다. 종료 코드를 조건으로 사용 하려면 **errorlevel**합니다.
-   사용 하는 경우 **정의**, 다음과 같은 세 개의 변수는 환경에 추가 됩니다: **%errorlevel%**, **%cmdcmdline%**, 및 **%cmdextversion%** 합니다.  
    -   **%errorlevel%** ERRORLEVEL 환경 변수의 현재 값의 문자열 표현으로 확장 됩니다. 이 있다고 가정 하지 ERRORLEVEL 이름의 기존 환경 변수-없는 경우, 받습니다 ERRORLEVEL 값을 대신 합니다.
    -   **%cmdcmdline%** Cmd.exe에 의해 처리 되기 전에 Cmd.exe에 전달 된 원래 명령 줄으로 확장 합니다. 이 있다고 가정 하지 CMDCMDLINE 이름의 기존 환경 변수-없는 경우, 받습니다 CMDCMDLINE 값 대신 합니다.
    -   **%cmdextversion%** 의 현재 값의 문자열 표현으로 확장 **cmdextversion**합니다. 이 있다고 가정 하지 CMDEXTVERSION 이름의 기존 환경 변수-없는 경우, 받습니다 CMDEXTVERSION 값 대신 합니다.
-   사용 해야는 **다른** 절 뒤의 명령과 동일한 줄에는 **경우**합니다.

## <a name="BKMK_examples"></a>예제

메시지를 표시 하려면 "데이터 파일을 찾을 수 없습니다" 파일 Product.dat을 찾을 수 없는 입력 합니다.
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
```
IF EXIST Product.dat (del Product.dat) ELSE (echo The Product.dat file is missing.)
```
배치 파일을 실행 한 후 ERRORLEVEL 환경 변수의 값을 에코 하려면 배치 파일에서 다음 줄을 입력 합니다.
```
goto answer%errorlevel%
:answer1
echo Program had return code 1
:answer0
echo Program had return code 0
goto end
:end
echo Done! 
```
ERRORLEVEL 환경 변수의 값이 1 보다 작거나 "무방" 레이블로 이동:
```
if %errorlevel% LEQ 1 goto okay
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)

[If](if.md)

[Goto](goto.md)