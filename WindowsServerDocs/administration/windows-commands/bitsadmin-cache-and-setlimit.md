---
title: bitsadmin cache and setlimit
description: 캐시 크기 제한을 설정 하는 bitsadmin cache 및 setlimit 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 46578835-d5ce-423b-be4d-62ddb9e1908d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a4c41102bfb87ff6d48113c4e85a821b821b5b01
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718285"
---
# <a name="bitsadmin-cache-and-setlimit"></a>bitsadmin cache and setlimit

캐시 크기 제한을 설정합니다.

## <a name="syntax"></a>구문

```
bitsadmin /cache /setlimit percent
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| percent | 전체 하드 디스크 공간의 백분율로 정의 된 캐시 제한입니다. |

## <a name="examples"></a>예

캐시 크기 제한을 50%로 설정 하려면 다음을 수행 합니다.

```
bitsadmin /cache /setlimit 50
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin cache 명령](bitsadmin-cache.md)
