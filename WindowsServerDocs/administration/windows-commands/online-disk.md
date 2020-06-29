---
title: online disk
description: 온라인 디스크 명령에 대 한 참조 항목으로, 오프 라인 디스크를 온라인 상태로 전환 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bc44a783-eaa4-40ca-be01-5703b5bf4eb3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 954e52788f3236cb9b2898a23edae25d5b22deb8
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85472688"
---
# <a name="online-disk"></a>online disk

오프 라인 디스크를 온라인 상태로 전환 합니다. 기본 디스크의 경우이 명령은 선택한 디스크와 해당 디스크의 모든 볼륨을 온라인 상태로 전환 하려고 시도 합니다. 동적 디스크의 경우이 명령은 로컬 컴퓨터에 외부로 표시 되지 않은 모든 디스크를 온라인 상태로 만들려고 합니다. 또한 동적 디스크 집합의 모든 볼륨을 온라인 상태로 만들려고 합니다.

디스크 그룹의 동적 디스크가 온라인 상태가 되 고 그룹의 유일한 디스크인 경우 원래 그룹이 다시 만들어지고 디스크가 해당 그룹으로 이동 됩니다. 그룹에 다른 디스크가 있고 온라인 상태인 경우에는 디스크가 그룹에 다시 추가 됩니다. 선택한 디스크의 그룹이 미러 또는 RAID-5 볼륨을 포함 하는 경우에도이 명령은 이러한 볼륨을 다시 동기화 합니다.

> [!NOTE]
> **온라인 디스크** 명령을 성공적으로 수행 하려면 디스크를 선택 해야 합니다. 사용 된 [디스크 선택](select-disk.md) 디스크를 선택 하 고 포커스를 이동 하는 명령입니다.

> [!IMPORTANT]
> 이 명령은 읽기 전용 디스크에서 사용 되는 경우 실패 합니다.

## <a name="syntax"></a>구문

```
online disk [noerr]
```

### <a name="parameters"></a>매개 변수

이 명령을 사용 하는 방법에 대 한 지침은 [누락 되었거나 오프 라인 동적 디스크 다시 활성화](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732026(v=ws.11))를 참조 하세요.

| 매개 변수 | 설명 |
|--|--|
| noerr | 스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다. |

### <a name="examples"></a>예제

온라인으로 포커스가 있는 디스크를 사용 하려면 다음을 입력 합니다.

```
online disk
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
