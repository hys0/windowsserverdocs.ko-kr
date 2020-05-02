---
title: bitsadmin list
description: 현재 사용자가 소유한 전송 작업을 나열 하는 bitsadmin list 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1416965e-e0e6-49cf-b1d4-b286d3cf8716
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 262589293a147cc1bae98da8fdca047c5f914094
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717427"
---
# <a name="bitsadmin-list"></a>bitsadmin list

현재 사용자가 소유 하 고 전송 작업을 나열 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /list [/allusers][/verbose]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| /allusers | (선택 사항) 모든 사용자에 대 한 작업을 나열 합니다. 이 매개 변수를 사용 하려면 관리자 권한이 있어야 합니다. |
| /verbose | (선택 사항) 각 작업에 대 한 자세한 정보를 제공 합니다. |

## <a name="examples"></a>예

현재 사용자가 소유 하 고 있는 작업에 대 한 정보를 검색 합니다.

```
bitsadmin /list
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
