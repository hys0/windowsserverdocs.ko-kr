---
title: 일시 중지
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cab3afc3-d046-432f-a0bf-6282f0099032
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 109d162e8d5c4bdd59871a21f16b6f568df4fbd6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861664"
---
# <a name="pause"></a>일시 중지



일괄 프로그램의 처리를 일시 중단 하 고 다음과 같은 메시지가 표시 됩니다.
```
Press any key to continue . . .
```
이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
pause
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   실행 하는 경우는 **일시 중지** 명령, 다음과 같은 메시지가 나타납니다.  
    ```
    Press any key to continue . . .
    ```  
-   일괄 처리 프로그램을 중지 하려면 CTRL + C를 누를 경우 다음과 같은 메시지가 표시 됩니다.  
    ```
    Terminate batch job (Y/N)?
    ```  
    이 메시지에 대 한 응답에서 (예) Y를 누를 경우 일괄 처리 프로그램이 종료 되 고 컨트롤의 운영 체제에 반환 합니다.
-   삽입할 수 있습니다 합니다 **일시 중지** 명령을 처리 하지 않을 배치 파일의 섹션 앞입니다. 때 **일시 중지** 일시 중단 일괄 프로그램의 처리, CTRL + c를 일괄 처리 프로그램을 중지 하려면 Y를 누릅니다.

## <a name="BKMK_examples"></a>예제

디스크 드라이브 중 하나를 변경 하 라는 메시지를 표시 하는 일괄 처리 프로그램을 만들려면 다음을 입력 합니다.
```
@echo off 
:Begin 
copy a:*.* 
echo Put a new disk into drive A 
pause 
goto begin
```
이 예제에서는 드라이브에서 디스크의 모든 파일을 현재 디렉터리에 복사 합니다. A 드라이브에 새 디스크를 배치 하는 메시지가 표시 됩니다 후 합니다 **일시 중지** 명령은 디스크를 변경 하 고 처리를 다시 시작 하려면 아무 키나 누릅니다 수 있도록 처리를 일시 중지 합니다. 이 일괄 처리 프로그램을 무한 루프로 실행-합니다 **goto 시작** 명령은 배치 파일의 시작 레이블에 명령 인터프리터를 보냅니다. 이 일괄 처리 프로그램을 중지 하려면 CTRL + C를 누릅니다 하 고 Y를 누릅니다.

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)