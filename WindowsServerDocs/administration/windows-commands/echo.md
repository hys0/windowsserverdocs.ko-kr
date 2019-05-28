---
title: echo
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fb9fcd0f-5e73-4504-aa95-78204e1a79d3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: eb5c9650b95703f1316e6f5f179b910d22574f68
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/25/2019
ms.locfileid: "66222961"
---
# <a name="echo"></a>echo



메시지를 표시 하거나 명령 에코 기능의 해제 하거나 설정 합니다. 매개 변수 없이 사용 하는 경우 **echo** 현재 에코 설정을 표시 합니다.

이 명령을 사용하는 방법의 예는 [예](#examples)를 참조하세요.

## <a name="syntax"></a>구문

```
echo [<Message>]
echo [on | off]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|[에서 \| off]|또는 명령 에코 기능의 해제를 설정 합니다. 기본적으로 켜져 명령 에코 합니다.|
|\<Message>|화면에 표시할 텍스트를 지정 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   합니다 **echo** *메시지* 명령은 특히 유용 **echo** 해제 됩니다. 여러 줄 메시지를 표시 하려면 모든 명령을 표시 하지 않고는 여러 **echo** *메시지* 후 명령는 **오프 에코** 명령을 프로그램 일괄 처리 프로그램입니다.
-   때 **echo** 꺼져, 명령 프롬프트 명령 프롬프트 창에 나타나지 않습니다. 명령 프롬프트를 표시 하려면 입력 **화면 표시 합니다.**
-   배치 파일에서 사용 하는 경우 **화면 표시** 및 **오프 에코** 명령 프롬프트에서 설정 하는 데 영향을 주지 않습니다.
-   배치 파일에서 특정 명령 출력을 방지 하려면 삽입는 at 기호 (@) 명령 앞에 있습니다. 배치 파일에서 모든 명령 에코를 방지 하려면 포함는 **오프 에코** 파일의 시작 부분에 명령 합니다.
-   파이프를 표시 하려면 ( **|** ) 또는 리디렉션 문자 ( **<** 또는 **>** ) 사용 하는 **echo**, 리디렉션 또는 파이프 문자 바로 앞에 캐럿 (^)를 사용 하 여 (예를 들어 **^|** , **^>** , 또는 **^<** ). 캐럿을 표시 하려면 두 캐럿 연속으로 입력 합니다 ( **^^** ).

## <a name="examples"></a>예

현재 표시 하려면 **echo** 설정에 입력 합니다.
```
echo
```
화면에 빈 줄을 에코를 하려면 다음을 입력 합니다.
```
echo.
```

> [!NOTE]
> 마침표 앞에 공백을 포함 하지 마십시오. 그렇지 않으면 기간에 빈 줄 대신 표시 됩니다.

방지 하기 위해 명령 프롬프트에서 명령을 에코를 입력 합니다.
```
echo off 
```

> [!NOTE]
> 때 **echo** 꺼져, 명령 프롬프트 명령 프롬프트 창에 나타나지 않습니다. 명령 프롬프트를 다시 표시 하려면 다음을 입력 **화면 표시**합니다.

배치 파일에서 모든 명령을 방지 하기 위해 (포함 하는 **오프 에코** 명령)에서 일괄 처리 파일 형식의 첫 번째 줄에서 화면에 표시:
```
@echo off
```
사용할 수는 **echo** 의 일부분으로 명령은 **경우** 문입니다. 예를 들어를 이러한 파일을 찾지 못하면 에코 메시지 및.rpt 파일 이름 확장명과 파일에 대 한 현재 디렉터리를 검색 하려면 다음을 입력 합니다.
```
if exist *.rpt echo The report has arrived.
```
다음 배치 파일.txt 파일 이름 확장명을 사용 하 여 파일에 대 한 현재 디렉터리를 검색 하 고 검색 결과 나타내는 메시지를 표시 합니다.
```
@echo off
if not exist *.txt (
echo This directory contains no text files.
) else (
   echo This directory contains the following text files:
   echo.
   dir /b *.txt
   )
```
배치 파일을 실행할 때.txt 파일이 발견 되 면 다음 메시지가 표시 됩니다.
```
This directory contains no text files.
```
.Txt 파일은 배치 파일을 실행 하는 경우 발견 되 면 다음과 같은 출력이 표시 됩니다 (이 예에서는 File1.txt, File2.txt, 및 존재 File3.txt 파일 가정):
```
This directory contains the following text files:
File1.txt
File2.txt
File3.txt
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)
