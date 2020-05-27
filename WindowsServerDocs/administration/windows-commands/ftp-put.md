---
title: ftp put
description: 현재 파일 전송 형식을 사용 하 여 로컬 파일을 원격 컴퓨터에 복사 하는 ftp put 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 95cc1e3f-523d-4374-98b8-16e6c276b2ca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/30/2020
ms.openlocfilehash: aee76b95ac538868122d5137958723326575eb18
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820373"
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

로컬 파일 *test.txt* 를 복사 하 고 원격 컴퓨터에서 이름을 *test1* 로 설정 하려면 다음을 입력 합니다.

```
put test.txt test1.txt
```

로컬 파일 *프로그램* 을 원격 컴퓨터에 복사 하려면 다음을 입력 합니다.

```
put program.exe
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [ftp ascii 명령](ftp-ascii.md)

- [ftp 이진 명령](ftp-binary.md)

- [추가 FTP 지침](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
