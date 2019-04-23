---
title: 새 DiscoverImage 명령을 사용 하 여
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ede9fbbb-0bba-4309-8c21-3cc13e1dc3cd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1212571fc07b912ab9fa3344b973ce5a25085d86
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835774"
---
# <a name="using-the-new-discoverimage-command"></a>새 DiscoverImage 명령을 사용 하 여



기존 부팅 이미지에서 새 검색 이미지를 만듭니다. 이미지는 Setup.exe 프로그램을 Windows 배포 서비스 모드에서 시작 하 고 다음 Windows 배포 서비스 서버를 검색 하도록 하는 부팅 이미지를 검색 합니다. 일반적으로 이러한 이미지를 PXE로 부팅할 수 없는 컴퓨터에 이미지 배포에 사용 됩니다. 자세한 내용은 참조 이미지 만들기 ([https://go.microsoft.com/fwlink/?LinkId=115311](https://go.microsoft.com/fwlink/?LinkId=115311)).

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

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|[/ 서버:\<서버 이름 >]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
|/ 이미지:\<이미지 이름 >|원본 부팅 이미지의 이름을 지정합니다.|
|/ 아키텍처: {x86 | ia64 | x64}|반환할 이미지의 아키텍처를 지정 합니다. 다른 아키텍처에서 다른 부팅 이미지에 대 한 동일한 이미지 이름을 가질 수 이기 때문에 아키텍처 값을 지정 하 WDSUTIL 올바른 이미지가 반환 하는 것을 확인 합니다.|
|[/ Filename:\<파일 이름 >]|이미지 이름으로 고유 하 게 식별할 수 없으면, 파일 이름을 지정 하려면이 옵션을 사용 해야 합니다.|
|/ DestinationImage|대상 이미지에 대 한 설정을 지정합니다. 다음 옵션을 사용 하 여 설정을 지정할 수 있습니다.</br>-/FilePath: < 파일 경로 및 이름 >-새 이미지에 대 한 전체 파일 경로 설정 합니다.</br>-[/Name:\<이름 >]-이미지의 표시 이름을 가져오거나 설정 합니다. 표시 이름이 없는 지정 하는 경우 원본 이미지의 표시 이름을 사용 됩니다.</br>-   [/Description: \<설명 >]-이미지의 설명을 설정 합니다.</br>-   [/WDSServer: \<서버 이름 >]-지정된 된 이미지에서 부팅 하는 모든 클라이언트는 설치 이미지를 다운로드 하려면에 게 문의 해야 하는 서버의 이름을 지정 합니다. 기본적으로이 이미지를 부팅 하는 모든 클라이언트가 올바른 Windows 배포 서비스 서버를 검색 합니다. 이 옵션을 사용 하 여 검색 기능을 무시 하 고 부팅된 클라이언트가 지정된 된 서버를 강제로 수행 합니다.</br>-[/Overwrite: {예 | 아니오 | 추가}]-파일에 지정 되었는지 여부를 결정 **/DestinationImage** 덮어써야 하면 해당 이름 가진 다른 파일의 /FilePath에 이미 있습니다. **예** 기존 파일을 덮어씁니다. **더** (기본값) 이면 오류가 동일한 이름 가진 다른 파일이 이미 있는 경우 발생 합니다. **추가** 기존.wim 파일 내에서 새 이미지로 생성 되는 이미지를 연결 합니다.|

## <a name="BKMK_examples"></a>예제

부팅 이미지에서 검색 이미지를 만들고 WinPEDiscover.wim 이름을 입력 합니다.
```
WDSUTIL /New-DiscoverImage /Image:"WinPE boot image" /Architecture:x86 /DestinationImage /FilePath:"C:\Temp\WinPEDiscover.wim"
```
부팅 이미지에서 검색 이미지를 만들고 지정 된 설정을 사용 하 여 WinPEDiscover.wim 이름을 하려면 다음을 입력 합니다.
```
WDSUTIL /Verbose /Progress /New-DiscoverImage /Server:MyWDSServer
/Image:"WinPE boot image" /Architecture:x64 /Filename:boot.wim /DestinationImage /FilePath:"\\Server\Share\WinPEDiscover.wim" 
/Name:"New WinPE image" /Description:"WinPE image for WDS Client discovery" /Overwrite:No
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)