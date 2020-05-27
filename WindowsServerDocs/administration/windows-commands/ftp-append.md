---
title: ftp 추가
description: 현재 파일 형식 설정을 사용 하 여 원격 컴퓨터의 파일에 로컬 파일을 추가 하는 ftp append 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7c1a133c-31dc-41a4-9eb9-258efd79804d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7d1b6ab4a6ae0c1654d4335d24f135b2893bdcb7
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83819143"
---
# <a name="ftp-append"></a>ftp 추가

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

현재 파일 형식 설정을 사용 하 여 원격 컴퓨터에서 파일을 로컬 파일을 추가 합니다.

## <a name="syntax"></a>구문

```
append <localfile> [remotefile]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<localfile>` | 추가할 로컬 파일을 지정 합니다. |
| remotefile | 원격 컴퓨터에서 파일을 지정 <localfile> 추가 됩니다. 이 매개 변수를 사용 하지 않으면 `<localfile>` 이름이 원격 파일 이름 대신 사용 됩니다. |

### <a name="examples"></a>예

*File1* 을 원격 컴퓨터의 *file2* 에 추가 하려면 다음을 입력 합니다.

```
append file1.txt file2.txt
```

원격 컴퓨터의 *파일 이름에* 로컬 파일 이름 *.txt* 를 추가 합니다.

```
append file1.txt
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [추가 FTP 지침](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
