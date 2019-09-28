---
title: 추가 ImageGroup 명령을 사용 하 여
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6ca88671-51de-4924-b969-88f3dfd84270
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5e870bd5435e1aa2b155fee880d32c0d784ac398
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363680"
---
# <a name="using-the-add-imagegroup-command"></a>추가 ImageGroup 명령을 사용 하 여

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows 배포 서비스 서버에 이미지 그룹을 추가 합니다.
## <a name="syntax"></a>구문
```
wdsutil [Options] /add-ImageGroumediaGroup:<Image group name> [/Server:<Server name>]
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
mediaGroup: <Image group name>|추가할 수 있는 이미지 그룹의 이름을 지정 합니다.|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름을 지정 하지 않으면 로컬 서버가 사용 됩니다.|
## <a name="BKMK_examples"></a>예와
이미지 그룹을 추가 하려면 다음 중 하나를 입력 합니다.
```
wdsutil /add-ImageGroumediaGroup:ImageGroup2
wdsutil /verbose /add-ImageGroumediaGroup:"My Image Group" /Server:MyWDSServer
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[get AllImageGroups 명령을 사용 하 여](using-the-get-allimagegroups-command.md)
[get ImageGroup 명령을 사용 하 여](using-the-get-imagegroup-command.md)
[제거 ImageGroup 명령을 사용 하 여](using-the-remove-imagegroup-command.md)
[하위 명령: ImageGroup 집합](subcommand-set-imagegroup.md)
