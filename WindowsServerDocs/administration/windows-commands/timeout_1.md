---
title: 제한 시간
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e26b4a84-0e30-46e1-aa10-0667b7d3cb4c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3997399b732c494050797c83a0a52938574986bd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830174"
---
# <a name="timeout"></a>제한 시간



지정 된 기간 (초)에 대 한 명령 처리기를 일시 중지합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
timeout /t <TimeoutInSeconds> [/nobreak] 
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/t \<TimeoutInSeconds>|명령 프로세서 처리를 계속 하기 전에 대기 하는 10 진수 (-1에서 99999) 사이 시간 (초)을 지정 합니다. 값-1 하면 컴퓨터의 키 입력을 무기한 대기 합니다.|
|/nobreak|사용자 키 입력을 무시 하도록 지정 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   **timeout** 명령은 배치 파일에서 일반적으로 사용 됩니다.
-   사용자 키 입력 제한 시간 만료 되지 않은 경우에 즉시 명령 프로세서 실행을 계속 합니다.
-   와 함께에서 사용 하는 경우는 **절전** 명령을 **제한 시간** 비슷합니다는 **일시 중지** 명령입니다.

## <a name="BKMK_examples"></a>예제

명령 프로세서를 10 초 동안 일시 중지 하려면 다음을 입력 합니다.
```
timeout /t 10
```
명령 프로세서에 100 초 동안 일시 중지 하 고 모든 키 입력을 무시 하려면 다음을 입력 합니다.
```
timeout /t 100 /nobreak
```
키를 누를 때까지 무한정 명령 프로세서 일시 중지 하려면 다음을 입력 합니다.
```
timeout /t -1
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)
