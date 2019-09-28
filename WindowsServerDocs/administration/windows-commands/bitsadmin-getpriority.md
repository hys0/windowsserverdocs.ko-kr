---
title: bitsadmin getpriority
description: '**Bitsadmin getpriority** 에 대 한 Windows 명령 항목-지정 된 작업의 우선 순위를 검색 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 0b8914f27c690aa9bb9cbf30430b3edf55f2eb92
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381435"
---
# <a name="bitsadmin-getpriority"></a>bitsadmin getpriority

지정된 된 작업의 우선 순위를 검색합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetPriority <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="remarks"></a>설명

우선 순위는 **전경**, **높음**, **보통**, **낮음**또는 **알 수 없음**입니다.

## <a name="BKMK_examples"></a>예와

다음 예제에서는 명명 된 작업에 대 한 우선 순위를 검색 *myDownloadJob*합니다.
```
C:\>bitsadmin /GetPriority myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)
