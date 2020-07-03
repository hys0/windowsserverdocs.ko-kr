---
title: 활성
description: 기본 디스크에 있는 활성 명령에 대 한 참조 문서는 포커스가 있는 파티션을 활성으로 표시 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1f25da2e-87fc-4392-a7ee-f38d09b7873c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a5df2f67c087be31190c512be0f6b20d8a1d72cb
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85924147"
---
# <a name="active"></a>활성

기본 디스크에 활성으로 포커스가 있는 파티션을 표시합니다. 파티션만 활성으로 표시할 수 있습니다. 이 작업을 수행 하려면 파티션을 선택 해야 합니다. 사용 된 **파티션을 선택** 파티션을 선택 하 고 포커스를 이동 하는 명령입니다.

> [!CAUTION]
> DiskPart는 BIOS (기본 입출력 시스템) 또는 확장 가능 펌웨어 인터페이스 (EFI)에 게 파티션 또는 볼륨이 유효한 시스템 파티션 또는 시스템 볼륨 이며 운영 체제 시작 파일을 포함할 수 있음을 알립니다. 파티션의 내용을 확인 하지 않습니다. 파티션을 활성으로 잘못 표시 하는 경우 운영 체제 시작 파일을 포함 하지 않는 컴퓨터 시작할 수 없습니다.

## <a name="syntax"></a>구문

```
active
```

## <a name="examples"></a>예

파티션을 활성 파티션으로 포커스가 있는 상태를 표시 하려면 다음을 입력 합니다.

```
active
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [파티션 선택 명령](select-partition.md)
