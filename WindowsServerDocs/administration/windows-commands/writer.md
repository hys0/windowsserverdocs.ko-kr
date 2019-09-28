---
title: 저자
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7cf98295-411d-4705-8573-f898ff45c140
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6c00f6067cd5f6cf741cddbd6d62c5bcbb1f37a9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361862"
---
# <a name="writer"></a>저자



기록기 또는 구성 요소 포함 또는 백업 또는 복원 프로시저에서 기록기 또는 구성 요소를 제외를 확인 합니다. 매개 변수 없이 사용 하는 경우 **기록기** 명령 프롬프트에서 도움말을 표시 합니다.

## <a name="syntax"></a>구문

```
writer verify [<Writer> | <Component>]
writer exclude [<Writer> | <Component>]
```

## <a name="parameters"></a>매개 변수

| 매개 변수  |                                                                                      설명                                                                                      |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   확인   | 백업 또는 복원 프로시저에는 지정 된 작성기 나 구성 요소가 포함 되어 있는지 확인 합니다. 백업 또는 복원 프로시저는 작성기 나 구성 요소가 포함 되어 있지 않으면 실패 합니다. |
|  Exclude   |                                                   백업 또는 복원 프로시저에서 지정 된 작성기 또는 구성 요소를 제외합니다.                                                    |
| [\<Writer > |                                                                                     <Component>]                                                                                      |

## <a name="BKMK_examples"></a>예와

해당 GUID (이 예에서는 4dc3bdd4-ab48-4d07-adb0-3bee2926fd7f)를 지정 하 여 작성기를 확인 하려면 다음을 입력 합니다.
```
writer verify {4dc3bdd4-ab48-4d07-adb0-3bee2926fd7f}
```
"시스템 기록기" 라는 이름의 기록기를 제외 하려면 다음을 입력 합니다.
```
writer exclude "System Writer"
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)