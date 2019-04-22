---
title: Get TransportServer 명령을 사용 하 여
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: de634123-0179-41b2-9c6f-726508130ff5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 08aa1273d09ba92de15e13f7bfcc8283ac2fedb6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817424"
---
# <a name="using-the-get-transportserver-command"></a>Get TransportServer 명령을 사용 하 여

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정 된 전송 서버에 대 한 정보를 표시합니다.
## <a name="syntax"></a>구문
```
wdsutil [Options] /Get-TransportServer [/Server:<Server name>] /Show:{Config}
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
|/ 표시: {Config}|지정된 된 전송 서버에 대 한 구성 정보를 반환합니다.|
## <a name="BKMK_examples"></a>예제
서버에 대 한 정보를 보려면 다음을 입력 합니다.
```
wdsutil /Get-TransportServer /Show:Config
```
구성 정보를 보려면 다음을 입력 합니다.
```
wdsutil /Get-TransportServer /Server:MyWDSServer /Show:Config
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[TransportServer 사용 안 함 명령을 사용 하 여](using-the-disable-transportserver-command.md)
[사용 TransportServer 명령을 사용 하 여](using-the-enable-transportserver-command.md)
[하위 명령: 집합 TransportServer](subcommand-set-transportserver.md)
[하위 명령: 시작 TransportServer](subcommand-start-transportserver.md)
[하위 명령: TransportServer 중지](subcommand-stop-transportserver.md)
