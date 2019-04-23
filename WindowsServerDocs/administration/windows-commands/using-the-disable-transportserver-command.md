---
title: 사용 안 함 TransportServer 명령을 사용 하 여
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a009706b-8e89-486b-8e3d-512cd9f4de74
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d653aacf225333ac8a8b090ef53fb6826e84ab5c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59836984"
---
# <a name="using-the-disable-transportserver-command"></a>사용 안 함 TransportServer 명령을 사용 하 여

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

전송 서버에 대 한 모든 서비스를 사용 하지 않도록 설정 합니다.
## <a name="syntax"></a>구문
```
wdsutil [Options] /Disable-TransportServer [/Server:<Server name>]
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|[/ 서버:<Server name>]|사용 하지 않도록 설정할 전송 서버의 이름을 지정 합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 전송 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
## <a name="BKMK_examples"></a>예제
서버를 사용 하지 않으려면 다음을 입력 합니다.
```
wdsutil /Disable-TransportServer
wdsutil /verbose /Disable-TransportServer /Server:MyWDSServer
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[사용 TransportServer 명령을 사용 하 여](using-the-enable-transportserver-command.md)
[get TransportServer 명령을 사용 하 여](using-the-get-transportserver-command.md)
[하위 명령: 집합 TransportServer](subcommand-set-transportserver.md)
[하위 명령: 시작 TransportServer](subcommand-start-transportserver.md)
[하위 명령: TransportServer 중지](subcommand-stop-transportserver.md)
