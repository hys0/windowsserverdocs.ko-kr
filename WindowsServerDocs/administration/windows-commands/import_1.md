---
title: diskpart 가져오기
description: 로컬 컴퓨터의 디스크 그룹으로 외부 디스크 그룹을 가져오는 가져오기 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4b9d2751-7637-4738-83b0-8c578eb28f27
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 072c012e5e2cc8d49811fbfa1cff5140b2c745a1
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85924427"
---
# <a name="import-diskpart"></a>import (diskpart)

로컬 컴퓨터의 디스크 그룹에 외부 디스크 그룹을 가져옵니다. 이 명령은 포커스가 있는 디스크와 동일한 그룹에 있는 모든 디스크를 가져옵니다.

> 중요 한 이 명령을 사용 하려면 먼저 [디스크 선택 명령을](select-disk.md) 사용 하 여 외부 디스크 그룹에서 동적 디스크를 선택 하 고 포커스를 이동 해야 합니다.

## <a name="syntax"></a>구문

```
import [noerr]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| --------- | ----------- |
| noerr | 스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다. |

### <a name="examples"></a>예

로컬 컴퓨터의 디스크 그룹에 포커스가 있는 디스크와 같은 디스크 그룹에 있는 모든 디스크를 가져오려면 다음을 입력 합니다.

```
import
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [diskpart 명령](diskpart.md)
