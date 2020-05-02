---
title: -DriverGroupFilter 추가
description: 서버에 드라이버 그룹에 필터를 추가 하는 추가 DriverGroupFilter에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a66c5e68-99ea-4e47-b68d-8109633ae336
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 45ed82940e89f4ab760fda4eed640cd62056daf8
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721125"
---
# <a name="add-drivergroupfilter"></a>-DriverGroupFilter 추가

서버에 드라이버 그룹에 필터를 추가합니다.

## <a name="syntax"></a>구문

```
WDSUTIL /Add-DriverGroupFilter /DriverGroup:<Group Name> [/Server:<Server name>] /FilterType:<Filter Type> /Policy:{Include | Exclude} /Value:<Value> [/Value:<Value> ...]
```

### <a name="parameters"></a>매개 변수

|         매개 변수          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                            설명                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /DriverGroup:\<그룹 이름> |                                                                                                                                                                                                                                                                                                                                                                                                                                                              드라이버 그룹의 이름을 지정합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|  [/Server:\<서버 이름>]  |                                                                                                                                                                                                                                                                                                                                                                                                               서버 이름을 지정합니다. 이 NetBIOS 이름이 나 FQDN 수 있습니다. 서버 이름을 지정 하지, 로컬 서버가 사용 됩니다.                                                                                                                                                                                                                                                                                                                                                                                                               |
| /FilterType:\<FilterType>  |                                                                                                                                                                                                   그룹에 추가 하는 필터의 유형을 지정 합니다. 단일 명령에서 여러 종류의 필터를 지정할 수 있습니다. 각 필터 형식 뒤에 야 **/Policy** 하나 이상 포함 하 고 **/v**합니다. \<FilterType> **BiosVendor**, **BiosVersion**, **ChassisType**, **Manufacturer**, **Uuid**, **OsVersion**, **OsEdition**또는 **OsLanguage**일 수 있습니다. 다른 모든 필터 형식에 대 한 값을 가져오는 방법에 대 한 자세한 내용은 [드라이버 그룹 필터](https://go.microsoft.com/fwlink/?LinkID=155158) (<https://go.microsoft.com/fwlink/?LinkID=155158>)를 참조 하십시오.                                                                                                                                                                                                    |
|     [/Policy: {Include      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                             Exclude}]                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|     [/값:\<값>]      | 에 해당 하는 클라이언트 값을 지정 **/FilterType**합니다. 단일 형식에 대 한 여러 값을 지정할 수 있습니다. 다음 목록에 대 한 유효한 값에 대 한 참조 **ChassisType**합니다. 다른 모든 필터 형식에 대 한 값을 가져오는 방법에 대 한 자세한 내용은 [드라이버 그룹 필터](https://go.microsoft.com/fwlink/?LinkID=155158) (<https://go.microsoft.com/fwlink/?LinkID=155158>)를 참조 하십시오.</br>**기타**</br>**UnknownChassis**</br>**데스크톱**</br>**LowProfileDesktop**</br>**PizzaBox**</br>**미니 타워**</br>**타워**</br>**이식 가능**</br>**랩톱**</br>**Notebook**</br>**핸드헬드**</br>**DockingStation**</br>**AllInOne**</br>**SubNotebook**</br>**SpaceSaving**</br>**LunchBox**</br>**MainSystemChassis**</br>**ExpansionChassis**</br>**하위 섀시**</br>**BusExpansionChassis**</br>**PeripheralChassis**</br>**StorageChassis**</br>**RackMountChassis**</br>**SealedCaseComputer**</br>**MultiSystemChassis**</br>**CompactPci**</br>**AdvancedTca** |

## <a name="examples"></a>예

드라이버 그룹에 필터를 추가 하려면 다음 중 하나를 입력 합니다.
```
WDSUTIL /Add-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /Policy:Include /Value:Name1 /Value:Name2
```
```
WDSUTIL /Add-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /Policy:Include /Value:Name1 /FilterType:ChassisType /Policy:Exclude /Value:Tower /Value:MiniTower
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

