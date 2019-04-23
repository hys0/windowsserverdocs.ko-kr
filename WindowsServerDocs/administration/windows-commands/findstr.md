---
title: findstr
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c2d803fb-4cd2-46a1-a1b7-6f5e0249c418
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 82ba51cdb49501492c1fa38c6c93933f4aee90d8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890464"
---
# <a name="findstr"></a>findstr



파일에서 텍스트의 패턴을 검색 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
findstr [/b] [/e] [/l | /r] [/s] [/i] [/x] [/v] [/n] [/m] [/o] [/p] [/f:<File>] [/c:<String>] [/g:<File>] [/d:<DirList>] [/a:<ColorAttribute>] [/off[line]] <Strings> [<Drive>:][<Path>]<FileName>[ ...]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/b|줄의 시작 부분에는 텍스트 패턴을 일치 합니다.|
|/e|줄의 끝에 있으면 텍스트 패턴을 찾습니다.|
|/l|프로세스는 문자 그대로 문자열을 검색 합니다.|
|/r|프로세스 검색 문자열을 정규식으로 사용 합니다. 이 값은 기본 설정입니다.|
|/s|현재 디렉터리와 모든 하위 디렉터리를 검색합니다.|
|/i|문자열을 검색할 때는 문자의 대/소문자를 무시 합니다.|
|/x|정확히 일치 하는 줄을 표시 합니다.|
|/v|일치 하는 항목을 포함 하지 않는 줄만 표시 합니다.|
|/n|일치 하는 각 줄의 줄 번호를 인쇄 합니다.|
|/m|파일에는 일치 하는 항목을 포함 하는 경우 파일 이름만을 출력 합니다.|
|/o|일치 하는 각 줄 앞에 문자 오프셋을 표시 합니다.|
|/p|인쇄할 수 없는 문자를 사용 하 여 파일을 건너뜁니다.|
|설정 / 해제 [line]|오프 라인 특성 집합이 있는 파일을 건너뛰지 않습니다.|
|/f:\<File>|지정된 된 파일에서 파일 목록을 가져옵니다.|
|/c:\<String>|지정된 된 텍스트를 사용 하 여 리터럴 검색 문자열입니다.|
|/g:\<File>|지정된 된 파일에서 문자열을 검색 하는 가져옵니다.|
|/d:\<DirList>|지정된 된 디렉터리 목록을 검색합니다. 예를 들어 각 디렉터리는 세미콜론 (;)으로 구분 해야 `dir1;dir2;dir3`합니다.|
|/a:\<ColorAttribute>|두 개의 16 진수가 color 특성을 지정합니다. 형식 `color /?` 추가 정보에 대 한 합니다.|
|\<Strings>|검색할 텍스트를 지정 *FileName*합니다. 필수 사항입니다.|
|[\<Drive>:][<Path>]<FileName>[ ...]|검색할 파일 및 파일 또는 위치를 지정 합니다. 하나 이상의 파일에 이름이 필요 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   모든 **findstr** 명령줄 옵션 앞에 야 *문자열* 및 *FileName* 명령 문자열에 있습니다.
-   정규식 리터럴 문자와 메타 문자를 사용 하 여 텍스트의 패턴 보다 정확한 문자열을 찾을 수 있습니다. 리터럴 문자는 정규식 구문에서 특별 한 의미가 없는 문자를 해당 문자의 회입니다. 예를 들어 문자와 숫자는 리터럴 문자. 메타 문자는 정규식 구문에서 특별 한 의미 (연산자나 구분 기호) 기호입니다.

    다음 표에 나와 있는 메타 문자는 **findstr** 허용 합니다.  
    |메타 문자|값|
    |-------------|-----|
    |.|모든 문자에 와일드 카드:|
    |*|반복: 0 개 이상의 일치 이전 문자 또는 클래스|
    |^|줄 위치: 줄의 시작|
    |$|줄 위치: 줄의 끝|
    |[클래스]|문자 클래스: 집합에 있는 한 문자|
    |[^ 클래스]|역 클래스: 집합에 없는 임의의 한 문자|
    |[x-y]|범위: 지정된 된 범위 내 문자|
    |\x|메타 문자 x: 이스케이프 리터럴 사용|
    |\\<string|단어 위치: 단어의 시작|
    |string\>|단어 위치: 단어의 끝|

    정규식 구문에 특수 문자 력이 가장 함께 사용 하는 경우. 예를 들어, 와일드 카드 문자 (.)는 다음과 같은 조합을 사용 하 여 및 문자의 문자열 일치 시키려면 문자 (*)를 반복 합니다.  
    ```
    .*
    ```  
    식을 사용 하 여 다음 더 큰 수식의 일부로 "b"로 시작 하 고 "ing"로 끝나는 문자열 일치 합니다.  
    ```
    b.*ing
    ```

## <a name="BKMK_examples"></a>예제

인수는 접두사로 붙습니다 하지 않는 한 여러 개의 검색 문자열을 구분 하 공간을 사용 하 여 **/c**합니다.

"Hello"를 검색 하려면 "there" 파일 x.y를 입력 합니다.
```
findstr "hello there" x.y 
```
"안녕" x.y 파일에서에서를 검색 하려면 다음을 입력 합니다.
```
findstr /c:"hello there" x.y 
```
단어의 모든 항목 "Windows" (초기 자본 문자 W)로 Proposal.txt 파일에서을 찾으려면 다음을 입력 합니다.
```
findstr Windows proposal.txt 
```
현재 디렉터리 및 모든 하위 디렉터리에 관계 없이 대/소문자, Windows, 단어를 포함 하는 모든 파일을 검색 하려면 다음을 입력 합니다.
```
findstr /s /i Windows *.* 
```
"FOR"로 시작 하며 앞에 0 개 이상의 공백 (예: 컴퓨터 프로그램 루프)을 하는 줄을 모두 찾습니다 고 발생 하는 각가 있는 줄 번호를 표시 하려면 다음을 입력 합니다.
```
findstr /b /n /r /c:"^ *FOR" *.bas 
```
파일 집합에 여러 문자열을 검색 하려면 별도 줄에 각 검색 조건을 포함 하는 텍스트 파일을 만듭니다. 또한 텍스트 파일에서 검색 하려는 정확한 파일을 나열할 수 있습니다. 예를 들어, 검색 조건으로 Stringlist.txt 파일을 사용 하려면 Filelist.txt에 나열 된 파일을 검색 하 고 Results.out, 형식 파일에 결과 저장 합니다.
```
findstr /g:stringlist.txt /f:filelist.txt > results.out 
```
현재 디렉터리와 대/소문자, 모든 하위 디렉터리 내에서 "컴퓨터" 라는 단어를 포함 하는 모든 파일을 나열 하려면 다음을 입력 합니다.
```
findstr /s /i /m "\<computer\>" *.*
```
"컴퓨터" 단어 및 형식 "구성" (예: "칭찬" 및 "경쟁")로 시작 하는 다른 모든 단어를 포함 하는 모든 파일을 나열:
```
findstr /s /i /m "\<comp.*" *.*
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)