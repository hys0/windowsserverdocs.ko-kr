---
title: 바꾸기-이미지
description: 기존 이미지를 해당 이미지의 새 버전으로 대체 하는 대체 이미지에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 68ded3df-e309-420f-9f5d-caeb609385a5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b98bf14b944ce75a21efbbb38a211e60ca952d39
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931350"
---
# <a name="using-the-replace-image-command"></a>바꾸기 이미지 명령을 사용 하 여

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

해당 이미지의 새 버전으로 기존 이미지를 대체합니다.
## <a name="syntax"></a>구문
부팅 이미지의 경우:
```
wdsutil [Options] /replace-Imagmedia:<Image name> [/Server:<Server name>]
   mediatype:Boot
     /Architecture:{x86 | ia64 | x64}
     [/Filename:<File name>]
     /replacementImage
       mediaFile:<wim file path>
         [/Name:<Image name>]
         [/Description:<Image description>]
```
설치 이미지:
```
wdsutil [Options] /replace-Imagmedia:<Image name> [/Server:<Server name>]
   mediatype:Install
    mediaGroup:<Image group name>]
     [/Filename:<File name>]
     /replacementImage
       mediaFile:<wim file path>
         [/SourceImage:<Source image name>]
         [/Name:<Image name>]
         [/Description:<Image description>]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
미디어만<Image name>|교체 이미지의 이름을 지정 합니다.|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
미디어 미디어: {Boot &#124; 설치}|교체는 이미지의 유형을 지정 합니다.|
|/ 아키텍처: {x86 &#124;ia64 &#124; x64}|교체 이미지의 아키텍처를 지정 합니다. 다른 아키텍처에서 다른 부팅 이미지에 대 한 동일한 이미지 이름을 가질 수 있기 때문에 아키텍처를 지정 하 하면 올바른 이미지 대체 됩니다.|
|[/ 파일 이름:<File name>]|이미지를 이름으로 고유 하 게 식별할 수 없는 경우에는이 옵션을 사용 하 여 파일 이름을 지정 해야 합니다.|
|/replacementImage|대체 이미지에 대 한 설정을 지정합니다. 다음 옵션을 사용 하 여 이러한 설정을 설정할 수 있습니다.<p>-mediaFile: <file path> -이름 및 새.wim 파일의 위치 (전체 경로)을 지정 합니다.<br />-[/ SourceImage: <image name>]-.wim 파일에 여러 이미지가 포함 된 경우 사용할 이미지를 지정 합니다. 이 옵션은 설치 이미지에만 적용 됩니다.<br />-[/Name: <Image name> ] 이미지의 표시 이름을 설정 합니다.<br />-[/ 설명:<Image description>]-이미지의 설명을 설정 합니다.|
## <a name="examples"></a>예
부팅 이미지를 대체 하려면 다음 중 하나를 입력 합니다.
```
wdsutil /replace-Imagmedia:WinPE Boot Imagemediatype:Boot /Architecture:x86 /replacementImagmediaFile:C:\MyFolder\Boot.wim
wdsutil /verbose /Progress /replace-Imagmedia:WinPE Boot Image /Server:MyWDSServemediatype:Boot /Architecture:x64 /Filename:boot.wim
/replacementImagmediaFile:\\MyServer\Share\Boot.wim /Name:My WinPE Image /Description:WinPE Image with drivers
```
설치 이미지를 대체 하려면 다음 중 하나를 입력 합니다.
```
wdsutil /replace-Imagmedia:Windows Vista Homemediatype:Install /replacementImagmediaFile:C:\MyFolder\Install.wim
wdsutil /verbose /Progress /replace-Imagmedia:Windows Vista Pro /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1
/Filename:Install.wim /replacementImagmediaFile:\\MyServer\Share \Install.wim /SourceImage:Windows Vista Ultimate /Name:Windows Vista Desktop /Description:Windows Vista Ultimate with standard business applications.
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md) 
 [추가 이미지 명령을](using-the-add-image-command.md) 
 사용 하 여 [복사 이미지 명령을](using-the-copy-image-command.md) 
 사용 하 여 [내보내기 이미지 명령 사용](using-the-export-image-command.md) 
 [Get 이미지 명령을](using-the-get-image-command.md) 
 사용 하 여 [Replace 이미지 명령을](using-the-replace-image-command.md) 
 사용 하 여 [하위 명령: 설정 이미지](subcommand-set-image.md)
