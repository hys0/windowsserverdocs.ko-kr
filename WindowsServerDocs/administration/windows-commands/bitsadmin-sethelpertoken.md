---
title: bitsadmin sethelpertoken
description: Bitsadmin sethelpertoken에 대 한 Windows 명령 항목 현재 명령 프롬프트의 기본 토큰 또는 임의의 로컬 사용자 계정 토큰 (지정 된 경우)을 BITS 전송 작업의 도우미 토큰으로 설정 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: a1e8fd0054cadf3bf06b6e5b7bdf5010b18781e1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849536"
---
# <a name="bitsadmin-sethelpertoken"></a>bitsadmin sethelpertoken

현재 명령 프롬프트의 기본 토큰 또는 임의의 로컬 사용자 계정 토큰 (지정 된 경우)을 BITS 전송 작업의 [도우미 토큰](/windows/desktop/bits/helper-tokens-for-bits-transfer-jobs)으로 설정 합니다.

**BITS 3.0 및 이전 버전**: 지원 되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetHelperToken <Job> [\<username@domain\> \<password\>]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID입니다.|
|\<username@domain\> \<암호\>|선택적&mdash;사용할 토큰을 포함 하는 로컬 사용자 계정의 자격 증명입니다.|

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
