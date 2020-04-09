---
title: goto
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e0de1458-1f78-48ff-a746-c285a945a510
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 928a9031a7f86261789676257afe95ffc3be8a99
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80842566"
---
# <a name="goto"></a>goto



Cmd.exe를 지정 된 행에 배치 프로그램에 지시합니다. 일괄 처리 프로그램 내에서 **goto** 레이블로 식별 하는 선 명령 처리를 보냅니다. 레이블이 발견 되 면 처리가 계속 다음 줄에서 시작 하는 명령을 사용 하 여 시작 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
goto <Label> 
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<레이블 >|일괄 처리 프로그램에서 레이블로 사용 되는 텍스트 문자열을 지정 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>주의

-   명령 확장 사용

    명령 확장을 사용 (기본값) 하 고 대상 레이블이 **EOF**인 **goto** 명령을 사용 하는 경우 현재 배치 스크립트 파일의 끝으로 제어를 전송 하 고 레이블을 정의 하지 않고 배치 스크립트 파일을 종료 합니다. 사용 하는 경우 **goto** 와 **: EOF** 레이블 레이블 앞에 콜론을 삽입 해야 합니다. 예를 들면 다음과 같습니다.  
    ```
    goto:EOF
    ```  
-   유효한 *레이블* 값 사용

    *레이블* 매개 변수에 공백을 사용할 수 있지만 다른 구분 기호 (예: 세미콜론 또는 등호)를 포함할 수 없습니다.
-   일괄 처리 프로그램 *에서 레이블과 레이블 일치*

    지정 하는 *레이블* 값은 batch 프로그램의 레이블과 일치 해야 합니다. 일괄 프로그램 내에서 레이블을 콜론 (:)로 시작 해야 합니다. 줄이 콜론으로 시작 하는 경우 레이블을으로 처리 됩니다 하 고 해당 줄의 모든 명령이 무시 됩니다. 일괄 프로그램에서 지정 하는 레이블을 포함 하지 않습니다 *레이블*, 일괄 프로그램이 중지 하 고 다음 메시지가 표시 됩니다.  
    ```
    Label not found
    ```  
-   조건 작업에 **goto** 사용

    다른 명령과 함께 **goto** 를 사용 하 여 조건부 작업을 수행할 수 있습니다. 사용 하는 방법에 대 한 자세한 내용은 **goto** 조건부 작업에 대 한 참조는 [경우](if.md) 명령 참조 합니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와

A: 드라이브에서 디스크 시스템 디스크를 설정 하는 다음 일괄 처리 프로그램입니다. 작업이 성공한 경우의 **goto** 명령은 프로세싱을 **: 끝** 레이블:
```
echo off
format a: /s
if not errorlevel 1 goto end
echo An error occurred during formatting.
:end
echo End of batch program. 
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

[Cmd](cmd.md)

[때](if.md)