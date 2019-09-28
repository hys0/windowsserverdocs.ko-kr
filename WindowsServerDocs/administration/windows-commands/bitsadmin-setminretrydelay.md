---
title: bitsadmin setminretrydelay
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ce8674ca-6cc5-4bb2-8dda-7dfbb1cd6830
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 379dfa8bfdc48969f268fd1c9544d3bee8bbe646
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380507"
---
# <a name="bitsadmin-setminretrydelay"></a>bitsadmin setminretrydelay

임시 오류가 발생 한 후 BITS에서 파일 전송을 시도 하기 전에 대기 하는 최소 시간 (초)을 설정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetMinRetryDelay <Job> <RetryDelay>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|Retrydelay는|시간 (초)로 표현 된 숫자입니다.|

## <a name="BKMK_examples"></a>예와

다음 예제에서는 명명 된 작업에 대 한 최소 재시도 지연 *myDownloadJob* 35 초입니다.
```
C:\>bitsadmin /SetMinRetryDelay myDownloadJob 35
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)