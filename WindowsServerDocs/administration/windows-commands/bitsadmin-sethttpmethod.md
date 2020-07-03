---
title: bitsadmin sethttpmethod
description: 사용할 HTTP 동사를 설정 하는 bitsadmin sethttpmethod 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 86d4749de294871a05176239cc1265974d8a7590
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927751"
---
# <a name="bitsadmin-sethttpmethod"></a>bitsadmin sethttpmethod

사용할 HTTP 동사를 설정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /sethttpmethod <job> <httpmethod>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |
| httpmethod | 사용할 HTTP 동사입니다. 사용 가능한 동사에 대 한 자세한 내용은 [메서드 정의](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)를 참조 하세요. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
