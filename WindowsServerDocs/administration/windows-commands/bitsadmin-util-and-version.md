---
title: bitsadmin util 및 버전
description: BITS 서비스의 버전을 표시 하는 bitsadmin util 및 버전에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 98f17328-dfbd-4cbb-93c1-b8d424bc3f0a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 087cc1033166ab93e7496caaa7335433cafd6249
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848836"
---
# <a name="bitsadmin-util-and-version"></a>bitsadmin util 및 버전

BITS 서비스의 버전을 표시 합니다 (예: 2.0).

**Bitsadmin 1.5 및 이전 버전**: 지원 되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /Util /Version [/Verbose]
```

## <a name="remarks"></a>주의

**자세한 정보** 표시 스위치는 다음을 수행 합니다.
-   각 비트 관련된 DLL에 대 한 파일 버전을 표시합니다.
-   BITS 서비스를 시작할 수 확인
-   비트 그룹 정책 값 (Windows Vista에만 해당)를 표시합니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 BITS 서비스의 버전입니다.
```
C:\>bitsadmin /Util /Version
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)