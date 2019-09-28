---
title: Get AllDevices 명령을 사용 하 여
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5824b3d2-2df1-4ed6-a289-e6c47c13fea2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5b7d2ce709c7e3fbaf7ab4f0e49be14c98ba1cd9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71401978"
---
# <a name="using-the-get-alldevices-command"></a>Get AllDevices 명령을 사용 하 여

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

모든 사전 준비 된 컴퓨터의 Windows 배포 서비스 속성을 표시합니다. 사전 준비 된 컴퓨터는 active directory 도메인 서비스의 컴퓨터 계정에 연결 된 물리적 컴퓨터입니다.
## <a name="syntax"></a>구문
```
wdsutil [Options] /Get-AllDevices [/forest:{Yes | No}] [/ReferralServer:<Server name>]
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|[포리스트/: {Yes &#124; No}]|Windows 배포 서비스 전체 포리스트 또는 로컬 도메인에서 컴퓨터를 반환할지 여부를 지정 합니다. 기본 설정은 **No**, 로컬 도메인의 컴퓨터만 반환 되는 의미입니다.|
|[/ ReferralServer:<Server name>]|지정된 된 서버에 대 한 사전 준비 하는 컴퓨터만 반환 합니다.|
## <a name="BKMK_examples"></a>예와
모든 컴퓨터를 보려면 다음 중 하나를 입력 합니다.
```
wdsutil /Get-AllDevices
wdsutil /verbose /Get-AllDevices /forest:Yes /ReferralServer:MyWDSServer
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[하위 명령: /set-device](subcommand-set-device.md)
[장치 추가 명령을 사용 하 여](using-the-add-device-command.md)
[get 장치 명령을 사용 하 여](using-the-get-device-command.md)
