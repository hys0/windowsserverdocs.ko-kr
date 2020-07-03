---
title: ftp mls
description: Ftp mls 명령에 대 한 참조 문서로, 원격 디렉터리에 있는 파일 및 하위 디렉터리의 축약 된 목록을 표시 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4738fd49-0e80-4bdf-a773-0f973db3a710
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6c2e87cbf0455fccb99435e0a8b67fd30164e35b
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925857"
---
# <a name="ftp-mls"></a>ftp mls

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 디렉터리에서 파일 및 하위 디렉터리의 축약 된 목록을 표시 합니다.

## <a name="syntax"></a>구문

```
mls <remotefile>[ ] <localfile>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<remotefile>` | 목록을 보려는 파일을 지정 합니다. *Remotefiles*를 지정 하는 경우 하이픈을 사용 하 여 원격 컴퓨터의 현재 작업 디렉터리를 나타냅니다. |
| `<localfile>` | 목록을 저장할 로컬 파일을 지정 합니다. *Localfile*을 지정 하는 경우 하이픈을 사용 하 여 화면에 목록을 표시 합니다. |

### <a name="examples"></a>예

*Dir1* 및 *dir2*에 대 한 파일 및 하위 디렉터리의 축약 된 목록을 표시 하려면 다음을 입력 합니다.

```
mls dir1 dir2 -
```

*Dir1* 및 *dir2* 에 대 한 간략 한 파일 및 하위 디렉터리 목록을 로컬 파일 *dirlist.txt*에 저장 하려면 다음을 입력 합니다.

```
mls dir1 dir2 dirlist.txt
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [추가 FTP 지침](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
