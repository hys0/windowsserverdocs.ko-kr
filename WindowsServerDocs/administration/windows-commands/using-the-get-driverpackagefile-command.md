---
title: Get DriverPackageFile 명령을 사용 하 여
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f01a2c67-7e9c-4aad-b625-383f5a1fca25
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 264bdb6d51622e6323be00b44014b86cd9662e61
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440505"
---
# <a name="using-the-get-driverpackagefile-command"></a>Get DriverPackageFile 명령을 사용 하 여



드라이버 및 포함 된 파일을 포함 하 여 드라이버 패키지에 대 한 정보를 표시 합니다.

## <a name="syntax"></a>구문

```
WDSUTIL /Get-DriverPackageFile /InfFile:<Inf File path> [/Architecture:{x86 | ia64 | x64}] [/Show:{Drivers | Files | All}]
```

## <a name="parameters"></a>매개 변수

|         매개 변수         |                              설명                               |
|---------------------------|------------------------------------------------------------------------|
| / InfFile:\<Inf 파일 경로 > | 드라이버 패키지.inf 파일의 전체 경로 파일 이름을 지정합니다. |
|    [/ 아키텍처: {x86    |                                  ia64                                  |
|     [표시 /: {드라이버      |                                 파일                                  |

## <a name="BKMK_examples"></a>예제

드라이버 파일에 대 한 정보를 보려면 다음을 입력 합니다.
```
WDSUTIL /Get-DriverPackageFile /InfFile:"C:\temp\1394.inf" /Architecture:x86
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)