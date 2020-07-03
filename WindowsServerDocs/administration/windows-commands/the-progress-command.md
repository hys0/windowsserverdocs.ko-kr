---
title: progress
description: 명령이 실행 되는 동안 진행률을 표시 하는 진행률에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8ce5e77b-e13f-4ac3-948d-31770a6c7e25
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9e9650a980d74f15bc0ec5c88d8df2dc93a3d8b0
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85934595"
---
# <a name="progress"></a>progress

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