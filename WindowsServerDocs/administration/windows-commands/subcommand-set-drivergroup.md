---
title: 하위 명령 설정-DriverGroup
description: 서버에 있는 기존 드라이버 그룹의 속성을 설정 하는 하위 명령 집합-DriverGroup에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e4ba9b1c-8c52-4fd5-969b-f7905611b364
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c70db688e17d185813298cea4fcee3b664f53d64
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721738"
---
# <a name="subcommand-set-drivergroup"></a>하위 명령: 집합 DriverGroup

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

서버의 기존 드라이버 그룹의 속성을 설정합니다.

## <a name="syntax"></a>구문
```
wdsutil /Set-DriverGroup /DriverGroup:<Group Name> [/Server:<Server Name>] [/Name:<New Group Name>] [/Enabled:{Yes | No}] [/Applicability:{Matched | All}]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|DriverGroup<Group Name>|드라이버 그룹의 이름을 지정합니다.|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름이 나 FQDN 수 있습니다. 서버 이름을 지정 하지 않으면 로컬 서버가 사용 됩니다.|
|[/Name:<New Group Name>]|드라이버 그룹에 대 한 새 이름을 지정합니다.|
|[/ 활성화: {예 & #124; No}|드라이버 그룹을 사용 하지 않도록 설정 하거나 사용 합니다.|
|[/ 적응성: {일치 (& a) #124; 모든}]|필터 조건이 충족 되는 경우 설치 하는 패키지를 지정 합니다. **일치** 함은 클라이언트 하드웨어와 일치 하는 드라이버 패키지만 설치 합니다. **모든** 의미를 클라이언트의 하드웨어에 관계 없이 모든 패키지를 설치 합니다.|
## <a name="examples"></a>예
드라이버 그룹에 대 한 속성을 설정 하려면 다음 중 하나를 입력 합니다.
```
wdsutil /Set-DriverGroup /DriverGroup:printerdrivers /Enabled:Yes
```
```
wdsutil /Set-DriverGroup /DriverGroup:printerdrivers /Name:colorprinterdrivers /Applicability:All
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)
[하위 명령: set drivergroupfilter](subcommand-set-drivergroupfilter.md)
