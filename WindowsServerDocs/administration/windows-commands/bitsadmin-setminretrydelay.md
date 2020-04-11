---
title: bitsadmin setminretrydelay
description: BITS가 파일을 전송 하기 전에 일시적 오류가 발생 한 후 대기 하는 최소 시간 (초)을 설정 하는 **bitsadmin setminretrydelay**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ce8674ca-6cc5-4bb2-8dda-7dfbb1cd6830
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ddae9a62a49ca07bb03649f131a0a1ebad8ee3fe
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122885"
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
| 제출 | 작업의 표시 이름 또는 GUID입니다. |
| retrydelay | 전송 하는 동안 오류가 발생 한 후 BITS가 대기 하는 최소 시간 (초)입니다. |

## <a name="examples"></a>예

다음 예제에서는 명명 된 작업에 대 한 최소 재시도 지연 *myDownloadJob* 35 초입니다.

```
C:\>bitsadmin /setminretrydelay myDownloadJob 35
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)