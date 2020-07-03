---
title: MulticastTransmission
description: 지정 된 이미지에 대 한 멀티 캐스트 전송에 대 한 정보를 표시 하는 MulticastTransmission에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b733737b-1e81-43d4-a058-d6985a613bef
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a764aa0a975fe29daed54e50b7ab0284a12a399f
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932204"
---
# <a name="get-multicasttransmission"></a>MulticastTransmission

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정된 된 이미지에 대 한 멀티 캐스트 전송에 대 한 정보를 표시합니다.

## <a name="syntax"></a>구문
**Windows Server 2008**
```
wdsutil [Options] /Get-MulticastTransmissiomedia:<Image name> [/Server:<Server name>mediatype:InstallmediaGroup:<Image group name>]
[/Filename:<File name>] [/Show:Clients]
```
부팅 이미지 전송용 **Windows Server 2008 R2** :
```
wdsutil [Options] /Get-MulticastTransmissiomedia:<Image name>
    [/Server:<Server name>]
    [/details:Clients]
  mediatype:Boot
    /Architecture:{x86 | ia64 | x64}
        [/Filename:<File name>]
```
설치 이미지 전송의 경우:
```
wdsutil [Options] /Get-MulticastTransmissiomedia:<Image name>
         [/Server:<Server name>]
         [/details:Clients]
       mediatype:Install
    mediaGroup:<Image Group>]
     [/Filename:<File name>]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
미디어만<Image name>|이 이미지와 연결 된 멀티 캐스트 전송을 표시 합니다.|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름을 지정 하지, 로컬 서버가 사용 됩니다.|
미디어 미디어: 설치|이미지 유형을 지정합니다. 이 옵션을 설정 해야 하는 참고 **설치**합니다.|
|\mediaGroup:<Image group name>]|이미지가 포함 된 이미지 그룹을 지정 합니다. 이미지 그룹 이름을 지정 하지 않으면 하나의 이미지 그룹 서버에 존재 하는 경우에 해당 이미지 그룹이 사용 됩니다. 이미지 그룹 둘 이상의 서버에 있는 경우에 이미지 그룹을 지정 하려면이 옵션을 사용 해야 합니다.|
|/ 아키텍처: {x86 &#124;ia64 &#124; x64}|연결에서 전송 된 부팅 이미지의 아키텍처를 지정 합니다. 다른 아키텍처에서 부팅 이미지에 동일한 이미지 이름을 가질 수 있기 때문에 올바른 이미지를 사용 해야 하는 아키텍처를 지정 해야 합니다.|
|[/ 파일 이름:<File name>]|이미지를 포함 하는 파일을 지정 합니다. 이미지 이름으로 고유 하 게 식별할 수 없으면, 파일 이름을 지정 하려면이 옵션을 사용 해야 합니다.|
|[/ 쇼: 클라이언트]<p>또는<p>[/세부 정보: 클라이언트]|멀티 캐스트 전송에 연결 된 클라이언트 컴퓨터에 대 한 정보를 표시 합니다.|
## <a name="examples"></a>예
**Windows Server 2008** Office를 사용 하 여 Vista 라는 이미지의 전송에 대 한 정보를 보려면 다음 중 하나를 입력 합니다.
```
wdsutil /Get-MulticastTransmissiomedia:Vista with Officemediatype:Install
wdsutil /Get-MulticastTransmission /Server:MyWDSServemedia:Vista with Officemediatype:InstalmediaGroup:ImageGroup1 /Filename:install.wim /Show:Clients
```
**Windows Server 2008 R2** Office를 사용 하 여 Vista 라는 이미지의 전송에 대 한 정보를 보려면 다음 중 하나를 입력 합니다.
```
wdsutil /Get-MulticastTransmissiomedia:Vista with Office
 /Imagetype:Install
```
```
wdsutil /Get-MulticastTransmission /Server:MyWDSServemedia:Vista with Officemediatype:InstalmediaGroup:ImageGroup1 /Filename:install.wim /details:Clients
```
```
wdsutil /Get-MulticastTransmission /Server:MyWDSServemedia:X64 Boot Imagemediatype:Boot /Architecture:x64 /Filename:boot.wim /details:Clients
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md) 
 [AllMulticastTransmissions 명령 사용](using-the-get-allmulticasttransmissions-command.md) 
 [MulticastTransmission 명령 사용](using-the-new-multicasttransmission-command.md) 
 [MulticastTransmission 명령 사용](using-the-remove-multicasttransmission-command.md) 
 [하위 명령: MulticastTransmission](subcommand-start-multicasttransmission.md)
