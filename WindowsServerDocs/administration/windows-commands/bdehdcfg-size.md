---
title: bdehdcfg size
description: 새 시스템 드라이브를 만들 때 시스템 파티션의 크기를 지정 하는 bdehdcfg size 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 80f55b1d-a28d-4edf-9997-1fb918b7b5a1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 365ed82e90b00189a400725cfcaaec09b0ba3b53
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923429"
---
# <a name="bdehdcfg-size"></a>bdehdcfg: 크기

새 시스템 드라이브를 만들 때 시스템 파티션의 크기를 지정 합니다. 크기를 지정 하지 않으면 도구 기본값인 300MB를 사용 합니다. 시스템 드라이브의 최소 크기는 100MB입니다. 저장 하려는 경우 다른 시스템 도구 또는 시스템 복구 시스템 파티션에, 크기를 늘려야는 적절 하 게 합니다.

> [!NOTE]
> **Size** 명령은 명령과 함께 사용할 수 없습니다 `target <drive_letter> merge` .

## <a name="syntax"></a>구문

```
bdehdcfg -target {default|unallocated|<drive_letter> shrink} -size <size_in_mb>
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<size_in_mb>` | 메가바이트 (MB)는 새 파티션의 사용 하 여 수를 나타냅니다. |

## <a name="examples"></a>예

기본 시스템 드라이브에 500 MB를 할당 하려면 다음을 수행 합니다.

```
bdehdcfg -target default -size 500
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bdehdcfg](bdehdcfg.md)
