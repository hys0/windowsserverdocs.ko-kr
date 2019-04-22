---
title: bitsadmin nowrap
description: Windows 명령 항목에 대 한 **bitsadmin nowrap** -출력 명령 창 맨 오른쪽 가장자리로 벗어난 텍스트의 줄을 자릅니다.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 4130f606a6b1874e1ea31952160de44d6e09c6b6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822924"
---
# <a name="bitsadmin-nowrap"></a>bitsadmin nowrap

출력 명령 창 맨 오른쪽 가장자리로 벗어난 텍스트의 줄을 자릅니다.

## <a name="syntax"></a>구문

```
bitsadmin /NoWrap
```

## <a name="remarks"></a>설명

기본적으로 모든 스위치를 제외 합니다 **모니터** 전환, 출력을 래핑합니다. 지정 된 **NoWrap** 다른 스위치 전에 전환 합니다.

## <a name="BKMK_examples"></a>예제

다음 예제에서는 명명 된 작업에 대 한 상태를 검색 *myDownloadJob* 고 출력 래핑하지 않습니다
```
C:\>bitsadmin /NoWrap /GetState myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)