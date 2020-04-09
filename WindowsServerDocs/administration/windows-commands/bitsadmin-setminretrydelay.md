---
title: bitsadmin setminretrydelay
description: BITS가 파일을 전송 하기 전에 일시적 오류가 발생 한 후 대기 하는 최소 시간 (초)을 설정 하는 bitsadmin setminretrydelay에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ce8674ca-6cc5-4bb2-8dda-7dfbb1cd6830
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fb2fe4c6d0e4f90c6ec49fa1da63404393d4f634
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849366"
---
# <a name="bitsadmin-setminretrydelay"></a>bitsadmin setminretrydelay

임시 오류가 발생 한 후 BITS에서 파일 전송을 시도 하기 전에 대기 하는 최소 시간 (초)을 설정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetMinRetryDelay <Job> <RetryDelay>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|Retrydelay는|시간 (초)로 표현 된 숫자입니다.|

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 명명 된 작업에 대 한 최소 재시도 지연 *myDownloadJob* 35 초입니다.
```
C:\>bitsadmin /SetMinRetryDelay myDownloadJob 35
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)