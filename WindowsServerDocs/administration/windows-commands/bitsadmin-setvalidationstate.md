---
title: bitsadmin setvalidationstate
description: 작업 내에서 지정 된 파일의 콘텐츠 유효성 검사 상태를 설정 하는 **bitsadmin setvalidationstate**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e8fc8e8c-171c-4681-8057-6986b018e576
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6bec42ae926050cd21df594a38f1c441a40a527f
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122716"
---
# <a name="bitsadmin-setvalidationstate"></a>bitsadmin setvalidationstate

작업 내에서 지정된 된 파일의 콘텐츠 유효성 검사 상태를 설정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /setvalidationstate <job> <file_index> <TRUE|FALSE>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ---------- |
| 작업 | 작업의 표시 이름 또는 GUID입니다. |
| file_index | 0에서 시작 합니다. |
| TRUE 또는 FALSE | **TRUE** 로 설정 하면 지정 된 파일에 대 한 콘텐츠 유효성 검사가 설정 되지만 **FALSE** 는 해제 됩니다. |

## <a name="examples"></a>예

다음 예에서는 파일 2의 콘텐츠 유효성 검사 상태를 *Mydownloadjob*이라는 작업에 대해 TRUE로 설정 합니다.

```
C:\>bitsadmin /setvalidationstate myDownloadJob 2 TRUE
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)