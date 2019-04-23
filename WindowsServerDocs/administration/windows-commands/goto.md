---
title: goto
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e0de1458-1f78-48ff-a746-c285a945a510
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f1ad0190519d58bd879ae391f378d800760c204f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857534"
---
# <a name="goto"></a>goto



Cmd.exe를 지정 된 행에 배치 프로그램에 지시합니다. 일괄 처리 프로그램 내에서 **goto** 레이블로 식별 하는 선 명령 처리를 보냅니다. 레이블이 발견 되 면 처리가 계속 다음 줄에서 시작 하는 명령을 사용 하 여 시작 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
goto <Label> 
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<Label>|일괄 처리 프로그램에서 레이블로 사용 되는 텍스트 문자열을 지정 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   명령 확장 사용

    명령 확장을 사용 (기본값)를 사용 하는 **goto** 의 대상 레이블에 명령과 **: EOF**, 현재 일괄 처리 스크립트 파일의 끝에 제어를 전송 하 고 배치 스크립트 파일을 종료 레이블을 받아들입니다. 사용 하는 경우 **goto** 와 **: EOF** 레이블 레이블 앞에 콜론을 삽입 해야 합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  
    ```
    goto:EOF
    ```  
-   유효한를 사용 하 여 *레이블* 값

    에 공백을 사용할 수는 *레이블* 수 있지만 매개 변수 (예를 들어, 세미콜론 또는 등호) 다른 구분 기호를 포함할 수 없습니다.
-   일치 *레이블* 일괄 프로그램의 레이블과

    합니다 *레이블* 지정 하는 값은 일괄 처리 프로그램의 레이블과 일치 해야 합니다. 일괄 프로그램 내에서 레이블을 콜론 (:)로 시작 해야 합니다. 줄이 콜론으로 시작 하는 경우 레이블을으로 처리 됩니다 하 고 해당 줄의 모든 명령이 무시 됩니다. 일괄 프로그램에서 지정 하는 레이블을 포함 하지 않습니다 *레이블*, 일괄 프로그램이 중지 하 고 다음 메시지가 표시 됩니다.  
    ```
    Label not found
    ```  
-   사용 하 여 **goto** 조건부 작업에 대 한

    사용할 수 있습니다 **goto** 조건부 작업을 수행 하려면 다른 명령을 사용 합니다. 사용 하는 방법에 대 한 자세한 내용은 **goto** 조건부 작업에 대 한 참조는 [경우](if.md) 명령 참조 합니다.

## <a name="BKMK_examples"></a>예제

A: 드라이브에서 디스크 시스템 디스크를 설정 하는 다음 일괄 처리 프로그램입니다. 작업이 성공한 경우의 **goto** 명령은 프로세싱을 **: 끝** 레이블:
```
echo off
format a: /s
if not errorlevel 1 goto end
echo An error occurred during formatting.
:end
echo End of batch program. 
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)

[Cmd](cmd.md)

[If](if.md)