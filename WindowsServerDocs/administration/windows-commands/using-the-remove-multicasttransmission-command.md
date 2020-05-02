---
title: MulticastTransmission
description: 이미지에 대 한 멀티 캐스트 전송을 사용 하지 않도록 설정 하는 MulticastTransmission에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9a7f5c31-bfbf-425d-9129-a6f9173fe83d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 41dea341216979d6ed7298f11c16458e4d3f2f50
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720345"
---
# <a name="using-the-remove-multicasttransmission-command"></a>제거 MulticastTransmission 명령을 사용 하 여

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이미지에 대 한 멀티 캐스트 전송 하는 사용 하지 않도록 설정 합니다. **/Force**를 지정 하지 않는 한 기존 클라이언트는 이미지 전송을 완료 하지만 새 클라이언트는 참가할 수 없습니다.

## <a name="syntax"></a>구문
**Windows Server 2008**
```
wdsutil /remove-MulticastTransmissiomedia:<Image name> [/Server:<Server name>mediatype:InstallmediaGroup:<Image Group>] [/Filename:<File name>] [/force]
```
부팅 이미지에 대 한 **Windows Server 2008 R2** :
```
wdsutil [Options] /remove-MulticastTransmissiomedia:<Image name>
\x20    [/Server:<Server name>]
\x20  mediatype:Boot
\x20    /Architecture:{x86 | ia64 | x64}
\x20    [/Filename:<File name>]
```
설치 이미지:
```
wdsutil [Options] /remove-MulticastTransmissiomedia:<Image name>
        [/Server:<Server name>]
      mediatype:Install
       mediaGroup:<Image Group
        [/Filename:<File name>]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
미디어만<Image name>|이미지의 이름을 지정합니다.|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름을 지정 하지, 로컬 서버가 사용 됩니다.|
미디어 미디어: {설치&#124;부팅}|이미지 유형을 지정합니다. 이 옵션을 설정 해야 하는 참고 **설치** Windows Server 2008 용입니다.|
|/ 아키텍처: {x86 &#124;ia64 &#124; x64}|전송이 시작 되도록 연관 된 부팅 이미지의 아키텍처를 지정 합니다. 다른 아키텍처에서 부팅 이미지에 동일한 이미지 이름을 가질 수 있기 때문에 올바른 전송이 사용 되도록 아키텍처를 지정 해야 합니다.|
|\mediaGroup:<Image group name>]|이미지가 포함 된 이미지 그룹을 지정 합니다. 이미지 그룹 이름을 지정 하지 않으면 하나의 이미지 그룹 서버에 존재 하는 경우에 해당 이미지 그룹이 사용 됩니다. 이미지 그룹 둘 이상의 서버에 있는 경우 이미지 그룹 이름을 지정 하려면이 옵션을 사용 해야 합니다.|
|[/ 파일 이름:<File name>]|파일 이름을 지정합니다. 원본 이미지 이름으로 고유 하 게 식별할 수 없으면, 파일 이름을 지정 하려면이 옵션을 사용 해야 합니다.|
|/force|전송을 제거 하 고 모든 클라이언트를 종료 합니다. **/Force** 옵션에 대 한 값을 지정 하지 않으면 기존 클라이언트는 이미지 전송을 완료할 수 있지만 새 클라이언트는 참가할 수 없습니다.|
## <a name="examples"></a>예
네임 스페이스를 중지 하려면 (현재 클라이언트는 전송을 완료 됩니다 있지만 새 클라이언트에 연결할 수 없습니다) 유형:
```
wdsutil /remove-MulticastTransmissiomedia:Vista with Office
/Imagetype:Install
```
```
wdsutil /remove-MulticastTransmissiomedia:x64 Boot Image
/Imagetype:Boot /Architecture:x64
```
모든 클라이언트의 종료를 강제 하려면 다음을 입력 합니다.
```
wdsutil /remove-MulticastTransmission /Server:MyWDSServer
/Image:Vista with Officemediatype:InstalmediaGroup:ImageGroup1
/Filename:install.wim /force
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)
[AllMulticastTransmissions 명령을](using-the-get-allmulticasttransmissions-command.md)
사용 하 여[MulticastTransmission 명령을](using-the-get-multicasttransmission-command.md)
사용 하 여[MulticastTransmission 명령](using-the-new-multicasttransmission-command.md)
[하위 명령: MulticastTransmission](subcommand-start-multicasttransmission.md)
