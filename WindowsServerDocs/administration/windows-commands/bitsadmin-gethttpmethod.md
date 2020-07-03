---
title: bitsadmin gethttpmethod
description: 작업에 사용할 HTTP 동사를 가져오는 bitsadmin gethttpmethod 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 3a963eb275c6e635849094906c52fedf90dccd0d
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927027"
---
# <a name="bitsadmin-gethttpmethod"></a>bitsadmin gethttpmethod

작업에 사용할 HTTP 동사를 가져옵니다.

## <a name="syntax"></a>구문

```
bitsadmin /gethttpmethod <Job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a>예

*Mydownloadjob*이라는 작업과 함께 사용할 HTTP 동사를 검색 하려면 다음을 수행 합니다.

```
bitsadmin /gethttpmethod myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
