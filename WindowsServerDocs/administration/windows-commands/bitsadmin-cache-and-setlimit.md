---
title: bitsadmin 캐시 및 setlimit
description: '**Bitsadmin cache 및 setlimit** 의 Windows 명령 항목-캐시 크기 제한을 설정 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 46578835-d5ce-423b-be4d-62ddb9e1908d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 88a10ce8599202e237daa6822cf62806d3c21429
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381944"
---
# <a name="bitsadmin-cache-and-setlimit"></a>bitsadmin 캐시 및 setlimit



캐시 크기 제한을 설정합니다.

## <a name="syntax"></a>구문

```
bitsadmin /Cache /SetLimit Percent
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|Percent|총 하드 디스크 공간의 백분율로 정의 된 캐시 제한...|

## <a name="BKMK_examples"></a>예와

다음 예제에서는 캐시 크기 50%를 제한합니다.
```
C:\>bitsadmin /Cache /SetLimit 50 
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)