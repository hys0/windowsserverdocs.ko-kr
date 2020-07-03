---
title: reg import
description: 내보낸 레지스트리 하위 키, 항목 및 값을 포함 하는 파일의 내용을 로컬 컴퓨터의 레지스트리로 복사 하는 reg import 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0be103de-08fc-4f02-b590-361782680b3e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 77c8284dd2341f37292afdfd810b2182686aad68
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931864"
---
# <a name="reg-import"></a>reg import

포함 된 파일의 내용을 복사 하는 로컬 컴퓨터의 레지스트리로 레지스트리 하위 키, 항목 및 값을 내보냅니다.

## <a name="syntax"></a>구문

```
reg import <filename>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
|--|--|
| `<filename>` | 로컬 컴퓨터의 레지스트리로 복사 되는 콘텐츠를 포함 하는 파일의 경로 이름을 지정 합니다. 이 파일을 사용 하 여 사전에 만들 수 있어야 **reg 내보내기**합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- **Reg 가져오기** 작업의 반환 값은 다음과 같습니다.

    | 값 | 설명 |
    |--|--|
    | 0 | 성공 |
    | 1 | 실패 |

### <a name="examples"></a>예

레지스트리 항목에서 AppBkUp.reg 라는 파일을 가져오려면 다음을 입력 합니다.

```
reg import AppBkUp.reg
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [reg export 명령](reg-export.md)
