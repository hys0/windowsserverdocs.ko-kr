---
title: bitsadmin getvalidationstate
description: 작업 내에서 지정 된 파일의 콘텐츠 유효성 검사 상태를 보고 하는 bitsadmin getvalidationstate 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6ada3f1f-9967-4262-9d22-ed641e23f516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ca753b20a1b7834d2e05d4ff8729a08332256f8c
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717457"
---
# <a name="bitsadmin-getvalidationstate"></a>bitsadmin getvalidationstate

작업 내에서 지정된 된 파일의 콘텐츠 유효성 검사 상태를 보고합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getvalidationstate <job> <file_index>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |
| file_index | 0부터 시작 합니다. |

## <a name="examples"></a>예

*Mydownloadjob*이라는 작업 내에서 파일 2의 콘텐츠 유효성 검사 상태를 검색 하려면 다음을 수행 합니다.

```
bitsadmin /getvalidationstate myDownloadJob 1
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
