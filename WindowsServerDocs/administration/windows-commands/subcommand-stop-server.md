---
title: 하위 명령 중지-서버
description: Windows 배포 서비스 서버에서 모든 서비스를 중지 하는 하위 명령 중지 서버에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 09f411c0-099f-4591-95fd-b77b3fd9118a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 68cc73ac016e2ffded774567034801e1c11944d1
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721629"
---
# <a name="subcommand-stop-server"></a>하위 명령: 서버 중지

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows 배포 서비스 서버에서 모든 서비스를 중지합니다.

## <a name="syntax"></a>구문
```
wdsutil [Options] /Stop-Server [/Server:<Server name>]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
## <a name="examples"></a>예
서비스를 중지 하려면 다음 중 하나를 입력 합니다.
```
wdsutil /Stop-Server
wdsutil /verbose /Stop-Server /Server:MyWDSServer
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)
[사용 안 함](using-the-disable-server-command.md)
[Using the enable-Server Command](using-the-enable-server-command.md)
-서버 명령을 사용 하 여 서버를 사용 하 여 명령을 사용 하 여[get](using-the-get-server-command.md)
서버 명령을 사용 하 여[Initialize](using-the-initialize-server-command.md)
서버 명령을 사용 하 여 명령을 사용 하 여 서버를 시작
합니다. 서버[하위](subcommand-start-server.md)명령[:](subcommand-set-server.md)
서버를 초기화 합니다. 서버[옵션](the-uninitialize-server-option.md)
