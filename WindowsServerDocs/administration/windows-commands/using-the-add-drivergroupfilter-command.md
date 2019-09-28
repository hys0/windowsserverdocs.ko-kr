---
title: 추가 DriverGroupFilter 명령을 사용 하 여
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a66c5e68-99ea-4e47-b68d-8109633ae336
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a332c804fd3c78598eb9b1a6ba8cb5bdae0b3f1c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363835"
---
# <a name="using-the-add-drivergroupfilter-command"></a>추가 DriverGroupFilter 명령을 사용 하 여



서버에 드라이버 그룹에 필터를 추가합니다.

## <a name="syntax"></a>구문

```
WDSUTIL /Add-DriverGroupFilter /DriverGroup:<Group Name> [/Server:<Server name>] /FilterType:<Filter Type> /Policy:{Include | Exclude} /Value:<Value> [/Value:<Value> ...]
```

## <a name="parameters"></a>매개 변수

|         매개 변수          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                            설명                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /DriverGroup: \< 그룹 이름 > |                                                                                                                                                                                                                                                                                                                                                                                                                                                              드라이버 그룹의 이름을 지정합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|  [/Server: \<Server name >]  |                                                                                                                                                                                                                                                                                                                                                                                                               서버 이름을 지정합니다. 이 NetBIOS 이름이 나 FQDN 수 있습니다. 서버 이름을 지정 하지, 로컬 서버가 사용 됩니다.                                                                                                                                                                                                                                                                                                                                                                                                               |
| /FilterType: @no__t 0FilterType >  |                                                                                                                                                                                                   그룹에 추가 하는 필터의 유형을 지정 합니다. 단일 명령에서 여러 종류의 필터를 지정할 수 있습니다. 각 필터 형식 뒤에 야 **/Policy** 하나 이상 포함 하 고 **/v**합니다. \<FilterType >은 **BiosVendor**, **BiosVersion**, **ChassisType**, **Manufacturer**, **Uuid**, **OsVersion**, **OsEdition**또는 **OsLanguage**일 수 있습니다. 다른 모든 필터 형식에 대 한 값을 가져오는 방법에 대 한 자세한 내용은 [드라이버 그룹 필터](https://go.microsoft.com/fwlink/?LinkID=155158) (<https://go.microsoft.com/fwlink/?LinkID=155158>)를 참조 하세요.                                                                                                                                                                                                    |
|     [/Policy: {Include      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                             Exclude}]                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|     [/값: \< 값 >]      | 에 해당 하는 클라이언트 값을 지정 **/FilterType**합니다. 단일 형식에 대 한 여러 값을 지정할 수 있습니다. 다음 목록에 대 한 유효한 값에 대 한 참조 **ChassisType**합니다. 다른 모든 필터 형식에 대 한 값을 가져오는 방법에 대 한 자세한 내용은 [드라이버 그룹 필터](https://go.microsoft.com/fwlink/?LinkID=155158) (<https://go.microsoft.com/fwlink/?LinkID=155158>)를 참조 하세요.</br>**기타**</br>**UnknownChassis**</br>**바탕 화면**</br>**LowProfileDesktop**</br>**PizzaBox**</br>**MiniTower**</br>**타워**</br>**향상**</br>**주기적**</br>**필기장이**</br>**핸드헬드**</br>**DockingStation**</br>**AllInOne**</br>**SubNotebook**</br>**SpaceSaving**</br>**LunchBox**</br>**MainSystemChassis**</br>**ExpansionChassis**</br>**SubChassis**</br>**BusExpansionChassis**</br>**PeripheralChassis**</br>**StorageChassis**</br>**RackMountChassis**</br>**SealedCaseComputer**</br>**MultiSystemChassis**</br>**CompactPci**</br>**AdvancedTca** |

## <a name="BKMK_examples"></a>예와

드라이버 그룹에 필터를 추가 하려면 다음 중 하나를 입력 합니다.
```
WDSUTIL /Add-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /Policy:Include /Value:Name1 /Value:Name2
```
```
WDSUTIL /Add-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /Policy:Include /Value:Name1 /FilterType:ChassisType /Policy:Exclude /Value:Tower /Value:MiniTower
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)

