---
title: bitsadmin nowrap
description: '**Bitsadmin nowrap** 에 대 한 Windows 명령 항목-명령 창의 가장 오른쪽 가장자리를 벗어나 확장 되는 출력 텍스트 줄을 자릅니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 85a47b90-783a-41e4-96f2-81f26ae8ca93
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3806ec51161eeae498e3c9b367b2aacf0bd32c99
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381047"
---
# <a name="bitsadmin-nowrap"></a>bitsadmin nowrap

출력 명령 창 맨 오른쪽 가장자리로 벗어난 텍스트의 줄을 자릅니다.

## <a name="syntax"></a>구문

```
bitsadmin /NoWrap
```

## <a name="remarks"></a>설명

기본적으로 **모니터** 스위치를 제외한 모든 스위치는 출력을 래핑합니다. 다른 스위치 앞에 **NoWrap** 스위치를 지정 합니다.

## <a name="BKMK_examples"></a>예와

다음 예제에서는 명명 된 작업에 대 한 상태를 검색 *myDownloadJob* 고 출력 래핑하지 않습니다
```
C:\>bitsadmin /NoWrap /GetState myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)