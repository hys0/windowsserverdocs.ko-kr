---
title: ftp get
description: 현재 파일 전송 형식을 사용 하 여 원격 파일을 로컬 컴퓨터에 복사 하는 ftp get 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d70355c4-58ef-43e0-916b-c7ecf77e6ee4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: de084813ee837ecea2f0871589218d3262b40bba
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925920"
---
# <a name="ftp-get"></a>ftp get

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

현재 파일 전송 형식을 사용 하 여 원격 파일을 로컬 컴퓨터에 복사 합니다.

> [!NOTE]
> 이 명령은 [ftp recv 명령과](ftp-recv.md)동일 합니다.

## <a name="syntax"></a>구문

```
get <remotefile> [<localfile>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<remotefile>` | 복사할 원격 파일을 지정 합니다. |
| `[<localfile>]` | 로컬 컴퓨터에서 사용할 파일의 이름을 지정 합니다. *Localfile* 을 지정 하지 않으면 *remotefile*이름이 파일에 지정 됩니다. |

### <a name="examples"></a>예

현재 파일 전송을 사용 하 여 로컬 컴퓨터에 *test.txt* 를 복사 하려면 다음을 입력 합니다.

```
get test.txt
```

현재 파일 전송을 사용 하 여 *test1.txt* 로컬 컴퓨터에 *test.txt* 를 복사 하려면 다음을 입력 합니다.

```
get test.txt test1.txt
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [ftp recv 명령](ftp-recv.md)

- [ftp ascii 명령](ftp-ascii.md)

- [ftp 이진 명령](ftp-binary.md)

- [추가 FTP 지침](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
