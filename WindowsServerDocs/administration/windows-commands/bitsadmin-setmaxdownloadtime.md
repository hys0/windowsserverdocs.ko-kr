---
title: bitsadmin setmaxdownloadtime
description: 다운로드 제한 시간 (초)을 설정 하는 bitsadmin setmaxdownloadtime 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 16b96cf1-5738-415c-9b9d-c4ea8d5e4fec
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8192826570c9dae6aa9d286596336c3e589c9cbd
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719685"
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
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |
| 시간 제한 | 다운로드 제한 시간 (초)입니다. |

## <a name="examples"></a>예

작업에 대 한 시간 제한을 *Mydownloadjob* 을 10 초로 설정 합니다.

```
bitsadmin /setmaxdownloadtime myDownloadJob 10
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
