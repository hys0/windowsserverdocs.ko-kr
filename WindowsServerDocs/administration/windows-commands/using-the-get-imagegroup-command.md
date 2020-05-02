---
title: ImageGroup
description: 이미지 그룹 및 해당 이미지에 대 한 정보를 검색 하는 ImageGroup에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0fc25aca-a529-44ee-bc8e-96bc8affb458
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 30a87085cb935f95a209ffdd78ecf2b9fb45dc15
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719897"
---
# <a name="get-imagegroup"></a>ImageGroup

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이미지 그룹 및 그 안에 이미지에 대 한 정보를 검색합니다.

## <a name="syntax"></a>구문
```
wdsutil [Options] /Get-ImageGroumediaGroup:<Image group name> [/Server:<Server name>] [/detailed]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
mediaGroup:<Image group name>|이미지 그룹의 이름을 지정합니다.|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
|자세한/|각 이미지에 대 한 이미지 메타 데이터를 반환합니다. 이 매개 변수 사용 없는 경우 기본 동작은 이미지 이름, 설명 및 파일 이름을 반환할 합니다.|
## <a name="examples"></a>예
이미지 그룹에 대 한 정보를 보려면 다음을 입력 합니다.
```
wdsutil /Get-ImageGroumediaGroup:ImageGroup1
```
메타 데이터를 포함 하 여 정보를 보려면 다음을 입력 합니다.
```
wdsutil /verbose /Get-ImageGroumediaGroup:ImageGroup1 /Server:MyWDSServer /detailed
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)
[ImageGroup](using-the-add-imagegroup-command.md)
명령을 사용 하 여[AllImageGroups 명령을](using-the-get-allimagegroups-command.md)
사용 하 여[ImageGroup 명령](using-the-remove-imagegroup-command.md)
[하위 명령: ImageGroup](subcommand-set-imagegroup.md)
