---
title: bitsadmin geterror
description: 지정 된 작업에 대 한 자세한 오류 정보를 검색 하는 bitsadmin geterror 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cbe5bca1-d2dd-4ce6-903f-f85de4a2ec6a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1d729b946df4af33da3a55ff8051c59fbb5d7efe
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928307"
---
# <a name="bitsadmin-geterror"></a>bitsadmin geterror

지정 된 작업에 대 한 자세한 오류 정보를 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /geterror <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a>예

이름이 *Mydownloadjob*인 작업에 대 한 오류 정보를 검색 하려면 다음을 수행 합니다.

```
bitsadmin /geterror myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
