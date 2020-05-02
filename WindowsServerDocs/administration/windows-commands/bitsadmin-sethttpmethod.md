---
title: bitsadmin sethttpmethod
description: 사용할 HTTP 동사를 설정 하는 bitsadmin sethttpmethod 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: daf1c23565bc4f398fd29e51aaaeef23b3b0d018
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719355"
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
