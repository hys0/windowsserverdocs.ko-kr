---
title: 이미지 내보내기 명령을 사용 하 여
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a9b8b467-0f2d-4754-8998-55503a262778
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: efa9b2d09c37a383a91883ee02c995eedb2f235e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823144"
---
# <a name="using-the-export-image-command"></a>이미지 내보내기 명령을 사용 하 여

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

다른 Windows 이미지 (.wim) 파일에 이미지 저장소에서 기존 이미지를 내보냅니다.
## <a name="syntax"></a>구문
부팅 이미지:
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
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
미디어:<Image name>|내보낼 이미지의 이름을 지정 합니다.|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
mediatype: {부팅 &#124; 설치}|내보낼 수는 이미지의 유형을 지정 합니다.|
|\mediaGroup:<Image group name>]|내보낼 이미지가 포함 된 이미지 그룹을 지정 합니다. 이미지 그룹 이름을 지정 하지 않으면 하나의 이미지 그룹 서버에 존재 하는 경우에 해당 이미지 그룹 기본적으로 사용 됩니다. 이미지 그룹 둘 이상의 서버에 있는 경우에 이미지 그룹을 지정 되어야 합니다.|
|/ 아키텍처: {x86 & #124 ia64 & #124; x64}|내보낼 이미지의 아키텍처를 지정 합니다. 다른 아키텍처에서 부팅 이미지에 동일한 이미지 이름을 가질 수 있기 때문에 아키텍처 값을 지정 하는 올바른 이미지를 반환할 것을 확인 합니다.|
|[/ 파일 이름:<Filename>]|이미지 이름으로 고유 하 게 식별할 수 없으면, 파일 이름을 지정 해야 합니다.|
|/ DestinationImage|대상 이미지에 대 한 설정을 지정합니다. 다음 옵션을 사용 하 여 이러한 설정을 지정할 수 있습니다.<br /><br />-/Filepath:<File path and name> -새 이미지에 대 한 전체 파일 경로 지정 합니다.<br />-[/Name:<Name>]-이미지의 표시 이름을 설정 합니다. 이름이 없는 지정 하는 경우 원본 이미지의 표시 이름을 사용 됩니다.<br />-   [/Description: <Description>]-이미지의 설명을 설정 합니다.|
|[/Overwrite: {예 &#124; 아니요 &#124; 추가}]|파일에 지정 되었는지 여부를 결정 합니다 **/DestinationImage** 옵션 해당 이름 가진 기존 파일의 /filepath 이미 있으면 덮어씁니다.<br /><br />-   **예** 하면 기존 파일을 덮어쓸 수 있습니다.<br />-   **이상** (기본 옵션) 하면 오류가 동일한 이름의 파일이 이미 있는 경우 발생 합니다.<br />-   **추가** 하면 생성 된 이미지가 기존.wim 파일 내에서 새 이미지로 추가 합니다.|
## <a name="BKMK_examples"></a>예제
부팅 이미지를 내보내려면 다음 중 하나를 입력 합니다.
```
wdsutil /Export-Imagmedia:"WinPE boot imagemediatype:Boot /Architecture:x86 /DestinationImage /Filepath:"C:\temp\boot.wim"
wdsutil /verbose /Progress /Export-Imagmedia:"WinPE boot image" /Server:MyWDSServemediatype:Boot /Architecture:x64 /Filename:boot.wim 
/DestinationImage /Filepath:"\\Server\Share\ExportImage.wim" /Name:"Exported WinPE image" /Description:"WinPE Image from WDS server" /Overwrite:Yes
```
설치 이미지를 내보내려면 다음 중 하나를 입력 합니다.
```
wdsutil /Export-Imagmedia:"Windows Vista with Officemediatype:Install /DestinationImage /Filepath:"C:\Temp\Install.wim"
wdsutil /verbose /Progress /Export-Imagmedia:"Windows Vista with Office" /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 
/Filename:install.wim /DestinationImage /Filepath:\\server\share\export.wim /Name:"Exported Windows image" /Description:"Windows Vista image from WDS server" /Overwrite:append
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[추가 이미지 명령을 사용 하 여](using-the-add-image-command.md)
[복사 이미지 명령을 사용 하 여](using-the-copy-image-command.md)
[get 이미지 명령을 사용 하 여](using-the-get-image-command.md)
[제거 이미지 명령을 사용 하 여](using-the-remove-image-command.md)
[바꾸기 이미지 명령을 사용 하 여](using-the-replace-image-command.md)
[하위 명령: 설정 이미지](subcommand-set-image.md)
