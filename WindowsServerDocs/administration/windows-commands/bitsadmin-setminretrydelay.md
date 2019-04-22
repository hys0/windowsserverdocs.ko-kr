---
title: bitsadmin setminretrydelay
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 640492cf690a934e3e3b8d0ecf8ca7a0d6a7dc2f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813084"
---
# <a name="bitsadmin-setminretrydelay"></a>bitsadmin setminretrydelay

BITS는 일시적인 오류가 발생 하는 파일을 전송 하기 전에 대기 하는 초 단위로 시간의 최소 길이 설정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetMinRetryDelay <Job> <RetryDelay>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|Retrydelay는|시간 (초)로 표현 된 숫자입니다.|

## <a name="BKMK_examples"></a>예제

다음 예제에서는 명명 된 작업에 대 한 최소 재시도 지연 *myDownloadJob* 35 초입니다.
```
C:\>bitsadmin /SetMinRetryDelay myDownloadJob 35
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)