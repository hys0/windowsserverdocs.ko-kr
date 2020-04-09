---
title: diskcopy
description: Windows 명령 항목-diskcopy는 원본 드라이브의 플로피 디스크 내용을 대상 드라이브의 포맷 되거나 포맷 되지 않은 플로피 디스크로 복사 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5fd21efa-52cc-4e70-a7fe-35125a435106
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 05/07/2018
ms.openlocfilehash: 675694503cab207f05fd6b48e0d17c23196f85d0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80845546"
---
# <a name="diskcopy"></a>diskcopy

원본 드라이브의 플로피 디스크 콘텐츠를 대상 드라이브의 포맷 되거나 포맷 되지 않은 플로피 디스크로 복사 합니다. 매개 변수 없이 사용 하는 경우 **diskcopy** 원본 디스크와 대상 디스크에 현재 드라이브를 사용 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

> [!NOTE]
> 이 명령은 Windows 10에는 포함 되어 있지 않습니다.

## <a name="syntax"></a>구문

```
diskcopy [<Drive1>: [<Drive2>:]] [/v]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<Drive1 >|원본 디스크를 포함 하는 드라이브를 지정 합니다.|
|\<Drive2 >|대상 디스크를 포함 하는 드라이브를 지정 합니다.|
|/v|정보가 올바르게 복사 되었는지 확인 합니다. 이 옵션을 선택 하면 복사 프로세스가 느려집니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>주의

-   디스크 사용

    **Diskcopy** 는 플로피 디스크와 같은 이동식 디스크 에서만 작동 하며 동일한 유형 이어야 합니다. **Diskcopy** 는 하드 디스크와 함께 사용할 수 없습니다. *Drive1* 또는 *Drive2*에 대해 하드 디스크 드라이브를 지정 하는 경우 **diskcopy** 는 다음 오류 메시지를 표시 합니다.  
    ```
    Invalid drive specification
    Specified drive does not exist or is nonremovable
    ```  
    **Diskcopy** 명령은 원본 및 대상 디스크를 삽입 하 라는 메시지를 표시 하 고 계속 하기 전에 키보드의 키를 누를 때까지 기다립니다.

    디스크를 복사한 후에는 **diskcopy** 다음 메시지를 표시 합니다.  
    ```
    Copy another diskette (Y/N)?
    ```  
    Y 키를 누르면 다음 복사 작업을 위해 원본 및 대상 디스크를 삽입 **하 라는 메시지가 표시 됩니다.** **Diskcopy** 프로세스를 중지 하려면 **N**을 누릅니다.

    *Drive2*의 포맷 되지 않은 플로피 디스크에 복사 하는 경우 **에는** *Drive1*의 디스크에 있는 것과 동일한 수의 쪽 및 섹터 수로 디스크의 형식이 지정 됩니다. **Diskcopy** 는 디스크를 포맷 하 고 파일을 복사 하는 동안 다음 메시지를 표시 합니다.  
    ```
    Formatting while copying
    ```  
-   디스크 일련 번호

    원본 디스크에 볼륨 일련 번호가 있는 경우 **diskcopy** 는 대상 디스크에 대 한 새 볼륨 일련 번호를 만들고 복사 작업이 완료 되 면 숫자를 표시 합니다.
-   드라이브 매개 변수 생략

    *Drive2* 매개 변수를 생략 하는 경우 **diskcopy** 는 현재 드라이브를 대상 드라이브로 사용 합니다. 두 드라이브 매개 변수를 모두 생략 하면 **diskcopy** 는 현재 드라이브를 모두 사용 합니다. 현재 드라이브가 *Drive1*와 동일한 경우에는 필요에 따라 **디스크를 교환 하 라는 메시지가** 표시 됩니다.
-   한 드라이브를 사용 하 여 복사

    플로피 디스크 드라이브가 아닌 드라이브 (예: C 드라이브)에서 **diskcopy** 를 실행 합니다. 플로피 디스크 *Drive1* 및 플로피 디스크 *Drive2* 동일한 경우에는 **diskcopy** 는 디스크를 전환 하 라는 메시지를 표시 합니다. 디스크에 사용할 수 있는 메모리 보다 더 많은 정보가 포함 되어 있는 경우에는 **diskcopy** 가 모든 정보를 한 번에 읽을 수 없습니다. **Diskcopy** 는 원본 디스크를 읽고 대상 디스크에 쓴 다음 원본 디스크를 다시 넣으라는 메시지를 표시 합니다. 이 프로세스는 전체 디스크를 복사할 때까지 계속 됩니다.
-   디스크 조각화 방지

    조각화는 디스크에 있는 기존 파일 사이에 사용 되지 않는 디스크 공간의 작은 영역이 있음을 말합니다. 조각화 된 원본 디스크는 파일의 찾기, 읽기 또는 쓰기 프로세스를 늦출 수 있습니다.

    **Diskcopy** 는 대상 디스크에서 원본 디스크를 정확 하 게 복사 하므로 원본 디스크의 조각화는 대상 디스크에 전송 됩니다. 한 디스크에서 다른 디스크로의 조각화를 전송 하지 않도록 하려면 **복사** 또는 **xcopy** 를 사용 하 여 디스크를 복사 합니다. **Copy** 및 **xcopy** 는 파일을 순차적으로 복사 하기 때문에 새 디스크가 조각화 되지 않습니다.

> [!NOTE]
> **Xcopy** 를 사용 하 여 시작 디스크를 복사할 수는 없습니다.

### <a name="understanding-diskcopy-exit-codes"></a>**Diskcopy** 종료 코드 이해

    The following table explains each exit code.
    
    |종료 코드|설명|
    |---------|-----------|
    |0|복사 작업이 성공 했습니다.|
    |1|심각 하지 않은 읽기/쓰기 오류가 발생 했습니다.|
    |3|심각한 하드 오류 발생|
    |4|초기화 오류가 발생 했습니다.|

    To process the exit codes that are returned by **diskcomp**, you can use the *ERRORLEVEL* environment variable on the **if** command line in a batch program.

## <a name="examples"></a><a name=BKMK_examples></a>예와

B 드라이브의 디스크를 드라이브 A의 디스크에 복사 하려면 다음을 입력 합니다.
```
diskcopy b: a:
```
플로피 디스크 드라이브 A를 사용 하 여 플로피 디스크 하나를 다른 디스크에 복사 하려면 먼저 C 드라이브로 전환한 후 다음을 입력 합니다.

diskcopy a: a:

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)