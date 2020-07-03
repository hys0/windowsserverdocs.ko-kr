---
title: get AllDriverGroups
description: 서버에 있는 모든 드라이버 그룹에 대 한 정보를 표시 하는 get AllDriverGroups에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f245ba53-f150-41b1-8418-38dcf0410a05
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4c254ee19cb7f447d0fb071469c50107205de98b
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935210"
---
# <a name="get-alldrivergroups"></a>get AllDriverGroups

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

서버에 있는 모든 드라이버 그룹에 대 한 정보를 표시합니다.

## <a name="syntax"></a>구문
```
wdsutil /Get-AllDriverGroups [/Server:<Server name>] [/Show:{PackageMetaData | Filters | All}]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름이 나 FQDN 수 있습니다. 서버 이름을 지정 하지 않으면 로컬 서버가 사용 됩니다.|
|[표시 /: {PackageMetaData & #124; #124; 및 필터 모든}]|지정된 된 그룹의 모든 드라이버 패키지에 대 한 메타 데이터를 표시합니다. **PackageMetaData** 드라이버 그룹에 대 한 모든 필터에 대 한 정보를 표시 합니다. **필터** 모든 드라이버 패키지에 대 한 메타 데이터 및 그룹에 대 한 필터를 표시 합니다.|
## <a name="examples"></a>예
드라이버 파일에 대 한 정보를 보려면 다음을 입력 합니다.
```
wdsutil /Get-AllDriverGroups /Server:MyWdsServer /Show:All
```
```
wdsutil /Get-AllDriverGroups [/Show:PackageMetaData]
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md) 
 [Get DriverGroup 명령을 사용 하 여](using-the-get-drivergroup-command.md)
