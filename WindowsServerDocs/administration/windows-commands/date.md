---
title: date
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ce6700fb-32f9-4350-a1af-5aee61d4448c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d7328b2b5d3c78fdfd741918d76e26195f0af4a1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378820"
---
# <a name="date"></a>date



표시 하거나 시스템 날짜를 설정 합니다. 매개 변수 없이 사용 하는 경우 **날짜** 설정 현재 시스템 날짜를 표시 하 고 새 날짜를 입력 하 라는 메시지가 표시 됩니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
date [/t | <Month-Day-Year>]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|@no__t-월-일-연도 >|위치, 날짜를 설정 *월* 은 월 (하나 또는 두 개의 자리) *일* 일인지 (하나 또는 두 개의 자리) 및 *년* 은 연도 (2 대 또는 4 자리).|
|/t|입력 하 라는 새로운 날짜 없이 현재 날짜를 표시 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   현재 날짜를 변경 하려면 관리자 자격 증명이 있어야 합니다.
-   에 대 한 값을 구분 해야 *달*, *일*, 및 *년* 이며 마침표 (.), 하이픈 (-) 또는 슬래시 (/) 표시 됩니다.
-   유효한 *달* 값은 1부터 12입니다.
-   유효한 *일* 값은 1부터 31입니다.
-   유효한 *년* 값은 00부터 99 또는 1980에서 2099입니다. 두 자리 숫자를 사용 하면 80부터 99 까지의 값 1980 년에서 1999 년에 해당 합니다.

## <a name="BKMK_examples"></a>예와

명령 확장을 사용 하는 경우 현재 시스템 날짜를 표시 하려면 입력 합니다.
```
date /t
```
2007 년 8 월 3 일을 현재 시스템 날짜를 변경 하려면 다음 중 하나를 입력할 수 있습니다.
```
date 08.03.2007
date 08-03-07
date 8/3/07
```
뒤에 새 날짜를 입력 하 라는 메시지가 현재 시스템 날짜를 표시 하려면 다음을 입력 합니다.
```
The current date is: Mon 04/02/2007
Enter the new date: (mm-dd-yy)
```
현재 날짜를 유지 하 고 명령 프롬프트를 반환 하려면 enter 키를 누릅니다. 현재 날짜를 변경 하려면 새 날짜를 입력 한 다음 ENTER 키를 누릅니다.

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)