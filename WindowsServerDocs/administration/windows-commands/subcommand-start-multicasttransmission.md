---
title: 하위 명령 시작-MulticastTransmission
description: 이미지의 예약 된 캐스트 전송을 시작 하는 하위 명령 MulticastTransmission에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a1b2d459-1ece-49d4-997c-9d206c463b61
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: adb09457e2bf26242da9f6d31ee5e71882d7c10a
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936967"
---
# <a name="subcommand-start-multicasttransmission"></a>시작-MulticastTransmission 하위 명령:

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이미지의 예약 된 캐스트 전송을 시작합니다.

## <a name="syntax"></a>구문
**Windows Server 2008**
```
wdsutil /start-MulticastTransmissiomedia:<Image name> [/Server:<Server namemediatype:InstallmediaGroup:<Image group name>] [/Filename:<File name>]
```
부팅 이미지에 대 한 **Windows Server 2008 R2** :
```
wdsutil [Options] /start-MulticastTransmissiomedia:<Image name>
        [/Server:<Server name>]
      mediatype:Boot
        /Architecture:{x86 | ia64 | x64}
        [/Filename:<File name>]
```
설치 이미지:
```
wdsutil [Options] /start-MulticastTransmissiomedia:<Image name>
        [/Server:<Server name>]
      mediatype:Install
       mediaGroup:<Image Group>]
        [/Filename:<File name>]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
미디어만<Image name>|이미지의 이름을 지정합니다.|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
미디어 미디어: {설치&#124;부팅}|이미지 유형을 지정합니다. 이 옵션을 설정 해야 하는 참고 **설치** Windows Server 2008 용입니다.|
|/ 아키텍처: {x86 &#124;ia64 &#124; x64}|연결 된 전송 시작 하는 부팅 이미지의 아키텍처입니다. 다른 아키텍처에서 부팅 이미지에 동일한 이미지 이름을 가질 수 있기 때문 올바른 전송이 사용 되도록 아키텍처를 지정 해야 합니다.|
|\mediaGroup:<Image group name>]|이미지의 이미지 그룹을 지정합니다. 이미지 그룹 이름을 지정 하지 않으면 하나의 이미지 그룹 서버에 존재 하는 경우 해당 이미지 그룹 사용 됩니다. 이미지 그룹 둘 이상의 서버에 있는 경우 이미지 그룹 이름을 지정 하려면이 옵션을 사용 해야 합니다.|
|[/ 파일 이름:<File name>]|이미지를 포함 하는 파일의 이름을 지정 합니다. 이미지 이름으로 고유 하 게 식별할 수 없으면, 파일 이름을 지정 하려면이 옵션을 사용 해야 합니다.|
## <a name="examples"></a>예
멀티 캐스트 전송을 시작 하려면 다음 중 하나를 입력 합니다.
```
wdsutil /start-MulticastTransmissiomedia:Vista with Office
/Imagetype:Install
wdsutil /start-MulticastTransmission /Server:MyWDSServemedia:Vista with Officemediatype:InstalmediaGroup:ImageGroup1 /Filename:install.wim
```
부팅을 시작 하려면 Windows Server 2008 R2, 형식에 대 한 멀티 캐스트 전송을 이미지:
```
wdsutil /start-MulticastTransmission /Server:MyWDSServemedia:X64 Boot Imagemediatype:Boot /Architecture:x64
/Filename:boot.wim\n\
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md) 
 [AllMulticastTransmissions 명령 사용](using-the-get-allmulticasttransmissions-command.md) 
 [MulticastTransmission 명령 사용](using-the-get-multicasttransmission-command.md) 
 [MulticastTransmission 명령 사용](using-the-new-multicasttransmission-command.md) 
 [MulticastTransmission 명령 사용](using-the-remove-multicasttransmission-command.md)
