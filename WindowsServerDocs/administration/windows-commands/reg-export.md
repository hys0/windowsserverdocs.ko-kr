---
title: reg 내보내기
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0ad9526f-1e29-4fa5-9d2d-feaa92f12d7c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5901014511fed0c17a641e1ed183ddbf40dd44c8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80836496"
---
# <a name="reg-export"></a>reg 내보내기



다른 서버에 전송 하기 위해서는 파일에 지정 된 하위 키, 항목 및 로컬 컴퓨터의 값을 복사합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
Reg export KeyName FileName [/y]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<KeyName >|하위 키의 전체 경로 지정합니다. 내보내기 작업이 로컬 컴퓨터 에서만 작동합니다. 키 이름에는 유효한 루트 키를 포함 해야 합니다. 유효한 루트 키가: HKLM, HKCU, HKCR, HKU, 및 HKCC 합니다.|
|\<파일 이름 >|작업 중에 만든 파일의 경로 이름을 지정 합니다. 파일은 확장명이.reg 인이 있어야 합니다.|
|/y|이름의 기존 파일을 덮어씁니다 *FileName* 확인 메시지를 표시 하지 않고 있습니다.|
|/?|에 대 한 도움말을 표시 **reg 내보내기** 명령 프롬프트입니다.|

## <a name="remarks"></a>주의

다음 표에 대 한 반환 값은 **reg 내보내기** 작업 합니다.

|값|설명|
|-----|-----------|
|0|성공|
|1|실패|

## <a name="examples"></a><a name=BKMK_examples></a>예와

모든 하위 키의 내용과 MyApp 키의 값 AppBkUp.reg 파일을 내보내려면 다음을 입력 합니다.
```
reg export HKLM\Software\MyCo\MyApp AppBkUp.reg
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)