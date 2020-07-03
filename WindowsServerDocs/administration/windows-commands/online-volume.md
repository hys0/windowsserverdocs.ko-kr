---
title: online volume
description: 온라인 볼륨 명령에 대 한 참조 문서로, 오프 라인 볼륨을 온라인 상태로 전환 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5da073fd-578d-4691-ad0f-605ba66e0c7e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2378b4cbc4f0624a0f1d65c62337d4c1a856648c
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933522"
---
# <a name="online-disk"></a>online disk

오프 라인 볼륨을 온라인 상태로 전환 합니다. 이 명령은 실패 하거나, 실패 하거나, 중복 된 중복성 상태가 아닌 볼륨에서 작동 합니다.

> [!NOTE]
> **온라인 볼륨** 명령을 성공적으로 수행 하려면 볼륨을 선택 해야 합니다. 사용 하 여는 [볼륨 선택](select-volume.md) 볼륨을 선택 하 고 포커스를 이동 하는 명령입니다.

> [!IMPORTANT]
> 이 명령은 읽기 전용 디스크에서 사용 되는 경우 실패 합니다.

## <a name="syntax"></a>구문

```
online volume [noerr]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|--|--|
| noerr | 스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다. |

### <a name="examples"></a>예

온라인으로 포커스가 있는 볼륨을 사용 하려면 다음을 입력 합니다.

```
online volume
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
