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
ms.openlocfilehash: ed9518fae07745502d01dc0084b7443a1332db83
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859804"
---
# <a name="using-the-get-driverpackagefile-command"></a>Get DriverPackageFile 명령을 사용 하 여



드라이버 및 포함 된 파일을 포함 하 여 드라이버 패키지에 대 한 정보를 표시 합니다.

## <a name="syntax"></a>구문

```
WDSUTIL /Get-DriverPackageFile /InfFile:<Inf File path> [/Architecture:{x86 | ia64 | x64}] [/Show:{Drivers | Files | All}]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/ InfFile:\<Inf 파일 경로 >|드라이버 패키지.inf 파일의 전체 경로 파일 이름을 지정합니다.|
|[/ 아키텍처: {x86 | ia64 | x64}]|드라이버 패키지의 아키텍처를 지정합니다.|
|[표시 /: {드라이버 | 파일 | All}]|패키지 정보를 표시를 나타냅니다. 경우 **표시/** 를 지정 하지 않으면 기본값은 드라이버만 패키지 메타 데이터를 반환 합니다. **드라이버** 패키지에 드라이버 목록이 표시 됩니다. **파일** 패키지에 파일 목록이 표시 됩니다. **모든** 드라이버와 파일이 표시 됩니다.|

## <a name="BKMK_examples"></a>예제

드라이버 파일에 대 한 정보를 보려면 다음을 입력 합니다.
```
WDSUTIL /Get-DriverPackageFile /InfFile:"C:\temp\1394.inf" /Architecture:x86
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)