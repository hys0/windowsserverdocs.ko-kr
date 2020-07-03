---
title: MulticastTransmission
description: 이미지에 대 한 새 멀티 캐스트 전송을 만드는 MulticastTransmission에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c1f1dc46-dd50-4eb9-9f72-cf0e5d71bd3d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c3d9c2b507243b9a024728e99885c7a429b34178
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932449"
---
# <a name="new-multicasttransmission"></a>MulticastTransmission

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이미지에 대 한 새 멀티 캐스트 전송을 만듭니다. 이 명령은 Windows 배포 서비스 mmc 스냅인을 사용 하 여 전송을 만드는 것과 같습니다 ( **멀티 캐스트** 전송 노드를 마우스 오른쪽 단추로 클릭 한 다음 **멀티 캐스트 전송 만들기**클릭). 배포 서버 역할 서비스와 전송 서버 역할 서비스 (기본 설치)가 모두 설치 되어 있는 경우이 명령을 사용 해야 합니다. 전송 서버 역할 서비스만 설치한 경우에는 [새 네임 스페이스 명령을 사용 하 여](using-the-new-namespace-command.md)를 사용 합니다.
## <a name="syntax"></a>구문
설치 이미지 전송의 경우:
```
wdsutil [Options] /New-MulticastTransmissiomedia:<Image name>
        [/Server:<Server name>]
        /FriendlyName:<Friendly name>
        [/Description:<Description>]
        /Transmissiontype: {AutoCast | ScheduledCast}
            [/time:<YYYY/MM/DD:hh:mm>]
            [/Clients:<Num of Clients>]
      mediatype:Install
       mediaGroup:<Image Group>]
        [/Filename:<File name>]
```
부팅 이미지 전송의 경우 (Windows Server 2008 r 2에만 지원 됨):
```
wdsutil [Options] /New-MulticastTransmissiomedia:<Image name>
        [/Server:<Server name>]
        /FriendlyName:<Friendly name>
        [/Description:<Description>]
        /Transmissiontype: {AutoCast | ScheduledCast}
            [/time:<YYYY/MM/DD:hh:mm>]
            [/Clients:<Num of Clients>]
      mediatype:Boot
        /Architecture:{x86 | ia64 | x64}
        [/Filename:<File name>]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
미디어만<Image name>|멀티 캐스팅을 사용 하 여 전송할 이미지의 이름을 지정 합니다.|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
|#B1<Friendly name>|전송의 이름을 지정 합니다.|
|/Description<Description>]|전송에 대 한 설명을 지정 합니다.|
mediatype: {부팅&#124;설치}|멀티 캐스팅을 사용 하 여 전송할 이미지 유형을 지정 합니다. 참고 **부팅** 은 Windows Server 2008 r 2에만 지원 됩니다.|
|\mediaGroup:<Image group name>]|이미지가 포함 된 이미지 그룹을 지정 합니다. 이미지 그룹 이름을 지정 하지 않으면 하나의 이미지 그룹 서버에 존재 하는 경우에 해당 이미지 그룹이 사용 됩니다. 이미지 그룹 둘 이상의 서버에 있는 경우 이미지 그룹 이름을 지정 하려면이 옵션을 사용 해야 합니다.|
|[/ 파일 이름:<File name>]|파일 이름을 지정합니다. 원본 이미지 이름으로 고유 하 게 식별할 수 없으면, 파일 이름을 지정 하려면이 옵션을 사용 해야 합니다.|
|/ Transmissiontype: {AutoCast &#124;; 예약 된 캐스트}|전송을 자동으로 시작할지 (AutoCast) 아니면 지정 된 시작 조건 (ScheduledCast)을 기준으로 시작할지를 지정 합니다.<p><ul><li>**자동 캐스트**. 이 전송 유형은 해당 클라이언트가 설치 이미지를 요청 하는 즉시 선택한 이미지의 멀티 캐스트 전송이 시작 됨을 나타냅니다. 다른 클라이언트가 동일한 이미지를 요청 하면 이미 시작 된 전송에 조인 됩니다.</li><li>**예약 된 캐스트**입니다. 이 전송 유형은 이미지를 요청 하는 클라이언트 수 및/또는 특정 날짜와 시간을 기준으로 전송에 대 한 시작 조건을 설정 합니다. 다음 옵션을 지정할 수 있습니다.<p><ul><li>[/시간: <time> ] -YYYY/MM/DD: hh: MM 형식을 사용 하 여 전송이 시작 되어야 하는 시간을 설정 합니다.</li><li>[/클라이언트: <Number of clients> ] -전송이 시작 되기 전에 대기 하는 최소 클라이언트 수를 설정 합니다.</li></ul></li></ul>|
|/ 아키텍처: {x86 &#124;ia64 &#124; x64}|멀티 캐스팅을 사용 하 여 전송할 부팅 이미지의 아키텍처를 지정 합니다. 서로 다른 아키텍처의 부팅 이미지에 동일한 이름을 사용할 수 있기 때문에 올바른 이미지를 사용 하도록 아키텍처를 지정 해야 합니다.|
|[/ 파일 이름:<File name>]|파일 이름을 지정합니다. 원본 이미지 이름으로 고유 하 게 식별할 수 없으면, 파일 이름을 지정 해야 합니다.|
## <a name="examples"></a>예
Windows Server 2008 r 2에서 부팅 이미지의 자동 캐스트 전송을 만들려면 다음을 입력 합니다.
```
wdsutil /New-MulticastTransmission /FriendlyName:WDS Boot Transmission
/Image:X64 Boot Imagemediatype:Boot /Architecture:x64 /Transmissiontype:AutoCast
```
설치 이미지의 자동 캐스트 전송을 만들려면 다음을 입력 합니다.
```
wdsutil /New-MulticastTransmission /FriendlyName:WDS AutoCast Transmission
/Image:Vista with Officemediatype:Install /Transmissiontype:AutoCast
```
설치 이미지의 예약 된 캐스트 전송을 만들려면 다음을 입력 합니다.
```
wdsutil /New-MulticastTransmission /FriendlyName:WDS SchedCast Transmission /Server:MyWDSServemedia:Vista with Officemediatype:Install
/Transmissiontype:ScheduledCast /time:2006/11/20:17:00 /Clients:100
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md) 
 [AllMulticastTransmissions 명령 사용](using-the-get-allmulticasttransmissions-command.md) 
 [MulticastTransmission 명령 사용](using-the-get-multicasttransmission-command.md) 
 [MulticastTransmission 명령 사용](using-the-remove-multicasttransmission-command.md) 
 [하위 명령: MulticastTransmission](subcommand-start-multicasttransmission.md)
