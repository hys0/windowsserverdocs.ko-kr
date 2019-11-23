---
title: 제거-네임 스페이스 명령을 사용 하 여
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4eb758b6-8519-4e26-9fe0-2e19bb0e8702
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b4c087442c43fd885fe4554cb29f9b2788420e05
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362793"
---
# <a name="using-the-remove-namespace-command"></a>제거-네임 스페이스 명령을 사용 하 여

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

사용자 지정 네임 스페이스를 제거 합니다.
## <a name="syntax"></a>구문
```
wdsutil /remove-Namespace /Namespace:<Namespace name> [/Server:<Server name>] [/force]
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|/Namespace:<Namespace name>|네임 스페이스의 이름을 지정합니다. 이 이름, 아니며 고유 해야 합니다.<br /><br />-   **배포 서버 역할 서비스**: 네임 스페이스 이름에 대 한 구문은/NAMESPACE: WDS:<ImageGroup>/<ImageName>/<Index>입니다. 예를 들어: **WDS:ImageGroup1/install.wim/1**<br />-   **전송 서버 역할 서비스**:이 값은 서버에서 만들 때 네임 스페이스에 지정 된 이름과 일치 해야 합니다.|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름을 지정 하지, 로컬 서버가 사용 됩니다.|
|/force|네임 스페이스를 즉시 제거 하 고 모든 클라이언트를 종료 합니다. **/Force**를 지정 하지 않으면 기존 클라이언트는 전송을 완료할 수 있지만 새 클라이언트는 참가할 수 없습니다.|
## <a name="BKMK_examples"></a>예와
네임 스페이스를 중지 하려면 (현재 클라이언트 전송을 완료할 수 있지만 새 클라이언트를 연결할 수 없는 경우), 유형:
```
wdsutil /remove-Namespace /Namespace:"Custom Auto 1"
```
모든 클라이언트의 종료를 강제 하려면 다음을 입력 합니다.
```
wdsutil /remove-Namespace /Server:MyWDSServer /Namespace:"Custom Auto 1" /force
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[get AllNamespaces 명령을 사용 하 여](using-the-get-allnamespaces-command.md)
[새 네임 스페이스 명령을 사용 하 여](using-the-new-namespace-command.md)
[하위 명령: 시작 네임 스페이스](subcommand-start-namespace.md)
