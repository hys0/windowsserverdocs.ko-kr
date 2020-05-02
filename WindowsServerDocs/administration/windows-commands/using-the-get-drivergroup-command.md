---
title: DriverGroup
description: 서버에 드라이버 그룹에 대 한 정보를 표시 하는 get DriverGroup에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7cfe10c3-a63f-48e7-bef9-f6b474b4ddbe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4804b699959b4fba2551e84379db97243f093ce7
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719950"
---
# <a name="get-drivergroup"></a>DriverGroup

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

서버에 드라이버 그룹에 대 한 정보를 표시합니다.

## <a name="syntax"></a>구문
```
wdsutil /Get-DriverGroup /DriverGroup:<Group Name> [/Server:<Server name>]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|DriverGroup<Group Name>|드라이버 그룹의 이름을 지정합니다.|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름이 나 FQDN 수 있습니다.  서버 이름을 지정 하지 않으면 로컬 서버가 사용 됩니다.|
|[표시 /: {PackageMetaData & #124; #124; 및 필터 모든}]|지정된 된 그룹의 모든 드라이버 패키지에 대 한 메타 데이터를 표시합니다. **PackageMetaData** 드라이버 그룹에 대 한 모든 필터에 대 한 정보를 표시 합니다. **필터** 모든 드라이버 패키지에 대 한 메타 데이터 및 그룹에 대 한 필터를 표시 합니다.|
## <a name="examples"></a>예
드라이버 파일에 대 한 정보를 보려면 다음을 입력 합니다.
```
wdsutil /Get-DriverGroup /DriverGroup:printerdrivers /Show:PackageMetaData
```
```
wdsutil /Get-DriverGroup /DriverGroup:printerdrivers /Server:MyWdsServer /Show:Filters
```
## <a name="additional-references"></a>추가 참조
- [Command-Line Syntax Key](command-line-syntax-key.md)
[Get alldrivergroups 명령을 사용 하 여](using-the-get-alldrivergroups-command.md) 명령줄 구문 키
