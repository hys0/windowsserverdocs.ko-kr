---
title: 초기화 서버 옵션
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 015efb04-fe84-469f-bd81-49d0046296b2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 73f1ff67331ae41fa0d88cb3a16df5095e0b6d66
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873984"
---
# <a name="the-uninitialize-server-option"></a>초기화 서버 옵션

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

초기 서버를 구성 하는 동안 서버에 대 한 변경 내용이 되돌립니다. 변경 내용을 여기에 **/initialize-server** 옵션 또는 Windows 배포 서비스 mmc 스냅인입니다. 이 명령은 구성 되지 않은 상태로 서버를 다시 설정 하는 참고 합니다. 이 명령은 remoteInstall 공유 폴더의 내용을 수정 하지 않습니다. 대신, 서버를 다시 초기화할 수 있도록 서버의 상태에 재설정 합니다.
## <a name="syntax"></a>구문
```
wdsutil [Options] /Uninitialize-Server [/Server:<Server name>]
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
## <a name="BKMK_examples"></a>예제
서버를 다시 초기화 하려면 다음 중 하나를 입력 합니다.
```
wdsutil /Uninitialize-Server
wdsutil /verbose /Uninitialize-Server /Server:MyWDSServer
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[는 서버 사용 안 함-명령을 사용 하 여](using-the-disable-server-command.md)
[enable 서버 명령 사용 하 여](using-the-enable-server-command.md)
[사용 합니다 get 서버 명령](using-the-get-server-command.md)
[Initialize 서버 명령을 사용 하 여](using-the-initialize-server-command.md)
[하위 명령: 서버 설정](subcommand-set-server.md) 
 [ 하위 명령: 서버 시작](subcommand-start-server.md)
[하위 명령: 서버 중지](subcommand-stop-server.md)
