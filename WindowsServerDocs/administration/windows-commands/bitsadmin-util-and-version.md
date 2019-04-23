---
title: bitsadmin util 및 버전
description: Windows 명령 항목에 대 한 **bitsadmin util 및 버전** -BITS 서비스의 버전을 표시 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98f17328-dfbd-4cbb-93c1-b8d424bc3f0a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2e768ec5ae43fc17c480b9deede698cca01c6291
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882874"
---
# <a name="bitsadmin-util-and-version"></a>bitsadmin util 및 버전

BITS 서비스 (예: 2.0)의 버전을 표시 합니다.

**BITSAdmin 1.5 및 이전 버전**: 지원되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /Util /Version [/Verbose]
```

## <a name="remarks"></a>설명

합니다 **Verbose** 스위치는 다음을 수행 합니다.
-   각 비트 관련된 DLL에 대 한 파일 버전을 표시합니다.
-   BITS 서비스를 시작할 수 확인
-   비트 그룹 정책 값 (Windows Vista에만 해당)를 표시합니다.

## <a name="BKMK_examples"></a>예제

다음 예제에서는 BITS 서비스의 버전입니다.
```
C:\>bitsadmin /Util /Version
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)