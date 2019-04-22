---
title: color
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f5b67131-d196-45ec-a3f9-b5d9f091fd86
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f8d23cc1bb5739b47c755d90c927cbcf82b8da7f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825024"
---
# <a name="color"></a>color



현재 세션의 명령 프롬프트 창에서 색이 전경색 및 배경색 변경 됩니다. 매개 변수 없이 사용 하는 경우 **color** 기본 명령 프롬프트 창을 전경 및 배경 색을 복원 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
color [[<B>]<F>]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<B>|배경색을 지정합니다.|
|\<F>|전경색을 지정 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   다음 표에서 대 한 값으로 사용할 수 있는 유효한 16 진수 *B* 하 고 *F*합니다.  
    |값|색|
    |-----|-----|
    |0|검정|
    |1|파랑|
    |2|녹색|
    |3|Aqua|
    |4|빨강|
    |5|자주색|
    |6|노랑|
    |7|하얀|
    |8|회색|
    |9|연한 파랑|
    |변수를 잠그기 위한|연한 녹색|
    |B|연한 옥색|
    |C|연한 빨간색|
    |d|옅은 자주|
    |E|밝은 노랑|
    |F|밝은 백서|
-   사이 공백을 넣지 마십시오 *B* 하 고 *F*합니다.
-   하나의 16 진수를 지정 하는 경우 해당 색 전경색으로 사용 됩니다 하 고 배경색 기본 색으로 설정 됩니다.
-   명령 프롬프트 창의 기본 색을 설정 하려면 명령 프롬프트 창의 왼쪽 위 모퉁이 클릭 하 고 **기본값**를 클릭 합니다 **색** 탭을 클릭 합니다 에대한사용하려는색 **텍스트를 화면** 하 고 **배경 화면**합니다.
-   하는 경우 *B* 및 *F* 동일 합니다 **색** ERRORLEVEL 1로 설정 하는 명령 및 전경색 또는 배경색 변경 되지 않습니다.

## <a name="BKMK_examples"></a>예제

명령 프롬프트 창의 배경색을 회색 및 전경색을 빨강으로 변경 하려면 다음을 입력 합니다.
```
color 84
```
밝은 노랑으로 명령 프롬프트 창의 전경색을 변경 하려면 다음을 입력 합니다.
```
color e
```

> [!NOTE]
> 이 예제에서는 백그라운드 하나만 진수 지정 되기 때문에 기본 색으로 설정 됩니다.

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)