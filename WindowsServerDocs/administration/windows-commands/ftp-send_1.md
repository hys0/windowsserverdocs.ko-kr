---
title: ftp send
description: 현재 파일 전송 형식을 사용 하 여 로컬 파일을 원격 컴퓨터에 복사 하는 ftp send 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 000aa80a-60a0-4b51-815f-3237a4f3e0f4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4d261db79483800507d62e9d4253a58b2b9359fe
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925691"
---
# <a name="ftp-send"></a>ftp send

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

현재 파일 전송 형식을 사용 하 여 원격 컴퓨터에 로컬 파일을 복사 합니다.

> [!NOTE]
> 이 명령은 [ftp put 명령과](ftp-put.md)동일 합니다.

## <a name="syntax"></a>구문

```
send <localfile> [<remotefile>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<localfile>` | 복사할 로컬 파일을 지정 합니다. |
| `<remotefile>` | 원격 컴퓨터에서 사용 하 여 이름을 지정 합니다. *Remotefile*을 지정 하지 않으면 파일에 *localfile* 이름이 표시 됩니다. |

### <a name="examples"></a>예

로컬 파일 *test.txt* 를 복사 하 고 원격 컴퓨터에 *test1.txt* 이름을 입력 하려면 다음을 입력 합니다.

```
send test.txt test1.txt
```

원격 컴퓨터에 *program.exe* 로컬 파일을 복사 하려면 다음을 입력 합니다.

```
send program.exe
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [추가 FTP 지침](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
