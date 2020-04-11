---
title: bitsadmin sethelpertoken
description: '**Bitsadmin sethelpertoken**에 대 한 Windows 명령 항목 현재 명령 프롬프트의 기본 토큰 또는 임의의 로컬 사용자 계정 토큰 (지정 된 경우)을 BITS 전송 작업의 도우미 토큰으로 설정 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: ba4b9a4ed1b59d1b1aeda30353317739b7fdfa9e
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122989"
---
# <a name="bitsadmin-sethelpertoken"></a>bitsadmin sethelpertoken

현재 명령 프롬프트의 기본 토큰 또는 임의의 로컬 사용자 계정 토큰 (지정 된 경우)을 BITS 전송 작업의 [도우미 토큰](https://docs.microsoft.com/windows/win32/bits/helper-tokens-for-bits-transfer-jobs)으로 설정 합니다.

> [!NOTE]
> 이 명령은 BITS 3.0 이전 버전에서는 지원 되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /sethelpertoken <job> [<user_name@domain> <password>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |
| `<username@domain>` `<password>` | (선택 사항) 사용할 토큰에 대 한 로컬 사용자 계정 자격 증명입니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
