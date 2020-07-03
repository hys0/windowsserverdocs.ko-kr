---
title: bitsadmin cache and setexpirationtime
description: 캐시 만료 시간을 설정 하는 bitsadmin cache 및 setexpirationtime 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 00ea6e4e-b707-4b31-88dd-b61a78565c8d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 60372a74acc6ea5312afb5dafcb3ab7b3299f4d2
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923254"
---
# <a name="bitsadmin-cache-and-setexpirationtime"></a>bitsadmin cache and setexpirationtime

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

캐시 만료 시간을 설정합니다.

## <a name="syntax"></a>구문

```
bitsadmin /cache /setexpirationtime secs
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 초 | 캐시 만료 될 때까지 시간 (초) 수입니다. |

## <a name="examples"></a>예

캐시가 60 초 후에 만료 되도록 설정 하려면 다음을 수행 합니다.

```
bitsadmin /cache / setexpirationtime 60
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin cache 명령](bitsadmin-cache.md)
