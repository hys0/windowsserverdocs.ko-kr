---
title: DriverPackageFile 가져오기
description: 드라이버 패키지 및 드라이버 패키지에 대 한 정보를 표시 하는 드라이버 패키지에 대 한 정보를 표시 하는 get DriverPackageFile에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f01a2c67-7e9c-4aad-b625-383f5a1fca25
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 71fc38e31471a1deb9d6be29b04d3cd911be1bd6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719929"
---
# <a name="get-driverpackagefile"></a>DriverPackageFile 가져오기

드라이버 및 포함 된 파일을 포함 하 여 드라이버 패키지에 대 한 정보를 표시 합니다.

## <a name="syntax"></a>구문

```
WDSUTIL /Get-DriverPackageFile /InfFile:<Inf File path> [/Architecture:{x86 | ia64 | x64}] [/Show:{Drivers | Files | All}]
```

### <a name="parameters"></a>매개 변수

|         매개 변수         |                              설명                               |
|---------------------------|------------------------------------------------------------------------|
| /InfFile:\<Inf 파일 경로> | 드라이버 패키지.inf 파일의 전체 경로 파일 이름을 지정합니다. |
|    [/아키텍처: {x86    |                                  ia64                                  |
|     [/Show: {Drivers      |                                 파일                                  |

## <a name="examples"></a>예

드라이버 파일에 대 한 정보를 보려면 다음을 입력 합니다.
```
WDSUTIL /Get-DriverPackageFile /InfFile:C:\temp\1394.inf /Architecture:x86
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)