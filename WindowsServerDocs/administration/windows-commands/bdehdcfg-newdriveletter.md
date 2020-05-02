---
title: bdehdcfg newdriveletter
description: Bdehdcfg newdriveletter 명령에 대 한 참조 항목으로, 시스템 드라이브로 사용 되는 드라이브 부분에 새 드라이브 문자를 할당 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f1f200a0-6850-4f0d-9047-f9f982a590f8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: da09ae1469c6fc8370e6bd0f2f7a8f3efd8dc4f0
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718669"
---
# <a name="bdehdcfg-newdriveletter"></a>bdehdcfg: newdriveletter

시스템 드라이브로 사용할 드라이브의 부분에 새 드라이브 문자를 할당 합니다. 시스템 드라이브에 드라이브 문자를 할당 하지 않는 것이 좋습니다.

## <a name="syntax"></a>구문

```
bdehdcfg -target {default|unallocated|<drive_letter> shrink|<drive_letter> merge} -newdriveletter <drive_letter>
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------| ----------- |
| `<drive_letter>` | 지정 된 대상 드라이브에 할당할 드라이브 문자를 정의 합니다. |

## <a name="examples"></a>예

기본 드라이브에 드라이브 문자 `P`를 할당 하려면 다음을 수행 합니다.

```
bdehdcfg -target default -newdriveletter P:
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bdehdcfg](bdehdcfg.md)
