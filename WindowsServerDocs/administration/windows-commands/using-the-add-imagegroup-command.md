---
title: ImageGroup
description: ImageGroup에 대 한 Windows 명령 항목-이미지 그룹을 Windows 배포 서비스 서버에 추가 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6ca88671-51de-4924-b969-88f3dfd84270
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f12ed27ca1a809ec34dbefbc4ff7288ff194a83e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80831896"
---
# <a name="add-imagegroup"></a>ImageGroup

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

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
## <a name="examples"></a><a name=BKMK_examples></a>예와
이미지 그룹을 추가 하려면 다음 중 하나를 입력 합니다.
```
wdsutil /add-ImageGroumediaGroup:ImageGroup2
wdsutil /verbose /add-ImageGroumediaGroup:My Image Group /Server:MyWDSServer
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)
[get AllImageGroups 명령을 사용 하 여](using-the-get-allimagegroups-command.md)
[get ImageGroup 명령을 사용 하 여](using-the-get-imagegroup-command.md)
[제거 ImageGroup 명령을 사용 하 여](using-the-remove-imagegroup-command.md)
[하위 명령: ImageGroup 집합](subcommand-set-imagegroup.md)
