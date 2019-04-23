---
title: fc
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 485fc3d8-b7c5-496d-87be-0011112f27d5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 98fd96c73b962a13c0e715420ebbe6f3cd19a42b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888684"
---
# <a name="fc"></a>fc



두 개의 파일 또는 파일의 설정와 비교 이들 간의 차이 표시 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
fc /a [/c] [/l] [/lb<N>] [/n] [/off[line]] [/t] [/u] [/w] [/<NNNN>] [<Drive1>:][<Path1>]<FileName1> [<Drive2>:][<Path2>]<FileName2>
fc /b [<Drive1:>][<Path1>]<FileName1> [<Drive2:>][<Path2>]<FileName2>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/ a|ASCII 비교의 출력을 줄여서 표시 합니다. 다른 줄을 모두 표시 하는 대신 **fc** 차이의 각 집합에 대 한 첫 번째 및 마지막 줄이 표시 됩니다.|
|/b|바이트 단위로 이진 모드에서 두 개의 파일을 비교 하 여 불일치를 찾은 후 파일을 다시 동기화를 시도 하지 않습니다. 이 다음과 같은 파일 확장명을 가진 파일을 비교 하기 위한 기본 모드:.exe,.com,.sys,.obj,.lib 또는.bin 합니다.|
|/c|대/소문자를 무시합니다.|
|/l|비교는 ASCII 모드, 및의 파일 줄 단위로 불일치가 발견 되 면 파일을 다시 동기화 하려고 합니다. 이 다음 파일 확장명의 파일을 제외 하 고 파일을 비교 하기 위한 기본 모드:.exe,.com,.sys,.obj,.lib 또는.bin 합니다.|
|/lb\<N>|내부 버퍼에 대 한 줄의 수를 설정 *N*합니다. 줄 버퍼의 기본 길이 100 줄입니다. 파일 비교 하는 100 개 이상의 연속 된 여러 줄에 있으면 **fc** 는 비교를 취소 합니다.|
|/n|ASCII 비교 하는 동안 줄 번호를 표시 합니다.|
|설정 / 해제 [line]|오프 라인 특성 집합이 있는 파일을 건너뛰지 않습니다.|
|/t|방지 **fc** 탭을 공백으로 변환 합니다. 기본 동작은 탭 각각 8 번째 문자 위치에서 중지 공백으로 처리 하는 것입니다.|
|/u|유니코드 텍스트 파일로 파일을 비교합니다.|
|/w|비교 시 공백 (즉, 탭과 공백)을 압축합니다. 한 줄에 많은 연속 된 공백이 나 탭 **/w** 단일 공간으로 이러한 문자를 처리 합니다. 와 함께 사용할 경우 **/w**, **fc** 줄의 시작과 끝에 있는 공백을 무시 합니다.|
|/\<NNNN>|전에 일치 하지 않습니다 다음 일치 하는 연속 된 줄의 수를 지정 **fc** 가 파일을 다시 동기화 할 수 있습니다. 파일에서 일치 하는 줄의 수는 보다 작은 *NNNN*, **fc** 차이점으로 일치 하는 줄을 표시 합니다. 기본값은 2입니다.|
|[\<Drive1>:][<Path1>]<FileName1>|첫 번째 파일의 이름 또는 집합 비교 하는 파일의 위치를 지정 합니다. *FileName1* 가 필요 합니다.|
|[\<Drive2>:][<Path2>]<FileName2>|두 번째 파일의 이름 또는 집합 비교 하는 파일의 위치를 지정 합니다. *FileName2* 가 필요 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   이 명령은 c:\WINDOWS\fc.exe 여 implemeted입니다. PowerShell 내에서이 명령을 사용 하 여 수 있지만 'fc' 사용자 지정 형식에 대 한 별칭 이므로 전체 실행 파일 (fc.exe)를 나열 해야 합니다.

-   ASCII 비교에 대 한 파일 간의 차이점을 보고

    사용 하는 경우 **fc** ASCII 비교에 대 한 **fc** 다음 순서 대로 두 개의 파일 간의 차이 표시 합니다.  
    -   첫 번째 파일의 이름
    -   행 *FileName1* 파일 간에 다른
    -   두 파일에서 일치 하는 첫 번째 줄
    -   두 번째 파일의 이름
    -   행 *FileName2* 다른
    -   일치 하는 첫 번째 줄
-   사용 하 여 **/b** 이진 비교

    **/ b** 다음 구문에서 이진 비교 중에 발견 된 불일치 항목 표시:

    `\<XXXXXXXX: YY ZZ>`

    변수의 *XXXXXXXX* 파일의 시작 부분에서 측정 한 바이트 쌍에 대 한 16 진수 상대 주소를 지정 합니다. 주소는 00000000에서 시작 합니다. 에 대 한 16 진수 값 *YY* 및 *ZZ* 의 짝이 맞지 않는 바이트를 나타내는 *FileName1* 및 *FileName2*, 각각.
-   와일드 카드 문자 사용

    와일드 카드 문자를 사용할 수 있습니다 (**&#42;** 하 고 **?**)에서 *FileName1* 하 고 *FileName2*. 에 와일드 카드를 사용 하는 경우 *FileName1*, **fc** 파일 또는 지정 된 파일 집합에 지정 된 모든 파일을 비교 *FileName2*합니다. 에 와일드 카드를 사용 하는 경우 *FileName2*, **fc** 에서 해당 값을 사용 하 여 *FileName1*합니다.
-   메모리 사용

    ASCII 파일을 비교할 때 **fc** 내부 버퍼 (유지할 만큼 큰 100 줄)를 사용 하 여 저장소로. 파일이 있는 경우는 버퍼 보다 큰 **fc** 버퍼에 로드할 수 있는 기능을 비교 합니다. 하는 경우 **fc** 일치 항목을 찾지 못한 파일의 로드 부분을 중지 하 고 다음 메시지가 표시 됩니다.

    `Resynch failed. Files are too different.`

    사용 가능한 메모리 보다 큰 이진 파일을 비교할 때 **fc** 두 파일 디스크의 다음 부분을 사용 하 여 메모리 부분 겹치게 완전히 비교 합니다. 출력은 메모리 용량을 초과 하는 파일에 대 한 동일 하 게 됩니다.

## <a name="BKMK_examples"></a>예제

Monthly.rpt 및 Sales.rpt, 두 개의 텍스트 파일의 ASCII 비교 확인 약식 형태로 결과 표시를 입력 합니다.
```
fc /a monthly.rpt sales.rpt 
```
Profits.bat 및 Earnings.bat, 두 개의 일괄 처리 파일의 이진 비교를 위해 다음을 입력 합니다.
```
fc /b profits.bat earnings.bat
```
결과 표시와 비슷합니다.
```
00000002: 72 43
00000004: 65 3A
0000000E: 56 92
...
...
...
000005E8: 00 6E
FC: Earnings.bat longer than Profits.bat
```
Profits.bat 및 Earnings.bat 파일 동일 하면 **fc** 다음 메시지가 표시 됩니다.
```
Comparing files Profits.bat and Earnings.bat
FC: no differences encountered
```
New.bat 현재 디렉터리의 모든.bat 파일을 비교 하려면 다음을 입력 합니다.
```
fc *.bat new.bat
```
D 드라이브에서 파일과 New.bat C 드라이브에 New.bat 파일을 비교 하려면 다음을 입력 합니다.
```
fc c:new.bat d:*.bat
```
D 드라이브의 루트 디렉터리에 같은 이름의 파일을 C 드라이브의 루트 디렉터리에 각 배치 파일을 비교 하려면 다음을 입력 합니다.
```
fc c:*.bat d:*.bat
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)
