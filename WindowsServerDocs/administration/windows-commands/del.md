---
title: del
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 346eede2-2085-44f5-9936-6877b5d5a833
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a1c2756e53d9f047160ddd037b3868e47d6e3181
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822994"
---
# <a name="del"></a>del



하나 이상의 파일을 삭제합니다. 이 명령은 같습니다는 **지우기** 명령입니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
del [/p] [/f] [/s] [/q] [/a[:]<Attributes>] <Names>
erase [/p] [/f] [/s] [/q] [/a[:]<Attributes>] <Names>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<이름 >|하나 이상의 파일 또는 디렉터리 목록을 지정합니다. 여러 파일을 삭제 하려면 와일드 카드를 사용할 수 있습니다. 디렉터리를 지정 하는 경우 디렉터리 내의 모든 파일이 삭제 됩니다.|
|/p|지정된 된 파일을 삭제 하기 전에 확인 메시지를 표시 합니다.|
|/f|읽기 전용 파일을 강제로 삭제 합니다.|
|/s|지정 된 현재 디렉터리와 모든 하위 디렉터리에서 파일을 삭제 합니다. 삭제 될 파일의 이름을 표시 됩니다.|
|/q|자동 모드를 지정합니다. 삭제 확인 필요 하지 않습니다.|
|/a[:]\<Attributes>|다음과 같은 파일 특성에 따라 파일을 삭제 합니다.</br>**r** 읽기 전용 파일</br>**h** 숨김 파일</br>**i** 하지 인덱싱된 파일의 내용</br>**s** 시스템 파일</br>**** 기록 파일</br>**l** 재분석 지점</br>-의미 하는 접두사 'not'|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

> [!CAUTION]
> 사용 하는 경우 **del** 디스크에서 파일을 삭제 하려면 사용자는 복구할 수 없습니다.
-   사용 하는 경우 **/p**하십시오 **del** 파일의 이름을 표시 하 고 다음 메시지를 전송 합니다.

    `FileName, Delete (Y/N)?`

    삭제를 확인 하려면 Y를 누릅니다. 취소 하려면 다음 파일 이름 지정 (즉, 지정한 경우 파일 그룹), 삭제 및 표시를 누릅니다 명사. 중지 하는 **del** 명령, CTRL + C를 누릅니다.
-   명령 확장을 사용 하지 않도록 설정 하는 경우 **/s** 삭제 되는 파일의 이름을 표시 하는 대신 발견 되지 않은 모든 파일의 이름이 표시 됩니다 (즉, 동작은 역순입니다).
-   폴더를 지정 하는 경우 *이름*, 폴더에 파일을 모두 삭제 됩니다. 예를 들어, 다음 명령을 모든 \Work 폴더의 파일을 삭제합니다.  
    ```
    del \work
    ```  
-   와일드 카드를 사용할 수 있습니다 (**&#42;** 하 고 **?**)를 한 번에 둘 이상의 파일을 삭제 합니다. 그러나 파일을 실수로 삭제를 방지 하려면 사용할지 신중 하 게 된 와일드 카드는 **del** 명령입니다. 예를 들어, 다음 명령을 입력 합니다.  
    ```
    del *.*
    ```  
    합니다 **del** 명령에 다음과 같은 메시지가 표시 됩니다.

    `Are you sure (Y/N)?`

    모든 현재 디렉터리에 파일을 삭제 하려면 Y를 누릅니다 하 고 ENTER를 누릅니다. 삭제를 취소 하려면 N 키를 눌러 다음 ENTER 키를 누릅니다.

> [!NOTE]
> 와일드 카드 문자를 사용 하기 전에 **del** 명령와 같은 와일드 카드 문자를 사용 하 여는 **dir** 명령을 삭제 하 여 모든 파일을 나열 합니다.
-   **del** 다른 매개 변수와 함께 명령을 복구 콘솔에서 사용할 수 있습니다.

## <a name="BKMK_examples"></a>예제

C 드라이브에 Test 라는 폴더에 있는 모든 파일을 삭제 하려면 다음 중 하나를 입력 합니다.
```
del c:\test
del c:\test\*.*
```
현재 디렉터리에서.bat 파일 이름 확장명을 사용 하 여 모든 파일을 삭제 하려면 다음을 입력 합니다.
```
del *.bak
```
현재 디렉터리의 모든 읽기 전용 파일을 삭제 하려면 다음을 입력 합니다.
```
del /a:r *.*
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)