---
title: comp
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 40319d23-704d-4da1-be93-8259547275d0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d10b86176d97e1afd76085516fbfc00bdc36577f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854684"
---
# <a name="comp"></a>comp



두 파일의 내용을 가져오거나 파일 바이트 단위로 비교합니다. 매개 변수 없이 사용 하는 경우 **comp** 비교할 파일을 입력 하 라는 메시지가 표시 됩니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
comp [<Data1>] [<Data2>] [/d] [/a] [/l] [/n=<Number>] [/c]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<Data1>|첫 번째 파일의 이름 또는 집합 비교 하려는 파일의 위치를 지정 합니다. 와일드 카드 문자를 사용할 수 있습니다 (**&#42;** 하 고 **?**) 여러 파일을 지정 합니다.|
|\<Data2>|두 번째 파일의 이름 또는 집합 비교 하려는 파일의 위치를 지정 합니다. 와일드 카드 문자를 사용할 수 있습니다 (**&#42;** 하 고 **?**) 여러 파일을 지정 합니다.|
|/d|10 진수 형식의 차이점을 표시합니다. (기본 형식은 16 진수입니다.)|
|/ a|문자로 차이 표시합니다.|
|/l|바이트 오프셋을 표시 하는 대신 차이가 발생 하는 줄의 번호를 표시 합니다.|
|/n=\<Number>|파일 크기가 다른 경우에 각 파일에 대해 지정 된 줄 번호만 비교 합니다.|
|/c|대/소문자 구분 되지 않는 비교를 수행 합니다.|
|설정 / 해제 [line]|오프 라인 특성 집합을 사용 하 여 파일을 처리합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   하는 방법을 **comp** 일치 하지 않는 정보를 식별 하는 명령

    비교 하는 동안 **comp** 파일 간에 같지 않은 정보가 있는 위치를 식별 하는 메시지를 표시 합니다. 각 메시지 바이트의 내용과 같지 않은 바이트 오프셋된의 메모리 주소를 나타냅니다 (16 진수 표기법의 경우가 아니면 합니다 **/a** 또는 **/d** 명령줄 매개 변수를 지정). 다음 형식으로 메시지가 표시 됩니다.

    `Compare error at OFFSET xxxxxxxx`

    `file1 = xx`

    `file2 = xx`

    10 같지 않음 비교를 뒤 **comp** 파일 비교를 중지 하 고 다음 메시지가 표시 됩니다.

    `10 Mismatches - ending compare`
-   에 대 한 특수 사례를 처리 *Data1* 고 *Data2*  
    -   필수 구성 요소 중 하나를 생략 하면 *Data1* 또는 *Data2* 생략 하는 경우 또는 *Data2*, **comp** 누락 된 정보에 대 한 라는 메시지가 표시 됩니다.
    -   하는 경우 *Data1* 드라이브 문자나 파일 이름이 없는 디렉터리 이름 포함 **comp** 에 지정 된 파일에 지정된 된 디렉터리에 파일을 모두 비교 *Data1*합니다.
    -   하는 경우 *Data2* 드라이브 문자나 디렉터리 이름에 대 한 기본 파일 이름 포함 *Data2* 와 동일 *Data1*합니다.
    -   하는 경우 **comp** 묻는 메시지가 다른 파일을 비교 것인지 여부를 확인 하는 메시지를 사용 하 여, 지정 된 파일을 찾을 수 없습니다.
-   서로 다른 위치에서 파일 비교

    **Comp** 같은 드라이브에 서로 다른 드라이브에 및 동일한 디렉터리 또는 다른 디렉터리에 파일을 비교할 수 있습니다. 때 **comp** 파일을 비교 하 여 해당 위치와 파일 이름을 표시 합니다.
-   같은 이름의 파일 비교

    파일 비교 하는 경우 다른 드라이브 또는 다른 디렉터리에서 동일한 파일 이름이 있습니다. 파일 이름을 지정 하지 않으면 *Data2*에 대 한 기본 파일 이름을 *Data2* 에서 파일 이름을 동일 *Data1*합니다. 와일드 카드 문자를 사용할 수 있습니다 (**&#42;** 하 고 **?**) 파일 이름을 지정 합니다.
-   다양 한 크기의 파일 비교

    지정 해야 합니다 **/n** 다양 한 크기의 파일을 비교 합니다. 파일 크기가 다른 경우 및 **/n** 지정 하지 않으면 **comp** 다음 메시지가 표시 됩니다.

    `Files are different sizes`

    `Compare more files (Y/N)?`

    이러한 파일을 비교할 않으려면 N 키를 **comp** 명령입니다. 그런 다음 다시 실행 합니다 **comp** 명령과 **/n** 각 파일의 첫 번째 부분만 비교 하는 옵션입니다.
-   파일을 순서 대로 비교

    와일드 카드 문자를 사용 하는 경우 (**&#42;** 하 고 **?**) 여러 파일을 지정 하려면 **comp** 일치 하는 첫 번째 파일을 찾습니다 *Data1* 해당 파일을 사용 하 여 비교 *Data2*존재 하는 경우. 합니다 **comp** 일치 하는 각 파일에 대 한 비교의 결과 보고 하는 명령 *Data1*합니다. 완료 되 면 **comp** 다음 메시지가 표시 됩니다.

    `Compare more files (Y/N)?`

    더 많은 파일을 비교 하려면 Y를 누릅니다. 합니다 **comp** 명령을 새 파일의 이름과 위치를 묻는 메시지를 표시 합니다. 비교를 사용 하지 않으려면 N 키를 누릅니다 Y 키를 누르면 **comp** 명령줄 옵션 사용에 대 한 라는 메시지가 표시 됩니다. 명령줄 옵션을 지정 하지 않는 경우 **comp** 하기 전에 지정 된 것을 사용 합니다.

## <a name="BKMK_examples"></a>예제

백업 디렉터리를 사용 하 여 C:\Reports 디렉터리의 내용을 비교 하기가 \\ \\Sales\Backup\April, 유형:
```
comp c:\reports \\sales\backup\april
```
\Invoice 디렉터리에 있는 텍스트 파일의 처음 10 개의 줄을 비교 하 고 10 진수 형식으로 결과 표시 하려면 다음을 입력 합니다.
```
comp \invoice\*.txt \invoice\backup\*.txt /n=10 /d
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)