---
title: 오프 라인 디스크
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8fb9b3c3-0b2c-4192-a2e7-f706292653e3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f28d473cdb557d6adb3aaf235bebdfbc4e78b24a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372605"
---
# <a name="offline-disk"></a>오프 라인 디스크



포커스가 있는 온라인 디스크는 오프 라인 상태로 이동합니다.

> [!IMPORTANT]
> 이 DiskPart 명령을 Windows Vista의 모든 버전에서 사용할 수 없는 경우

## <a name="syntax"></a>구문

```
offline disk [noerr]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|noerr|스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다.|

## <a name="remarks"></a>설명

-   이 명령은 SAN 온라인 모드에 있는 디스크에서 작동 합니다. 자신의 SAN 모드를 오프 라인으로 변경 됩니다.
-   디스크의 상태가으로 변경 된 동적 디스크의 디스크 그룹을 오프 라인 상태인 경우 **누락** 그룹은 오프 라인 상태인 디스크를 보여 줍니다. 손실 된 디스크는 잘못 된 그룹으로 이동 됩니다. 동적 디스크 그룹의 마지막 디스크 이면 디스크의 상태가으로 변경 됩니다 **오프 라인**, 빈 그룹을 제거 됩니다.
-   디스크를 선택 해야는 **오프 라인 디스크** 명령을 성공적으로 합니다. 사용 된 **디스크 선택** 디스크를 선택 하 고 포커스를 이동 하는 명령입니다.

## <a name="BKMK_examples"></a>예와

포커스가 있는 디스크를 오프 라인으로 다음을 입력 합니다.
```
offline disk
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)

