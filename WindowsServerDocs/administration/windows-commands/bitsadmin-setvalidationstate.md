---
title: bitsadmin setvalidationstate
description: '**Bitsadmin setvalidationstate** 에 대 한 Windows 명령 항목-작업 내에서 지정 된 파일의 콘텐츠 유효성 검사 상태를 설정 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e8fc8e8c-171c-4681-8057-6986b018e576
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 37d7fa3a8a91abf1e7b6ac5a51b6cebd78984a91
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380402"
---
# <a name="bitsadmin-setvalidationstate"></a>bitsadmin setvalidationstate



작업 내에서 지정된 된 파일의 콘텐츠 유효성 검사 상태를 설정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetValidationState <Job> <file index> <true|false> 
```

## <a name="parameters"></a>매개 변수

| 매개 변수  |          설명           |
|------------|--------------------------------|
|    작업     | 작업의 표시 이름 또는 GUID |
| 파일 인덱스 |         0부터 시작          |
|    True    |             False              |

## <a name="BKMK_examples"></a>예와

2 파일의 콘텐츠 유효성 검사 상태 라는 작업에 대해 TRUE로 설정 하는 다음 예제에서는 *myJob*합니다.
```
C:\>bitsadmin /SetValidationState myJob 2 TRUE 
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)