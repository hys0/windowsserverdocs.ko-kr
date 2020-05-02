---
title: bitsadmin getfilestransferred
description: 지정 된 작업에 대해 전송 된 파일 수를 검색 하는 bitsadmin getfilestransferred 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e282815c-938b-4ac0-a09d-9baafb656dcb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ed11739029338ecce5fc4efbe1918873a7f37f62
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717920"
---
# <a name="bitsadmin-getfilestransferred"></a>bitsadmin getfilestransferred

지정 된 작업에 대해 전송 된 파일 수를 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getfilestransferred <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a>예

*Mydownloadjob*이라는 작업에서 전송 된 파일 수를 검색 하려면 다음을 수행 합니다.

```
bitsadmin /getfilestransferred myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
