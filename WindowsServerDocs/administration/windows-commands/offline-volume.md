---
title: offline volume
description: 오프 라인 상태에 포커스가 있는 온라인 볼륨을 사용 하는 오프 라인 볼륨 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b8f7192f-ea38-47d0-9d4e-58ef68336ae6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e49a88671285bed69cfbb9c4e7bc950eb100b3e6
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85472719"
---
# <a name="offline-volume"></a>offline volume

포커스가 있는 온라인 볼륨을 오프 라인 상태로 이동합니다.

> [!NOTE]
> **오프 라인 볼륨** 명령을 성공적으로 수행 하려면 볼륨을 선택 해야 합니다. 사용 하 여는 [볼륨 선택](select-volume.md) 디스크를 선택 하 고 포커스를 이동 하는 명령입니다.

## <a name="syntax"></a>구문

```
offline volume [noerr]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| noerr | 스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다. |

### <a name="examples"></a>예제

포커스가 있는 디스크를 오프 라인으로 다음을 입력 합니다.

```
offline volume
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
