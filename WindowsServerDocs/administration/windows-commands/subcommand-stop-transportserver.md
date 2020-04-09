---
title: 하위 명령 중지-서버
description: Stop-서버에 대 한 Windows 명령 항목
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: dc1b1eec-6893-445e-81dc-16b3fae287fa
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 44d62332307ffda4dcfa6af286c7b95cb12423dc
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80833706"
---
# <a name="subcommand-stop-transportserver"></a>중지-TransportServer 하위 명령:

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

전송 서버에서 모든 서비스를 중지합니다.
## <a name="syntax"></a>구문
```
wdsutil [Options] /Stop-TransportServer [/Server:<Server name>]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|[/ 서버:<Server name>]|전송 서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 없는 전송 서버를 지정 하는 경우 로컬 서버 사용 됩니다.|
## <a name="examples"></a><a name="BKMK_examples"></a>예와
서비스를 중지 하려면 다음 중 하나를 입력 합니다.
```
wdsutil /Stop-TransportServer
wdsutil /verbose /Stop-TransportServer /Server:MyWDSServer
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)
[TransportServer 사용 안 함 명령을 사용 하 여](using-the-disable-transportserver-command.md)
[사용 TransportServer 명령을 사용 하 여](using-the-enable-transportserver-command.md)
[get TransportServer 명령을 사용 하 여](using-the-get-transportserver-command.md)
[하위 명령: 집합 TransportServer](subcommand-set-transportserver.md)
[하위 명령: TransportServer 시작](subcommand-start-transportserver.md)
