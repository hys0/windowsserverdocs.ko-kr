---
title: Get AutoaddDevices 명령을 사용 하 여
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 24b4b688-55b0-4bd9-a2f5-7ef4b3dfe2f2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 337c8e76923fe243982ba9c10d18f2e5a5e7d9ff
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885744"
---
# <a name="using-the-get-autoadddevices-command"></a>Get AutoaddDevices 명령을 사용 하 여

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows 배포 서비스 서버에 자동 추가 데이터베이스에 있는 모든 컴퓨터가 표시 됩니다.
## <a name="syntax"></a>구문
```
wdsutil [Options] /Get-AutoaddDevices [/Server:<Server name>] /Devicetype:{PendingDevices | RejectedDevices | ApprovedDevices}
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
|/ 장치 유형: {PendingDevices &#124; RejectedDevices &#124; ApprovedDevices}|컴퓨터를 복구의 유형을 지정 합니다.<br /><br />-   **PendingDevices** 보류 중 상태에 있는 데이터베이스의 모든 컴퓨터를 반환 합니다.<br />-   **RejectedDevices** 는 있는 상태가 거부 데이터베이스에 모든 컴퓨터를 반환 합니다.<br />-   **ApprovedDevices** 는 상태를 승인한 데이터베이스의 모든 컴퓨터를 반환 합니다.|
## <a name="BKMK_examples"></a>예제
모든 승인 된 컴퓨터를 보려면 다음을 입력 합니다.
```
wdsutil /Get-AutoaddDevices /Devicetype:ApprovedDevices
```
모든 거부 된 컴퓨터를 보려면 다음을 입력 합니다.
```
wdsutil /verbose /Get-AutoaddDevices /Devicetype:RejectedDevices /Server:MyWDSServer
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[delete AutoaddDevices 명령을 사용 하 여](using-the-delete-autoadddevices-command.md)
[승인 AutoaddDevices 명령을 사용 하 여](using-the-approve-autoadddevices-command.md) 
 [ 거부 AutoaddDevices 명령을 사용 하 여](using-the-reject-autoadddevices-command.md)
