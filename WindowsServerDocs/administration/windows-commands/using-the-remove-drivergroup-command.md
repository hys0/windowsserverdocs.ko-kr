---
title: 제거 DriverGroup 명령을 사용 하 여
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1fefe9df-9782-433c-8abe-3f1a35e50da2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b56f162861caf4493550f9e063065e9544e52eae
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885754"
---
# <a name="using-the-remove-drivergroup-command"></a>제거 DriverGroup 명령을 사용 하 여



서버에서 드라이버 그룹을 제거합니다.

## <a name="syntax"></a>구문

```
WDSUTIL /Remove-DriverGroup /DriverGroup:<Group Name> [/Server:<Server name>]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/ DriverGroup:\<그룹 이름 >|제거할 드라이버 그룹의 이름을 지정 합니다.|
|[/ 서버:\<서버 이름 >]|서버 이름을 지정합니다. 이 NetBIOS 이름이 나 FQDN 수 있습니다. 서버 이름을 지정 하지 않으면 로컬 서버가 사용 됩니다.|

## <a name="BKMK_examples"></a>예제

드라이버 그룹을 제거 하려면 다음 중 하나를 입력 합니다.
```
WDSUTIL /Remove-DriverGroup /DriverGroup:PrinterDrivers
```
```
WDSUTIL /Remove-DriverGroup /DriverGroup:PrinterDrivers /Server:MyWdsServer
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)