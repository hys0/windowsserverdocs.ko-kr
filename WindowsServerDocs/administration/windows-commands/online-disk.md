---
title: 온라인 디스크
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bc44a783-eaa4-40ca-be01-5703b5bf4eb3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3d798bf34ec2f9d2f01b5470c4ec52f936674135
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372514"
---
# <a name="online-disk"></a>온라인 디스크



현재 온라인 상태로 오프 라인인 디스크를 제공 합니다.

> [!IMPORTANT]
> 모든 버전의 Windows Vista에서는이 명령을 사용할 수 없습니다.

> [!IMPORTANT]
> 이 명령은 읽기 전용 디스크에 사용 되는 경우 실패 합니다.

이 명령을 사용 하는 방법에 대 한 지침은 [없거나 오프 라인 동적 디스크 다시 활성화](https://go.microsoft.com/fwlink/?LinkId=207046) (https://go.microsoft.com/fwlink/?LinkId=207046) 을 참조 하세요.

## <a name="syntax"></a>구문

```
online disk [noerr]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|noerr|스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다.|

## <a name="remarks"></a>설명

-   Windows Vista에서 매개 변수 없이 사용 하는 경우이 명령은 디스크 그룹에서 작동 합니다. 기본 디스크를는 그룹당 둘 이상의 디스크 되지 않습니다. 동적 디스크의 경우이 그룹에는 모든 비 외부 동적 디스크가 포함 됩니다.
-   기본 디스크의 경우이 명령은 온라인 선택한 디스크와 모든 볼륨을 해당 디스크에 하려고 합니다.
-   동적 디스크의 경우이 명령은 로컬 컴퓨터에서 외부 디스크로 표시 되지 않는 모든 디스크를 온라인 상태로 하려고 합니다. 동적 디스크 세트에 모든 볼륨을 온라인 상태로 시도 합니다.
-   디스크 그룹에 동적 디스크가 온라인 상태가 될 경우 그룹에만 디스크는 원래 그룹은 다시 만들어집니다. 그리고 디스크가 해당 그룹으로 이동 합니다. 그룹의 다른 디스크 되는 경우 온라인 디스크 다시 그룹에 추가 하면 됩니다.
-   선택한 디스크의 그룹이 미러 또는 RAID-5 볼륨을 포함 하는 경우에도이 명령은 이러한 볼륨을 다시 동기화 합니다.
-   이 명령을 성공적으로 디스크를 선택 해야 합니다. 사용 된 **디스크 선택** 디스크를 선택 하 고 포커스를 이동 하는 명령입니다.

## <a name="BKMK_examples"></a>예와

온라인에 포커스가 있는 디스크를 상태로 전환 하려면 다음을 입력 합니다.
```
online disk
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)

