---
title: 서버 초기화 명령을 사용 하 여
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68a26ad9-5eb2-4490-b782-b7cd46b8000d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4a1f3a1c02eb21f630aaff7219610864cd1db2a7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825194"
---
# <a name="using-the-initialize-server-command"></a>서버 초기화 명령을 사용 하 여

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

서버 역할을 설치한 후 초기 사용을 위해 Windows 배포 서비스 서버를 구성 합니다. 이 명령은 실행 한 후 사용 해야 합니다 [추가 이미지 명령을 사용 하 여](using-the-add-image-command.md) 서버로 추가 이미지 명령을 합니다.
## <a name="syntax"></a>구문
```
wdsutil /Initialize-Server [/Server:<Server name>] /remInst:<Full path> [/Authorize]
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
|/remInst:"<Full path>"|RemoteInstall 폴더의 이름과 전체 경로 지정합니다. 지정한 폴더가 아직 없는 경우이 옵션은 만듭니다이 명령이 실행 되는 경우. 항상 원격 컴퓨터 하는 경우에 로컬 경로 입력 해야 합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다. **D:\remoteInstall**.|
|[/ 권한 부여]|서버에서 호스트 제어 프로토콜 DHCP (동적)에 권한을 부여합니다. 이 옵션은 필요한 DHCP rogue 검색을 사용 하는 경우에 즉 Windows 배포 서비스 PXE 서버 해야 수에서 권한이 부여 된 DHCP 클라이언트 컴퓨터의 서비스를 제공할 수 있습니다. DHCP rogue 검색은 기본적으로 비활성화 하는 참고 합니다.|
## <a name="BKMK_examples"></a>예제
서버를 초기화 하 고 f: 드라이브를 공유 remoteInstall 폴더를 설정 하려면 다음을 입력 합니다.
```
wdsutil /Initialize-Server /remInst:"F:\remoteInstall"
```
서버를 초기화 하 고 c: 드라이브로 remoteInstall 공유 폴더를 설정 하려면 다음을 입력 합니다.
```
wdsutil /verbose /Progress /Initialize-Server /Server:MyWDSServer /remInst:"C:\remoteInstall"
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[는 서버 사용 안 함-명령을 사용 하 여](using-the-disable-server-command.md)
[enable 서버 명령 사용 하 여](using-the-enable-server-command.md)
[사용 합니다 get 서버 명령](using-the-get-server-command.md)
[하위 명령: 서버 설정](subcommand-set-server.md)
[하위 명령: 서버 시작](subcommand-start-server.md)
[하위 명령: 서버 중지](subcommand-stop-server.md)
[초기화 서버 옵션](the-uninitialize-server-option.md)
