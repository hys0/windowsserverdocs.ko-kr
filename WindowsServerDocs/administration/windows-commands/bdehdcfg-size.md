---
title: bdehdcfg 크기
description: Windows 명령 항목-새 시스템 드라이브를 만들 때 시스템 파티션의 크기를 지정 합니다.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 80f55b1d-a28d-4edf-9997-1fb918b7b5a1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6ec42cdb5716c63c7210ea6cfde8ce8884833b45
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382202"
---
# <a name="bdehdcfg-size"></a>bdehdcfg: 크기



새 시스템 드라이브를 만들 때 시스템 파티션의 크기를 지정 합니다. 이 명령을 사용할 수 있는 방법을의 예제를 참조 하십시오. [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink} -size <SizeinMB>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<SizeinMB >|메가바이트 (MB)는 새 파티션의 사용 하 여 수를 나타냅니다.|

## <a name="remarks"></a>설명

크기를 지정 하지 않으면 도구 기본값인 300MB를 사용 합니다. 시스템 드라이브의 최소 크기는 100MB입니다. 저장 하려는 경우 다른 시스템 도구 또는 시스템 복구 시스템 파티션에, 크기를 늘려야는 적절 하 게 합니다.

> [!NOTE]
> **Size** 명령은 **대상** \<DriveLetter > **merge** 명령과 함께 사용할 수 없습니다.

## <a name="BKMK_Examples"></a>예와

다음 예제를 사용 하는 **크기** 500MB의 기본 시스템 드라이브에 할당 하기 위해 명령입니다.
```
bdehdcfg -target default -size 500
```

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)
-   [Bdehdcfg](bdehdcfg.md)