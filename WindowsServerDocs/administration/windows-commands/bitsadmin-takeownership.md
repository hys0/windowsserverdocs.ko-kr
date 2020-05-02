---
title: bitsadmin takeownership
description: 관리 권한이 있는 사용자가 지정 된 작업의 소유권을 가질 수 있도록 하는 bitsadmin takeownership 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ea0ce7cb-440a-498f-a3ef-8368fa43e399
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5369cb3fa143ebde77ae8cabf04b9a38eed5b9c5
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720441"
---
# <a name="bitsadmin-takeownership"></a>bitsadmin takeownership

관리자 권한으로는 사용자가 지정된 된 작업의 소유권을 가져올 수 있습니다.

## <a name="syntax"></a>구문

```
bitsadmin /takeownership <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ---------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a>예

이름이 *Mydownloadjob*인 작업의 소유권을 가져올 수 있습니다.

```
bitsadmin /takeownership myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
