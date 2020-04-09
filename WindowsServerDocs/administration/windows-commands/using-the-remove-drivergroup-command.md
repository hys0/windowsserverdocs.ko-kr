---
title: -DriverGroup 제거
description: 서버에서 드라이버 그룹을 제거 하는 DriverGroup에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.topic: article
ms.assetid: 1fefe9df-9782-433c-8abe-3f1a35e50da2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 56622c30b8b0af88a57c476eb4f03d598703d603
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830526"
---
# <a name="remove-drivergroup"></a>-DriverGroup 제거

서버에서 드라이버 그룹을 제거합니다.

## <a name="syntax"></a>구문

```
WDSUTIL /Remove-DriverGroup /DriverGroup:<Group Name> [/Server:<Server name>]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/DriverGroup:\<그룹 이름 >|제거할 드라이버 그룹의 이름을 지정 합니다.|
|[/Server:\<서버 이름 >]|서버 이름을 지정합니다. 이 NetBIOS 이름이 나 FQDN 수 있습니다. 서버 이름을 지정 하지 않으면 로컬 서버가 사용 됩니다.|

## <a name="examples"></a><a name=BKMK_examples></a>예와

드라이버 그룹을 제거 하려면 다음 중 하나를 입력 합니다.
```
WDSUTIL /Remove-DriverGroup /DriverGroup:PrinterDrivers
```
```
WDSUTIL /Remove-DriverGroup /DriverGroup:PrinterDrivers /Server:MyWdsServer
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)