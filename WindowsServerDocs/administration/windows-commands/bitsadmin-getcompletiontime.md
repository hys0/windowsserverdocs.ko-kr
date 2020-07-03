---
title: bitsadmin getcompletiontime
description: 작업에서 데이터 전송을 완료 한 시간을 검색 하는 bitsadmin getcompletiontime 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7a4b3c1c-9832-4724-86b2-cce3c01bfa28
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e07dd6a345cd1bd58277ef08e08802a62d6e6772
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923109"
---
# <a name="bitsadmin-getcompletiontime"></a>bitsadmin getcompletiontime

작업에서 데이터 전송을 완료 한 시간을 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getcompletiontime <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a>예

*Mydownloadjob* 이라는 작업에서 데이터 전송을 완료 한 시간을 검색 하려면 다음을 수행 합니다.

```
bitsadmin /getcompletiontime myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
