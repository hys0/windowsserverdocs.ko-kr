---
title: bitsadmin 캐시 및 deleteurl
description: Windows 명령 항목에 대 한 **bitsadmin 캐시 및 deleteurl** -지정된 된 URL에 대 한 모든 캐시 항목을 삭제 합니다.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: a831c49e1461761cb7466b46e7a5ad8e037f4ec9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816654"
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

## <a name="BKMK_examples"></a>예제

다음 예제에 대 한 모든 캐시 항목을 삭제합니다. https://www.microsoft.com/en/us/default.aspx
```
C:\>bitsadmin /DeleteURL https://www.microsoft.com/en/us/default.aspx 
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)