---
title: bitsadmin getmodificationtime
description: 작업이 마지막으로 수정 되었거나 데이터가 성공적으로 전송 된 시간을 검색 하는 bitsadmin getmodificationtime 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e543945e-92c4-491e-8c2d-344f8a3e342d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9055c0ac70bc2360601ecd1b1f91c8ad3908d704
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928166"
---
# <a name="bitsadmin-getmodificationtime"></a>bitsadmin getmodificationtime

작업이 마지막으로 수정 되었거나 데이터가 성공적으로 전송 된 시간을 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getmodificationtime <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a>예

*Mydownloadjob*이라는 작업의 마지막 수정 시간을 검색 하려면 다음을 수행 합니다.

```
bitsadmin /getmodificationtime myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
