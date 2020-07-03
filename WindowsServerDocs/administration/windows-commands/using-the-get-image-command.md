---
title: 가져오기-이미지
description: 이미지에 대 한 정보를 검색 하는 get 이미지에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0ecaa999-72ad-4191-adb5-a418de42a001
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d37989fa681e5694b0c15b77aa1baddcfebbeecf
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932236"
---
# <a name="get-image"></a>가져오기-이미지

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이미지에 대 한 정보를 검색합니다.

## <a name="syntax"></a>구문
부팅 이미지의 경우:
```
wdsutil [Options] /Get-Imagmedia:<Image name> [/Server:<Server name>mediatype:Boot /Architecture:{x86 | ia64 | x64} [/Filename:<File name>]
```
설치 이미지:
```
wdsutil [Options] /Get-Imagmedia:<Image name> [/Server:<Server name>mediatype:InstallmediaGroup:<Image group name>] [/Filename:<File name>]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
미디어만<Image name>|이미지의 이름을 지정합니다.|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
미디어 미디어: {Boot &#124; 설치}|이미지의 유형을 지정합니다.|
|/ 아키텍처: {x86 &#124;ia64 &#124; x64}|이미지의 아키텍처를 지정합니다. 다른 아키텍처에서 부팅 이미지에 동일한 이미지 이름을 가질 수 있기 때문에 아키텍처 값을 지정 하 하면 올바른 이미지가 반환 됩니다.|
|[/ 파일 이름:<File name>]|이미지를 이름으로 고유 하 게 식별할 수 없는 경우에는이 옵션을 사용 하 여 파일 이름을 지정 해야 합니다.|
|\mediaGroup:<Image group name>]|이미지가 포함 된 이미지 그룹을 지정 합니다. 지정 된 이미지 그룹이 없고 하나의 이미지 그룹 서버에 존재 하는 경우 해당 그룹 사용 됩니다. 이미지 그룹 둘 이상의 서버에 있는 경우에 이미지 그룹을 지정 하려면이 매개 변수를 사용 해야 합니다.|
## <a name="examples"></a>예
부팅 이미지에 대 한 정보를 검색 하려면 다음 중 하나를 입력 합니다.
```
wdsutil /Get-Imagmedia:WinPE boot imagemediatype:Boot /Architecture:x86
wdsutil /verbose /Get-Imagmedia:WinPE boot image /Server:MyWDSServemediatype:Boot /Architecture:x86 /Filename:boot.wim
```
설치 이미지에 대 한 정보를 검색 하려면 다음 중 하나를 입력 합니다.
```
wdsutil /Get-Imagmedia:Windows Vista with Officemediatype:Install
wdsutil /verbose /Get-Imagmedia:Windows Vista with Office /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 /Filename:install.wim
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md) 
 [추가 이미지 명령을](using-the-add-image-command.md) 
 사용 하 여 [복사 이미지 명령을](using-the-copy-image-command.md) 
 사용 하 여 [내보내기 이미지 명령 사용](using-the-export-image-command.md) 
 [제거 이미지 명령을](using-the-remove-image-command.md) 
 사용 하 여 [Replace 이미지 명령을](using-the-replace-image-command.md) 
 사용 하 여 [하위 명령: 설정 이미지](subcommand-set-image.md)
