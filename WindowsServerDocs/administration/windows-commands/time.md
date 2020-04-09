---
title: time
description: 시스템 시간을 설정 하 고 표시 하는 방법을 알아봅니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1276a257-7283-41da-ae80-fb4cfb311f9d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5b6efff57a512a2e0519b3294c51c073f1f44d8d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80832836"
---
# <a name="time"></a>time



표시 하거나 시스템 시간을 설정 합니다. 매개 변수 없이 사용 하는 경우 **시간** 현재 시스템 시간을 표시 하 고 새 시간을 입력 하 라는 메시지가 표시 됩니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
time [/t | [<HH>[:<MM>[:<SS>]] [am|pm]]]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<HH > [:\<MM > [:\<SS > [.\<NN >]]] [am\|pm]|여기서 지정 된 시간에 시스템 시간을 설정 *HH* (필수) 시간에 *MM* 는 분으로 및 *SS* (초)입니다. *NN* 1/100 초를 지정 하는 것입니다. 경우 **고** 또는 **오후** 를 지정 하지 않으면 **시간** 기본적으로 24 시간 형식을 사용 합니다.|
|/t|새 시간에 대 한 메시지를 표시 하지 않고 현재 시간을 표시 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>주의

-   현재 시간을 변경 하려면 관리자 자격 증명이 있어야 합니다.
-   에 대 한 값을 구분 해야 *HH*, *MM*, 및 *SS* 콜론 (:)으로 합니다. *SS* 및 *NN* 마침표 (.)로 구분 해야 합니다.
-   유효한 *HH* 값은 0-24입니다.
-   유효한 *MM* 및 *SS* 값은 0부터 59까지 합니다.

## <a name="examples"></a><a name="BKMK_examples"></a>예와

명령 확장을 사용 하는 경우 현재 시스템 시간을 표시 하려면 입력 합니다.
```
time /t
```
현재 시스템 시간이 오후 5 시 30 분을 변경 하려면 다음 중 하나를 입력 합니다.
```
time 17:30:00
time 5:30 pm
```
뒤에 새 시간을 입력 하 라는 메시지가 현재 시스템 시간을 표시 하려면 다음을 입력 합니다.
```
The current time is: 17:33:31.35
Enter the new time:
```
현재 시간을 유지 하 고 명령 프롬프트를 반환 하려면 enter 키를 누릅니다. 현재 시간을 변경 하려면 새 시간을 입력 한 다음 ENTER 키를 누릅니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)