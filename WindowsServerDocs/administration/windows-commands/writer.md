---
title: 기록기
description: 기록기 또는 구성 요소가 백업 또는 복원 프로시저에서 기록기 또는 구성 요소를 포함 하거나 제외 하는지 확인 하는 기록기에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7cf98295-411d-4705-8573-f898ff45c140
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 16746f2f070b87e0c287f3a49b19a480ba5399c9
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936097"
---
# <a name="writer"></a>기록기



기록기 또는 구성 요소 포함 또는 백업 또는 복원 프로시저에서 기록기 또는 구성 요소를 제외를 확인 합니다. 매개 변수 없이 사용 하는 경우 **기록기** 명령 프롬프트에서 도움말을 표시 합니다.

## <a name="syntax"></a>구문

```
writer verify [<Writer> | <Component>]
writer exclude [<Writer> | <Component>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수  |                                                                                      설명                                                                                      |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   verify   | 백업 또는 복원 프로시저에는 지정 된 작성기 나 구성 요소가 포함 되어 있는지 확인 합니다. 백업 또는 복원 프로시저는 작성기 나 구성 요소가 포함 되어 있지 않으면 실패 합니다. |
|  제외   |                                                   백업 또는 복원 프로시저에서 지정 된 작성기 또는 구성 요소를 제외합니다.                                                    |
| [\<Writer> |                                                                                     <Component>]                                                                                      |

## <a name="examples"></a>예

해당 GUID (이 예에서는 4dc3bdd4-ab48-4d07-adb0-3bee2926fd7f)를 지정 하 여 작성기를 확인 하려면 다음을 입력 합니다.
```
writer verify {4dc3bdd4-ab48-4d07-adb0-3bee2926fd7f}
```
이름 시스템 기록기를 사용 하 여 기록기를 제외 하려면 다음을 입력 합니다.
```
writer exclude System Writer
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)