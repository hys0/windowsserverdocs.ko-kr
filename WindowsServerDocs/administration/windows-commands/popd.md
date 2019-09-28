---
title: popd
description: 디렉터리를 pushd 명령으로 가장 최근에 저장 한 디렉터리로 변경 하는 방법에 대해 알아봅니다.
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 8a9e0a301a5f8b46e1907a4f43c5ed9247b85f77
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372234"
---
# <a name="popd"></a>popd

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

현재 디렉터리를 **pushd** 명령으로 가장 최근에 저장 한 디렉터리로 변경 합니다.
이 명령을 사용 하는 방법에 대 한 예는 [예제](#BKMK_examples)를 참조 하세요.

## <a name="syntax"></a>구문
```
popd
```

### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명
-   **Pushd** 명령을 사용할 때마다 단일 디렉터리를 사용할 수 있도록 저장 됩니다. 그러나 **pushd** 명령을 여러 번 사용 하 여 여러 디렉터리를 저장할 수 있습니다.
    디렉터리는 가상 스택에 순차적으로 저장 됩니다. **Pushd** 명령을 한 번 사용 하는 경우 명령을 사용 하는 디렉터리가 스택의 맨 아래에 배치 됩니다. 명령을 다시 사용 하는 경우 첫 번째 디렉터리가 첫 번째 디렉터리 위에 배치 됩니다. **Pushd** 명령을 사용할 때마다 프로세스가 반복 됩니다.
    **Popd** 명령을 사용 하 여 현재 디렉터리를 **pushd** 명령으로 가장 최근에 저장 한 디렉터리로 변경할 수 있습니다. **Popd** 명령을 사용 하면 스택의 맨 위에 있는 디렉터리가 스택에서 제거 되 고 현재 디렉터리가 해당 디렉터리로 변경 됩니다. 사용 하는 경우는 **popd** 명령을 다시, 스택에서 다음 디렉터리에서 제거 됩니다.
-   명령 확장을 사용 하도록 설정 하면 **popd** 명령은 **pushd**에서 만든 드라이브 문자 assignations 제거 합니다.

## <a name="BKMK_examples"></a>예와
다음 예에서는 배치 프로그램에서 **pushd** 명령과 **popd** 명령을 사용 하 여 batch 프로그램이 실행 된 디렉터리에서 현재 디렉터리를 변경한 다음 다시 변경 하는 방법을 보여 줍니다.

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

