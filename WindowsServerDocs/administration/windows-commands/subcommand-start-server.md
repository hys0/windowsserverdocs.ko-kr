---
title: 하위 명령 시작-서버
description: Windows 배포 서비스 서버에 대 한 모든 서비스를 시작 하는 하위 명령 시작 서버에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1e4343e2-0a16-4e65-8769-c09adaef5680
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 112f60897d96479d627fc61eb70f79de84d1514a
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936957"
---
# <a name="subcommand-start-server"></a>하위 명령: 서버 시작

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows 배포 서비스 서버에 대 한 모든 서비스를 시작합니다.

## <a name="syntax"></a>구문
```
wdsutil [Options] /start-Server [/Server:<Server name>]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|[/ 서버:<Server name>]|시작할 서버 이름을 지정 합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
## <a name="examples"></a>예
서버를 시작 하려면 다음 중 하나를 입력 합니다.
```
wdsutil /start-Server
wdsutil /verbose /start-Server /Server:MyWDSServer
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md) 
 [Disable Server 명령 사용](using-the-disable-server-command.md) 
 [Enable-Server 명령 사용](using-the-enable-server-command.md) 
 [Get Server 명령 사용](using-the-get-server-command.md) 
 [Initialize 서버 명령을](using-the-initialize-server-command.md) 
 사용 하 여 [하위 명령: 설정-서버](subcommand-set-server.md) 
 [하위 명령: 중지 서버](subcommand-stop-server.md) 
 [초기화 서버 옵션](the-uninitialize-server-option.md)
