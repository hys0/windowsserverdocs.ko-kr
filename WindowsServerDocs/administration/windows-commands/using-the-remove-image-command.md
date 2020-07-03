---
title: 제거-이미지
description: 서버에서 이미지를 삭제 하는 이미지 제거에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ce5e2384-2264-4b22-92af-74eec8c10ae0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: badcb079b12cf4357cba85d5711cfc5b6a50a2a4
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931239"
---
# <a name="remove-image"></a>제거-이미지

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

서버에서 이미지를 삭제합니다.

## <a name="syntax"></a>구문
부팅 이미지의 경우:
```
wdsutil [Options] /remove-Imagmedia:<Image name> [/Server:<Server name>mediatype:Boot /Architecture:{x86 | ia64 | x64} [/Filename:<Filename>]
```
설치 이미지:
```
wdsutil [Options] /remove-Imagmedia:<Image name> [/Server:<Server name>mediatype:InstallmediaGroup:<Image group name>] [/Filename:<Filename>]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
미디어만<Image name>|이미지의 이름을 지정합니다.|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
미디어 미디어: {Boot &#124; 설치}|이미지의 유형을 지정합니다.|
|/ 아키텍처: {x86 &#124;ia64 &#124; x64}|이미지의 아키텍처를 지정합니다. 다른 아키텍처에서 다른 부팅 이미지에 대 한 동일한 이미지 이름을 가질 수 있기 때문에 아키텍처 값을 지정 하는 올바른 이미지를 제거할 것을 확인 합니다.|
|\mediaGroup:<Image group name>]|이미지가 포함 된 이미지 그룹을 지정 합니다. 이미지 그룹 이름을 지정 하지 않으면 하나의 이미지 그룹 서버에 존재 하는 경우 해당 이미지 그룹 사용 됩니다. 이미지 그룹을 여러 개 있는 경우에 이미지 그룹을 지정 하려면이 옵션을 사용 해야 합니다.|
|[/ 파일 이름:<File name>]|이미지를 이름으로 고유 하 게 식별할 수 없는 경우에는이 옵션을 사용 하 여 파일 이름을 지정 해야 합니다.|
## <a name="examples"></a>예
부팅 이미지를 제거 하려면 다음을 입력 합니다.
```
wdsutil /remove-Imagmedia:WinPE Boot Imagemediatype:Boot /Architecture:x86
```
```
wdsutil /verbose /remove-Imagmedia:WinPE Boot Image /Server:MyWDSServemediatype:Boot /Architecture:x64 /Filename:boot.wim
```
설치 이미지를 제거 하려면 다음을 입력 합니다.
```
wdsutil /remove-Imagmedia:Windows Vista with Officemediatype:Install
```
```
wdsutil /verbose /remove-Imagmedia:Windows Vista with Office /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 /Filename:install.wim
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md) 
 [추가 이미지 명령을](using-the-add-image-command.md) 
 사용 하 여 [복사 이미지 명령을](using-the-copy-image-command.md) 
 사용 하 여 [내보내기 이미지 명령 사용](using-the-export-image-command.md) 
 [Get 이미지 명령을](using-the-get-image-command.md) 
 사용 하 여 [Replace 이미지 명령을](using-the-replace-image-command.md) 
 사용 하 여 [하위 명령: 설정 이미지](subcommand-set-image.md)
