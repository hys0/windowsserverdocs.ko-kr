---
title: nslookup set root
description: 쿼리에 사용 되는 루트 서버의 이름을 변경 하는 nslookup set root 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8ad5393c-d4fd-4594-8187-576b1dcde60a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 866cc0f9c7c7e4ea99416c1be1fd8de3d374ca64
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935675"
---
# <a name="nslookup-set-root"></a>nslookup set root

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

쿼리에 사용 되는 루트 서버 이름을 변경 합니다.

> [!NOTE]
> 이 명령은 [nslookup root](nslookup-root.md) 명령을 지원 합니다.

## <a name="syntax"></a>구문

```
set root=<rootserver>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ---------- |
| `<rootserver>` | 루트 서버에 대 한 새 이름을 지정합니다. 기본값은 **ns.nic.ddn.mil**입니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |
| /help | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [nslookup root](nslookup-root.md)
