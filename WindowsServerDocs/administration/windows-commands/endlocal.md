---
title: endlocal
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 765fae3c-0c0a-4639-99a4-cf613489b949
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f007a9ec1e86093192630011c5197740dfefe922
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719373"
---
# <a name="endlocal"></a>endlocal



배치 파일에서 환경 변경의 지역화를 종료 하 고 해당 전에 환경 변수 값으로 복원 **setlocal** 명령을 실행 합니다.



## <a name="syntax"></a>구문

```
endlocal
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   **endlocal** 스크립트 또는 배치 파일의 외부 명령에는 영향을 주지 않습니다.
-   암시적인 **endlocal** 배치 파일의 끝에 명령 합니다.
-   명령 확장을 사용 하는 경우 (명령 확장을 기본적으로 사용)는 **endlocal** 명령은 명령 확장 (즉, 사용 또는 사용 안 함)의 상태는 해당 전에 복원 **setlocal** 명령이 실행 합니다.

> [!NOTE]
> 명령 확장을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 참조 [Cmd](cmd.md)합니다.

## <a name="examples"></a>예

배치 파일에서 환경 변수를 지역화할 수 있습니다. 예를 들어 다음 프로그램 superapp 일괄 프로그램 네트워크에서 시작 되 고 출력 파일을 고 메모장에서 파일을 표시.
```
@echo off
setlocal
path=g:\programs\superapp;%path%
call superapp>c:\superapp.out
endlocal
start notepad c:\superapp.out
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)