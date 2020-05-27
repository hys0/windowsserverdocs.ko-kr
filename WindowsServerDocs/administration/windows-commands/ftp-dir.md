---
title: ftp 디렉터리
description: 원격 컴퓨터의 디렉터리 파일 및 하위 디렉터리 목록을 표시 하는 ftp dir 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a29a92a5-7b79-4e6e-95cf-2ccb38bb6fb2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6a120691964b7303cf3241ffef2f11d81573ba4d
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83819863"
---
# <a name="ftp-dir"></a>ftp 디렉터리

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 컴퓨터의 디렉터리 파일 및 하위 디렉터리 목록을 표시 합니다.

## <a name="syntax"></a>구문

```
dir [<remotedirectory>] [<localfile>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ------- | -------- |
| `[<remotedirectory>]` | 목록을 보려는 디렉터리를 지정 합니다. 디렉터리가 지정 되지 않은 경우 원격 컴퓨터의 현재 작업 디렉터리를 사용 합니다. |
| `[<localfile>]` | 디렉터리 목록을 저장할 로컬 파일을 지정 합니다. 로컬 파일을 지정 하지 않으면 결과가 화면에 표시 됩니다. |

### <a name="examples"></a>예

원격 컴퓨터에 *dir1* 에 대 한 디렉터리 목록을 표시 하려면 다음을 입력 합니다.

```
dir dir1
```

원격 컴퓨터의 현재 디렉터리 목록을 로컬 파일의 파일 목록에 저장 하려면 다음을 입력 *합니다*.

```
dir . dirlist.txt
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [추가 FTP 지침](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
