---
title: 이미지 추가
description: Windows 배포 서비스 서버에 이미지를 추가 하는 추가 이미지에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d5b6f4da-90ba-4b0e-9423-66c8ef5172e2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0fb252fb5e10cc18d421c44d6edca893879905a5
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721077"
---
# <a name="add-image"></a>이미지 추가

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows 배포 서비스 서버에 이미지를 추가합니다.

## <a name="syntax"></a>구문
부팅 이미지의 경우 다음 구문을 사용 합니다.
```
wdsutil /add-ImagmediaFile:<wim file path> [/Server:<Server name>mediatype:Boot [/Skipverify] [/Name:<Image name>] [/Description:<Image description>] 
[/Filename:<New wim file name>]
```
설치 이미지의 경우 다음 구문을 사용 합니다.
```
wdsutil /add-ImagmediaFile:<wim file path>
     [/Server:<Server name>]
   mediatype:Install
     [/Skipverify]
    mediaGroup:<Image group name>]
     [/SingleImage:<Single image name>]
         [/Name:<Name>]
         [/Description:<Description>]
     [/Filename:<File name>]
     [/UnattendFile:<Unattend file path>]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
mediaFile: <.wim 파일 경로 >|추가 될 이미지가 포함 된 Windows 이미지 (.wim) 파일의 전체 경로 파일 이름을 지정 합니다.|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름을 지정 하지 않으면 로컬 서버가 사용 됩니다.|
mediatype: {부팅&#124;설치}|추가할 이미지의 유형을 지정 합니다.|
|[/Skipverify]|무결성을 확인은 수행 되지 않도록 원본 이미지 파일에 이미지를 추가 하기 전에 지정 합니다.|
|[/Name:<Name>]|이미지의 표시 이름을 설정합니다.|
|/Description<Description>]|이미지에 대 한 설명을 설정합니다.|
|[/ 파일 이름:<Filename>]|.Wim 파일에 대 한 새 파일 이름을 지정합니다. 이 이미지를 추가할 때.wim 파일의 파일 이름을 변경할 수 있습니다. 파일 이름이 지정 되는 원본 이미지 파일 이름이 사용 됩니다. 모든 경우에 Windows 배포 서비스는 대상 컴퓨터의 부팅 이미지 저장소에 파일 이름이 고유한 지 확인 하 여 확인 합니다.|
|\mediaGroup:<Image group name>]|추가할 이미지는 이미지 그룹의 이름을 지정 합니다. 이미지 그룹 둘 이상의 서버에 있는 경우에 이미지 그룹을 지정 되어야 합니다. 이것은 이미지 그룹이 아직 없는 경우 새 이미지 그룹 생성 됩니다. 그렇지 않으면 기존 이미지 그룹 사용 됩니다.|
|[/SingleImage:<Single image name>] [/name:<Name>] [/설명:<Description>]|.Wim 파일에서 지정된 된 단일 이미지를 복사 하 고 이미지의 표시 이름과 설명을 설정 합니다.|
|[/ UnattendFile:<Unattend file path>]|추가 되는 이미지와 연결 되도록 무인된 설치 파일의 전체 경로 지정 합니다. 경우 **/SingleImage** 를 지정 하지 않으면 동일한 무인 파일이 모든.wim 파일에 이미지와 연결 됩니다.|
## <a name="examples"></a>예
부팅 이미지를 추가 하려면 다음을 입력 합니다.
```
wdsutil /add-ImagmediaFile:C:\MyFolder\Boot.wimmediatype:Boot
wdsutil /verbose /Progress /add-ImagmediaFile:\\MyServer\Share\Boot.wim /Server:MyWDSServemediatype:Boot /Name:My WinPE Image 
/Description:WinPE Image containing the WDS Client /Filename:WDSBoot.wim
```
설치 이미지를 추가 하려면 다음 중 하나를 입력 합니다.
```
wdsutil /add-ImagmediaFile:C:\MyFolder\Install.wimmediatype:Install
wdsutil /verbose /Progress /add-ImagmediaFile:\\MyServer\Share \Install.wim /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 
/SingleImage:Windows Pro /Name:My WDS Image
/Description:Windows Pro image with Microsoft Office /Filename:Win Pro.wim /UnattendFile:\\server\share\unattend.xml
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)
[복사](using-the-copy-image-command.md)
이미지 명령을 사용 하 여 이미지[내보내기](using-the-export-image-command.md)
명령을 사용 하 여[get](using-the-get-image-command.md)
이미지 명령을 사용 하 여[제거](using-the-remove-image-command.md)
이미지 명령을 사용 하 여[바꾸기 이미지](using-the-replace-image-command.md)
명령을 사용 하 여[하위 명령: 설정 이미지](subcommand-set-image.md)
