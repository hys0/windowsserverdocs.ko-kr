---
title: Enable 서버 명령 사용
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 939ffbfb-cf3c-4310-9627-6e7e0c0644d6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fdf03a778a6c646aa79c2f844212b1728c5c73eb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852724"
---
# <a name="using-the-enable-server-command"></a>Enable 서버 명령 사용

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows 배포 서비스에 대 한 모든 서비스를 활성화 합니다.
## <a name="syntax"></a>구문
```
wdsutil [Options] /Enable-Server [/Server:<Server name>]
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
## <a name="BKMK_examples"></a>예제
서버에서 서비스를 사용 하려면 다음 중 하나를 실행 합니다.
```
wdsutil /Enable-Server
wdsutil /verbose /Enable-Server /Server:MyWDSServer
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[는 서버 사용 안 함-명령을 사용 하 여](using-the-disable-server-command.md)
[get 서버 명령을 사용 하 여](using-the-get-server-command.md)
[Initialize 서버 명령을 사용 하 여](using-the-initialize-server-command.md)
[하위 명령: 서버 설정](subcommand-set-server.md)
[하위 명령: 서버 시작](subcommand-start-server.md)
[하위 명령: 서버 중지](subcommand-stop-server.md)
[초기화 서버 옵션](the-uninitialize-server-option.md)
