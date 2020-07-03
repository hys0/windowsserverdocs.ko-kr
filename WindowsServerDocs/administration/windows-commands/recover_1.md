---
title: recover
description: 디스크 그룹에 있는 모든 디스크의 상태를 새로 고치고, 잘못 된 디스크 그룹의 디스크를 복구 하 고, 오래 된 데이터를 가진 RAID-5 볼륨 및 미러 볼륨을 다시 동기화 하는 DiskPart 복구 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8cc3a73d-9456-41a0-b375-2b4cc37c3992
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 19272e09147bb730e07d51d42926c01262bfb433
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85924792"
---
# <a name="recover"></a>recover

디스크 그룹에 있는 모든 디스크의 상태를 새로 고치고, 잘못 된 디스크 그룹의 디스크를 복구 하 고, 오래 된 데이터를 가진 RAID-5 볼륨 및 미러 볼륨을 다시 동기화 합니다. 이 명령은 실패 한 디스크 또는 실패에 작동 합니다. 중복 실패 상태 또는 실패 한을 실패 한 볼륨에서 작동 합니다.

이 명령은 동적 디스크 그룹에 대해 작동 합니다. 이 명령을 기본 디스크가 있는 그룹에서 사용 하는 경우 오류가 반환 되지 않지만 아무 동작도 수행 되지 않습니다.

> [!NOTE]
>  이 작업을 수행 하려면 디스크 그룹의 일부인 디스크를 선택 해야 합니다. 디스크 [선택 명령을](select-disk.md) 사용 하 여 디스크를 선택 하 고 포커스를 이동 합니다.



## <a name="syntax"></a>구문

```
recover [noerr]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|--|--|
| noerr | 스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다. |

## <a name="examples"></a>예

포커스가 있는 디스크를 포함 하 여 디스크 그룹을 복구 하려면 다음을 입력 합니다.

```
recover
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
