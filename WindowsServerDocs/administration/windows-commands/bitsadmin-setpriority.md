---
title: bitsadmin setpriority
description: 지정 된 작업의 우선 순위를 설정 하는 bitsadmin setpriority 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 90788363-01a2-4d7c-a560-a3eba45b5e9e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 556a1d94700780ea22acc1e4c2f32961c0e43342
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717261"
---
# <a name="bitsadmin-setpriority"></a>bitsadmin setpriority

지정된 된 작업의 우선 순위를 설정합니다.

## <a name="syntax"></a>구문

```
bitsadmin /setpriority <job> <priority>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |
| priority | 다음을 포함 하 여 작업의 우선 순위를 설정 합니다.<ul><li>FOREGROUND</li><li>HIGH</li><li>NORMAL</li><li>LOW</li></ul> |

## <a name="examples"></a>예

*Mydownloadjob* 이라는 작업의 우선 순위를 normal로 설정 하려면 다음을 수행 합니다.

```
bitsadmin /setpriority myDownloadJob NORMAL
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
