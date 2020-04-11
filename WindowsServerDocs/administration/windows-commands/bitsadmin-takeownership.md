---
title: bitsadmin takeownership
description: 관리 권한이 있는 사용자가 지정 된 작업의 소유권을 가질 수 있도록 하는 **bitsadmin takeownership**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ea0ce7cb-440a-498f-a3ef-8368fa43e399
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a04f54747e3e06aa61166c2c9f9cedfdfbc8d42a
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122693"
---
# <a name="bitsadmin-takeownership"></a>bitsadmin takeownership

관리자 권한으로는 사용자가 지정된 된 작업의 소유권을 가져올 수 있습니다.

## <a name="syntax"></a>구문

```
bitsadmin /takeownership <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ---------- |
| 작업 | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a>예

다음 예제에서는 명명 된 작업의 소유권을 갖습니다 *myDownloadJob*합니다.

```
C:\>bitsadmin /takeownership myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)