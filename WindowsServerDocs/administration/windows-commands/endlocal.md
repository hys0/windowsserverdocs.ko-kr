---
title: endlocal
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 765fae3c-0c0a-4639-99a4-cf613489b949
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 16d2b7b445a2220a10f88f21029948ed10ee96e4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377566"
---
# <a name="endlocal"></a>endlocal



배치 파일에서 환경 변경의 지역화를 종료 하 고 해당 전에 환경 변수 값으로 복원 **setlocal** 명령을 실행 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
endlocal
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   **endlocal** 스크립트 또는 배치 파일의 외부 명령에는 영향을 주지 않습니다.
-   암시적인 **endlocal** 배치 파일의 끝에 명령 합니다.
-   명령 확장을 사용 하는 경우 (명령 확장을 기본적으로 사용)는 **endlocal** 명령은 명령 확장 (즉, 사용 또는 사용 안 함)의 상태는 해당 전에 복원 **setlocal** 명령이 실행 합니다.

> [!NOTE]
> 명령 확장을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 참조 [Cmd](cmd.md)합니다.

## <a name="BKMK_examples"></a>예와

배치 파일에서 환경 변수를 지역화할 수 있습니다. 예를 들어 다음 프로그램 superapp 일괄 프로그램 네트워크에서 시작 되 고 출력 파일을 고 메모장에서 파일을 표시.
```
@echo off
setlocal
path=g:\programs\superapp;%path%
call superapp>c:\superapp.out
endlocal
start notepad c:\superapp.out
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)