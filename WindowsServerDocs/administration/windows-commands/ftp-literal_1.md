---
title: ftp literal
description: 원격 ftp 서버에 축 자 인수를 보내는 ftp 리터럴 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fb81aa2d-07fa-4e79-bf44-1fb5526fdf14
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e71d80b5ddf8e3c92f810e295e21dee28376f03d
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933141"
---
# <a name="ftp-literal"></a>ftp literal

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

축 자 인수를 원격 ftp 서버에 보냅니다. 단일 ftp 회신 코드가 반환 됩니다.

> [!NOTE]
> 이 명령은 [ftp quote 명령과](ftp-quote.md)동일 합니다.

## <a name="syntax"></a>구문

```
literal <argument> [ ]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<argument>` | Ftp 서버에 보낼 인수를 지정 합니다. |

### <a name="examples"></a>예

**Quit** 명령을 원격 ftp 서버에 보내려면 다음을 입력 합니다.

```
literal quit
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [ftp 인용 명령](ftp-quote.md)

- [추가 FTP 지침](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
