---
title: Get ImageGroup 명령을 사용 하 여
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0fc25aca-a529-44ee-bc8e-96bc8affb458
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d6531a3b69840a0a4910b2effdd3e349b76edf2c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363122"
---
# <a name="using-the-get-imagegroup-command"></a>Get ImageGroup 명령을 사용 하 여

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이미지 그룹 및 그 안에 이미지에 대 한 정보를 검색합니다.
## <a name="syntax"></a>구문
```
wdsutil [Options] /Get-ImageGroumediaGroup:<Image group name> [/Server:<Server name>] [/detailed]
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
mediaGroup: <Image group name>|이미지 그룹의 이름을 지정합니다.|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
|자세한/|각 이미지에 대 한 이미지 메타 데이터를 반환합니다. 이 매개 변수 사용 없는 경우 기본 동작은 이미지 이름, 설명 및 파일 이름을 반환할 합니다.|
## <a name="BKMK_examples"></a>예와
이미지 그룹에 대 한 정보를 보려면 다음을 입력 합니다.
```
wdsutil /Get-ImageGroumediaGroup:ImageGroup1
```
메타 데이터를 포함 하 여 정보를 보려면 다음을 입력 합니다.
```
wdsutil /verbose /Get-ImageGroumediaGroup:ImageGroup1 /Server:MyWDSServer /detailed
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[추가 ImageGroup 명령을 사용 하 여](using-the-add-imagegroup-command.md)
[get AllImageGroups 명령을 사용 하 여](using-the-get-allimagegroups-command.md)
[제거 ImageGroup 명령을 사용 하 여](using-the-remove-imagegroup-command.md)
[하위 명령: ImageGroup 집합](subcommand-set-imagegroup.md)
