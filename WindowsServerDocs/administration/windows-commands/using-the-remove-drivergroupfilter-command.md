---
title: -DriverGroupFilter 제거
description: 서버에 있는 드라이버 그룹에서 필터 규칙을 제거 하는 DriverGroupFilter에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 837bd5d4-c79d-4714-942d-9875bd8e61dc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 98d2253cc5148ba4581399d688b74cd426a649fb
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936335"
---
# <a name="remove-drivergroupfilter"></a>-DriverGroupFilter 제거



서버에 드라이버 그룹에서 필터 규칙을 제거합니다.

## <a name="syntax"></a>구문

```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:<Group Name> [/Server:<Server name>] /FilterType:<Filter Type>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|DriverGroup\<Group Name>|드라이버 그룹의 이름을 지정합니다.|
|[/ 서버:\<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름이 나 FQDN 수 있습니다. 서버 이름을 지정 하지 않으면 로컬 서버가 사용 됩니다.|
|[/ FilterType:\<FilterType>]|그룹에서 제거할 필터의 유형을 지정 합니다. \<FilterType>다음 중 하나일 수 있습니다.</br>**BiosVendor**</br>**BiosVersion**</br>**ChassisType**</br>**제조업체**</br>**Uuid**</br>**OsVersion**</br>**OsEdition**</br>**OsLanguage**|

## <a name="examples"></a>예

필터를 제거 하려면 다음 중 하나를 입력 합니다.
```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer
```
```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /FilterType:OSLanguage
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)