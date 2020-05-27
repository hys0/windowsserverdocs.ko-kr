---
title: ftp ls
description: Ftp ls 명령에 대 한 참조 항목으로, 원격 컴퓨터에서 파일 및 하위 디렉터리의 축약 된 목록을 표시 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5e03c7db-1e2b-419c-acb2-8a68f3db9615
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9ae913f001c3ddffce9ff81c9c5c5fd32f436da5
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820173"
---
# <a name="ftp-ls"></a>ftp ls

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 컴퓨터에 있는 파일 및 하위 디렉터리의 축약 된 목록을 표시 합니다.

## <a name="syntax"></a>구문

```
ls [<remotedirectory>] [<localfile>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- |------------ |
| `[<remotedirectory>]` | 목록을 보려는 디렉터리를 지정 합니다. 디렉터리가 지정 되지 않은 경우 원격 컴퓨터의 현재 작업 디렉터리를 사용 합니다. |
| `[<localfile>]` | 목록을 저장할 로컬 파일을 지정 합니다. 로컬 파일을 지정 하지 않으면 결과가 화면에 표시 됩니다. |

### <a name="examples"></a>예

원격 컴퓨터에서 파일 및 하위 디렉터리의 축약 된 목록을 표시 하려면 다음을 입력 합니다.

```
ls
```

원격 컴퓨터에 있는 *dir1* 의 축약 된 디렉터리 목록을 가져오고이를 파일 *목록 .txt*라는 로컬 파일에 저장 하려면 다음을 입력 합니다.

```
ls dir1 dirlist.txt
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [추가 FTP 지침](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
