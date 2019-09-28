---
title: 거부 AutoaddDevices 명령을 사용 하 여
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ea25a4b2-5fad-4360-9c47-c2c9df7ea31f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2e8fda3037ef921e2b2a7a0acb616b8a67545ff9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362997"
---
# <a name="using-the-reject-autoadddevices-command"></a>거부 AutoaddDevices 명령을 사용 하 여

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

관리자의 승인이 보류 중인 컴퓨터를 거부 합니다. 자동 추가 정책을 사용 하는 경우 알 수 없는 컴퓨터 (사전 준비 되지 않은 컴퓨터)에서 이미지를 설치할 수 있으려면 관리자 승인이 필요 합니다. 서버 속성 페이지의 **PXE 응답** 탭을 사용 하 여이 정책을 사용 하도록 설정할 수 있습니다.
## <a name="syntax"></a>구문
```
wdsutil [Options] /Reject-AutoaddDevices [/Server:<Server name>] /RequestId:<Request ID or ALL>
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
|/ 요청 Id: < ID & #124; 요청 모든 >|보류 중인 컴퓨터에 할당 된 요청 ID를 지정 합니다. 모든 보류 중인 컴퓨터를 거부 하려면 지정 **모든**합니다.|
## <a name="BKMK_examples"></a>예와
단일 컴퓨터를 거부 하려면 다음을 입력 합니다.
```
wdsutil /Reject-AutoaddDevices /RequestId:12
```
모든 컴퓨터를 거부 하려면 다음을 입력 합니다.
```
wdsutil /verbose /Reject-AutoaddDevices /Server:MyWDSServer /RequestId:ALL
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
 @no__t[승인-](using-the-approve-autoadddevices-command.md)autoadddevices 명령을 사용 하 여-3[delete](using-the-delete-autoadddevices-command.md)autoadddevices 명령을 사용 하 여 
[get autoadddevices 명령을](using-the-get-autoadddevices-command.md) 사용 하 여
