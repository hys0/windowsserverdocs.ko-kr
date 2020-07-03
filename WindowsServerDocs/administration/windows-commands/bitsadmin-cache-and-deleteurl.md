---
title: bitsadmin 캐시 및 deleteURL
description: 지정 된 URL에 대 한 모든 캐시 항목을 삭제 하는 bitsadmin cache 및 deleteURL 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e108b76b-fae9-4c16-bf4c-d74c9f025953
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8d1ed4710bfeeefa721308c54075ddc8da5c5216
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923334"
---
# <a name="bitsadmin-cache-and-deleteurl"></a>bitsadmin 캐시 및 deleteURL

지정된 된 URL에 대 한 모든 캐시 항목을 삭제합니다.

## <a name="syntax"></a>구문

```
bitsadmin /deleteURL URL
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| URL | 원격 파일을 식별 하는 Uniform Resource Locator |

## <a name="examples"></a>예

다음에 대 한 모든 캐시 항목을 삭제 하려면 `https://www.contoso.com/en/us/default.aspx` :

```
bitsadmin /deleteURL https://www.contoso.com/en/us/default.aspx
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin cache 명령](bitsadmin-cache.md)
