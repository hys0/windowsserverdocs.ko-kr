---
title: ftp recv
description: 현재 파일 전송 형식을 사용 하 여 원격 파일을 로컬 컴퓨터에 복사 하는 ftp recv 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f249ce61-247d-421b-9b93-48bce5108800
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 01f9fc1d8e233d8e2c38f606dea12f5d342d5e44
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925787"
---
# <a name="ftp-recv"></a>ftp recv

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

현재 파일 전송 형식을 사용 하 여 원격 파일을 로컬 컴퓨터에 복사 합니다.

> [!NOTE]
> 이 명령은 [ftp get 명령과](ftp-get.md)같습니다.

## <a name="syntax"></a>구문

```
recv <remotefile> [<localfile>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<remotefile>` | 복사할 원격 파일을 지정 합니다. |
| `[<localfile>]` | 로컬 컴퓨터에서 사용할 파일의 이름을 지정 합니다. *Localfile* 을 지정 하지 않으면 *remotefile*이름이 파일에 지정 됩니다. |

### <a name="examples"></a>예

현재 파일 전송을 사용 하 여 로컬 컴퓨터에 *test.txt* 를 복사 하려면 다음을 입력 합니다.

```
recv test.txt
```

현재 파일 전송을 사용 하 여 *test1.txt* 로컬 컴퓨터에 *test.txt* 를 복사 하려면 다음을 입력 합니다.

```
recv test.txt test1.txt
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [ftp get 명령](ftp-get.md)

- [ftp ascii 명령](ftp-ascii.md)

- [ftp 이진 명령](ftp-binary.md)

- [추가 FTP 지침](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
