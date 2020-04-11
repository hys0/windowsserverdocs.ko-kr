---
title: bitsadmin sethttpmethod
description: '**Bitsadmin sethttpmethod**에 대 한 Windows 명령 항목으로, 사용할 HTTP 동사를 설정 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: d349dcad7bdf6a6fc566ed961c3160836d7f49da
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122963"
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
| 제출 | 작업의 표시 이름 또는 GUID입니다. |
| httpmethod | 사용할 HTTP 동사입니다. 사용 가능한 동사에 대 한 자세한 내용은 [메서드 정의](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)를 참조 하세요. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)