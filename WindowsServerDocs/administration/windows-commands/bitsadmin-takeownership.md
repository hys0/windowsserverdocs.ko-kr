---
title: bitsadmin takeownership
description: 관리 권한이 있는 사용자가 지정 된 작업의 소유권을 가질 수 있도록 하는 bitsadmin takeownership 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ea0ce7cb-440a-498f-a3ef-8368fa43e399
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bc406d1d5f7c9553082f85f3315ab7622f6bc7db
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927461"
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
