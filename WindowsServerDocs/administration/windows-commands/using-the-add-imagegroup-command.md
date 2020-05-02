---
title: ImageGroup
description: Windows 배포 서비스 서버에 이미지 그룹을 추가 하는 ImageGroup에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6ca88671-51de-4924-b969-88f3dfd84270
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b08042ac6b33c0ccfe0b66bb0fec70805d55d75f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721049"
---
# <a name="add-imagegroup"></a>ImageGroup

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows 배포 서비스 서버에 이미지 그룹을 추가합니다.

## <a name="syntax"></a>구문
```
wdsutil [Options] /add-ImageGroumediaGroup:<Image group name> [/Server:<Server name>]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
mediaGroup:<Image group name>|추가할 수 있는 이미지 그룹의 이름을 지정 합니다.|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름을 지정 하지 않으면 로컬 서버가 사용 됩니다.|
## <a name="examples"></a>예
이미지 그룹을 추가 하려면 다음 중 하나를 입력 합니다.
```
wdsutil /add-ImageGroumediaGroup:ImageGroup2
wdsutil /verbose /add-ImageGroumediaGroup:My Image Group /Server:MyWDSServer
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)
[AllImageGroups 명령을](using-the-get-allimagegroups-command.md)
사용 하 여[ImageGroup](using-the-get-imagegroup-command.md)
명령을 사용 하 여[ImageGroup 명령](using-the-remove-imagegroup-command.md)
[하위 명령: ImageGroup](subcommand-set-imagegroup.md)
