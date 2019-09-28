---
title: 디스크 세부 정보
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6b09cf40-8d93-452b-b449-5242e62a4102
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ff78a3f9e27cde35a7e19bdf1565c515a127261b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378579"
---
# <a name="detail-disk"></a>디스크 세부 정보



해당 디스크에 선택된 된 디스크와 볼륨의 속성을 표시합니다.

## <a name="syntax"></a>구문

```
detail disk
```

## <a name="remarks"></a>설명

-   이 작업을 수행 하려면 디스크를 선택 해야 합니다. 사용 된 **디스크 선택** 디스크를 선택 하 고 포커스를 이동 하는 명령입니다.
-   선택한 디스크가 VHD (가상 하드 디스크) 인 경우 **정보 디스크** 는 디스크의 버스 유형을 가상으로 보고 합니다.

## <a name="BKMK_examples"></a>예와

디스크의 볼륨에 대 한 정보와 선택한 디스크 속성을 보려면 다음을 입력 합니다.
```
detail disk
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)

