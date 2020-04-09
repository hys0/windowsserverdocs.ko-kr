---
title: bitsadmin list
description: 현재 사용자가 소유한 전송 작업을 나열 하는 **bitsadmin 목록의**Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1416965e-e0e6-49cf-b1d4-b286d3cf8716
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1883da7bfa71a41952f6f67e25eca4dbbdd3353c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850326"
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

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 현재 사용자가 소유한 작업에 대 한 정보를 검색 합니다.

```
C:\>bitsadmin /list
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)