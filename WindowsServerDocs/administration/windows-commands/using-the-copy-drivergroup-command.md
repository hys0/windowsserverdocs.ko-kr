---
title: DriverGroup 복사 명령을 사용 하 여
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0aaf6fa5-8b5b-4a1e-ae9b-8b5c6d89f571
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c08ce616c9b0e2bf79c7f13f922e27d7f7f7ca62
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363586"
---
# <a name="using-the-copy-drivergroup-command"></a>DriverGroup 복사 명령을 사용 하 여



기존 드라이버 그룹 필터, 드라이버 패키지 및 사용/사용 안 함 상태를 포함 하 여 서버에 복제 합니다.

## <a name="syntax"></a>구문

```
WDSUTIL /Copy-DriverGroup [/Server:<Server name>] /DriverGroup:<Source Group Name> /GroupName:<New Group Name>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|[/Server: \<Server name >]|서버 이름을 지정합니다. 이 NetBIOS 이름이 나 FQDN 수 있습니다. 서버 이름을 지정 하지, 로컬 서버가 사용 됩니다.|
|/DriverGroup: \<Source 그룹 이름 >|원본 드라이버 그룹의 이름을 지정합니다.|
|/Cname: \< 새 그룹 이름 >|새 드라이버 그룹의 이름을 지정합니다.|

## <a name="BKMK_examples"></a>예와

드라이버 그룹을 복사 하려면 다음 중 하나를 입력 합니다.
```
WDSUTIL /Copy-DriverGroup /Server:MyWdsServer /DriverGroup:PrinterDrivers /GroupName:X86PrinterDrivers
```
```
WDSUTIL /Copy-DriverGroup /DriverGroup:PrinterDrivers /GroupName:ColorPrinterDrivers
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)