---
title: bitsadmin getpriority
description: 지정 된 작업의 우선 순위를 검색 하는 bitsadmin getpriority 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 39ce769e2eb1dcf7a05d416dc2a66c6c082c9ae4
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926853"
---
# <a name="bitsadmin-getpriority"></a>bitsadmin getpriority

지정된 된 작업의 우선 순위를 검색합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getpriority <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

#### <a name="output"></a>출력

이 명령에 대해 반환 된 우선 순위는 다음과 같을 수 있습니다.

- **전경색**

- **최고**

- **일반적**

- **거의**

- **UNKNOWN**

## <a name="examples"></a>예

*Mydownloadjob*이라는 작업의 우선 순위를 검색 하려면 다음을 수행 합니다.

```
bitsadmin /getpriority myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
