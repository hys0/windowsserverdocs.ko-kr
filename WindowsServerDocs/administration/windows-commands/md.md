---
title: Md
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82162d00-cc34-4776-9e55-4b4836dbd6a9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3751b185677bfee9d0519b9a617bea1df063c1e7
ms.sourcegitcommit: 51e0b575ef43cd16b2dab2db31c1d416e66eebe8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2020
ms.locfileid: "76259078"
---
# <a name="md"></a>Md



디렉터리 또는 하위 디렉터리를 만듭니다.

> [!NOTE]
> 이 명령은 같습니다는 **mkdir** 명령입니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
md [<Drive>:]<Path>
mkdir [<Drive>:]<Path>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<드라이브 >:|새 디렉터리를 만들고 원하는 드라이브를 지정 합니다.|
|\<경로 >|필수입니다. 새 디렉터리의 위치와 이름을 지정합니다. 단일 경로의 최대 길이 파일 시스템에 의해 결정 됩니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

기본적으로 사용 하도록 설정 된 명령 확장을 사용 하면 단일을 사용할 수 있도록 **md** 지정된 된 경로에서 중간 디렉터리를 만드는 명령입니다.

## <a name="BKMK_examples"></a>예제

현재 디렉터리 내에서 Directory1 라는 디렉터리를 만들려면 다음을 입력 합니다.
```
md Directory1
```
루트 디렉터리 내에서 다음 디렉터리 트리 Taxes\Property\Current 명령 확장 사용을 만들려면 다음을 입력 합니다.
```
md \Taxes\Property\Current
```
이전 예제와 같이 하지만 명령 확장을 사용 하지 않도록 설정 하는 루트 디렉터리 안에 Taxes\Property\Current 디렉터리 트리를 만들려면 다음 명령 시퀀스를 입력 합니다.
```
md \Taxes
md \Taxes\Property
md \Taxes\Property\Current
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)

[Cmd](cmd.md)