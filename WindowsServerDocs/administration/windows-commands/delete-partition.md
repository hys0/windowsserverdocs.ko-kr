---
title: 파티션 삭제
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 65752312-cb16-46f6-870f-1b95c507b101
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 46a214f26e7c21f6ae08eb16d95fd898bd949b0f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378659"
---
# <a name="delete-partition"></a>파티션 삭제



포커스가 있는 파티션을 삭제합니다.

## <a name="syntax"></a>구문

```
delete partition [noerr] [override]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|재정의|DiskPart를 유형에 관계 없이 모든 파티션을 삭제할 수 있습니다. 일반적으로 DiskPart만 사용 하면 알려진된 데이터 파티션을 삭제할 수 있습니다.|
|noerr|스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다.|

## <a name="remarks"></a>설명

> [!CAUTION]
> 동적 디스크의 파티션을 삭제 있으므로 모든 데이터를 삭제 하 고 디스크 손상 된 상태로 두면 디스크의 모든 동적 볼륨을 삭제할 수 있습니다. 동적 볼륨을 삭제 하려면 항상 사용은 **볼륨을 삭제** 명령을 사용 합니다. 동적 디스크에서 파티션을 삭제할 수 있지만 이러한를 만들 수 없습니다. 예를 들어 동적 GPT 디스크에서 인식할 수 없는 GPT (GUID 파티션 테이블) 파티션을 삭제할 수 있습니다. 이러한 파티션을 삭제 하는 경우에 결과 생긴 여유 공간을 사용할 수 있는 발생 하지 않습니다. 이 명령은 reclame 응급 상황에서 손상된 된 오프 라인 동적 디스크 공간을 허용 하면 만들어졌습니다 여기서는 **정리** DiskPart에서 명령을 사용할 수 없습니다.
> -   시스템 파티션, 부팅 파티션 또는 활성 페이징 파일이 나 크래시 덤프 정보를 포함 하는 파티션의 삭제할 수 없습니다.
> -   이 작업을 수행 하려면 파티션을 선택 해야 합니다. 사용 된 **파티션을 선택** 파티션을 선택 하 고 포커스를 이동 하는 명령입니다.

## <a name="BKMK_examples"></a>예와

포커스가 있는 파티션을 삭제 하려면 다음을 입력 합니다.
```
delete partition
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)

