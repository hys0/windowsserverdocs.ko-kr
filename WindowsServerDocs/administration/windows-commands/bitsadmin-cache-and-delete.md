---
title: bitsadmin cache and delete
description: 특정 캐시 항목을 삭제 하는 bitsadmin cache 및 delete 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 22540273-55a5-46ea-869b-6df2aa6808a1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 62c0c3d5b2cc188e8a8987c7ca502cdeaf932410
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718456"
---
# <a name="bitsadmin-cache-and-delete"></a>bitsadmin cache and delete

특정 캐시 엔트리를 삭제합니다.

## <a name="syntax"></a>구문

```
bitsadmin /cache /delete recordID
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| recordID | 캐시 항목에 연결 된 GUID입니다. |

## <a name="examples"></a>예

RecordID {6511FB02-E195-40A2-B595-E8E2F8F47702}를 사용 하 여 캐시 엔트리를 삭제 하려면:

```
bitsadmin /cache /delete {6511FB02-E195-40A2-B595-E8E2F8F47702}
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin cache 명령](bitsadmin-cache.md)
