---
title: bitsadmin setmaxdownloadtime
description: '**Bitsadmin setmaxdownloadtime**에 대 한 Windows 명령 항목으로, 다운로드 제한 시간 (초)을 설정 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 16b96cf1-5738-415c-9b9d-c4ea8d5e4fec
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f07931dfb9fabaec272384dced6d60f1335b6a94
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122919"
---
# <a name="bitsadmin-setmaxdownloadtime"></a>bitsadmin setmaxdownloadtime

다운로드 제한 시간을 초 단위로 설정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /setmaxdownloadtime <job> <timeout>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |
| timeout | 다운로드 제한 시간 (초)입니다. |

## <a name="examples"></a>예

다음 예제에서는 명명 된 작업에 대 한 제한 시간 설정 *myDownloadJob* 으로 10 초로 설정 합니다.

```
C:\>bitsadmin /setmaxdownloadtime myDownloadJob 10
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)