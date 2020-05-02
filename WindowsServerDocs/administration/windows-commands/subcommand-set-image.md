---
title: 하위 명령 집합 이미지
description: 이미지의 특성을 변경 하는 하위 명령 집합 이미지에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2ae03c86-7a13-4e38-9182-32e55fffd504
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e24b20093a726e7553474871ef25e6877223e21f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721708"
---
# <a name="subcommand-set-image"></a>하위 명령: 설정 이미지

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이미지의 특성을 변경 합니다.

## <a name="syntax"></a>구문
부팅 이미지의 경우:
```
wdsutil /Set-Imagmedia:<Image name> [/Server:<Server name>mediatype:Boot /Architecture:{x86 | ia64 | x64} [/Filename:<File name>] [/Name:<Name>] 
[/Description:<Description>] [/Enabled:{Yes | No}]
```
설치 이미지:
```
wdsutil /Set-Imagmedia:<Image name> [/Server:<Server name>]
   mediatype:InstallmediaGroup:<Image group name>]
     [/Filename:<File name>]
     [/Name:<Name>]
     [/Description:<Description>]
     [/UserFilter:<SDDL>]
     [/Enabled:{Yes | No}]
     [/UnattendFile:<Unattend file path>]
         [/OverwriteUnattend:{Yes | No}]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
미디어만<Image name>|이미지의 이름을 지정합니다.|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
미디어 미디어: {Boot &#124; 설치}|이미지의 유형을 지정합니다.|
|/ 아키텍처: {x86 &#124;ia64 &#124; x64}|이미지의 아키텍처를 지정합니다. 다른 부팅 이미지에 대 한 같은 이미지 이름에 다른 아키텍처를 가질 수 있으므로 올바른 이미지가 수정 되 하면 아키텍처를 지정 합니다.|
|[/ 파일 이름:<File name>]|이미지를 이름으로 고유 하 게 식별할 수 없는 경우에는이 옵션을 사용 하 여 파일 이름을 지정 해야 합니다.|
|[/ 이름]|이미지의 이름을 지정합니다.|
|/Description<Description>]|이미지에 대 한 설명을 설정합니다.|
|[/ 활성화: {예 & #124; No}]|이미지를 사용 하지 않도록 설정 하거나 사용 합니다.|
|\mediaGroup:<Image group name>]|이미지가 포함 된 이미지 그룹을 지정 합니다. 이미지 그룹 이름을 지정 하지 않으면 하나의 이미지 그룹 서버에 존재 하는 경우 해당 이미지 그룹 사용 됩니다. 이미지 그룹 둘 이상의 서버에 있는 경우에 이미지 그룹을 지정 하려면이 옵션을 사용 해야 합니다.|
|[/ UserFilter:<SDDL>]|이미지에 사용자 필터를 설정합니다. 필터 문자열 설명자 정의 SDDL (Security Language) 형식 이어야 합니다. 이때 달리는 **/Security** 옵션 이미지 그룹의 경우이 옵션만 제한 된 이미지 정 및 실제 이미지 파일 리소스를 볼 수 있는 사람입니다. 파일 리소스에 대 한 액세스를 제한 하 고 따라서 이미지 그룹 내의 모든 이미지에 대 한 액세스를 이미지 그룹 자체에 대 한 보안을 설정 해야 합니다.|
|[/ UnattendFile:<Unattend file path>]|이미지와 연결 되도록 무인 파일의 전체 경로 설정 합니다. 예를 들어: **D:\Files\Unattend\Img1Unattend.xml**|
|[/ OverwriteUnattend: {예 & #124; No}]|지정할 수 있습니다 **/overwrite** 이미지에 연결 된 무인 파일 이미 있으면 무인 파일을 덮어쓸 수 있습니다. 기본값은 **No**합니다.|
## <a name="examples"></a>예
부팅 이미지에 대 한 값을 설정 하려면 다음 중 하나를 입력 합니다.
```
wdsutil /Set-Imagmedia:WinPE boot imagemediatype:Boot /Architecture:x86 /Description:New description
wdsutil /verbose /Set-Imagmedia:WinPE boot image /Server:MyWDSServemediatype:Boot /Architecture:x86 /Filename:boot.wim 
/Name:New Name /Description:New Description /Enabled:Yes
```
설치 이미지에 대 한 값을 설정 하려면 다음 중 하나를 입력 합니다.
```
wdsutil /Set-Imagmedia:Windows Vista with Officemediatype:Install /Description:New description 
wdsutil /verbose /Set-Imagmedia:Windows Vista with Office /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 
/Filename:install.wim /Name:New name /Description:New description /UserFilter:O:BAG:DUD:AI(A;ID;FA;;;SY)(A;ID;FA;;;BA)(A;ID;0x1200a9;;;AU) /Enabled:Yes /UnattendFile:\\server\share\unattend.xml /OverwriteUnattend:Yes
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)
[추가 이미지](using-the-add-image-command.md)
명령을 사용 하 여 복사 이미지 명령을 사용 하 여[복사](using-the-copy-image-command.md)
[Using the Export-Image Command](using-the-export-image-command.md)
이미지 명령을 사용 하 여[get](using-the-get-image-command.md)
이미지 명령을 사용 하 여[제거](using-the-remove-image-command.md)
이미지 명령을 사용 하 여 바꾸기 이미지 명령을 사용 하 여[바꾸기](using-the-replace-image-command.md) 이미지 명령을 사용 하 여
