---
title: 복구
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cc3a73d-9456-41a0-b375-2b4cc37c3992
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 261bfd79d74323ad324246e21b84a5eb798ebcdf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867184"
---
# <a name="recover"></a>복구



디스크 그룹의 모든 디스크의 상태를 새로 고쳐, 잘못 된 디스크 그룹에서 디스크를 복구 하려고 및 미러 볼륨 및 raid-5 볼륨 오래 된 데이터가 포함 된 다시 동기화 합니다.

> [!IMPORTANT]
> 이 DiskPart 명령을 Windows Vista의 모든 버전에서 사용할 수 없는 경우

## <a name="syntax"></a>구문

```
recover [noerr]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|noerr|만 스크립팅 합니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다.|

## <a name="remarks"></a>설명

-   이 명령은 디스크 그룹에서 작동합니다.
-   이 명령은 그룹의 동적 디스크에만 적용 됩니다. 기본 디스크를 갖는 그룹에이 명령을 사용 하는 경우 오류를 반환 하지 않습니다 하지만 아무 작업도 수행 되지 않습니다.
-   이 명령은 실패 한 디스크 또는 실패에 작동 합니다. 중복 실패 상태 또는 실패 한을 실패 한 볼륨에서 작동 합니다.
-   이 명령을 제대로 수행 하려면 디스크 그룹의 일부인 디스크를 선택 해야 합니다. 사용 된 **디스크 선택** 디스크를 선택 하 고 포커스를 이동 하는 명령입니다.

## <a name="BKMK_examples"></a>예제

포커스가 있는 디스크를 포함 하 여 디스크 그룹을 복구 하려면 다음을 입력 합니다.
```
recover
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)

