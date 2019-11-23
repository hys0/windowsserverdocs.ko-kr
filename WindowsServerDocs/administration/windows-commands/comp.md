---
title: comp
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 84604cea36b0b4c9543a7169002551c0da4f0493
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379261"
---
# <a name="comp"></a>comp



바이트 단위로 두 파일 또는 파일 집합의 내용을 비교 합니다. 매개 변수 없이 사용 하는 경우 **comp** 비교할 파일을 입력 하 라는 메시지를 표시 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
comp [<Data1>] [<Data2>] [/d] [/a] [/l] [/n=<Number>] [/c]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<Data1 >|비교할 첫 번째 파일 또는 파일 집합의 위치와 이름을 지정 합니다. 와일드 카드 문자 ( **&#42;** 및 **?** )를 사용 하 여 여러 파일을 지정할 수 있습니다.|
|\<Data2 >|비교할 두 번째 파일 또는 파일 집합의 위치와 이름을 지정 합니다. 와일드 카드 문자 ( **&#42;** 및 **?** )를 사용 하 여 여러 파일을 지정할 수 있습니다.|
|/d|소수 형식의 차이를 표시 합니다. 기본 형식은 16 진수입니다.|
|/ a|차이점을 문자로 표시 합니다.|
|/l|바이트 오프셋을 표시 하는 대신 차이가 발생 하는 줄 번호를 표시 합니다.|
|/n =\<Number >|파일 크기가 서로 다른 경우에도 각 파일에 지정 된 줄 수를 비교 합니다.|
|/c|대/소문자를 구분 하지 않는 비교를 수행 합니다.|
|설정 / 해제 [line]|오프 라인 특성 집합을 사용 하 여 파일을 처리 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   **Comp** 명령이 일치 하지 않는 정보를 식별 하는 방법

    비교 하는 동안 **comp** 는 파일 간에 동일 하지 않은 정보의 위치를 식별 하는 메시지를 표시 합니다. 각 메시지는 같지 않은 바이트의 오프셋 메모리 주소와 바이트의 내용 ( **/a** 또는 **/d** 명령줄 매개 변수를 지정 하지 않은 경우 16 진수 표기법)을 나타냅니다. 메시지는 다음과 같은 형식으로 표시 됩니다.

    `Compare error at OFFSET xxxxxxxx`

    `file1 = xx`

    `file2 = xx`

    10 개의 같지 않은 비교 후에 **comp** 는 파일 비교를 중지 하 고 다음 메시지를 표시 합니다.

    `10 Mismatches - ending compare`
-   *Data1* 및 *Data2* 의 특수 사례 처리  
    -   *Data1* 또는 *data2* 의 필수 구성 요소를 생략 하거나 *data2*를 생략 하면 **comp** 는 누락 된 정보를 묻는 메시지를 표시 합니다.
    -   *Data1* 이 파일 이름이 없는 드라이브 문자 또는 디렉터리 이름만 포함 하는 경우 **comp** 는 지정 된 디렉터리의 모든 파일을 *Data1*에 지정 된 파일과 비교 합니다.
    -   *Data2* 에 드라이브 문자 또는 디렉터리 이름만 포함 된 경우 *data2* 의 기본 파일 이름은 *Data1*의 기본 파일 이름과 동일 합니다.
    -   **Comp** 지정한 파일을 찾을 수 없는 경우 더 많은 파일을 비교할지 여부를 확인 하는 메시지를 표시 합니다.
-   다른 위치에 있는 파일 비교

    **Comp** 는 동일한 드라이브나 다른 드라이브, 같은 디렉터리 또는 다른 디렉터리에 있는 파일을 비교할 수 있습니다. **Comp** 가 파일을 비교할 때 해당 위치와 파일 이름을 표시 합니다.
-   같은 이름의 파일 비교

    서로 다른 디렉터리나 다른 드라이브에 있는 경우 비교 하는 파일의 파일 이름이 동일할 수 있습니다. *Data2*의 파일 이름을 지정 하지 않은 경우 *data2* 의 기본 파일 이름은 *Data1*의 파일 이름과 동일 합니다. 와일드 카드 문자 ( **&#42;** 및 **?** )를 사용 하 여 파일 이름을 지정할 수 있습니다.
-   서로 다른 크기의 파일 비교

    다른 크기의 파일을 비교 하려면 **/n** 을 지정 해야 합니다. 파일 크기가 다르고 **/n** 을 지정 하지 않은 경우 **comp** 는 다음과 같은 메시지를 표시 합니다.

    `Files are different sizes`

    `Compare more files (Y/N)?`

    이러한 파일을 비교 하려면 N을 눌러 **comp** 명령을 중지 합니다. 그런 다음 **/n** 옵션과 함께 **comp** 명령을 다시 실행 하 여 각 파일의 첫 번째 부분만 비교 합니다.
-   순차적으로 파일 비교

    와일드 **&#42;** 카드 문자 (및 **?** )를 사용 하 여 여러 파일을 지정 하는 경우 **comp** 는 *Data1* 과 일치 하는 첫 번째 파일을 찾아서 *Data2*의 해당 파일과 비교 합니다 (있는 경우). **Comp** 명령은 *Data1*과 일치 하는 각 파일에 대 한 비교 결과를 보고 합니다. 완료 되 면 **comp** 다음 메시지를 표시 합니다.

    `Compare more files (Y/N)?`

    더 많은 파일을 비교 하려면 Y를 누릅니다. **Comp** 명령은 새 파일의 위치와 이름을 입력 하 라는 메시지를 표시 합니다. 비교를 중지 하려면 N을 누릅니다. Y 키를 누르면 **comp** 는 사용할 명령줄 옵션을 묻는 메시지를 표시 합니다. 명령줄 옵션을 지정 하지 않으면 **comp** 는 이전에 지정한를 사용 합니다.

## <a name="BKMK_examples"></a>예와

디렉터리 C:\Reports의 내용을 백업 디렉터리와 비교 하려면 다음을 입력 \\\\Sales\Backup\April
```
comp c:\reports \\sales\backup\april
```
\Invoice 디렉터리에 있는 텍스트 파일의 처음 10 줄을 비교 하 고 결과를 decimal 형식으로 표시 하려면 다음을 입력 합니다.
```
comp \invoice\*.txt \invoice\backup\*.txt /n=10 /d
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)