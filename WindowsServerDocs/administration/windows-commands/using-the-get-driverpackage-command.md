---
title: 드라이버 패키지 가져오기
description: 서버에 드라이버 패키지에 대 한 정보를 표시 하는 get DriverPackage에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 94d231e4-ff01-48e7-9bc8-7b0d97a4339e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4fc6bc327b46f8219a7c40fa47e85cc94b6fc749
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719940"
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
| [/Server:\<서버 이름>] |              서버 이름을 지정합니다. 이 NetBIOS 이름이 나 FQDN 수 있습니다. 서버 이름을 지정 하지, 로컬 서버가 사용 됩니다.               |
| [/Driverpackage:\<Name>] |                                                        표시 하는 드라이버 패키지의 이름을 지정 합니다.                                                         |
|    [/PackageId:\<ID>]    | 표시 하는 드라이버 패키지의 Windows 배포 서비스 ID를 지정 합니다. 드라이버 패키지 이름으로 고유 하 게 식별할 수 없는 경우에 ID를 지정 해야 합니다. |
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