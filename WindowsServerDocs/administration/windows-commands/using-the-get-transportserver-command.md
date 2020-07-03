---
title: 수신 서버
description: 지정 된 전송 서버에 대 한 정보를 표시 하는 가져오기-전송 서버에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: de634123-0179-41b2-9c6f-726508130ff5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 115942290679decd8b8c660e4113576efb30123d
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932173"
---
# <a name="get-transportserver"></a>수신 서버

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정 된 전송 서버에 대 한 정보를 표시합니다.

## <a name="syntax"></a>구문
```
wdsutil [Options] /Get-TransportServer [/Server:<Server name>] /Show:{Config}
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
|/ 표시: {Config}|지정된 된 전송 서버에 대 한 구성 정보를 반환합니다.|
## <a name="examples"></a>예
서버에 대 한 정보를 보려면 다음을 입력 합니다.
```
wdsutil /Get-TransportServer /Show:Config
```
구성 정보를 보려면 다음을 입력 합니다.
```
wdsutil /Get-TransportServer /Server:MyWDSServer /Show:Config
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md) 
 [Disable-서버 명령을](using-the-disable-transportserver-command.md) 
 사용 하 여 [Enable-서버 명령 사용](using-the-enable-transportserver-command.md) 
 [하위 명령: 설정-서버](subcommand-set-transportserver.md) 
 [하위 명령: 시작-서버](subcommand-start-transportserver.md) 
 [하위 명령: 중지-서버](subcommand-stop-transportserver.md)
