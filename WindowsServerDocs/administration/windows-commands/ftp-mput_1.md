---
title: ftp mput
description: 현재 파일 전송 형식을 사용 하 여 로컬 파일을 원격 컴퓨터에 복사 하는 ftp mput 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 980f15e7-7cf1-4813-9946-a8cc4edfb198
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5006c1ba19f0e017dea377b47bd0d89a68266382
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820413"
---
# <a name="ftp-mput"></a>ftp mput

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

현재 파일 전송 형식을 사용 하 여 원격 컴퓨터에 로컬 파일을 복사 합니다.

## <a name="syntax"></a>구문

```
mput <localfile>[ ]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<localfile>` | 원격 컴퓨터에 복사할 로컬 파일을 지정 합니다. |

### <a name="examples"></a>예

현재 파일 전송 형식을 사용 하 여 *Program1* 및 *program2.c* 을 원격 컴퓨터에 복사 하려면 다음을 입력 합니다.

```
mput Program1.exe Program2.exe
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [ftp ascii 명령](ftp-ascii.md)

- [ftp 이진 명령](ftp-binary.md)

- [추가 FTP 지침](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
