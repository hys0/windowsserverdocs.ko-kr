---
title: ftp put
description: 현재 파일 전송 형식을 사용 하 여 로컬 파일을 원격 컴퓨터에 복사 하는 ftp put 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 95cc1e3f-523d-4374-98b8-16e6c276b2ca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/30/2020
ms.openlocfilehash: 7b382673be838af739c29ffa294e3d853f0507c2
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925156"
---
# <a name="ftp-put"></a>ftp put

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

현재 파일 전송 형식을 사용 하 여 원격 컴퓨터에 로컬 파일을 복사 합니다.

> [!NOTE]
> 이 명령은 [ftp send 명령과](ftp-send_1.md)동일 합니다.

## <a name="syntax"></a>구문

```
put <localfile> [<remotefile>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<localfile>` | 복사할 로컬 파일을 지정 합니다. |
| `[<remotefile>]` | 원격 컴퓨터에서 사용 하 여 이름을 지정 합니다. *Remotefile*을 지정 하지 않으면 파일에 *localfile* 이름이 지정 됩니다.|

### <a name="examples"></a>예

로컬 파일 *test.txt* 를 복사 하 고 원격 컴퓨터에 *test1.txt* 이름을 입력 하려면 다음을 입력 합니다.

```
put test.txt test1.txt
```

원격 컴퓨터에 *program.exe* 로컬 파일을 복사 하려면 다음을 입력 합니다.

```
put program.exe
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [ftp ascii 명령](ftp-ascii.md)

- [ftp 이진 명령](ftp-binary.md)

- [추가 FTP 지침](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
