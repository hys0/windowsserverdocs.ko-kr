---
title: 진행률
description: 명령이 실행 되는 동안 진행률을 표시 하는 진행률에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8ce5e77b-e13f-4ac3-948d-31770a6c7e25
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3fcb06304df22208cef013d73a4ebf0af1991f88
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721428"
---
# <a name="progress"></a>진행률

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