---
title: bitsadmin setvalidationstate
description: 작업 내에서 지정 된 파일의 콘텐츠 유효성 검사 상태를 설정 하는 bitsadmin setvalidationstate에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e8fc8e8c-171c-4681-8057-6986b018e576
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: de6480596b55b3a483076297f32ce52a975915db
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849116"
---
# <a name="bitsadmin-setvalidationstate"></a>bitsadmin setvalidationstate

작업 내에서 지정된 된 파일의 콘텐츠 유효성 검사 상태를 설정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetValidationState <Job> <file index> <true|false> 
```

### <a name="parameters"></a>매개 변수

| 매개 변수  |          설명           |
|------------|--------------------------------|
|    작업     | 작업의 표시 이름 또는 GUID |
| 파일 인덱스 |         0부터 시작          |
|    True    |             False              |

## <a name="examples"></a><a name=BKMK_examples></a>예와

2 파일의 콘텐츠 유효성 검사 상태 라는 작업에 대해 TRUE로 설정 하는 다음 예제에서는 *myJob*합니다.
```
C:\>bitsadmin /SetValidationState myJob 2 TRUE 
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)