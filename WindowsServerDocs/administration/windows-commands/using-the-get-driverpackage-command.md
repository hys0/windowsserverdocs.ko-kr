---
title: 드라이버 패키지 가져오기
description: 서버에 드라이버 패키지에 대 한 정보를 표시 하는 get DriverPackage에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 94d231e4-ff01-48e7-9bc8-7b0d97a4339e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f0ca307b9f42d0921c896df2fe622c5b0f8a853d
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932256"
---
# <a name="get-driverpackage"></a>드라이버 패키지 가져오기

서버에 드라이버 패키지에 대 한 정보를 표시합니다.

## <a name="syntax"></a>구문

```
WDSUTIL /Get-DriverPackage [/Server:<Server name>] {/DriverPackage:<Package Name> | /PackageId:<ID>} [/Show:{Drivers | Files | All}]
```

### <a name="parameters"></a>매개 변수

|        매개 변수         |                                                                           설명                                                                            |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/ 서버:\<Server name>] |              서버 이름을 지정합니다. 이 NetBIOS 이름이 나 FQDN 수 있습니다. 서버 이름을 지정 하지, 로컬 서버가 사용 됩니다.               |
| [/ DriverPackage:\<Name>] |                                                        표시 하는 드라이버 패키지의 이름을 지정 합니다.                                                         |
|    [/ 패키지 Id:\<ID>]    | 표시 하는 드라이버 패키지의 Windows 배포 서비스 ID를 지정 합니다. 드라이버 패키지 이름으로 고유 하 게 식별할 수 없는 경우에 ID를 지정 해야 합니다. |
|     [/Show: {Drivers     |                                                                              파일                                                                               |

## <a name="examples"></a>예

드라이버 패키지에 대 한 정보를 보려면 다음 중 하나를 입력 합니다.
```
WDSUTIL /Get-DriverPackage /PackageId:{4D36E972-E325-11CE-BFC1-08002BE10318}
```
```
WDSUTIL /Get-DriverPackage /DriverPackage:MyDriverPackage /Show:All
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)