---
title: bitsadmin getvalidationstate
description: '**Bitsadmin getvalidationstate** 에 대 한 Windows 명령 항목-작업 내에서 지정 된 파일의 콘텐츠 유효성 검사 상태를 보고 합니다. '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6ada3f1f-9967-4262-9d22-ed641e23f516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ca4269a596010258edd0479f5a7e9844bc9c98df
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381263"
---
# <a name="bitsadmin-getvalidationstate"></a>bitsadmin getvalidationstate



작업 내에서 지정된 된 파일의 콘텐츠 유효성 검사 상태를 보고합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetValidationState <Job> <file index> 
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|파일 인덱스|0부터 시작|

## <a name="BKMK_examples"></a>예와

다음 예제에서는 명명 된 작업 내에서 2 파일의 콘텐츠 유효성 검사 상태를 가져옵니다 *myJob*합니다.
```
C:\>bitsadmin /GetValidationState myJob 1
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)