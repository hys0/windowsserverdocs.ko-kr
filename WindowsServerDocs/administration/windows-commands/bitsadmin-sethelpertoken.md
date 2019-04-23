---
title: bitsadmin sethelpertoken
description: Windows 명령 항목에 대 한 **bitsadmin sethelpertoken** -현재 명령 프롬프트의 주 토큰 (또는 임의의 로컬 사용자 계정 토큰을 지정 하는 경우)는 BITS 전송 작업의 도우미 토큰으로 설정 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 558a1aca66a7b3ec447136ceff9237d13efe4ede
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853004"
---
# <a name="bitsadmin-sethelpertoken"></a>bitsadmin sethelpertoken

BITS 전송 작업으로 현재 명령 프롬프트의 주 토큰 (또는 임의의 로컬 사용자 계정 토큰을 지정 하는 경우)를 설정 [도우미 토큰](/windows/desktop/bits/helper-tokens-for-bits-transfer-jobs)합니다.

**3.0 및 이전 비트**: 지원되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetHelperToken <Job> [\<username@domain\> \<password\>]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID입니다.|
|\<username@domain\> \<password\>|선택적&mdash;로컬 사용자의 자격 증명을 사용 하 여 토큰이 계정.|

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)
