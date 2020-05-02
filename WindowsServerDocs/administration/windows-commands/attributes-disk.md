---
title: 특성 디스크
description: 디스크의 특성을 표시, 설정 또는 삭제 하는 attributes disk 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: eed57071-c1c6-4394-9542-62b52a878c92
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c3d378439b30328e4df48020fa4b3288f7af31c6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718893"
---
# <a name="attributes-disk"></a>특성 디스크

표시 설정 하거나 디스크의 특성을 지웁니다. 이 명령을 사용 하 여 디스크의 현재 특성을 표시 하는 경우 시작 디스크 특성은 컴퓨터를 시작 하는 데 사용 되는 디스크를 나타냅니다. 동적 미러의 경우 부팅 볼륨의 부팅 플렉스를 포함 하는 디스크를 표시 합니다.

> [!IMPORTANT]
> 디스크를 선택 해야는 **특성 디스크** 명령을 성공적으로 합니다. 사용 된 **디스크 선택** 디스크를 선택 하 고 포커스를 이동 하는 명령입니다.

## <a name="syntax"></a>구문

```
attributes disk [{set | clear}] [readonly] [noerr]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| set | 포커스가 있는 디스크의 지정된 된 특성을 설정합니다. |
| 지우기 | 포커스가 있는 디스크의 지정된 된 특성을 지웁니다. |
| readonly | 디스크가 읽기 전용으로 지정 합니다. |
| noerr | 스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다. |

## <a name="examples"></a>예

선택된 된 디스크의 특성을 보려면 다음을 입력 합니다.

```
attributes disk
```

선택한 디스크를 읽기 전용으로 설정 하려면 다음을 입력 합니다.

```
attributes disk set readonly
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [디스크 선택 명령](select-disk.md)
