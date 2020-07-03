---
title: bitsadmin getbytestransferred
description: 지정 된 작업에 대해 전송 된 바이트 수를 검색 하는 bitsadmin getbytestransferred 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 47bbf184-e06f-4be0-b2ba-d32b10d82002
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6ca8561a0c5eb92bb4bd716f7b20bd9f7ceaf606
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923119"
---
# <a name="bitsadmin-getbytestransferred"></a>bitsadmin getbytestransferred

지정 된 작업에 대해 전송 된 바이트 수를 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getbytestransferred <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a>예

*Mydownloadjob*이라는 작업에 대해 전송 된 바이트 수를 검색 하려면 다음을 수행 합니다.

```
bitsadmin /getbytestransferred myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
