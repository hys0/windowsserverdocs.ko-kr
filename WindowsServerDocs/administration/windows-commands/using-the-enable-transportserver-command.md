---
title: -서버 사용
description: 전송 서버에 대 한 모든 서비스를 사용 하도록 설정 하는 사용 서버에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9d79dba1-4b57-4a00-8cba-877e6b8618e6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d4cd87b78e7a84255593464fede553bc294138c7
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936275"
---
# <a name="enable-transportserver"></a>-서버 사용

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

전송 서버에 대 한 모든 서비스를 활성화 합니다.

## <a name="syntax"></a>구문
```
wdsutil [Options] /Enable-TransportServer [/Server:<Server name>]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|[/ 서버:<Server name>]|전송 서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 이름이 지정 되지 않은, 로컬 서버를 사용 됩니다.|
## <a name="examples"></a>예
서버에서 서비스를 사용 하려면 다음 중 하나를 실행 합니다.
```
wdsutil /Enable-TransportServer
wdsutil /verbose /Enable-TransportServer /Server:MyWDSServer
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md) 
 [Disable-서버 명령을](using-the-disable-transportserver-command.md) 
 사용 하 여 [Get-서버 명령 사용](using-the-get-transportserver-command.md) 
 [하위 명령: 설정-서버](subcommand-set-transportserver.md) 
 [하위 명령: 시작-서버](subcommand-start-transportserver.md) 
 [하위 명령: 중지-서버](subcommand-stop-transportserver.md)
