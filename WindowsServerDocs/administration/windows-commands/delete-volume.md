---
title: delete volume
description: 볼륨 삭제 명령에 대 한 참조 문서로, 선택한 볼륨을 삭제 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f625933d-0f47-409e-93b2-a3e234049a5d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 217e9ff1ccb470b5431143360286d312b09a1951
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928719"
---
# <a name="delete-volume"></a>delete volume

선택한 볼륨을 삭제 합니다. 시작 하기 전에이 작업을 수행 하려면 볼륨을 선택 해야 합니다. 사용 하 여는 [볼륨 선택](select-volume.md) 볼륨을 선택 하 고 포커스를 이동 하는 명령입니다.

> [!IMPORTANT]
> 시스템 볼륨, 부팅 볼륨 또는 활성 페이징 파일이 나 크래시 덤프 (메모리 덤프)를 포함 하는 볼륨은 삭제할 수 없습니다.

## <a name="syntax"></a>구문

```
delete volume [noerr]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| noerr | 스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다. |

## <a name="examples"></a>예

포커스가 있는 볼륨을 삭제 하려면 다음을 입력 합니다.

```
delete volume
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [select volume](select-volume.md)

- [delete 명령](delete.md)