---
title: bitsadmin gettemporaryname
description: 작업 내에서 지정 된 파일의 임시 파일 이름을 보고 하는 bitsadmin gettemporaryname 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 68925edc-a801-4292-a812-7471c4f60fdd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f7780691f37fb78f1553fa993fd408d224be39ff
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717489"
---
# <a name="bitsadmin-gettemporaryname"></a>bitsadmin gettemporaryname

작업 내에서 지정된 된 파일의 임시 파일 이름을 보고합니다.

## <a name="syntax"></a>구문

```
bitsadmin /gettemporaryname <job> <file_index>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |
| file_index | 0부터 시작 합니다. |

## <a name="examples"></a>예

*Mydownloadjob*이라는 작업에 대해 파일 2의 임시 파일 이름을 보고 하려면 다음을 수행 합니다.

```
bitsadmin /gettemporaryname myDownloadJob 1
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
