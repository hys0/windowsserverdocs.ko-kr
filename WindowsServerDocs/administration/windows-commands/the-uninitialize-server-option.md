---
title: 초기화 서버 옵션
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 5c63e09738871c5b74c1b564a83c35ad28f4fa80
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385594"
---
# <a name="the-uninitialize-server-option"></a>초기화 서버 옵션

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

초기 서버 구성 중에 서버에 대 한 변경 내용을 되돌립니다. 여기에는 **/initialize-server** 옵션이 나 Windows 배포 서비스 mmc 스냅인에서 변경한 내용이 포함 됩니다. 이 명령은 서버를 구성 되지 않은 상태로 다시 설정 합니다. 이 명령은 remoteInstall 공유 폴더의 내용을 수정 하지 않습니다. 대신 서버를 다시 초기화할 수 있도록 서버 상태를 다시 설정 합니다.
## <a name="syntax"></a>구문
```
wdsutil [Options] /Uninitialize-Server [/Server:<Server name>]
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
## <a name="BKMK_examples"></a>예와
서버를 다시 초기화 하려면 다음 중 하나를 입력 합니다.
```
wdsutil /Uninitialize-Server
wdsutil /verbose /Uninitialize-Server /Server:MyWDSServer
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
 사용[안 함](using-the-disable-server-command.md)-서버 명령을 사용 하 여-1[@no__t 명령을 사용](using-the-enable-server-command.md)하 여-3 @no__t 명령을[사용 하 여 @no__t-](using-the-get-server-command.md)7[초기화 서버](using-the-initialize-server-command.md)명령을 사용 하 여 
[ 하위 명령: set-Server](subcommand-set-server.md)1[하위 명령: 시작-server](subcommand-start-server.md)3[하위 명령: 중지 서버](subcommand-stop-server.md)
