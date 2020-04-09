---
title: ImageGroup
description: ImageGroup에 대 한 Windows 명령 항목은 이미지 그룹 및 해당 이미지에 대 한 정보를 검색 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0fc25aca-a529-44ee-bc8e-96bc8affb458
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0066e5d52c1d10b1f78ea627ee7a476bfd98f19d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830956"
---
# <a name="get-imagegroup"></a>ImageGroup

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

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
## <a name="examples"></a><a name=BKMK_examples></a>예와
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
[추가 ImageGroup 명령을 사용 하 여](using-the-add-imagegroup-command.md)
[get AllImageGroups 명령을 사용 하 여](using-the-get-allimagegroups-command.md)
[제거 ImageGroup 명령을 사용 하 여](using-the-remove-imagegroup-command.md)
[하위 명령: ImageGroup 집합](subcommand-set-imagegroup.md)
