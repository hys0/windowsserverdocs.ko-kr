---
title: DriverPackageFile 가져오기
description: 드라이버 패키지와 여기에 포함 된 파일을 포함 하 여 드라이버 패키지에 대 한 정보를 표시 하는 가져오기 DriverPackageFile에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f01a2c67-7e9c-4aad-b625-383f5a1fca25
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d485a24479aa857270968a1bff7bd55a014347a3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80831036"
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
| /InfFile:\<Inf 파일 경로 > | 드라이버 패키지.inf 파일의 전체 경로 파일 이름을 지정합니다. |
|    [/아키텍처: {x86    |                                  ia64                                  |
|     [/Show: {Drivers      |                                 Files                                  |

## <a name="examples"></a><a name=BKMK_examples></a>예와

드라이버 파일에 대 한 정보를 보려면 다음을 입력 합니다.
```
WDSUTIL /Get-DriverPackageFile /InfFile:C:\temp\1394.inf /Architecture:x86
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)