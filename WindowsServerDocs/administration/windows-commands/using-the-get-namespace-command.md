---
title: Get-네임 스페이스 명령을 사용 하 여
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ea641bab-e97b-4909-918e-447730027dc1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bd11880b6e733850b522c3a06152ac7ce7a28841
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889664"
---
# <a name="using-the-get-namespace-command"></a>Get-네임 스페이스 명령을 사용 하 여

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

사용자 지정 네임 스페이스에 대 한 정보를 표시합니다.
## <a name="syntax"></a>구문
Windows Server 2008 R2
```
wdsutil /Get-Namespace /Namespace:<Namespace name> [/Server:<Server name>] [/Show:Clients]
```
Windows Server 2008 R2
```
wdsutil /Get-Namespace /Namespace:<Namespace name> [/Server:<Server name>] [/details:Clients]
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|/ Namespace:<Namespace name>|네임 스페이스의 이름을 지정합니다. Note 이름, 이것이 하 고 고유 해야 합니다.<br /><br />배포 서버: 네임 스페이스 이름에 대 한 구문은 /Namspace:WDS:<ImageGroup>/<ImageName>/<Index>합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다. **WDS:ImageGroup1/install.wim/1**<br />-전송 서버: 이 값은 서버에서 만들어졌을 때 네임 스페이스에 지정 된 이름과 일치 해야 합니다.|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름을 지정 하지, 로컬 서버가 사용 됩니다.|
|[/ 쇼: 클라이언트가] 또는 [/ 세부 정보: 클라이언트]|지정된 된 네임 스페이스에 연결 된 클라이언트 컴퓨터에 대 한 정보를 표시 합니다.|
## <a name="BKMK_examples"></a>예제
네임 스페이스에 대 한 정보를 보려면 다음을 입력 합니다.
```
wdsutil /Get-Namespace /Namespace:"Custom Auto 1"
```
네임 스페이스와 연결 된 클라이언트에 대 한 정보를 보려면 다음 중 하나를 입력 합니다.
-   Windows Server 2008: `wdsutil /Get-Namespace /Server:MyWDSServer /Namespace:"Custom Auto 1" /Show:Clients`
-   Windows Server 2008 R2: `wdsutil /Get-Namespace /Server:MyWDSServer /Namespace:"Custom Auto 1" /details:Clients`
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[get AllNamespaces 명령을 사용 하 여](using-the-get-allnamespaces-command.md)
[새 네임 스페이스 명령을 사용 하 여](using-the-new-namespace-command.md)
[제거 네임 스페이스 명령을 사용 하 여](using-the-remove-namespace-command.md)
[하위 명령: 시작 네임 스페이스](subcommand-start-namespace.md)
