---
title: 제거 DriverGroupFilter 명령을 사용 하 여
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 837bd5d4-c79d-4714-942d-9875bd8e61dc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a546ead7220273955368c582ac1e3f9b3f61c191
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883434"
---
# <a name="using-the-remove-drivergroupfilter-command"></a>제거 DriverGroupFilter 명령을 사용 하 여



서버에 드라이버 그룹에서 필터 규칙을 제거합니다.

## <a name="syntax"></a>구문

```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:<Group Name> [/Server:<Server name>] /FilterType:<Filter Type>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/ DriverGroup:\<그룹 이름 >|드라이버 그룹의 이름을 지정합니다.|
|[/ 서버:\<서버 이름 >]|서버 이름을 지정합니다. 이 NetBIOS 이름이 나 FQDN 수 있습니다. 서버 이름을 지정 하지 않으면 로컬 서버가 사용 됩니다.|
|[/FilterType:\<FilterType>]|그룹에서 제거할 필터의 유형을 지정 합니다. \<FilterType > 다음 중 하나일 수 있습니다.</br>**BiosVendor**</br>**BiosVersion**</br>**ChassisType**</br>**제조업체**</br>**uuid**</br>**OsVersion**</br>**OsEdition**</br>**OsLanguage**|

## <a name="BKMK_examples"></a>예제

필터를 제거 하려면 다음 중 하나를 입력 합니다.
```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer
```
```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /FilterType:OSLanguage
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)