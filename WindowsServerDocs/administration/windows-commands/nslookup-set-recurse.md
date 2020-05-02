---
title: nslookup set recurse
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d1b7a93f-dfb0-4ccd-b230-e0953057fada
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c4386bd5738806016b9ec15802faebf3efdcedf0
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723598"
---
# <a name="nslookup-set-recurse"></a>nslookup set recurse



정보가 없는 경우 다른 서버를 쿼리 하는 도메인 이름 시스템 (DNS) 이름 서버를 알려 줍니다.

## <a name="syntax"></a>구문

```
set [no]recurse
```

### <a name="parameters"></a>매개 변수

|   매개 변수   |                                                                  설명                                                                  |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| **norecurse** |                다른 서버에 쿼리 정보가 없는 경우에서 도메인 이름 시스템 (DNS) 이름 서버를 중지 합니다.                |
|  **recurse**  | 정보가 없는 경우 다른 서버를 쿼리 하는 도메인 이름 시스템 (DNS) 이름 서버를 알려 줍니다. 기본 구문은 **recurse**합니다. |
|     {도움말     |                                                                      ?}                                                                       |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)