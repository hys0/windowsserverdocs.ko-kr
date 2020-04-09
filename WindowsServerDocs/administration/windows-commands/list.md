---
title: list
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 57b6c8d0-872e-4dba-9715-1db8ab892e98
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d60c42b868a1e9a26e3168e4b489573f9f87e179
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841106"
---
# <a name="list"></a>list



작성자, 섀도 복사본 또는 시스템에 있는 현재 등록 된 섀도 복사본 공급자를 나열 합니다. 매개 변수 없이 사용 하는 경우 **목록** 명령 프롬프트에서 도움말을 표시 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
list writers [metadata | detailed | status]
list shadows {all | set <SetID> | id <ShadowID>}
list providers
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작성자|기록기를 나열합니다. 참조 [작성기 목록](list-writers.md) 구문 및 매개 변수입니다.|
|그림자|영구 및 기존 비영구 섀도 복사본을 나열 합니다. 참조 [그림자 목록](list-shadows.md) 구문 및 매개 변수입니다.|
|공급자|현재 목록 섀도 복사본 공급자를 등록 합니다. 참조 [공급자 나열](list-providers.md) 구문 및 매개 변수입니다.|

## <a name="examples"></a><a name=BKMK_examples></a>예와

모든 섀도 복사본을 나열 하려면 다음을 입력 합니다.
```
list shadows all
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)