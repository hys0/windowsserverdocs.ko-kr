---
title: bitsadmin getfilestotal
description: 지정 된 작업의 파일 수를 검색 하는 bitsadmin getfilestotal 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c5de113e-f29c-4cd3-9392-0e300018d516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5cf3b33c15bb18c8a141408f82fdd72a6e710817
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717972"
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
