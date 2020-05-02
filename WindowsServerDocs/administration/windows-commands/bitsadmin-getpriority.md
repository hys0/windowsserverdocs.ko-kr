---
title: bitsadmin getpriority
description: 지정 된 작업의 우선 순위를 검색 하는 bitsadmin getpriority 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 38f92e83ccf5b048d168ce6a21c6026f490b18bf
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717673"
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

- **HIGH**

- **일반적**

- **LOW**

- **없습니다**

## <a name="examples"></a>예

*Mydownloadjob*이라는 작업의 우선 순위를 검색 하려면 다음을 수행 합니다.

```
bitsadmin /getpriority myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
