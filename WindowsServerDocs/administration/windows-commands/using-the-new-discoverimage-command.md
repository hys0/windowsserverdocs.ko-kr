---
title: DiscoverImage
description: 기존 부팅 이미지에서 새 검색 이미지를 만드는 DiscoverImage에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ede9fbbb-0bba-4309-8c21-3cc13e1dc3cd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d6730dd2b5ffd7cbec2ed7ec9706747072b36fab
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932447"
---
# <a name="new-discoverimage"></a>DiscoverImage

기존 부팅 이미지에서 새 검색 이미지를 만듭니다. 검색 이미지는 Setup.exe 프로그램이 Windows 배포 서비스 모드에서 시작 되 게 한 다음 Windows 배포 서비스 서버를 검색 하도록 하는 부팅 이미지입니다. 일반적으로 이러한 이미지는 PXE로 부팅할 수 없는 컴퓨터에 이미지를 배포 하는 데 사용 됩니다. 자세한 내용은 이미지 만들기 ()를 참조 하십시오 [https://go.microsoft.com/fwlink/?LinkId=115311](https://go.microsoft.com/fwlink/?LinkId=115311) .

## <a name="syntax"></a>구문

```
WDSUTIL [Options] /New-DiscoverImage [/Server:<Server name>]
     /Image:<Image name>
     /Architecture:{x86 | ia64 | x64}
     [/Filename:<File name>]
     /DestinationImage
         /FilePath:<File path and name>
         [/Name:<Name>]
         [/Description:<Description>]
         [/WDSServer:<Server name>]
         [/Overwrite:{Yes | No | Append}]
```

### <a name="parameters"></a>매개 변수

|        매개 변수         |                                                                                                                                                                                                                                                                                                                                                                                                                       설명                                                                                                                                                                                                                                                                                                                                                                                                                       |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/ 서버:\<Server name>] |                                                                                                                                                                                                                                                                                                                                     서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.                                                                                                                                                                                                                                                                                                                                     |
|   이미지로\<Image name>   |                                                                                                                                                                                                                                                                                                                                                                                                      원본 부팅 이미지의 이름을 지정 합니다.                                                                                                                                                                                                                                                                                                                                                                                                       |
|    /아키텍처: {x86    |                                                                                                                                                                                                                                                                                                                                                                                                                          ia64                                                                                                                                                                                                                                                                                                                                                                                                                           |
| [/ 파일 이름:\<File name>] |                                                                                                                                                                                                                                                                                                                                                                         이미지 이름으로 고유 하 게 식별할 수 없으면, 파일 이름을 지정 하려면이 옵션을 사용 해야 합니다.                                                                                                                                                                                                                                                                                                                                                                          |
|    / DestinationImage     | 대상 이미지에 대 한 설정을 지정합니다. 다음 옵션을 사용 하 여 설정을 지정할 수 있습니다.</br>-/Sfilefiles: < 파일 경로 및 이름>-새 이미지에 대 한 전체 파일 경로를 설정 합니다.</br>-[/Name:\<Name>]-이미지의 표시 이름을 설정 합니다. 표시 이름을 지정 하지 않으면 원본 이미지의 표시 이름이 사용 됩니다.</br>-[/ 설명: \<Description>]-이미지의 설명을 설정 합니다.</br>-[/WDSServer: \<Server name> ]-지정 된 이미지에서 부팅 하는 모든 클라이언트가 설치 이미지를 다운로드 하기 위해 연결 해야 하는 서버의 이름을 지정 합니다. 기본적으로이 이미지를 부팅 하는 모든 클라이언트는 유효한 Windows 배포 서비스 서버를 검색 합니다. 이 옵션을 사용 하면 검색 기능이 무시 되 고 부팅 된 클라이언트가 지정 된 서버에 연결 하도록 강제 합니다.</br>-[/Overwrite: {예 |

## <a name="examples"></a>예

부팅 이미지에서 검색 이미지를 만들고 이름을 WinPEDiscover로 이름을 입력 합니다.
```
WDSUTIL /New-DiscoverImage /Image:WinPE boot image /Architecture:x86 /DestinationImage /FilePath:C:\Temp\WinPEDiscover.wim
```
부팅 이미지에서 검색 이미지를 만들고 지정 된 설정으로 WinPEDiscover 이름을 지정 하려면 다음을 입력 합니다.
```
WDSUTIL /Verbose /Progress /New-DiscoverImage /Server:MyWDSServer
/Image:WinPE boot image /Architecture:x64 /Filename:boot.wim /DestinationImage /FilePath:\\Server\Share\WinPEDiscover.wim
/Name:New WinPE image /Description:WinPE image for WDS Client discovery /Overwrite:No
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)