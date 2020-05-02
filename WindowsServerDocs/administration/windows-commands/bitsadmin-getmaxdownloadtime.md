---
title: bitsadmin getmaxdownloadtime
description: 다운로드 제한 시간 (초)을 검색 하는 bitsadmin getmaxdownloadtime 명령에 대 한 참조 항목입니다.
ms.prod: windows-servemr
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cdce64f6-7125-489d-be3c-4af1dfc8c46a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c63acee7629267ed10df11fb8cf4eeb0c911e118
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717863"
---
# <a name="bitsadmin-getmaxdownloadtime"></a>bitsadmin getmaxdownloadtime

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

다운로드 제한 시간 (초)을 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getmaxdownloadtime <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a>예

*Mydownloadjob* 이라는 작업의 최대 다운로드 시간 (초)을 가져오려면 다음을 수행 합니다.

```
bitsadmin /getmaxdownloadtime myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
