---
title: bitsadmin 캐시 및 setexpirationtime
description: 캐시 만료 시간을 설정 하는 **bitsadmin cache 및 setexpirationtime**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 00ea6e4e-b707-4b31-88dd-b61a78565c8d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bf283a0a8b94fd55c591609e3dcd1d127a2be81a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850886"
---
>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

# <a name="bitsadmin-cache-and-setexpirationtime"></a>bitsadmin 캐시 및 setexpirationtime

캐시 만료 시간을 설정합니다.

## <a name="syntax"></a>구문

```
bitsadmin /cache /setexpirationtime secs
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 초 | 캐시 만료 될 때까지 시간 (초) 수입니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 캐시에 60 초 내에 만료 됩니다.

```
C:\>bitsadmin /cache / setexpirationtime 60
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
