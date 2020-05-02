---
title: bitsadmin cache and info
description: 특정 캐시 항목을 덤프 하는 bitsadmin cache 및 info 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 15975cbf-dba6-49ca-a725-d15ce1952de5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3a50e6575a5496ff9f7bcd6a0dc429c7960c6933
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718343"
---
# <a name="bitsadmin-cache-and-info"></a>bitsadmin cache and info

특정 캐시 엔트리를 덤프합니다.

## <a name="syntax"></a>구문

```
bitsadmin /cache /info recordID [/verbose]
```

### <a name="parameters"></a>매개 변수

| Paramreter | 설명 |
| -------------- | -------------- |
| recordID | 캐시 항목에 연결 된 GUID입니다. |

## <a name="examples"></a>예

RecordID 값 {6511FB02-E195-40A2-B595-E8E2F8F47702}을 사용 하 여 캐시 엔트리를 덤프 합니다.

```
bitsadmin /cache /info {6511FB02-E195-40A2-B595-E8E2F8F47702}
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin cache 명령](bitsadmin-cache.md)
