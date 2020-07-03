---
title: bitsadmin getminretrydelay
description: 파일 전송을 시도 하기 전에 일시적 오류가 발생 한 후 서비스가 대기 하는 시간 (초)을 검색 하는 bitsadmin getminretrydelay 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 54f0abab-c129-40ed-a603-50f464d26011
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 066eb9a2c967d9d5e92aa8dbad2001a65a682796
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927012"
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
