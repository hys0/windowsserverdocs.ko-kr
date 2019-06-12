---
title: diskcopy
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5fd21efa-52cc-4e70-a7fe-35125a435106
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 05/07/2018
ms.openlocfilehash: aadb3a77cda7f1403cd2f04ced12c17617f046df
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439574"
---
# <a name="diskcopy"></a>diskcopy



대상 드라이브의 서식이 지정 되거나 지정 되지 않은 플로피 디스크에 원본 드라이브에 플로피 디스크의 콘텐츠를 복사합니다. 매개 변수 없이 사용 하는 경우 **diskcopy** 원본 디스크 및 대상 디스크에 대 한 현재 드라이브를 사용 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

> [!NOTE]
> 이 명령은 Windows 10에 포함 되지 않습니다.

## <a name="syntax"></a>구문

```
diskcopy [<Drive1>: [<Drive2>:]] [/v]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<Drive1>|원본 디스크를 포함 하는 드라이브를 지정 합니다.|
|\<Drive2>|대상 디스크를 포함 하는 드라이브를 지정 합니다.|
|/v|정보를 올바르게 복사 되는지 확인 합니다. 이 옵션은 복사 프로세스 속도가 느려집니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   디스크를 사용 하 여

    **Diskcopy** 동일한 형식 이어야 하는 플로피 디스크와 같은 이동식 디스크 에서만 작동 합니다. 사용할 수 없습니다 **diskcopy** 하드 디스크를 사용 합니다. 에 대 한 하드 디스크 드라이브를 지정 하는 경우 *Drive1* 또는 *드라이브 2*합니다 **diskcopy** 다음 오류 메시지가 표시 됩니다.  
    ```
    Invalid drive specification
    Specified drive does not exist or is nonremovable
    ```  
    합니다 **diskcopy** 명령 소스를 삽입 하 라는 메시지가 표시 하 고 대상 디스크를 계속 하기 전에 키보드에서 아무 키나 눌러 때까지 대기 합니다.

    디스크를 복사한 후 **diskcopy** 다음 메시지가 표시 됩니다.  
    ```
    Copy another diskette (Y/N)?
    ```  
    Y 키를 누르면 **diskcopy** 다음 복사 작업에 대 한 원본 및 대상 디스크를 삽입 하 라는 메시지가 표시 됩니다. 중지 하는 **diskcopy** 처리, 키를 눌러 **N**합니다.

    에 형식이 지정 되지 않은 플로피 디스크를 복사 하는 경우 *드라이브 2*를 **diskcopy** 면 및 트랙당 섹터 디스크에 수 만큼 디스크를 포맷 *Drive1*합니다. **Diskcopy** 는 디스크를 포맷 하 고 파일을 복사 하는 동안 다음 메시지가 표시 됩니다.  
    ```
    Formatting while copying
    ```  
-   디스크 일련 번호

    원본 디스크 볼륨 일련 번호, 있으면 **diskcopy** 대상 디스크에 대 한 새 볼륨 일련 번호를 만들고 복사 작업이 완료 될 때 수를 표시 합니다.
-   드라이브 매개 변수를 생략합니다.

    생략 하면 합니다 *드라이브 2* 매개 변수 **diskcopy** 대상 드라이브로 현재 드라이브를 사용 합니다. 두 드라이브 매개 변수를 생략 **diskcopy** 둘 다에 대 한 현재 드라이브를 사용 합니다. 현재 드라이브와 같으면 *Drive1*를 **diskcopy** 필요에 따라 디스크를 교환 하 라는 메시지가 표시 됩니다.
-   Onedrive를 사용 하 여 복사

    실행할 **diskcopy** 플로피 디스크 드라이브가 아닌 다른 드라이브에서 드라이브에 C 예입니다. 경우 플로피 디스크 *Drive1* 및 플로피 디스크 *드라이브 2* 같으면 **diskcopy** 디스크를 전환 하 라는 메시지가 표시 됩니다. 디스크 사용 가능한 메모리를 포함할 수 있는 수보다 더 많은 정보를 포함 하는 경우 **diskcopy** 모든 정보를 한 번에 읽을 수 없습니다. **Diskcopy** 원본 디스크에서 읽고 대상 디스크에 기록 하 고 원본 디스크를 다시 삽입 하 라는 메시지가 표시 됩니다. 이 프로세스는 전체 디스크를 복사할 때까지 계속 됩니다.
-   디스크 조각화를 방지합니다.

    조각화는 디스크에 기존 파일 사이 공백 사용 되지 않는 디스크의 작은 영역입니다. 조각화 된 원본 디스크 찾기, 읽기 및 쓰기 파일의 프로세스가 느려질 수 있습니다.

    때문에 **diskcopy** 사용 하면 대상 디스크가 원본 디스크, 원본 디스크의 조각화의 정확한 복사본을 대상 디스크에 전송 됩니다. 다른 한 디스크에서 조각화를 전송를 방지 하려면 사용 하 여 **복사본** 또는 **xcopy** 여 디스크를 복사 합니다. 때문에 **복사본** 하 고 **xcopy** 파일 순차적으로 복사 된 새 디스크 조각화 되지 않은 합니다.

> [!NOTE]
> 사용할 수 없습니다 **xcopy** 시동 디스크를 복사 합니다.
> -   이해 **diskcopy** 종료 코드

    The following table explains each exit code.  
    |종료 코드|설명|
    |---------|-----------|
    |0|복사 작업의 성공|
    |1|심각 하지 않은 읽기/쓰기 오류가 발생 했습니다.|
    |3|하드 오류가 발생 했습니다.|
    |4|초기화 오류가 발생 했습니다.|

    To process the exit codes that are returned by **diskcomp**, you can use the *ERRORLEVEL* environment variable on the **if** command line in a batch program.

## <a name="BKMK_examples"></a>예제

B 드라이브의 디스크 드라이브의 디스크에 복사 하려면 다음을 입력 합니다.
```
diskcopy b: a:
```
플로피 디스크 드라이브는 하나의 플로피 디스크를 다른 위치로 복사할를 사용 하려면 먼저 C 드라이브에 전환한 다음를 입력 합니다.

a: a: diskcopy

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)