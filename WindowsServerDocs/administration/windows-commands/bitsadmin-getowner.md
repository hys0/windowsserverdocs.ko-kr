---
title: bitsadmin getowner
description: '**Bitsadmin getowner** 에 대 한 Windows 명령 항목-지정 된 작업의 소유자를 검색 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5203f84c-a879-4f31-ae3e-7ea74bd63ca5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ab8151ba8b1379c101aa037504ae2021ff0df62f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381453"
---
# <a name="bitsadmin-getowner"></a>bitsadmin getowner

지정 된 작업의 소유자에 대 한 표시 이름 또는 GUID를 표시 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetOwner <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="BKMK_examples"></a>예와

다음 예에서는 이름이 *Mydownloadjob*인 작업의 소유자를 표시 합니다.
```
C:\>bitsadmin /GetOwner myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)