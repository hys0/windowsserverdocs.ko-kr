---
title: reg 내보내기
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0ad9526f-1e29-4fa5-9d2d-feaa92f12d7c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d7aeddb4b069b1baf5b8f7aaea2730a2b25bdad7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889654"
---
# <a name="reg-export"></a>reg 내보내기



다른 서버에 전송 하기 위해서는 파일에 지정 된 하위 키, 항목 및 로컬 컴퓨터의 값을 복사합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
Reg export KeyName FileName [/y]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<KeyName>|하위 키의 전체 경로 지정합니다. 내보내기 작업이 로컬 컴퓨터 에서만 작동합니다. 키 이름에는 유효한 루트 키를 포함 해야 합니다. 유효한 루트 키가 있습니다. HKLM, HKCU, HKCR, HKU, and HKCC.|
|\<FileName>|작업 중에 만든 파일의 경로 이름을 지정 합니다. 파일은 확장명이.reg 인이 있어야 합니다.|
|/y|이름의 기존 파일을 덮어씁니다 *FileName* 확인 메시지를 표시 하지 않고 있습니다.|
|/?|에 대 한 도움말을 표시 **reg 내보내기** 명령 프롬프트입니다.|

## <a name="remarks"></a>설명

다음 표에 대 한 반환 값은 **reg 내보내기** 작업 합니다.

|값|Description|
|-----|-----------|
|0|성공|
|1|실패|

## <a name="BKMK_examples"></a>예제

모든 하위 키의 내용과 MyApp 키의 값 AppBkUp.reg 파일을 내보내려면 다음을 입력 합니다.
```
reg export HKLM\Software\MyCo\MyApp AppBkUp.reg
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)