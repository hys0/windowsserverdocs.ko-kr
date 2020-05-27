---
title: 섀도 목록 표시
description: 시스템에 있는 영구적이 고 영구적이 지 않은 섀도 복사본을 나열 하는 shadows 목록 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fe568423-00ae-4ede-a1e7-07977cb50ad1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9e0261a25c7a70a0c8690d578cadc9e73ff9a62e
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83817173"
---
# <a name="list-shadows"></a>섀도 목록 표시

시스템에 있는 영구 및 기존 비영구 섀도 복사본을 나열 합니다.

## <a name="syntax"></a>구문

```
list shadows {all | set <setID> | id <shadowID>}
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ---------- |
| all | 모든 섀도 복사본을 나열합니다. |
| 설정`<setID>` | 섀도 복사본에 지정 된 섀도 복사본 세트 ID에 속하는 나열 |
| a-id`<shadowID>` | 지정 된 섀도 복사본 ID 가진 모든 섀도 복사본을 나열합니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)