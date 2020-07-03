---
title: bitsadmin getowner
description: 지정 된 작업의 소유자를 검색 하는 bitsadmin getowner 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5203f84c-a879-4f31-ae3e-7ea74bd63ca5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f530952e510fdff1a30dfd7c6081e112d841f401
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926899"
---
# <a name="bitsadmin-getowner"></a>bitsadmin getowner

지정 된 작업의 소유자에 대 한 표시 이름 또는 GUID를 표시 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getowner <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a>예

*Mydownloadjob*이라는 작업의 소유자를 표시 하려면:

```
bitsadmin /getowner myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
