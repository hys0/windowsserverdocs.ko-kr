---
title: 확인
description: 확인에 대 한 Windows 명령 항목. 파일이 디스크에 올바르게 기록 되었는지 확인할 지 여부를 **cmd** 에 알려 줍니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: dfe8bc91-d948-4e47-84ad-a79a60506ffa
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 91a0777999a604a23e2de83eda6b89c926cb241c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830056"
---
# <a name="verify"></a>확인



지시 **cmd** 파일이 디스크에 올바르게 쓰였는지 확인 하려면. 매개 변수 없이 사용 하는 경우 **확인** 현재 설정이 표시 됩니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
verify [on | off]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|[on \| 꺼짐]|스위치는 **확인** 설정 하거나 해제 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="examples"></a><a name=BKMK_examples></a>예와

현재 표시 하려면 **확인** 설정에 입력 합니다.
```
verify
```
설정 하는 **확인** 설정에 입력 합니다.
```
Verify on
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)