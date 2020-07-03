---
title: nslookup set retry
description: 지정 된 서버에서 정보를 가져오려고 시도 하는 횟수를 설정 하는 nslookup set retry 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 615fdfa2-fa29-47a8-8c9e-a6c5b45b3b71
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9ef38be2abfd423bb093ccf2b2ee6d701df28df3
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935699"
---
# <a name="nslookup-set-retry"></a>nslookup set retry

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

특정 시간 내에 응답이 수신 되지 않으면 시간 제한 기간이 두 배가 되 고 요청이 다시 전송 됩니다. 이 명령은 요청을 서버에 다시 보내는 횟수를 설정 합니다.

> [!NOTE]
> 요청 시간이 초과 되기 전 까지의 시간을 변경 하려면 [nslookup set timeout](nslookup-set-timeout.md) 명령을 사용 합니다.

## <a name="syntax"></a>구문

```
set retry=<number>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ---------- |
| `<number>` | 재시도 횟수에 대 한 새 값을 지정합니다. 기본 다시 시도 횟수는 **4**입니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |
| /help | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [nslookup set timeout](nslookup-set-timeout.md)
