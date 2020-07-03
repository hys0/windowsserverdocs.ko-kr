---
title: bitsadmin setmaxdownloadtime
description: 다운로드 제한 시간 (초)을 설정 하는 bitsadmin setmaxdownloadtime 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 16b96cf1-5738-415c-9b9d-c4ea8d5e4fec
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 65853180a22d49011e8edb10ed15ac98625cbc30
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927735"
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
