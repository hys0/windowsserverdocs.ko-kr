---
title: bitsadmin getmaxdownloadtime
description: '**Bitsadmin getmaxdownloadtime** 에 대 한 Windows 명령 항목-다운로드 제한 시간 (초)을 검색 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cdce64f6-7125-489d-be3c-4af1dfc8c46a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 39a19f86e97c1a525b5beb0c5f3b23dff349cb19
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381582"
---
# <a name="bitsadmin-getmaxdownloadtime"></a>bitsadmin getmaxdownloadtime

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

다운로드 제한 시간 (초)을 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetMaxDownloadtime <Job> 
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------|--------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="remarks"></a>설명

-   N\/A

## <a name="BKMK_examples"></a>예와
다음 예제에서는 *Mydownloadjob* 이라는 작업의 최대 다운로드 시간 (초)을 가져옵니다.

```
C:\>bitsadmin /GetMaxDownloadtime myDownloadJob
```

## <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)


