---
title: bitsadmin getmaxdownloadtime
description: 다운로드 제한 시간 (초)을 검색 하는 **bitsadmin getmaxdownloadtime**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-servemr
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cdce64f6-7125-489d-be3c-4af1dfc8c46a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8b6e4a45da76d5ba39edae151454ad7f28a74085
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850636"
---
# <a name="bitsadmin-getmaxdownloadtime"></a>bitsadmin getmaxdownloadtime

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

다운로드 제한 시간 (초)을 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getmaxdownloadtime <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 *Mydownloadjob* 이라는 작업의 최대 다운로드 시간 (초)을 가져옵니다.

```
C:\>bitsadmin /getmaxdownloadtime myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
