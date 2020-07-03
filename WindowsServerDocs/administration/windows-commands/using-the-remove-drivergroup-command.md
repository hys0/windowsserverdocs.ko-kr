---
title: -DriverGroup 제거
description: 서버에서 드라이버 그룹을 제거 하는 드라이버 그룹을 제거 하는 참조 문서입니다.
ms.prod: windows-server
ms.topic: article
ms.assetid: 1fefe9df-9782-433c-8abe-3f1a35e50da2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: baeeac57c04113e1e9dfc8e9d02fc40518a6689b
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932429"
---
# <a name="remove-drivergroup"></a>-DriverGroup 제거

서버에서 드라이버 그룹을 제거합니다.

## <a name="syntax"></a>구문

```
WDSUTIL /Remove-DriverGroup /DriverGroup:<Group Name> [/Server:<Server name>]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|DriverGroup\<Group Name>|제거할 드라이버 그룹의 이름을 지정 합니다.|
|[/ 서버:\<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름이 나 FQDN 수 있습니다. 서버 이름을 지정 하지 않으면 로컬 서버가 사용 됩니다.|

## <a name="examples"></a>예

드라이버 그룹을 제거 하려면 다음 중 하나를 입력 합니다.
```
WDSUTIL /Remove-DriverGroup /DriverGroup:PrinterDrivers
```
```
WDSUTIL /Remove-DriverGroup /DriverGroup:PrinterDrivers /Server:MyWdsServer
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)