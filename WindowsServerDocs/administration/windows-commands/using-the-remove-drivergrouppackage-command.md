---
title: -DriverGroupPackage 제거
description: 서버에 있는 드라이버 그룹에서 드라이버 패키지를 제거 하는 DriverGroupPackage 제거에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2e48616d-d6a4-45f0-a5c6-efe62bf6a0ed
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c63c6ef0ed9af49506d80a715f23111bfd62070f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720397"
---
# <a name="remove-drivergrouppackage"></a>-DriverGroupPackage 제거



서버에 드라이버 그룹에서 드라이버 패키지를 제거합니다.

## <a name="syntax"></a>구문

```
WDSUTIL /Remove-DriverGroupPackage /DriverGroup:<Group Name> [/Server:<Server Name>] {/DriverPackage:<Name> | /PackageId:<ID>}
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|[/Server:\<서버 이름>]|서버 이름을 지정합니다. 이 NetBIOS 이름이 나 FQDN 수 있습니다. 서버 이름을 지정 하지 않으면 로컬 서버가 사용 됩니다.|
|[/Driverpackage:\<Name>]|제거할 드라이버 패키지의 이름을 지정 합니다.|
|[/PackageId:\<ID>]|제거할 드라이버 패키지의 Windows 배포 서비스 ID를 지정 합니다. 드라이버 패키지 이름으로 고유 하 게 식별할 수 없는 경우이 옵션을 지정 해야 합니다.|

## <a name="examples"></a>예

```
WDSUTIL /Remove-DriverGroupPackage /DriverGroup:PrinterDrivers /PackageId:{4D36E972-E325-11CE-BFC1-08002BE10318}
```
```
WDSUTIL /Remove-DriverGroupPackage /DriverGroup:PrinterDrivers /DriverPackage:XYZ
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)