---
title: 가져오기-AllDevices
description: 모든 사전 준비 된 컴퓨터의 Windows 배포 서비스 속성을 표시 하는 가져오기 AllDevices에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5824b3d2-2df1-4ed6-a289-e6c47c13fea2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 26e114be7ecf104687da237636b54b79e4114591
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720898"
---
# <a name="get-alldevices"></a>가져오기-AllDevices

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

모든 사전 준비 된 컴퓨터의 Windows 배포 서비스 속성을 표시합니다. 사전 준비 된 컴퓨터는 active directory 도메인 서비스의 컴퓨터 계정에 연결 된 물리적 컴퓨터입니다.

## <a name="syntax"></a>구문
```
wdsutil [Options] /Get-AllDevices [/forest:{Yes | No}] [/ReferralServer:<Server name>]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|[포리스트/: {Yes &#124; No}]|Windows 배포 서비스 전체 포리스트 또는 로컬 도메인에서 컴퓨터를 반환할지 여부를 지정 합니다. 기본 설정은 **No**, 로컬 도메인의 컴퓨터만 반환 되는 의미입니다.|
|[/ ReferralServer:<Server name>]|지정된 된 서버에 대 한 사전 준비 하는 컴퓨터만 반환 합니다.|
## <a name="examples"></a>예
모든 컴퓨터를 보려면 다음 중 하나를 입력 합니다.
```
wdsutil /Get-AllDevices
wdsutil /verbose /Get-AllDevices /forest:Yes /ReferralServer:MyWDSServer
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)
[하위 명령:](subcommand-set-device.md)
get 장치 명령을[사용](using-the-get-device-command.md) 하 여 장치[추가 명령을](using-the-add-device-command.md)
사용 하 여 장치를 설정 합니다.
