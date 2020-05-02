---
title: rem
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1a45b585-a83c-4ff6-badd-ff40f34cec23
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d115548f15ff45087a771458062da8a3ef919eb3
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722460"
---
# <a name="rem"></a>rem



배치 파일 또는 구성의 레코드 주석 (설명). SYS입니다. 에 주석이 없음이 지정 된 경우 **rem** 세로 간격을 추가 합니다.



## <a name="syntax"></a>구문

```
rem [<Comment>]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<주석>|문자열을 주석으로 포함 하도록 지정 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   **rem** 명령 화면에서 설명을 표시 하지 않습니다. 사용 해야는 **화면 표시** 명령을 일괄 처리 또는 구성 합니다. 화면에 주석을 표시 하려면 SYS 파일입니다.
-   배치 파일 주석에는 리디렉션 문자 (**<** 또는 **>**) 또는 파이프 (**|**)를 사용할 수 없습니다.
-   사용할 수 있지만 **rem** 배치 파일에 세로 간격을 추가 하려면 설명 없이 사용할 수 있습니다 빈 줄. 일괄 처리 프로그램을 처리할 때 빈 줄은 무시 됩니다.

## <a name="examples"></a>예

설명에 대 한 설명 및 세로 간격을 사용 하는 배치 파일을 표시 합니다.
```
@echo off
rem  This batch program formats and checks new disks.
rem  It is named Checknew.bat.
rem
rem echo Insert new disk in Drive B.
pause 
format b: /v chkdsk b: 
```
앞에 설명 주석을 포함 하는 **프롬프트** config에서 명령입니다. SYS 파일을 구성 하려면 다음 줄을 추가 합니다. 시스템 드라이브:
```
rem Set prompt to indicate current directory
prompt $p$g
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)