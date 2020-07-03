---
title: fsutil hardlink
description: 기존 파일과 새 파일 간에 하드 링크를 만드는 fsutil hardlink create command에 대 한 참조 문서입니다.
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
ms.assetid: 835fc6f1-cc84-4189-b29a-dde90792469e
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: b4cbc3912339464a061c027234d0d22b2d73ea09
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932279"
---
# <a name="fsutil-hardlink"></a>fsutil hardlink

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

기존 파일 및 새 파일 간에 하드 링크를 만듭니다. 하드 링크는 파일에 대 한 디렉터리 항목입니다. 모든 파일을 하나 이상의 하드 링크 간주할 수 있습니다.

NTFS 볼륨에서 각 파일에는 여러 하드 링크가 있을 수 있으므로 단일 파일이 여러 디렉터리 (또는 이름이 다른 동일한 디렉터리에도 표시 될 수 있음)에 표시 될 수 있습니다. 동일한 파일을 참조 하는 모든 링크가 하므로 프로그램 링크 연 파일을 수정 합니다. 에 대 한 모든 링크를 삭제 한 후에 파일을 파일 시스템에서 삭제 됩니다. 하드 링크를 만든 후 프로그램에서 다른 파일 이름 처럼 사용할 수 있습니다.

## <a name="syntax"></a>구문

```
fsutil hardlink create <newfilename> <existingfilename>
fsutil hardlink list <filename>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| create | 기존 파일 및 새 파일 사이 NTFS 하드 링크를 설정합니다. NTFS 하드 링크는 POSIX 하드 링크와 유사 합니다. |
| \<newfilename> | 하드 링크를 만들려면 원하는 파일을 지정 합니다. |
| \<existingfilename> | 하드 링크를 만들 파일을 지정 합니다. |
| list | *파일 이름*에 대 한 하드 링크를 나열 합니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [fsutil](fsutil.md)
