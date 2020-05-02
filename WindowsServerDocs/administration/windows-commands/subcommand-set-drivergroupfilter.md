---
title: 하위 명령 설정-DriverGroupFilter
description: 드라이버 그룹에서 기존 드라이버 그룹 필터를 추가 하거나 제거 하는 하위 명령 집합-DriverGroupFilter에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 829ab1f0-4514-421e-9cc0-767b238da69c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f8a8d3567785b54a722b1787c519de7eb0b7a229
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721729"
---
# <a name="subcommand-set-drivergroupfilter"></a>하위 명령: 집합 DriverGroupFilter

추가 하거나 기존 드라이버 그룹 필터 드라이버 그룹에서 제거 합니다.

## <a name="syntax"></a>구문

```
WDSUTIL /Set-DriverGroupFilter /DriverGroup:<Group Name> [/Server:<Server name>] /FilterType:<Filter Type> [/Policy:{Include | Exclude}] [/AddValue:<Value> [/AddValue:<Value> ...]] [/RemoveValue:<Value> [/RemoveValue:<Value> ...]]
```

### <a name="parameters"></a>매개 변수

|         매개 변수          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                               설명                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /DriverGroup:\<그룹 이름> |                                                                                                                                                                                                                                                                                                                                                                                                                                                                 드라이버 그룹의 이름을 지정합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|  [/Server:\<서버 이름>]  |                                                                                                                                                                                                                                                                                                                                                                                                                서버 이름을 지정합니다. 이 NetBIOS 이름이 나 FQDN 수 있습니다. 서버 이름을 지정 하지 않으면 로컬 서버가 사용 됩니다.                                                                                                                                                                                                                                                                                                                                                                                                                 |
| /FilterType:\<FilterType>  |                                                                                                                                                                                                                                                                       드라이버 그룹 필터를 추가 하거나 제거 유형을 지정 합니다. 단일 명령으로 여러 필터를 지정할 수 있습니다. 각 **/FilterType**, 를 추가 하거나 사용 하 여 여러 값을 제거할 수 있습니다 **/RemoveValue** 및 **/AddValue**합니다. \<FilterType> 다음 중 하나일 수 있습니다.</br>**BiosVendor**</br>**BiosVersion**</br>**ChassisType**</br>**제조업체**</br>**Uuid**</br>**OsVersion**</br>**OsEdition**</br>**OsLanguage**                                                                                                                                                                                                                                                                        |
|     [/Policy: {Include      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                Exclude}]                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|    [값:\<값>]    | 필터에 추가할 새 클라이언트 값을 지정 합니다. 단일 필터 형식에 대 한 여러 값을 지정할 수 있습니다. 다음은 유효한 특성 값에 대 한 참조 **ChassisType**합니다. 다른 모든 필터 형식에 대 한 값을 가져오는 방법에 대 한 자세한 내용은 [드라이버 그룹 필터](https://go.microsoft.com/fwlink/?LinkID=155158) (<https://go.microsoft.com/fwlink/?LinkID=155158>)를 참조 하십시오.</br>**기타**</br>**UnknownChassis**</br>**데스크톱**</br>**LowProfileDesktop**</br>**PizzaBox**</br>**미니 타워**</br>**타워**</br>**이식 가능**</br>**랩톱**</br>**Notebook**</br>**핸드헬드**</br>**DockingStation**</br>**AllInOne**</br>**SubNotebook**</br>**SpaceSaving**</br>**LunchBox**</br>**MainSystemChassis**</br>**ExpansionChassis**</br>**하위 섀시**</br>**BusExpansionChassis**</br>**PeripheralChassis**</br>**StorageChassis**</br>**RackMountChassis**</br>**SealedCaseComputer**</br>**MultiSystemChassis**</br>**CompactPci**</br>**AdvancedTca** |
|  [/RemoveValue:\<값>]   |                                                                                                                                                                                                                                                                                                                                                                                                                                     기존 클라이언트 값으로 지정 된 대로 필터에서 제거 하려면 지정 **/AddValue**합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                      |

## <a name="examples"></a>예

필터를 제거 하려면 다음 중 하나를 입력 합니다.
```
WDSUTIL /Set-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /Policy:Include /AddValue:Name1 /RemoveValue:Name2
```
```
WDSUTIL /Set-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /Policy:Include /RemoveValue:Name1 /FilterType:ChassisType /Policy:Exclude /AddValue:Tower /AddValue:MiniTower
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)