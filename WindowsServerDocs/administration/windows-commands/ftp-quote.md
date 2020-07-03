---
title: ftp quote
description: 원격 ftp 서버에 축 자 인수를 보내는 ftp 인용 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4500a1d3-c091-42c7-a909-f61df7f2e993
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ce1f0c009ff9e68c4b8f1f9bc074d91d235d1955
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925075"
---
# <a name="ftp-quote"></a>ftp quote

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

축 자 인수를 원격 ftp 서버에 보냅니다. 단일 ftp 회신 코드가 반환 됩니다.

> [!NOTE]
> 이 명령은 [ftp 리터럴 명령과](ftp-literal_1.md)동일 합니다.

## <a name="syntax"></a>구문

```
quote <argument>[ ]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| --------- | ----------- |
| `<argument>` | Ftp 서버에 보낼 인수를 지정 합니다. |

### <a name="examples"></a>예

**Quit** 명령을 원격 ftp 서버에 보내려면 다음을 입력 합니다.

```
quote quit
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [ftp 리터럴 명령](ftp-literal_1.md)

- [추가 FTP 지침](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))