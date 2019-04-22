---
title: 추가 DriverGroup 명령을 사용 하 여
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2a92fe8f-03f9-462a-b99e-f23275259807
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 322a9a671f90bf56f6357289f7727c142a0145cc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825094"
---
# <a name="using-the-add-drivergroup-command"></a>추가 DriverGroup 명령을 사용 하 여

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

서버에 드라이버 그룹을 추가합니다.
이 명령을 사용 하는 방법을의 예제를 참조 하세요 [예제](#BKMK_examples)합니다.
## <a name="syntax"></a>구문
```
wdsutil /add-DriverGroup /DriverGroup:<Group Name>\n\
[/Server:<Server name>] [/Enabled:{Yes | No}] [/Applicability:{Matched | All}] [/Filtertype:<Filter type> /Policy:{Include | Exclude} /Value:<Value> [/Value:<Value> ...]]
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|/DriverGroup:<Group Name>|새 드라이버 그룹의 이름을 지정합니다.|
|/Server:<Server name>|서버 이름을 지정합니다. 이 NetBIOS 이름이 나 FQDN 수 있습니다. 서버 이름을 지정 하지, 로컬 서버가 사용 됩니다.|
|/ 사용 사용: {예 & #124; No}|패키지를 사용 하지 않도록 설정 하거나 사용 합니다.|
|/ 적응성: {일치 (& a) #124; 모든}|필터 조건을 충족 하는 경우 설치 하는 패키지를 지정 합니다. **일치** 의미의 클라이언트 하드웨어와 일치 하는 드라이버 패키지를 설치 합니다. **모든** 의미의 하드웨어에 관계 없이 클라이언트에 모든 패키지를 설치 합니다.|
|/Filtertype:<Filtertype>|그룹에 추가 하는 필터의 유형을 지정 합니다. 단일 명령에서 여러 종류의 필터를 지정할 수 있습니다. 각 필터 형식 뒤에 야 **/Policy** 와 하나 이상의 **/v**합니다. <Filtertype> 다음 중 하나일 수 있습니다.<br /><br />**BiosVendor**<br /><br />**Biosversion**<br /><br />**Chassistype**<br /><br />**제조업체**<br /><br />**uuid**<br /><br />**Osversion**<br /><br />**Osedition**<br /><br />**OsLanguage**<br /><br />다른 모든 필터 형식에 대 한 값을 얻는 방법에 대 한 자세한 내용은 [드라이버 그룹 필터](https://go.microsoft.com/fwlink/?LinkID=155158) (https://go.microsoft.com/fwlink/?LinkID=155158)합니다.|
|[/ 정책: {포함 (& a) #124; 제외}]|필터에 설정 될 정책을 지정 합니다. 경우 **/Policy** 로 설정 된 **포함**, 필터와 일치 하는 클라이언트 컴퓨터는이 그룹의 드라이버를 설치할 수 있습니다. 경우 **/Policy** 로 설정 된 **제외**, 다음 필터와 일치 하는 클라이언트 컴퓨터는이 그룹의 드라이버를 설치할 수 없습니다.|
|[/ 값:<Value>]|에 해당 하는 클라이언트 값 지정 **/Filtertype**합니다. 단일 형식에 대 한 여러 값을 지정할 수 있습니다. 특정 종류의 필터에 대 한 유효한 값에 대 한 다음 목록을 참조 하십시오. 에 대 한 다음 특성은 **Chassistype**합니다. 다른 모든 필터 형식에 대 한 값을 얻는 방법에 대 한 자세한 내용은 [드라이버 그룹 필터](https://go.microsoft.com/fwlink/?LinkID=155158) (https://go.microsoft.com/fwlink/?LinkID=155158)합니다.<br /><br />**기타**<br /><br />**UnknownChassis**<br /><br />**바탕 화면**<br /><br />**LowProfileDesktop**<br /><br />**PizzaBox**<br /><br />**MiniTower**<br /><br />**Tower**<br /><br />**이식 가능**<br /><br />**Laptop**<br /><br />**Notebook**<br /><br />**핸드헬드**<br /><br />**DockingStation**<br /><br />**AllInOne**<br /><br />**SubNotebook**<br /><br />**SpaceSaving**<br /><br />**LunchBox**<br /><br />**MainSystemChassis**<br /><br />**ExpansionChassis**<br /><br />**SubChassis**<br /><br />**BusExpansionChassis**<br /><br />**PeripheralChassis**<br /><br />**StoraeChassis**<br /><br />**RackmountChassis**<br /><br />**SealedCasecomputer**<br /><br />**MultiSystemChassis**<br /><br />**compactPci**<br /><br />**AdvancedTca**|
## <a name="BKMK_examples"></a>예제
드라이버 그룹을 추가 하려면 다음 중 하나를 입력 합니다.
```
wdsutil /add-DriverGroup /DriverGroup:printerdrivers /Enabled:Yes
```
```
wdsutil /add-DriverGroup /DriverGroup:printerdrivers /Applicability:All /Filtertype:Manufacturer /Policy:Include /Value:Name1 /Filtertype:Chassistype /Policy:Exclude /Value:Tower /Value:MiniTower
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[추가 DriverGroupPackage 명령을 사용 하 여](using-the-add-drivergrouppackage-command.md)
[추가 DriverGroupPackages 명령을 사용 하 여](using-the-add-drivergrouppackages-command.md)
[추가 DriverGroupFilter 명령을 사용 하 여](using-the-add-drivergroupfilter-command.md)
