---
title: bitsadmin getminretrydelay
description: 서비스에서 임시 오류가 발생 한 후 파일을 전송 하기 전에 대기 하는 시간 (초)을 검색 하는 bitsadmin getminretrydelay 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 54f0abab-c129-40ed-a603-50f464d26011
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a50b9d98fe0b873dc58b8e86dc672a8f4157208a
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717843"
---
# <a name="bitsadmin-getminretrydelay"></a>bitsadmin getminretrydelay

서비스에서 임시 오류가 발생 한 후 파일을 전송 하기 전에 대기 하는 시간 (초)을 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getminretrydelay <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a>예

*Mydownloadjob*이라는 작업의 최소 다시 시도 지연 시간을 검색 하려면 다음을 수행 합니다.

```
bitsadmin /getminretrydelay myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
