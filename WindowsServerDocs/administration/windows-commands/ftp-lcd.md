---
title: ftp lcd
description: 로컬 컴퓨터의 작업 디렉터리를 변경 하는 ftp lcd 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 60a25808-6abb-408b-8373-0bbdcd0994b4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c941adcc8c56d2598ad4ff56852309a256656878
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820133"
---
# <a name="ftp-lcd"></a>ftp lcd

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

로컬 컴퓨터의 작업 디렉터리를 변경 합니다. 기본적으로 작업 디렉터리는 **ftp** 명령이 시작 된 디렉터리입니다.

## <a name="syntax"></a>구문

```
lcd [<directory>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `[<directory>]` | 변경할 로컬 컴퓨터의 디렉터리를 지정 합니다. *디렉터리* 를 지정 하지 않으면 현재 작업 디렉터리가 기본 디렉터리로 변경 됩니다. |

### <a name="examples"></a>예

로컬 컴퓨터의 작업 디렉터리를 *c:\dir1*로 변경 하려면 다음을 입력 합니다.

```
lcd c:\dir1
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [추가 FTP 지침](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
