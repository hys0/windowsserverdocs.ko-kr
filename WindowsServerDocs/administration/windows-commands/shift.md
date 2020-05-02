---
title: 시프트
description: 일괄 처리 파일에서 일괄 처리 매개 변수의 위치를 변경 하는 shift에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b56574e8-570a-4cc9-bbac-1b94fbf6a47a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 617d7f712ccae13c522bc65db147c12c526b4efb
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721826"
---
# <a name="shift"></a>시프트

배치 파일에서 일괄 처리 매개 변수 위치를 변경합니다.



## <a name="syntax"></a>구문

```
shift [/n <N>]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/n \<n>|부터 변경 지정는 *N*번째 인수 여기서 *N* 모든 값을 0에서 8입니다. 기본적으로 사용 하도록 설정 된 명령 확장 해야 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

- **shift** 명령 일괄 처리 매개 변수 값을 변경 **%0** 통해 **%9** 이전에 각 매개 변수를 복사 하 여-값 **%1** 에 복사 됩니다 **%0**, 의 값 **%2** 에 복사 됩니다 **%1**, 등입니다. 이 임의 개수의 매개 변수에서 동일한 작업을 수행 하는 배치 파일을 작성할 때 유용 합니다.
- 명령 확장을 사용 하는 경우는 **shift** 지원 명령에서 **/n** 명령줄 옵션입니다. **/n** 번째 인수부터 변경 옵션을 지정 합니다. 여기서 **N** 0의에서 값을 8로는 합니다. 예를 들어 **SHIFT/2** 는 **%3** 를 **%2**, **%4** 에 **%3**, 등의 두고 **%0** 및 **%1** 영향을 받지 않습니다. 기본적으로 명령 확장을 사용 합니다.
- 사용할 수는 **shift** 명령을 10 개 이상의 일괄 처리 매개 변수를 받아들일 수 있는 일괄 처리 파일을 만듭니다. 명령줄에서 10 개 이상의 매개 변수를 지정 하는 경우 해당 표시 되는 열 번째 후 (**9**)에 한 번에 이동 된 두 번째 **9**합니다.
- **Shift** 명령은 ** % *** batch 매개 변수에는 영향을 주지 않습니다.
- 더 이전 버전과 **shift** 명령입니다. 구현한 후는 **shift** 명령을 일괄 처리 매개 변수를 복구할 수 없습니다 (**%0**) 하는 이동 전의 합니다.

## <a name="examples"></a>예

Mycopy.bat 라는 샘플 배치 파일에서 다음 줄에 사용 하는 방법을 보여 줍니다 **shift** 일괄 처리 매개 변수 수 있습니다. 이 예제에서는 Mycopy.bat 파일 목록이 특정 디렉터리에 복사합니다. 일괄 처리 매개 변수는 디렉터리 및 파일 이름 인수 별로 표시 됩니다.
```
@echo off 
rem MYCOPY.BAT copies any number of files
rem to a directory.
rem The command uses the following syntax:
rem mycopy dir file1 file2 ... 
set todir=%1
:getfile
shift
if %1== goto end
copy %1 %todir%
goto getfile
:end
set todir=
echo All done
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)