---
title: setlocal
description: 배치 파일에서 환경 변수를 지역화 하기 시작 하는 setlocal에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e4e4b6d3-3f1a-4851-a782-25ee2470e16e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4e990cf931e72bd8f6972db448d24db08c2e5208
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85934610"
---
# <a name="setlocal"></a>setlocal

배치 파일에서 환경 변수의 지역화를 시작합니다. 지역화 일치 될 때까지 계속 **endlocal** 명령이 나 배치 파일의 끝에 도달 했습니다.



## <a name="syntax"></a>구문

```
setlocal [enableextensions | disableextensions] [enabledelayedexpansion | disabledelayedexpansion]
```

## <a name="arguments"></a>인수

|인수|설명|
|--------|-----------|
|enableextensions|일치 하는 때까지 명령 확장을 사용 하면 **endlocal** 하기 전에 설정에 관계 없이 명령이 발견 되는 **setlocal** 명령이 실행 된 합니다.|
|disableextensions|일치 하는 때까지 명령 확장을 사용 하지 않도록 설정 **endlocal** 하기 전에 설정에 관계 없이 명령이 발견 되는 **setlocal** 명령이 실행 합니다.|
|enabledelayedexpansion|일치 하는 때까지 지연된 환경 변수 확장을 사용 하면 **endlocal** 하기 전에 설정에 관계 없이 명령이 발견 되는 **setlocal** 명령이 실행 합니다.|
|disabledelayedexpansion|일치 하는 때까지 지연된 환경 변수 확장을 사용 하지 않도록 설정 **endlocal** 하기 전에 설정에 관계 없이 명령이 발견 되는 **setlocal** 명령이 실행 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   사용 하 여 **setlocal**

    사용 하는 경우 **setlocal** 스크립트 또는 배치 파일을 외부에서 영향을 주지 않습니다.
-   환경 변수 변경

    사용 하 여 **setlocal** 배치 파일을 실행 하는 경우 환경 변수를 변경할 수 있습니다. 실행 한 후에 만들어진 환경 변화 **setlocal** 는 배치 파일에 로컬입니다. Cmd.exe 프로그램 발견 한 경우 이전 설정을 복원 하는 **endlocal** 명령 또는 배치 파일의 끝에 도달 합니다.
-   중첩 명령

    둘 이상의 **setlocal** 또는 **endlocal** 명령을 일괄 프로그램 (즉, 중첩 된 명령).
-   배치 파일에서 명령 확장에 대 한 테스트

    **setlocal** ERRORLEVEL 변수를 설정 하는 명령입니다. {**Enableextensions**  |  **disableextensions**} 또는 {**enabledelayedexpansion**  |  **disabledelayedexpansion**}를 전달 하는 경우 ERRORLEVEL 변수는 **0** (영)으로 설정 됩니다. 그렇지 않으면로 설정 됩니다 **1**합니다. 다음 예제와 같이 확장을 사용할 수 있는 지 확인 하기 위해 배치 스크립트에서이 정보를 사용할 수 있습니다.
    ```
    setlocal enableextensions
    verify other 2>nul
    if errorlevel 1 echo Unable to enable extensions
    ```
    때문에 **cmd** 명령 확장 비활성화 되 면 ERRORLEVEL 변수를 설정 하지 않는 **확인** 명령에 잘못 된 인수를 사용 하는 경우 0이 아닌 값으로 ERRORLEVEL 변수를 초기화 합니다. 또한 사용 하는 경우는 **setlocal** 명령 인수에 {**enableextensions** | **disableextensions**} 또는 {**enabledelayedexpansion** | **disabledelayedexpansion**} ERRORLEVEL 변수 설정 하지 않으므로 및 **1**, 명령 확장을 사용할 수 없습니다.

## <a name="examples"></a>예

다음 예제 스크립트에 표시 된 대로 배치 파일에서 환경 변수를 지역화할 수 있습니다.
```
rem *******Begin Comment**************
rem This program starts the superapp batch program on the network,
rem directs the output to a file, and displays the file
rem in Notepad.
rem *******End Comment**************
@echo off
setlocal
path=g:\programs\superapp;%path%
call superapp>c:\superapp.out
endlocal
start notepad c:\superapp.out
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)