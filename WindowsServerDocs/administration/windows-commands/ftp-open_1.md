---
title: ftp open
description: 지정 된 ftp 서버에 연결 하는 ftp open 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4b61926a-dc60-4b4c-96d3-64e5c91c18ba
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 888b8f917d82d72f47a737c2f0edc42451de7164
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925797"
---
# <a name="ftp-open"></a>ftp open

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정 된 ftp 서버에 연결 합니다.

## <a name="syntax"></a>구문

```
open <computer> [<port>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<computer>` | 연결 하려는 원격 컴퓨터를 지정 합니다. IP 주소 또는 컴퓨터 이름을 사용할 수 있습니다 .이 경우에는 DNS 서버 또는 호스트 파일을 사용할 수 있어야 합니다. |
| `[<port>]` | Ftp 서버에 연결 하는 데 사용할 TCP 포트 번호를 지정 합니다. 기본적으로 TCP 포트 21이 사용 됩니다. |

### <a name="examples"></a>예

*Ftp.microsoft.com*에서 ftp 서버에 연결 하려면 다음을 입력 합니다.

```
open ftp.microsoft.com
```

TCP 포트 *755*에서 수신 대기 하는 *ftp.microsoft.com* 에서 ftp 서버에 연결 하려면 다음을 입력 합니다.

```
open ftp.microsoft.com 755
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [추가 FTP 지침](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
