---
title: ftp remotehelp
description: 원격 명령에 대 한 도움말을 표시 하는 ftp remotehelp 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ef23adf3-ead4-44c8-ac1d-c8a6f4b2bf73
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 54d784751291515a022a561ca9600e3e967a9d8e
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925742"
---
# <a name="ftp-remotehelp"></a>ftp remotehelp

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 명령에 대 한 도움말을 표시 합니다.

## <a name="syntax"></a>구문

```
remotehelp [<command>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ------- | -------- |
| `[<command>]` | 도움말을 원하는 명령의 이름을 지정 합니다. `<command>`을 지정 하지 않으면이 명령은 모든 원격 명령 목록을 표시 합니다. [Ftp 따옴표](ftp-quote.md) 또는 [ftp 리터럴을](ftp-literal_1.md)사용 하 여 원격 명령을 실행할 수도 있습니다. |

### <a name="examples"></a>예

원격 명령 목록을 표시 하려면 다음을 입력 합니다.

```
remotehelp
```

*Feat* remote 명령의 구문을 표시 하려면 다음을 입력 합니다.

```
remotehelp feat
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [ftp quote](ftp-quote.md)

- [ftp literal](ftp-literal_1.md)

- [추가 FTP 지침](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
