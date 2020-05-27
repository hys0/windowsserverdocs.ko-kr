---
title: ftp mdir
description: Ftp mdir 명령에 대 한 참조 항목으로, 원격 디렉터리에서 파일 및 하위 디렉터리의 디렉터리 목록을 표시 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 90eec45b-558b-4b8d-bbe4-b56d98e1ca70
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b192e6de23105fcc696d8369ce0280167a201e20
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820223"
---
# <a name="ftp-mdir"></a>ftp mdir

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 디렉터리에서 파일 및 하위 디렉터리의 디렉터리 목록을 표시 합니다.

## <a name="syntax"></a>구문

```
mdir <remotefile>[...] <localfile>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<remotefile>` | 목록을 보려는 디렉터리 또는 파일을 지정 합니다. 여러 개의 *remotefiles*를 지정할 수 있습니다. 원격 컴퓨터에서 현재 작업 디렉터리를 사용 하려면 하이픈 (-)을 입력 합니다. |
| `<localfile>` | 목록을 저장할 로컬 파일을 지정 합니다. 이 매개 변수는 필수입니다. 화면에 목록을 표시 하려면 하이픈 (-)을 입력 합니다. |

### <a name="examples"></a>예

화면에 *dir1* 및 *dir2* 의 디렉터리 목록을 표시 하려면 다음을 입력 합니다.

```
mdir dir1 dir2 -
```

Dir1 및 *dir2* 의 결합 된 디렉터리 목록을 다른 로컬 파일 ( *dir1* 및)에 저장 하려면 *다음을 입력*합니다.

```
mdir dir1 dir2 dirlist.txt
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [추가 FTP 지침](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
