---
title: Get DriverPackage 명령을 사용 하 여
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 94d231e4-ff01-48e7-9bc8-7b0d97a4339e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b0f123d281625140b3c4ba46316cb9b773bf5fee
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440510"
---
# <a name="using-the-get-driverpackage-command"></a>Get DriverPackage 명령을 사용 하 여



서버에 드라이버 패키지에 대 한 정보를 표시합니다.

## <a name="syntax"></a>구문

```
WDSUTIL /Get-DriverPackage [/Server:<Server name>] {/DriverPackage:<Package Name> | /PackageId:<ID>} [/Show:{Drivers | Files | All}]
```

## <a name="parameters"></a>매개 변수

|        매개 변수         |                                                                           설명                                                                            |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/ 서버:\<서버 이름 >] |              서버 이름을 지정합니다. 이 NetBIOS 이름이 나 FQDN 수 있습니다. 서버 이름을 지정 하지, 로컬 서버가 사용 됩니다.               |
| [/DriverPackage:\<Name>] |                                                        표시 하는 드라이버 패키지의 이름을 지정 합니다.                                                         |
|    [/PackageId:\<ID>]    | 표시 하는 드라이버 패키지의 Windows 배포 서비스 ID를 지정 합니다. 드라이버 패키지 이름으로 고유 하 게 식별할 수 없는 경우에 ID를 지정 해야 합니다. |
|     [표시 /: {드라이버     |                                                                              파일                                                                               |

## <a name="BKMK_examples"></a>예제

드라이버 패키지에 대 한 정보를 보려면 다음 중 하나를 입력 합니다.
```
WDSUTIL /Get-DriverPackage /PackageId:{4D36E972-E325-11CE-BFC1-08002BE10318}
```
```
WDSUTIL /Get-DriverPackage /DriverPackage:MyDriverPackage /Show:All
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)