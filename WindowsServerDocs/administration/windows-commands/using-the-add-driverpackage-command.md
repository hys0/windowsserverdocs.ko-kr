---
title: -DriverPackage 추가
description: 서버에 드라이버 패키지를 추가 하는 드라이버 패키지를 추가 하는 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3ac9e8d5-63ec-4ce8-86fc-85d28011050b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e2ccdfcddd2f605eccd9cd32fed7b8c6921297fc
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80832016"
---
# <a name="add-driverpackage"></a>-DriverPackage 추가

서버에 드라이버 패키지를 추가합니다.

## <a name="syntax"></a>구문

```
WDSUTIL /Add-DriverPackage /InfFile:<Inf File path> [/Server:<Server name>] [/Architecture:{x86 | ia64 | x64}] [/DriverGroup:<Group Name>] [/Name:<Friendly Name>]
```

### <a name="parameters"></a>매개 변수

|          매개 변수           |                                                              설명                                                              |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
|   InfFile:\<Inf 파일 경로 >   |                                           추가할.inf 파일의 전체 경로 지정 합니다.                                            |
|    /Server:\<서버 이름 >    | 서버 이름을 지정합니다. 이 NetBIOS 이름이 나 FQDN 수 있습니다. 서버 이름을 지정 하지, 로컬 서버가 사용 됩니다. |
|      /아키텍처: {x86      |                                                                 ia64                                                                  |
| [/Drivergroup:\<그룹 이름 >] |                             패키지를 추가할 드라이버 그룹의 이름을 지정 합니다.                              |
|   [/Name:\<친근 한 이름 >]   |                                           드라이버 패키지에 대 한 이름을 알려 줍니다.                                            |

## <a name="examples"></a><a name=BKMK_examples></a>예와

드라이버 패키지를 추가 하려면 다음 중 하나를 입력 합니다.
```
WDSUTIL /verbose /Add-DriverPackage /InfFile:C:\Temp\Display.inf
```
```
WDSUTIL /Add-DriverPackage /Server:MyWDSServer /InfFile:C:\Temp\Display.inf /Architecture:x86 /DriverGroup:x86Drivers /Name:Display Driver
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

