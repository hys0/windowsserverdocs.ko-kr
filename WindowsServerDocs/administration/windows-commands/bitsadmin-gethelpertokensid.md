---
title: bitsadmin gethelpertokensid
description: BITS 전송 작업의 도우미 토큰에 대 한 SID (설정 된 경우)를 반환 하는 **bitsadmin gethelpertokensid**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: a2e26ff459b068595529fbd24e6165c130660570
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850646"
---
# <a name="bitsadmin-gethelpertokensid"></a>bitsadmin gethelpertokensid

설정 된 경우 BITS 전송 작업의 [도우미 토큰](https://docs.microsoft.com/windows/win32/bits/helper-tokens-for-bits-transfer-jobs)에 대 한 SID를 반환 합니다.

> [!NOTE]
> 이 명령은 BITS 3.0 이전 버전에서는 지원 되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /gethelpertokensid <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
