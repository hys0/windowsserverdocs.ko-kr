---
title: nslookup set timeout
description: 조회 요청에 대 한 회신을 대기 하는 초기 시간 (초)을 변경 하는 nslookup set timeout 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 07afdaf4-ffec-496f-a188-4e91cf1a28f8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6df8d1229dd57a84cb0dced3829bb328e41f092c
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85930349"
---
# <a name="nslookup-set-timeout"></a>nslookup set timeout

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

초기 조회 요청에 회신을 기다릴 시간 (초) 수를 변경 합니다. 지정 된 시간 내에 응답이 수신 되지 않으면 제한 시간이 두 배가 되 고 요청을 다시 보냅니다. [Nslookup set retry](nslookup-set-retry.md) 명령을 사용 하 여 요청을 보내려고 시도 하는 횟수를 확인 합니다.

## <a name="syntax"></a>구문

```
set timeout=<number>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ---------- |
| `<number>` | 회신을 기다릴 시간 (초) 수를 지정 합니다. 대기할 기본 시간 (초)은 **5**입니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |
| /help | 명령 프롬프트에 도움말을 표시합니다. |

### <a name="examples"></a>예

2 초에 대 한 응답 가져오기 제한 시간을 설정 하려면:

```
set timeout=2
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [nslookup set retry](nslookup-set-retry.md)
