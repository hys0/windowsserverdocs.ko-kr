---
title: add alias
description: 별칭 환경에 별칭을 추가 하는 add alias 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5fe12f5d-11e9-4f3d-b7f9-40b26c8685e5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 405c04b17b32477654f0349c04c6059cf246f804
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85924124"
---
# <a name="add-alias"></a>add alias

별칭 환경에 별칭을 추가합니다. 매개 변수 없이 사용 하는 경우 **별칭 추가** 명령 프롬프트에서 도움말을 표시 합니다. 별칭 메타 데이터 파일에 저장 되 고으로 로드 되는 **메타 데이터를 로드** 명령입니다.

## <a name="syntax"></a>구문

```
add alias <aliasname> <aliasvalue>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<aliasname>` | 별칭의 이름을 지정합니다. |
| `<aliasvalue>` | 별칭 값을 지정합니다. |
| `? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="examples"></a>예

해당 별칭을 포함 하 여 모든 그림자를 나열 하려면 다음을 입력 합니다.

```
list shadows all
```

다음 발췌에서는 기본 별칭 *VSS_SHADOW_x*가 할당 된 섀도 복사본을 보여 줍니다.

```
* Shadow Copy ID = {ff47165a-1946-4a0c-b7f4-80f46a309278}
%VSS_SHADOW_1%
```

이름이 *System1* 인 새 별칭을이 섀도 복사본에 할당 하려면 다음을 입력 합니다.

```
add alias System1 %VSS_SHADOW_1%
```

또는 섀도 복사본 ID를 사용 하 여 별칭을 할당할 수 있습니다.

```
add alias System1 {ff47165a-1946-4a0c-b7f4-80f46a309278}
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [메타 데이터 로드 명령](load-metadata.md)
