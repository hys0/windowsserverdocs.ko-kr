---
title: bitsadmin 캐시 및 삭제
description: '**Bitsadmin 캐시 및 삭제**에 대 한 Windows 명령 항목으로, 특정 캐시 엔트리를 삭제 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 22540273-55a5-46ea-869b-6df2aa6808a1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0fd7f1db83a62dd9c1085d6afdcf509c1c3ac8cf
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850946"
---
# <a name="bitsadmin-cache-and-delete"></a>bitsadmin 캐시 및 삭제

특정 캐시 엔트리를 삭제합니다.

## <a name="syntax"></a>구문

```
bitsadmin /cache /delete recordID
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| recordID | 캐시 항목에 연결 된 GUID입니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 {6511FB02-E195-40A2-B595-E8E2F8F47702}의 RecordID 캐시 항목을 삭제 합니다.

```
C:\>bitsadmin /cache /delete {6511FB02-E195-40A2-B595-E8E2F8F47702}
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)