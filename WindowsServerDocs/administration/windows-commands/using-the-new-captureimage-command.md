---
title: 새 CaptureImage 명령을 사용 하 여
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2dfd08f0-be59-4715-96e6-c498305873f4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7d9f402acb9904624bdb4193a4306d57b104eda8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888614"
---
# <a name="using-the-new-captureimage-command"></a>새 CaptureImage 명령을 사용 하 여



기존 부팅 이미지에서 새 캡처 이미지를 만듭니다. 캡처 이미지는 Windows 배포 서비스를 시작 하는 부팅 이미지 캡처 설치를 시작 하는 대신 유틸리티입니다. (Sysprep로 준비 된)는 참조 컴퓨터 캡처 이미지를 부팅 하면 마법사는 참조 컴퓨터의 설치 이미지를 만들고 Windows 이미지 (.wim) 파일로 저장 합니다. 미디어 (예: CD, DVD 또는 USB 드라이브), 이미지를 추가할 수도 수 있으며 그런 다음 해당 미디어에서 컴퓨터를 부팅할 수 있습니다. 설치 이미지를 만든 후에 PXE 부팅 배포에 대 한 서버에 이미지를 추가할 수 있습니다. 자세한 내용은 참조 이미지 만들기 ([https://go.microsoft.com/fwlink/?LinkId=115311](https://go.microsoft.com/fwlink/?LinkId=115311)).

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

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|[/ 서버:\<서버 이름 >]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
|/ 이미지:\<이미지 이름 >|원본 부팅 이미지의 이름을 지정합니다.|
|/ 아키텍처: {x 86 | ia64 | x64}|사용할 이미지의 아키텍처를 지정 합니다. 다른 아키텍처에서 다른 부팅 이미지에 대 한 동일한 이미지 이름을 가질 수 있으므로 이렇게 하면 올바른 이미지가 지정 됩니다.|
|[/Filename: \<파일 이름 >]|이미지 이름으로 고유 하 게 식별할 수 없으면, 파일 이름을 지정 하려면이 옵션을 사용 해야 합니다.|
|/ DestinationImage|대상 이미지에 대 한 설정을 지정합니다. 다음 옵션을 사용 하 여 설정을 지정할 수 있습니다.</br>-   /FilePath: \<파일 경로 및 이름 > 새 캡처 이미지에 대 한 전체 파일 경로 설정 합니다.</br>-   [/Name: \<이름 >]-이미지의 표시 이름을 가져오거나 설정 합니다. 표시 이름이 없는 지정 하는 경우 원본 이미지의 표시 이름을 사용 됩니다.</br>-   [/Description: \<설명 >]-이미지의 설명을 설정 합니다.</br>-[/Overwrite: {예 | 아니오 | 추가}]-파일에 지정 되었는지 여부를 결정 **/DestinationImage** 덮어써야 하면 해당 이름 가진 다른 파일의 /FilePath에 이미 있습니다. **예** 기존 파일을 덮어씁니다. **더** (기본값) 이면 오류가 동일한 이름 가진 다른 파일이 이미 있는 경우 발생 합니다. **추가** 기존.wim 파일 내에서 새 이미지로 생성 되는 이미지를 연결 합니다.</br>-   [/UnattendFilePath: \<파일 경로 >]-무인된 이미지 캡처 파일 이름과 전체 경로 설정 합니다.|

## <a name="BKMK_examples"></a>예제

캡처 이미지를 만들고 WinPECapture.wim 이름을 입력 합니다.
```
WDSUTIL /New-CaptureImage /Image:"WinPE boot image" /Architecture:x86 /DestinationImage /FilePath:"C:\Temp\WinPECapture.wim"

```
캡처 이미지를 만들고 지정된 된 설정을 적용 하려면 다음을 입력 합니다.
```
WDSUTIL /Verbose /Progress /New-CaptureImage /Server:MyWDSServer /Image:"WinPE boot image" /Architecture:x64 /Filename:boot.wim 
/DestinationImage /FilePath:"\\Server\Share\WinPECapture.wim" /Name:"New WinPE image" /Description:"WinPE image with capture utility" /Overwrite:No /UnattendFilePath:"\\Server\Share\WDSCapture.inf"
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)