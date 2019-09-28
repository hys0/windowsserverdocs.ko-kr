---
title: bitsadmin gettype
description: '**Bitsadmin gettype** 에 대 한 Windows 명령 항목-지정 된 작업의 작업 유형을 검색 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bec16f04-3e95-4587-889e-3de6ad03c9c8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ca46cb813809621f4fa79b3265198206729a392c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381343"
---
# <a name="bitsadmin-gettype"></a>bitsadmin gettype



지정된 된 작업의 작업 유형을 검색합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetType <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="remarks"></a>설명

형식을 다운로드를 사용할 수 업로드-회신 또는 알 수 없는 업로드 합니다.

## <a name="BKMK_examples"></a>예와

다음 예제에서는 명명 된 작업에 대 한 작업 유형을 검색 *myDownloadJob*합니다.
```
C:\>bitsadmin /GetType myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)