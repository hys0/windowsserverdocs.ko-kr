---
title: ftp mget
description: 현재 파일 전송 형식을 사용 하 여 원격 파일을 로컬 컴퓨터에 복사 하는 ftp mget 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6c85ae96-ec51-48a9-a227-7f02c7332c69
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7239f31fa0a9b40d9bba4db0c3e1e29df5c03108
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925894"
---
# <a name="ftp-mget"></a>ftp mget

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

현재 파일 전송 형식을 사용 하 여 원격 파일을 로컬 컴퓨터에 복사 합니다.

## <a name="syntax"></a>구문

```
mget <remotefile>[ ]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<remotefile>` | 로컬 컴퓨터에 복사할 원격 파일을 지정 합니다. |

### <a name="examples"></a>예

현재 파일 전송 형식을 사용 하 여 원격 파일 *a.exe* 및 *b.exe* 을 로컬 컴퓨터에 복사 하려면 다음을 입력 합니다.

```
mget a.exe b.exe
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [ftp ascii 명령](ftp-ascii.md)

- [ftp 이진 명령](ftp-binary.md)

- [추가 FTP 지침](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
