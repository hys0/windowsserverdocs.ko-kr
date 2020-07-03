---
title: CaptureImage
description: 기존 부팅 이미지에서 새 캡처 이미지를 만드는 CaptureImage에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2dfd08f0-be59-4715-96e6-c498305873f4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ec9da39ccef5efcea1792556ef8335bbf63c5fd6
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932152"
---
# <a name="new-captureimage"></a>CaptureImage

기존 부팅 이미지에서 새 캡처 이미지를 만듭니다. 캡처 이미지는 설치 프로그램을 시작 하는 대신 Windows 배포 서비스 캡처 유틸리티를 시작 하는 부팅 이미지입니다. Sysprep로 준비 된 참조 컴퓨터를 캡처 이미지로 부팅 하면 마법사에서 참조 컴퓨터의 설치 이미지를 만들어 Windows 이미지 (.wim) 파일로 저장 합니다. 미디어 (예: CD, DVD 또는 USB 드라이브)에 이미지를 추가한 다음 해당 미디어에서 컴퓨터를 부팅할 수도 있습니다. 설치 이미지를 만든 후 PXE 부팅 배포를 위해 서버에 이미지를 추가할 수 있습니다. 자세한 내용은 이미지 만들기 ()를 참조 하십시오 [https://go.microsoft.com/fwlink/?LinkId=115311](https://go.microsoft.com/fwlink/?LinkId=115311) .

## <a name="syntax"></a>구문

```
WDSUTIL [Options] /New-CaptureImage [/Server:<Server name>]
     /Image:<Image name>
     /Architecture:{x86 | ia64 | x64}
     [/Filename:<File name>]
     /DestinationImage
        /FilePath:<File path and name>
        [/Name:<Name>]
        [/Description:<Description>]
        [/Overwrite:{Yes | No | Append}]
        [/UnattendFilePath:<File path>]
```

### <a name="parameters"></a>매개 변수

|        매개 변수         |                                                                                                                                                                                                                         설명                                                                                                                                                                                                                          |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/ 서버:\<Server name>] |                                                                                                                                       서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.                                                                                                                                        |
|   이미지로\<Image name>   |                                                                                                                                                                                                         원본 부팅 이미지의 이름을 지정 합니다.                                                                                                                                                                                                         |
|   /아키텍처: {x86    |                                                                                                                                                                                                                             ia64                                                                                                                                                                                                                             |
| [/파일 이름: \<Filename> ] |                                                                                                                                                                            이미지 이름으로 고유 하 게 식별할 수 없으면, 파일 이름을 지정 하려면이 옵션을 사용 해야 합니다.                                                                                                                                                                            |
|    / DestinationImage     | 대상 이미지에 대 한 설정을 지정합니다. 다음 옵션을 사용 하 여 설정을 지정할 수 있습니다.</br>-/Sfilefiles: \<File path and name> 새 캡처 이미지의 전체 파일 경로를 설정 합니다.</br>-[/Name: \<Name> ]-이미지의 표시 이름을 설정 합니다. 표시 이름을 지정 하지 않으면 원본 이미지의 표시 이름이 사용 됩니다.</br>-[/ 설명: \<Description>]-이미지의 설명을 설정 합니다.</br>-[/Overwrite: {예 |

## <a name="examples"></a>예

캡처 이미지를 만들고 이름을 WinPECapture로 이름을 입력 하려면 다음을 입력 합니다.
```
WDSUTIL /New-CaptureImage /Image:WinPE boot image /Architecture:x86 /DestinationImage /FilePath:C:\Temp\WinPECapture.wim
```
캡처 이미지를 만들고 지정 된 설정을 적용 하려면 다음을 입력 합니다.
```
WDSUTIL /Verbose /Progress /New-CaptureImage /Server:MyWDSServer /Image:WinPE boot image /Architecture:x64 /Filename:boot.wim
/DestinationImage /FilePath:\\Server\Share\WinPECapture.wim /Name:New WinPE image /Description:WinPE image with capture utility /Overwrite:No /UnattendFilePath:\\Server\Share\WDSCapture.inf
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)