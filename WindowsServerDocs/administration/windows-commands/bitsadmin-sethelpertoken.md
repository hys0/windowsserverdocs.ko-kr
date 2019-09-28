---
title: bitsadmin sethelpertoken
description: '**Bitsadmin sethelpertoken** 에 대 한 Windows 명령 항목-현재 명령 프롬프트의 기본 토큰 또는 임의의 로컬 사용자 계정 토큰 (지정 된 경우)을 BITS 전송 작업의 도우미 토큰으로 설정 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 91c03366998168dad9ab4530ef36a5020b8ad6ec
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380573"
---
# <a name="bitsadmin-sethelpertoken"></a>bitsadmin sethelpertoken

현재 명령 프롬프트의 기본 토큰 또는 임의의 로컬 사용자 계정 토큰 (지정 된 경우)을 BITS 전송 작업의 [도우미 토큰](/windows/desktop/bits/helper-tokens-for-bits-transfer-jobs)으로 설정 합니다.

**BITS 3.0 및 이전 버전**: 지원되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetHelperToken <Job> [\<username@domain\> \<password\>]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID입니다.|
|\< @ no__t-1 @ no__t-2 \<password @ no__t-4|선택적 @ no__t-0은 사용할 토큰을 포함 하는 로컬 사용자 계정의 자격 증명입니다.|

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)
