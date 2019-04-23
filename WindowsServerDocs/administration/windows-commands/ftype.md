---
title: ftype
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6fb53cee-9bed-44dd-af5d-bc7cec1dd114
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c29ca0aa027d11fa8f981134e5367021227d3096
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881684"
---
# <a name="ftype"></a>ftype



표시 하거나 파일 이름 확장명 연결에 사용 되는 파일 형식을 수정 합니다. 대입 연산자 없이 사용 되는 경우 (**=**), **ftype** 지정된 된 파일 형식에 대 한 현재 열려 있는 명령 문자열을 표시 합니다. 매개 변수 없이 사용 하는 경우 **ftype** 열려 있는 명령 문자열을 정의 하는 파일 형식이 표시 됩니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
ftype [<FileType>[=[<OpenCommandString>]]]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<FileType>|표시 하거나 변경 하려면 파일 형식을 지정 합니다.|
|\<OpenCommandString>|지정 된 파일 형식의 파일을 열 때 사용 하 여 열려 있는 명령 문자열을 지정 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

다음 표에서 어떻게 **ftype** 열려 있는 명령 문자열 내에서 변수를 대체 합니다.

|변수|대체 값|
|--------|-----------------|
|0 또는 %1|연결을 통해 실행 되 고 파일 이름으로 대체 하 게 합니다.|
|%*|모든 매개 변수를 가져옵니다.|
|%2, %3, ...|첫 번째 매개 변수 (%2), 두 번째 매개 변수 (%3) 등에 가져옵니다.|
|%~\<N>|부터 나머지 매개 변수를 모두 가져옵니다는 *N*번째 매개 변수가 있는 *N* 2에서 9 사이의 숫자가 될 수 있습니다.|

## <a name="BKMK_examples"></a>예제

열려 있는 명령 문자열을 정의 하는 현재 파일 종류를 표시 하려면 다음을 입력 합니다.
```
ftype
```
에 대 한 현재 열려 있는 명령 문자열을 표시 하는 *txtfile* 파일 유형, 유형:
```
ftype txtfile
```
이 명령은 다음과 유사한 출력을 생성합니다.
```
txtfile=%SystemRoot%\system32\NOTEPAD.EXE %1
```
호출 하는 파일 형식에 대 한 열려 있는 명령 문자열을 삭제 하려면 *예제*, 유형:
```
ftype example=
```
하려면.pl 파일 이름 확장명 PerlScript 파일 형식과 연결 하 고 PERL을 실행 하려면 PerlScript 파일 형식을 사용 하도록 설정 합니다. EXE, 다음 명령을 입력 합니다.
```
assoc .pl=PerlScript 
ftype PerlScript=perl.exe %1 %*
```
Perl 스크립트를 호출할 때.pl 파일 이름 확장명을 입력할 필요가 제거 하려면 다음을 입력 합니다.
```
set PATHEXT=.pl;%PATHEXT%
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)