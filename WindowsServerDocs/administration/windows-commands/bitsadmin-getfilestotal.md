---
title: bitsadmin getfilestotal
description: 지정 된 작업의 파일 수를 검색 하는 bitsadmin getfilestotal 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c5de113e-f29c-4cd3-9392-0e300018d516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7592f783d17e31fe8a1e7fbf82cb41e20171c9fd
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928288"
---
# <a name="bitsadmin-getfilestotal"></a>bitsadmin getfilestotal

지정 된 작업의 파일 수를 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getfilestotal <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a>예

*Mydownloadjob*이라는 작업에 포함 된 파일 수를 검색 하려면 다음을 수행 합니다.

```
bitsadmin /getfilestotal myDownloadJob
```

## <a name="see-also"></a>참고 항목

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
