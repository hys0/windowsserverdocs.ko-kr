---
title: 그림자 삭제
description: 섀도 복사본을 삭제 하는 그림자 삭제 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e29a84d2-04d1-4eb1-910a-5a47bddbc24d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6b757314c96024741795c6770a98d10ac23b5bd0
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2020
ms.locfileid: "82993106"
---
# <a name="delete-shadows"></a>그림자 삭제

섀도 복사본을 삭제 합니다.

## <a name="syntax"></a>구문

```
delete shadows [all | volume <volume> | oldest <volume> | set <setID> | id <shadowID> | exposed {<drive> | <mountpoint>}]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| ---- | ---- |
| all | 모든 섀도 복사본을 삭제합니다. |
| 볼륨`<volume>` | 지정 된 볼륨의 모든 섀도 복사본을 삭제합니다. |
| 이전`<volume>` | 지정 된 볼륨의 가장 오래 된 섀도 복사본을 삭제합니다. |
| 설정`<setID>` | 지정 된 ID의 섀도 복사본 집합에 대 한 섀도 복사본을 삭제 현재 환경에 별칭이 있는 경우 기호를 **%** 사용 하 여 별칭을 지정할 수 있습니다. |
| a-id`<shadowID>` | 지정 된 ID의 섀도 복사본을 삭제합니다. 현재 환경에 별칭이 있는 경우 기호를 **%** 사용 하 여 별칭을 지정할 수 있습니다. |
| 노출 됨 {'<drive> | <mountpoint>} |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [delete 명령](delete.md)
