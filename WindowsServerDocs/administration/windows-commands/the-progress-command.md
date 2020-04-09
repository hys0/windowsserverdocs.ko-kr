---
title: 이므로
description: 명령이 실행 되는 동안 진행률을 표시 하는 진행률에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8ce5e77b-e13f-4ac3-948d-31770a6c7e25
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9957174203df8f2f5c02bf3ab8a4f3406701a8da
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80833126"
---
# <a name="progress"></a>이므로

명령이 실행 되는 동안 진행률을 표시 합니다. 사용할 수 있습니다 **진행률/** 실행 하는 다른 WDSUTIL 명령을 사용 합니다. 지정 해야 하는 참고 **/verbose** 및 **진행률/** 바로 뒤 **WDSUTIL**합니다.

## <a name="syntax"></a>구문

```
WDSUTIL /progress <commands>
```

## <a name="examples"></a>예

서버를 초기화 하 고 진행률을 표시 하려면 다음을 입력 합니다.
```
WDSUTIL /Verbose /Progress /Initialize-Server /Server:MyWDSServer /RemInst:C:\RemoteInstall
```