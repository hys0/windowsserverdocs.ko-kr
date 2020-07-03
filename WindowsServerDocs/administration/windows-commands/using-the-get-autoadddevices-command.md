---
title: get AutoaddDevices
description: Windows 배포 서비스 서버의 자동 추가 데이터베이스에 있는 모든 컴퓨터를 표시 하는 get AutoaddDevices에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 24b4b688-55b0-4bd9-a2f5-7ef4b3dfe2f2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f2d470f8443da4612e97a2aa488adef256727382
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935034"
---
# <a name="get-autoadddevices"></a>get AutoaddDevices

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows 배포 서비스 서버의 자동 추가 데이터베이스에 있는 모든 컴퓨터를 표시 합니다.

## <a name="syntax"></a>구문
```
wdsutil [Options] /Get-AutoaddDevices [/Server:<Server name>] /Devicetype:{PendingDevices | RejectedDevices | ApprovedDevices}
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
|/Devicetype: {PendingDevices &#124; RejectedDevices &#124; ApprovedDevices}|컴퓨터를 복구의 유형을 지정 합니다.<p>-   **PendingDevices** 는 데이터베이스에서 보류 중 상태의 모든 컴퓨터를 반환 합니다.<br />-   **RejectedDevices** 는 데이터베이스에서 상태가 거부 됨 인 모든 컴퓨터를 반환 합니다.<br />-   **ApprovedDevices** 는 데이터베이스에서 승인 됨 상태의 모든 컴퓨터를 반환 합니다.|
## <a name="examples"></a>예
모든 승인 된 컴퓨터를 보려면 다음을 입력 합니다.
```
wdsutil /Get-AutoaddDevices /Devicetype:ApprovedDevices
```
모든 거부 된 컴퓨터를 보려면 다음을 입력 합니다.
```
wdsutil /verbose /Get-AutoaddDevices /Devicetype:RejectedDevices /Server:MyWDSServer
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md) 
 [Delete AutoaddDevices 명령을](using-the-delete-autoadddevices-command.md) 
 사용 하 여 [승인 AutoaddDevices 명령을](using-the-approve-autoadddevices-command.md) 
 사용 하 여 [거부 AutoaddDevices 명령을 사용 하 여](using-the-reject-autoadddevices-command.md)
