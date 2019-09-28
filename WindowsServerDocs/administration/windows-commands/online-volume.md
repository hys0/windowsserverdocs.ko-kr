---
title: 온라인 볼륨
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5da073fd-578d-4691-ad0f-605ba66e0c7e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 06a3c81313180b2880c1e47c3b6c12236fda4245
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372520"
---
# <a name="online-volume"></a>온라인 볼륨



볼륨을 온라인 상태로 현재 오프 라인 상태를 제공 합니다.

> [!IMPORTANT]
> 모든 버전의 Windows Vista에서는이 명령을 사용할 수 없습니다.

> [!IMPORTANT]
> 이 명령은 읽기 전용 볼륨에 사용 되는 경우 실패 합니다.

## <a name="syntax"></a>구문

```
online volume [noerr]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|noerr|스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다.|

## <a name="remarks"></a>설명

-   이 명령은 실패 한, 실패 또는 중복 실패 상태에 있는 볼륨에서 작동 합니다.
-   이 명령을 성공적으로 볼륨을 선택 해야 합니다. 사용 하 여는 **볼륨 선택** 볼륨을 선택 하 고 포커스를 이동 하는 명령입니다.

## <a name="BKMK_examples"></a>예와

온라인에 포커스가 있는 볼륨을 상태로 전환 하려면 다음을 입력 합니다.
```
online volume
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)

