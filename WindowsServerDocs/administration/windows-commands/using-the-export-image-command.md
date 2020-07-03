---
title: 내보내기-이미지
description: 이미지 저장소에서 다른 Windows 이미지 (.wim) 파일로 기존 이미지를 내보내는 내보내기 이미지에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a9b8b467-0f2d-4754-8998-55503a262778
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 04ac9d5a7e58fb2f22f5b034ea35dee08bf2a01a
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935229"
---
# <a name="export-image"></a>내보내기-이미지

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

다른 Windows 이미지 (.wim) 파일에 이미지 저장소에서 기존 이미지를 내보냅니다.

## <a name="syntax"></a>구문
부팅 이미지의 경우:
```
wdsutil [Options] /Export-Imagmedia:<Image name> [/Server:<Server name>]
   mediatype:Boot /Architecture:{x86 | ia64 | x64} [/Filename:<File name>]
     /DestinationImage
         /Filepath:<File path and name>
         [/Name:<Name>]
         [/Description:<Description>]
     [/Overwrite:{Yes | No}]
```
설치 이미지:
```
wdsutil [Options] /Export-Imagmedia:<Image name> [/Server:<Server name>]
   mediatype:InstallmediaGroup:<Image group name>]
     [/Filename:<File name>]
     /DestinationImage
         /Filepath:<File path and name>
         [/Name:<Name>]
         [/Description:<Description>]
     [/Overwrite:{Yes | No | append}]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
미디어만<Image name>|내보낼 이미지의 이름을 지정 합니다.|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
미디어 미디어: {Boot &#124; 설치}|내보낼 수는 이미지의 유형을 지정 합니다.|
|\mediaGroup:<Image group name>]|내보낼 이미지가 포함 된 이미지 그룹을 지정 합니다. 이미지 그룹 이름을 지정 하지 않으면 하나의 이미지 그룹 서버에 존재 하는 경우에 해당 이미지 그룹 기본적으로 사용 됩니다. 이미지 그룹 둘 이상의 서버에 있는 경우에 이미지 그룹을 지정 되어야 합니다.|
|/ 아키텍처: {x86 &#124;ia64 &#124; x64}|내보낼 이미지의 아키텍처를 지정 합니다. 다른 아키텍처에서 부팅 이미지에 동일한 이미지 이름을 가질 수 있기 때문에 아키텍처 값을 지정 하는 올바른 이미지를 반환할 것을 확인 합니다.|
|[/ 파일 이름:<Filename>]|이미지를 이름으로 고유 하 게 식별할 수 없는 경우에는 파일 이름을 지정 해야 합니다.|
|/ DestinationImage|대상 이미지에 대 한 설정을 지정합니다. 다음 옵션을 사용 하 여 이러한 설정을 지정할 수 있습니다.<p>-/Sfilefiles: <File path and name> -새 이미지의 전체 파일 경로를 지정 합니다.<br />-[/Name:<Name>]-이미지의 표시 이름을 설정 합니다. 이름이 없는 지정 하는 경우 원본 이미지의 표시 이름을 사용 됩니다.<br />-[/설명: <Description>]-이미지에 대 한 설명을 설정 합니다.|
|[/Overwrite: {Yes &#124; No &#124; append}]|해당 이름의 기존 파일이 이미/Filepath에 있는 경우 **/DestinationImage** 옵션에 지정 된 파일을 덮어쓸지 여부를 결정 합니다.<p>-   **예** 를 설정 하면 기존 파일을 덮어씁니다.<br />-   **아니요** (기본 옵션)를 사용 하면 이름이 같은 파일이 이미 있는 경우 오류가 발생 합니다.<br />-   **추가** 를 수행 하면 생성 된 이미지가 기존 .wim 파일 내에 새 이미지로 추가 됩니다.|
## <a name="examples"></a>예
부팅 이미지를 내보내려면 다음 중 하나를 입력 합니다.
```
wdsutil /Export-Imagmedia:WinPE boot imagemediatype:Boot /Architecture:x86 /DestinationImage /Filepath:C:\temp\boot.wim
wdsutil /verbose /Progress /Export-Imagmedia:WinPE boot image /Server:MyWDSServemediatype:Boot /Architecture:x64 /Filename:boot.wim
/DestinationImage /Filepath:\\Server\Share\ExportImage.wim /Name:Exported WinPE image /Description:WinPE Image from WDS server /Overwrite:Yes
```
설치 이미지를 내보내려면 다음 중 하나를 입력 합니다.
```
wdsutil /Export-Imagmedia:Windows Vista with Officemediatype:Install /DestinationImage /Filepath:C:\Temp\Install.wim
wdsutil /verbose /Progress /Export-Imagmedia:Windows Vista with Office /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1
/Filename:install.wim /DestinationImage /Filepath:\\server\share\export.wim /Name:Exported Windows image /Description:Windows Vista image from WDS server /Overwrite:append
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md) 
 [추가 이미지 명령을](using-the-add-image-command.md) 
 사용 하 여 [복사 이미지 명령을](using-the-copy-image-command.md) 
 사용 하 여 [Get 이미지 명령을](using-the-get-image-command.md) 
 사용 하 여 [제거 이미지 명령을](using-the-remove-image-command.md) 
 사용 하 여 [Replace 이미지 명령을](using-the-replace-image-command.md) 
 사용 하 여 [하위 명령: 설정 이미지](subcommand-set-image.md)
