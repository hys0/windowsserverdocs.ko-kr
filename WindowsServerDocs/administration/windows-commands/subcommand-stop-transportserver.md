---
title: 하위 명령 중지-서버
description: 중지-서버에 대 한 참조 문서
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: dc1b1eec-6893-445e-81dc-16b3fae287fa
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ea749b9ff2f19b4b7c9e70e0a58024d4dd9e37f9
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933742"
---
# <a name="subcommand-stop-transportserver"></a>중지-TransportServer 하위 명령:

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

전송 서버에서 모든 서비스를 중지합니다.
## <a name="syntax"></a>구문
```
wdsutil [Options] /Stop-TransportServer [/Server:<Server name>]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|[/ 서버:<Server name>]|전송 서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 없는 전송 서버를 지정 하는 경우 로컬 서버 사용 됩니다.|
## <a name="examples"></a><a name="BKMK_examples"></a>예
서비스를 중지 하려면 다음 중 하나를 입력 합니다.
```
wdsutil /Stop-TransportServer
wdsutil /verbose /Stop-TransportServer /Server:MyWDSServer
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md) 
 [Disable-서버 명령을](using-the-disable-transportserver-command.md) 
 사용 하 여 [Enable-서버 명령 사용](using-the-enable-transportserver-command.md) 
 [Get-서버 명령 사용](using-the-get-transportserver-command.md) 
 [하위 명령: 설정-서버](subcommand-set-transportserver.md) 
 [하위 명령: 시작-서버](subcommand-start-transportserver.md)
