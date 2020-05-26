---
title: 목록 공급자
description: 시스템에 현재 등록 된 섀도 복사본 공급자를 나열 하는 목록 공급자 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 844b4036-c0b9-449d-8347-7d58ef9bf16d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 98615dfa92c24b91babb55ae3545065834887e5d
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83817243"
---
# <a name="list-providers"></a>목록 공급자

현재 시스템에 등록 되어 있는 섀도 복사본 공급자를 나열 합니다.

## <a name="syntax"></a>구문

```
list providers
```

### <a name="examples"></a>예

현재 등록 된 섀도 복사본 공급자를 나열 하려면 다음을 입력 합니다.

```
list providers
```

다음을 표시 하는 출력:

```
* ProviderID: {b5946137-7b9f-4925-af80-51abd60b20d5}
        Type: [1] VSS_PROV_SYSTEM
        Name: Microsoft Software Shadow Copy provider 1.0
        Version: 1.0.0.7
        CLSID: {65ee1dba-8ff4-4a58-ac1c-3470ee2f376a}
1 provider registered.
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)