---
title: bitsadmin setvalidationstate
description: 작업 내에서 지정 된 파일의 콘텐츠 유효성 검사 상태를 설정 하는 bitsadmin setvalidationstate 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e8fc8e8c-171c-4681-8057-6986b018e576
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ae776279b742e3af5af3cf555765007bbf0eb8de
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927491"
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

*Mydownloadjob*이라는 작업에 대해 파일 2의 콘텐츠 유효성 검사 상태를 TRUE로 설정 하려면 다음을 수행 합니다.

```
bitsadmin /setvalidationstate myDownloadJob 2 TRUE
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
