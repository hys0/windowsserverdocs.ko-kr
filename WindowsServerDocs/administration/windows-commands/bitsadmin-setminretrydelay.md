---
title: bitsadmin setminretrydelay
description: BITS가 임시 오류가 발생 한 후 파일을 전송 하기 전에 대기 하는 최소 시간 (초)을 설정 하는 bitsadmin setminretrydelay 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ce8674ca-6cc5-4bb2-8dda-7dfbb1cd6830
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7fc54b4466d8f0bac12bd42ebf6c5e2c66087a15
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720118"
---
# <a name="bitsadmin-setminretrydelay"></a>bitsadmin setminretrydelay

임시 오류가 발생 한 후 BITS에서 파일 전송을 시도 하기 전에 대기 하는 최소 시간 (초)을 설정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /setminretrydelay <job> <retrydelay>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |
| retrydelay | 전송 하는 동안 오류가 발생 한 후 BITS가 대기 하는 최소 시간 (초)입니다. |

## <a name="examples"></a>예

*Mydownloadjob*이라는 작업의 최소 다시 시도 지연 시간을 35 초로 설정 하려면 다음을 수행 합니다.

```
bitsadmin /setminretrydelay myDownloadJob 35
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
