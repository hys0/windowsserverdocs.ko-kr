---
title: 이미지 복사
description: 동일한 이미지 그룹 내에 있는 이미지를 복사 하는 복사 이미지에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bea41cf4-36e6-4181-afa5-00170ebd4fdc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 04af31680a99c5da60b721ad5dc31cbd3851538d
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933995"
---
# <a name="copy-image"></a>이미지 복사

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

동일한 이미지 그룹 내에 있는 이미지를 복사 합니다. 이미지 그룹 간에 이미지를 복사 하려면 사용 하 여는 [이미지 내보내기 명령을 사용 하 여](using-the-export-image-command.md) 명령을 차례로 [추가 이미지 명령을 사용 하 여](using-the-add-image-command.md) 명령입니다.

## <a name="syntax"></a>구문
```
wdsutil [Options] /copy-Imagmedia:<Image name> [/Server:<Server name>]
   mediatype:Install
    mediaGroup:<Image group name>]
     [/Filename:<File name>]
     /DestinationImage
         /Name:<Name>
         /Filename:<File name>
         [/Description:<Description>]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
미디어만<Image name>|복사할 이미지의 이름을 지정 합니다.|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
미디어 미디어: 설치|복사할 이미지의 유형을 지정 합니다. 이 옵션으로 설정 되어 있어야 **설치**합니다.|
|\mediaGroup:<Image group name>]|복사할 이미지를 포함 하는 이미지 그룹을 지정 합니다. 지정 된 이미지 그룹이 없고 하나의 그룹에만 서버에 존재 하는 경우 해당 이미지 그룹 기본적으로 사용 됩니다. 이미지 그룹 둘 이상의 서버에 있는 경우 이미지 그룹을 지정 해야 합니다.|
|[/ 파일 이름:<Filename>]|복사할 이미지의 파일 이름을 지정 합니다. 원본 이미지 이름으로 고유 하 게 식별할 수 없으면, 파일 이름을 지정 해야 합니다.|
|/ DestinationImage|다음 표에 설명 된 대로 대상 이미지에 대 한 설정을 지정 합니다.<p>-/Name:<Name> -복사할 이미지의 표시 이름을 설정 합니다.<br />-/Filename:<Filename> -이미지 복사본을 포함 하는 대상 이미지 파일의 이름을 설정 합니다.<br />-[/설명: <Description>]-이미지 복사본에 대 한 설명을 설정 합니다.|
## <a name="examples"></a>예
지정된 된 이미지의 복사본을 만들고 WindowsVista.wim 라는 이름을 지정 하려면 다음을 입력 합니다.
```
wdsutil /copy-Imagmedia:Windows Vista with Officemediatype:Install /DestinationImage /Name:copy of Windows Vista with Office /Filename:WindowsVista.wim
```
지정된 된 이미지의 복사본을 만들려면 지정 된 설정을 적용 하 고 복사 WindowsVista.wim, 형식 이름:
```
wdsutil /verbose /Progress /copy-Imagmedia:Windows Vista with Office /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1
/Filename:install.wim /DestinationImage /Name:copy of Windows Vista with Office /Filename:WindowsVista.wim /Description:This is a copy of the original Windows image with Office installed
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md) 
 [추가 이미지 명령을](using-the-add-image-command.md) 
 사용 하 여 [내보내기 이미지 명령 사용](using-the-export-image-command.md) 
 [Get 이미지 명령을](using-the-get-image-command.md) 
 사용 하 여 [제거 이미지 명령을](using-the-remove-image-command.md) 
 사용 하 여 [Replace 이미지 명령을](using-the-replace-image-command.md) 
 사용 하 여 [하위 명령: 설정 이미지](subcommand-set-image.md)
