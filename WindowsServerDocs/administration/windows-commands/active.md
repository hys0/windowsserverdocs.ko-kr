---
title: active
description: Windows 명령 항목에 대 한 **활성** -기본 디스크에 활성으로 포커스가 있는 파티션을 표시 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1f25da2e-87fc-4392-a7ee-f38d09b7873c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3a039e0200fb84d446739ac7017556b6c302f4af
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868764"
---
# <a name="active"></a>active



기본 디스크에 활성으로 포커스가 있는 파티션을 표시합니다.

> [!CAUTION]
> DiskPart는 파티션을 운영 체제 시작 파일이 포함 될 수 인지만 확인 합니다. 파티션의 내용을 확인 하지 않습니다. 파티션을 활성으로 잘못 표시 하는 경우 운영 체제 시작 파일을 포함 하지 않는 컴퓨터 시작할 수 없습니다.

## <a name="syntax"></a>구문

```
active
```

## <a name="remarks"></a>설명

-   이 통해 알립니다 기본 입/출력 시스템 (BIOS) 또는 인터페이스 EFI (Extensible Firmware) 파티션 또는 볼륨은 유효한 시스템 파티션 또는 시스템 볼륨입니다.
-   파티션만 활성으로 표시할 수 있습니다.
-   이 작업을 수행 하려면 파티션을 선택 해야 합니다. 사용 된 **파티션을 선택** 파티션을 선택 하 고 포커스를 이동 하는 명령입니다.

## <a name="BKMK_examples"></a>예제

파티션을 활성 파티션으로 포커스가 있는 상태를 표시 하려면 다음을 입력 합니다.
```
active
```

#### <a name="additional-references"></a>추가 참조

