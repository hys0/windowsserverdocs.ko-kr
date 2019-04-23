---
title: pushd
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 396bc545-0f41-473e-b0ac-76fbbb74d390
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 548f39921c1f6aa3837e6443e396922396eb84f7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887464"
---
# <a name="pushd"></a>pushd



사용 하 여 현재 디렉터리에 저장는 **popd** 명령 및 지정된 된 디렉터리에 다음 변경 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
pushd [<Path>]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<Path>|현재 디렉터리에 디렉터리를 지정 합니다. 이 명령은 상대 경로 지원 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   사용할 때마다 합니다 **pushd** 명령 사용에 대 한 단일 디렉터리에 저장 됩니다. 그러나 사용 하 여 여러 디렉터리를 저장할 수 있습니다 합니다 **pushd** 여러 번 명령입니다.

    디렉터리 가상 스택에 순차적으로 저장 됩니다. 사용 하는 경우는 **pushd** 명령을 사용 하는 디렉터리는 스택의 맨 아래에 배치 되 면 명령입니다. 명령을 다시 사용 하는 경우 두 번째 디렉터리는 첫 번째 위에 배치 됩니다. 프로세스를 사용할 때마다 반복 합니다 **pushd** 명령입니다.

    사용할 수는 **popd** 하 여 가장 최근에 저장 된 디렉터리를 현재 디렉터리를 변경 하는 명령 합니다 **pushd** 명령입니다. 사용 하는 경우는 **popd** 명령, 스택의 맨 위에 디렉터리 스택에서 제거 되 고 현재 디렉터리에는 해당 디렉터리로 변경 됩니다. 사용 하는 경우는 **popd** 명령을 다시, 스택에서 다음 디렉터리에서 제거 됩니다.
-   명령 확장을 사용 하는 경우는 **pushd** 명령에는 네트워크 경로 로컬 드라이브 문자 및 경로입니다.
-   네트워크 경로 지정 하는 경우는 **pushd** 명령은 지정 된 네트워크 리소스를 일시적으로 가장 높은 사용 하지 않는 드라이브 문자 (z:부터 시작)를 할당 합니다. 다음 명령은 새로 할당 된 드라이브에 지정된 된 디렉터리에 현재 드라이브 및 디렉터리를 변경합니다. 사용 하는 경우는 **popd** 명령을 명령 확장을 사용 하도록 설정 된 **popd** 명령을 제거 하 여 만든 드라이브 문자 할당 **pushd**합니다.

## <a name="BKMK_examples"></a>예제

다음 예제에서는 사용 하는 방법을 보여 줍니다는 **pushd** 명령 및 **popd** 일괄 프로그램 실행 되 고 다음 다시 변경 하는 것에서 현재 디렉터리를 변경 하려면 일괄 프로그램에서 명령을 합니다.
```
@echo off
rem This batch file deletes all .txt files in a specified directory
pushd %1
del *.txt
popd
cls
echo All text files deleted in the %1 directory
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)

[popd](popd.md)