---
title: bitsadmin 캐시 및 deleteurl
description: '**Bitsadmin cache 및 deleteurl** 에 대 한 Windows 명령 항목-지정 된 URL에 대 한 모든 캐시 항목을 삭제 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e108b76b-fae9-4c16-bf4c-d74c9f025953
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 869d3bc0f011cc82aaea9b7468667964051e1c00
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382062"
---
# <a name="bitsadmin-cache-and-deleteurl"></a>bitsadmin 캐시 및 deleteurl



지정된 된 URL에 대 한 모든 캐시 항목을 삭제합니다.

## <a name="syntax"></a>구문

```
bitsadmin /DeleteURL url
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|url|원격 파일을 식별 하는 Uniform Resource Locator|

## <a name="BKMK_examples"></a>예와

다음 예에서는에 대 한 모든 캐시 항목을 삭제 https://www.microsoft.com/en/us/default.aspx
```
C:\>bitsadmin /DeleteURL https://www.microsoft.com/en/us/default.aspx 
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)