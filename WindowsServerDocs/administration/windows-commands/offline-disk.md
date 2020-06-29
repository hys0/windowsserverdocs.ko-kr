---
title: offline disk
description: 오프 라인 상태에 포커스가 있는 온라인 디스크를 사용 하는 오프 라인 디스크 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8fb9b3c3-0b2c-4192-a2e7-f706292653e3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1c62a79db39a7c36e14a8430b47c634f80c0c0c8
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85472749"
---
# <a name="offline-disk"></a>offline disk

포커스가 있는 온라인 디스크는 오프 라인 상태로 이동합니다. 디스크 그룹의 동적 디스크를 오프 라인으로 전환 하는 경우 디스크의 상태가 **없음** 으로 변경 되 고 그룹에 오프 라인 상태인 디스크가 표시 됩니다. 손실 된 디스크는 잘못 된 그룹으로 이동 됩니다. 동적 디스크가 그룹의 마지막 디스크인 경우 디스크의 상태가 **오프 라인**으로 변경 되 고 빈 그룹이 제거 됩니다.

> [!NOTE]
> 디스크를 선택 해야는 **오프 라인 디스크** 명령을 성공적으로 합니다. 사용 된 [디스크 선택](select-disk.md) 디스크를 선택 하 고 포커스를 이동 하는 명령입니다.
>
> 이 명령은 san 모드를 오프 라인으로 변경 하 여 SAN 온라인 모드의 디스크 에서도 작동 합니다.

## <a name="syntax"></a>구문

```
offline disk [noerr]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| noerr | 스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다. |

### <a name="examples"></a>예제

포커스가 있는 디스크를 오프 라인으로 다음을 입력 합니다.

```
offline disk
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
