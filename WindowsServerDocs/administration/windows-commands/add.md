---
title: add
description: 섀도 복사할 볼륨 집합에 볼륨을 추가 하거나 별칭 환경에 별칭을 추가 하는 추가 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 47efce7a-86d2-4872-ae31-baa108757afd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7b409b0355f4e112773c3f847466586fe3c84654
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85924074"
---
# <a name="add"></a>add

볼륨 섀도 복사 되는 볼륨의 집합에 추가 하거나 별칭 환경에 별칭을 추가 합니다. 하위 없이 사용 하는 경우 **추가** 현재 볼륨 및 별칭을 나열 합니다.

> [!NOTE]
> 섀도 복사본이 만들어질 때까지 별칭 별칭 환경에 추가 되지 않습니다. 사용 하 여 즉시 수행 해야 하는 별칭을 추가 해야 **별칭 추가**합니다.

## <a name="syntax"></a>구문

```
add
add volume <volume> [provider <providerid>]
add alias <aliasname> <aliasvalue>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| 볼륨 | 볼륨의 섀도 복사본을 설정 하려면 되 섀도 복사 되는 볼륨의 집합에 추가 합니다. 구문 및 매개 변수에 대 한 [볼륨 추가](add-volume.md) 를 참조 하세요. |
| alias | 별칭 환경에 지정 된 이름과 값을 추가합니다. 구문 및 매개 변수에 대 한 [별칭 추가](add-alias.md) 를 참조 하세요. |
| /? | 명령줄에서 도움말을 표시 합니다. |

## <a name="examples"></a>예

추가 볼륨 및 현재 환경에 있는 별칭을 표시 하려면 다음을 입력 합니다.

```
add
```

다음과 같은 출력을 섀도 복사 설정 하려면 C 드라이브 추가 되어 있는지를 보여 줍니다.

```
Volume c: alias System1    GUID \\?\Volume{XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX}\
1 volume in Shadow Copy Set.
No Diskshadow aliases in the environment.
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)