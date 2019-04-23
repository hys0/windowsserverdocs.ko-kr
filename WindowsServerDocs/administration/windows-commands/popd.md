---
title: popd
description: Pushd 명령에 의해 가장 최근에 저장 된 디렉터리에 디렉터리를 변경 하는 방법에 알아봅니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8a4c52d5-9fd1-4eac-9c0c-5767b25728ed
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 6da6dc9d1fc2d8965f8a081831cb1150375209a4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827464"
---
# <a name="popd"></a>popd

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

가장 최근에 저장 한 디렉터리로 현재 디렉터리를 변경 합니다 **pushd** 명령입니다.
이 명령을 사용 하는 방법의 예제를 참조 하세요 [예제](#BKMK_examples)합니다.

## <a name="syntax"></a>구문
```
popd
```

### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명
-   사용할 때마다 합니다 **pushd** 명령 사용에 대 한 단일 디렉터리에 저장 됩니다. 그러나 사용 하 여 여러 디렉터리를 저장할 수 있습니다 합니다 **pushd** 여러 번 명령입니다.
    디렉터리 가상 스택에 순차적으로 저장 됩니다. 사용 하는 경우는 **pushd** 명령을 사용 하는 디렉터리는 스택의 맨 아래에 배치 되 면 명령입니다. 명령을 다시 사용 하는 경우 두 번째 디렉터리는 첫 번째 위에 배치 됩니다. 프로세스를 사용할 때마다 반복 합니다 **pushd** 명령입니다.
    사용할 수는 **popd** 하 여 가장 최근에 저장 된 디렉터리를 현재 디렉터리를 변경 하는 명령 합니다 **pushd** 명령입니다. 사용 하는 경우는 **popd** 명령, 스택의 맨 위에 디렉터리 스택에서 제거 되 고 현재 디렉터리에는 해당 디렉터리로 변경 됩니다. 사용 하는 경우는 **popd** 명령을 다시, 스택에서 다음 디렉터리에서 제거 됩니다.
-   명령 확장을 사용 하는 경우는 **popd** 명령을 사용 하 여 만든 모든 드라이브 문자 할당 제거 **pushd**합니다.

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

## <a name="additional-references"></a>추가 참조
-   [pushd](pushd.md)
-   [명령줄 구문 키](command-line-syntax-key.md)

