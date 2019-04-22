---
title: Get AllImageGroups 명령을 사용 하 여
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2ca06533-bcf5-4590-ac8e-263d6c9874f8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 917f61327a3d39ee97c5fd59072884f7844c487e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822354"
---
# <a name="using-the-get-allimagegroups-command"></a>Get AllImageGroups 명령을 사용 하 여

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

모든 이미지 그룹에 대 한 정보는 서버와 해당 이미지 그룹의 모든 이미지를 검색합니다.
## <a name="syntax"></a>구문
```
wdsutil [Options] /Get-AllImageGroups [/Server:<Server name>] [/detailed]
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
|[/detailed]|각 이미지에서 이미지 메타 데이터를 반환합니다. 이 매개 변수를 사용 하지 않으면 하는 경우 이미지 이름, 설명 및 각 이미지에 대 한 파일 이름을 반환 하는 기본 동작이입니다.|
## <a name="BKMK_examples"></a>예제
이미지 그룹에 대 한 정보를 보려면 다음 중 하나를 입력 합니다.
```
wdsutil /Get-AllImageGroups
wdsutil /verbose /Get-AllImageGroups /Server:MyWDSServer /detailed
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[추가 ImageGroup 명령을 사용 하 여](using-the-add-imagegroup-command.md)
[get ImageGroup 명령을 사용 하 여](using-the-get-imagegroup-command.md)
[제거 ImageGroup 명령을 사용 하 여](using-the-remove-imagegroup-command.md)
[하위 명령: ImageGroup 집합](subcommand-set-imagegroup.md)
