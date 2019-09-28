---
title: bitsadmin getminretrydelay
description: '**Bitsadmin getminretrydelay** 에 대 한 Windows 명령 항목-파일을 전송 하기 전에 일시적 오류가 발생 한 후 서비스가 대기 하는 시간 (초)을 검색 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 54f0abab-c129-40ed-a603-50f464d26011
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0a2bde6340034e48b97b4c86f48a3b2ef72560a5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381554"
---
# <a name="bitsadmin-getminretrydelay"></a>bitsadmin getminretrydelay



서비스에서 임시 오류가 발생 한 후 파일을 전송 하기 전에 대기 하는 시간 (초)을 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetMinRetryDelay <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="BKMK_examples"></a>예와

다음 예에서는 이름이 *Mydownloadjob*인 작업의 최소 다시 시도 지연을 검색 합니다.
```
C:\>bitsadmin /GetMinRetryDelay myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)